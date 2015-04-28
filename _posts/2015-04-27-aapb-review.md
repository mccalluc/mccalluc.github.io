---
layout: default
title: AAPB Review
---

A few things I think are done well on the [AAPB](http://americanarchive.org/) site,
and others that could be done better.

<!--more-->

## Overview

### Tools

- *Rails/Blacklight/Solr* because we're familiar with that stack.
- *AWS OpsWorks* ... hopefully not just because we're unfamiliar with it.
- *Sony Ci* for media. grumble: high cost; bells and wistles we don't need.
- *GitHub* for all contributors. mixed results.
- existing API for source data.

### Design Choices

Keep it simple!:
- Read-only: not the place to edit data
- Read-only: no user session stuff
- Read-only: no web admin: all config is checked in
- ActiveRecord not used

Keep it simple?:
- Blacklight provides a wrapper so you don't need to write XPath... 
  but [I like XPath](https://github.com/WGBH/AAPB2/blob/master/app/models/pb_core.rb).
- Blacklight provides dynamic Solr fields so types can be infered from name suffixes...
  but it prefer my configuration in [one place](https://github.com/WGBH/AAPB2/blob/master/jetty/solr/blacklight-core/conf/schema.xml#L485),
  rather than scattered across the code.
- Storing entire XML document in solr, rather than just the fields for display.
  Storage is cheap, reindexing is expensive, and people change their minds.


### Data Flow

![data flow diagram](https://cdn.rawgit.com/WGBH/AAPB2/master/docs/aapb-data-flow.svg?v2)


## Download / Clean / Ingest

Ingest tools grew slowly: Now there's one main script, but earlier
each of the sub-scripts had its own `if __FILE__ = $0`.

The source data was really messy: On the first pass just got every 10000th 
record, fixed those bugs, added [fixtures](https://github.com/WGBH/AAPB2/tree/master/spec/fixtures/pbcore),
then every 1000th, ... Thought about sending these cleaned versions back upstream, 
but that would be risky, and wouldn't actually do anything we need.

- [Download](https://github.com/WGBH/AAPB2/blob/master/scripts/lib/downloader.rb):
  - At one point, processed the files as they were downloaded,
    but more robust and flexible if downstream works from files.
  - Modes: all, recent, by query...
- [Clean](https://github.com/WGBH/AAPB2/blob/master/scripts/lib/cleaner.rb): 
  - No illusion that this will handle any problem, but it handles the ones I saw.
  - Get it to validate against schema,
  - and [map vocabularies](https://github.com/WGBH/AAPB2/blob/master/app/models/vocab_map.rb),
  - and put elements in canonical order by attribute value.
  - (Display order of repeating elements determined by XML order.)
- [Validate](https://github.com/WGBH/AAPB2/blob/master/app/models/validated_pb_core.rb)
  - Confirm schema conformance,
  - and hit each method.
- [Ingest](https://github.com/WGBH/AAPB2/blob/master/scripts/lib/pb_core_ingester.rb):
  - Fields for indexing must be specified.
  - Frequency of commits makes the biggest different on ingest speed.

All together now: [download_clean_ingest.rb](https://github.com/WGBH/AAPB2/blob/master/scripts/download_clean_ingest.rb)

~~~
  USAGE: download_clean_ingest.rb
           [--batch-commit] [--same-mount] [--stdout-log]
           [--just-reindex] [--skip-sitemap]
           ( --all [PAGE] | --back DAYS | --query 'QUERY'
             | --ids ID ... | --id-files ID_FILE ...
             | --files FILE ... | --dirs DIR ... )

  boolean flags:
    --batch-commit: Optionally, make just one commit at the end, rather than
      one commit per file.
    --same-mount: Optionally, allow same mount point for the script and the
      solr index. This is what you want in development, but the default, to
      disallow this, would have stopped me from running out of disk many times.
    --stdout-log: Optionally, log to stdout, rather than a log file.
    --just-reindex: Rather than querying the AMS, query the local solr. This
      is typically used when the indexing strategy has changed, but the AMS
      data has not changed.
    --skip-sitemap: Do not regenerate sitemap.xml. If no new records are
      ingested, the sitemaps will not change, and regeneration can be skipped.

  mutually exclusive modes:
    --all: Download, clean, and ingest all PBCore from the AMS. Optionally,
      supply a results page to begin with.
    --back: Download, clean, and ingest only those records updated in the
      last N days. (I don't trust the underlying API, so give yourself a
      buffer if you use this for daily updates.)
    --query: First obtain a list of IDs to update using the url query fragment.
      Unless --just-reindex is given, these records will be re-downloaded,
      cleaned, and ingested.
    --ids: Download (or query), clean, and ingest records with the given IDs.
      Will usually be used in conjunction with --batch-commit, rather than
      committing after each record.
    --id-files: Read the files, and then download (or query), clean, and
      ingest records with the given IDs. Again, this will usually be used in
      conjunction with --batch-commit, rather than committing after each record.
    --files: Clean and ingest the given files.
    --dirs: Clean and ingest the given directories. (While "--files dir/*"
      could suffice in many cases, for large directories it might not work,
      and this is easier than xargs.)
~~~

## The Site

Not many [routes](https://github.com/WGBH/AAPB2/blob/master/config/routes.rb):

- catalog: ([model](https://github.com/WGBH/AAPB2/blob/master/app/models/pb_core.rb), 
  [controller](https://github.com/WGBH/AAPB2/blob/master/app/controllers/catalog_controller.rb))
  Heavy lifting done by Blacklight.
- organizations: ([model](https://github.com/WGBH/AAPB2/blob/master/app/models/organization.rb), 
  [controller](https://github.com/WGBH/AAPB2/blob/master/app/controllers/organizations_controller.rb))
  Might have used ActiveRecord, but loading from 
  [config](https://github.com/WGBH/AAPB2/blob/master/config/organizations.yml) works.
- media: ([controller](https://github.com/WGBH/AAPB2/blob/master/app/controllers/media_controller.rb)) For video, page renders with `/media/...` URL: If requested, hits the Sony API,
  and then returns a redirect to the temp URL
- override: ([controller](https://github.com/WGBH/AAPB2/blob/master/app/controllers/override_controller.rb)) Static content is checked in as markdown. (Non-technical librarian has been
  maintaining these and making PRs: it has worked well.)

## Testing

- Good coverage, but perhaps too brittle?
- [Travis](https://travis-ci.org/WGBH/AAPB2) doesn't check everything:
  - Ci API requires key.
  - AMS Downloads can be unreasonably slow.
  - Links don't need to be checked with every push.

Interesting bits:
- In several places assertions are collected in an array which we iterate over: Concise, and maintainable,
  but no way to rerun just one failure. 
  [catalog_spec](https://github.com/WGBH/AAPB2/blob/master/spec/features/catalog_spec.rb#L83); 
  [pb_core_spec](https://github.com/WGBH/AAPB2/blob/master/spec/models/pb_core_spec.rb#L57);
  [override_spec](https://github.com/WGBH/AAPB2/blob/master/spec/features/override_spec.rb)
- Static content is checked in, rather than having a separate CMS, so links and xml syntax can be checked.
- Ingest script has both unit tests for the internals, and one test that just looks at stdout at the 
  [top level](https://github.com/WGBH/AAPB2/blob/master/spec/scripts/download_clean_ingest_spec.rb).

## Java-isms

- Exception chaining: 
  [definitions](https://github.com/WGBH/AAPB2/blob/master/scripts/lib/pb_core_ingester.rb#L108),
  [use](https://github.com/WGBH/AAPB2/blob/master/scripts/download_clean_ingest.rb#L170):
  There might be a better idiom, but I wanted to reclassify exceptions at a middle-level,
  but retain the original stack trace at the top. This does that.
- Inner classes: [Ci actions](https://github.com/WGBH/AAPB2/blob/master/scripts/ci/ci.rb#L50):
  "Inner classes" in Ruby are just namespacing, unlike Java where they get access to the containing instance.
  Since I have to pass in the "container" by hand, this organization doesn't make much sense.
- Discovered `singleton` late in the game: I should use it more widely.
- Subclassing to add behavior: 
  [`class ValidatedPBCore < PBCore`](https://github.com/WGBH/AAPB2/blob/master/app/models/validated_pb_core.rb)
  and
  [`class Ci < CiCore` and `class Detailer < CiClient`](https://github.com/WGBH/AAPB2/blob/master/scripts/ci/ci.rb):
  Not *bad*, but not necessary, either.

## Things that got dropped along the way.

- Organization config was originally in an Excel XML document,
  just because that's what it was being maintained in. That was 
  workable, but yaml is much more readable.
- Organization text had essentially been stored in a homebrewed
  markdown-lite: Much better to use the real thing.
- Sub-sampling during ingest was dropped once we had ingested
  everything... but if you were to start with a new, messy data source,
  you'd want it back.
- Each module in the ingest pipeline used to be callable on its own,
  and they were chained together in bash. All those `if __FILE__ = $0`
  clauses were not as well tested as the internal interfaces. 
- In the XML cleanup, folks wanted reports of what was changed in
  each document... but no one has ever looked at it. Should remove.
