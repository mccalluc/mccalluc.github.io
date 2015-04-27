---
layout: default
title: AAPB Review
---

A few things I think are done well in the AAPB site,
and others that could be done better.

<!--more-->

# Overview

## Tools

- *Rails/Blacklight/Solr* because we're familiar with that stack.
- *AWS OpsWorks* ... hopefully not just because we're unfamiliar with it.
- *Sony Ci* for media. grumble: high cost; bells and wistles we don't need.
- *GitHub* for all contributors. mixed results.
- existing API for source data.

## Design Choices

- Read-only: not the place to edit data
- Read-only: no user session stuff
- Read-only: no web admin: all config is checked in

## Data Flow

![data flow diagram](https://cdn.rawgit.com/WGBH/AAPB2/master/docs/aapb-data-flow.svg?v2)


# Download / Clean / Ingest

Ingest tools grew slowly: Now there's one main script, but earlier
each of the sub-scripts had its own `if __FILE__ = $0`.

The source data was really messy: On the first pass just got every 10000th 
record, fixed those bugs, added fixtures, then every 1000th, ... Thought about
sending these cleaned versions back upstream, but that would be risky, and 
wouldn't actually do anything for us.

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
- [Ingest](https://github.com/WGBH/AAPB2/blob/master/scripts/lib/pb_core_ingester.rb):
  - Frequency of commits makes the biggest different on ingest speed.

[`download_clean_ingest.rb`](https://github.com/WGBH/AAPB2/blob/master/scripts/download_clean_ingest.rb)
```
$ ruby scripts/download_clean_ingest.rb
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
```
