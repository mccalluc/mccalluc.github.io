---
layout: default
title: Projects
---

Projects where I was the only significant code contributor are _italicized_, but successful projects have gone well beyond what I could have done alone.

## HuBMAP components:
- [Data Portal](https://portal.hubmapconsortium.org/) ([source](https://github.com/hubmapconsortium/portal-ui) / [my PRs](https://github.com/hubmapconsortium/portal-ui/pulls?q=is%3Apr+is%3Aclosed+author%3Amccalluc)): Flask site with React frontend. I guided the work of two junior developers and a designer to align with the high-level goals set by our PI, and I worked with outside teams to define the APIs that support our frontend.
- [_ingest-validation-tools_](https://github.com/hubmapconsortium/ingest-validation-tools): Data submission guidelines, and tools to check that submissions adhere to those guidelines. Listened to data curators, pipeline authors, and lab scientists, and delivered scripts and a schema language that is used to validate submissions and generate documentation.

## Visualizations:
- [Vitessce](http://beta.vitessce.io/) ([source](https://github.com/vitessce/vitessce) / [my PRs](https://github.com/vitessce/vitessce/pulls?q=is%3Apr+is%3Aclosed+author%3Amccalluc)): “Visual Integration Tool for Exploration of Spatial Single-Cell Experiments”. Initial author of a Javascript library for declaratively specified, linked, interactive visualizations, repurposing the deck.gl geospatial library for microscopy and single-cell analysis.
- [_heatmap-scatter-dash_](https://github.com/refinery-platform/heatmap-scatter-dash): Simple heatmap + scatterplot using Plotly Dash.

## Python modules on Pypi:
- [_tableschema-to-template_](https://pypi.org/project/tableschema-to-template/): Generate Excel data entry templates from Tableschema definitions. A small reusable module factored out of the larger ingest-validation-tools.
- [_django-docker-engine_](https://pypi.org/project/django-docker-engine/): Docker engine wrapper + proxy server for containerized visualizations in Django. Generic visualization launch architecture, for which heatmap-scatter-dash was a demonstration client.

## Ruby:
- [American Archive of Public Broadcasting](http://americanarchive.org/) ([source](https://github.com/WGBH-MLA/AAPB2) / [my PRs](https://github.com/WGBH-MLA/AAPB2/pulls?q=is%3Apr+is%3Aclosed+author%3Amccalluc)) and [WGBH Stock Sales](http://wgbhstocksales.org/) ([source](https://github.com/WGBH-MLA/stock-sales-2) / [my PRs](https://github.com/WGBH-MLA/stock-sales-2/pulls?q=is%3Apr+is%3Aclosed+author%3Amccalluc)): One of two web developers on video-centric RoR projects for WGBH, building on the Solr/Blacklight framework to implement designs.
- [_CMLess_](https://github.com/WGBH-MLA/cmless): Rails gem to manage a site’s static content as markdown on github. Proposed and got buy-in for the idea that rather than maintaining a separate CMS, static pages on AAPB could be based on markdown in the repo, with frequent redeployments.

## Java:
- [_FP-DataEntry_](https://github.com/mccalluc/FP-DataEntry): Server + browser bookmarklet for copy cataloging in natural history collections. The Filtered Push project had proposed a distributed network for data-sharing across natural history collections. When that failed to engage, proposed and implemented a small tool to support interactive screen scraping and data alignment.

## Fun (?) non-work projects:
- [_walkle_](https://mccalluc.github.io/walkle/) ([source](https://github.com/mccalluc/walkle)) (2022): Like wordle, for walks
- [_spiro-font_](https://mccalluc.github.io/spiro-font/) ([source](https://github.com/mccalluc/spiro-font)) (2022): Font construction in the browser
- [_ploverlay_](http://mccalluc.github.io/ploverlay) ([source](https://github.com/mccalluc/ploverlay)) (2021): Uses the Geolocation API to show where you are in the real world
- [_dagsheet_](http://mccalluc.github.io/dagsheet) ([source](https://github.com/mccalluc/dagsheet)) (2017): A toy graphical functional programming environment
- [_yajt_](http://mccalluc.github.io/yajt) ([source](https://github.com/mccalluc/yajt)) (2016): Video processing and sound generation in the browser
- [_demo-data_](http://mccalluc.github.io/data-demo) ([source](https://github.com/mccalluc/data-demo)) (2015): Build PNG and MIDI files byte by byte

