---
layout: default
title: Chuck McCallum
---

Full-stack web developer with experience guiding small teams to deliver tools for researchers in the sciences and humanities.
Familiar with frameworks for data visualization, free-text search, and video delivery.
Interested in providing clear documentation and interfaces for users,
mentoring and supporting junior colleagues,
promoting software engineering best-practices across the organization,
and contributing back to open source software.

## Work History

**Visualization Software Developer, Department of Biomedical Informatics, Harvard Medical School
(August 2016-present)**: As part of the [Gehlenborg Lab](http://gehlenborglab.org/),
supported data visualization research and mentored new developers and interns.
Lead a four person team developing the the front-end and data curation tools for [HuBMAP](https://portal.hubmapconsortium.org/).
Initial author of [Vitessce](http://vitessce.io), which uses Deck.gl for interactive visualizations of spatial single-cell data,
and contributed to [HiGlass](http://higlass.io/) by simplifying deployment, and improving test coverage and input validation.

**Web Developer, Media Library and Archives, WGBH, Boston, Massachusetts
(August 2014-July 2016)**: Early developer on [americanarchive.org](https://americanarchive.org)
and [wgbhstocksales.org](https://github.com/WGBH-MLA/stock-sales-2),
ruby-on-rails applications with Solr backends for media collections. Developed AWS scripts for
creating EC2 instances and managing green/blue deployments across load balancers.

**Project Programmer, FilteredPush, Harvard Herbaria, Cambridge, Massachusetts
(August 2013-July 2014, funded for one year)**: Conceived and built a configurable
scriptlet generator to simplify “copy cataloging” workflows, particularly in natural
history collections. Used HTML5 Web Messaging API and jQuery on the client side,
with Solr and Jetty on the server side. Contributed to other components of the FilteredPush
project using JSF for the front end, and RDF/SPARQL, MongoDB, and MySQL on the back end.

**Software Engineer, Journal of Visualized Experiments, Cambridge,
Massachusetts (June 2011-July 2013)**:    Led the rearchitecting of
http://jove.com, using MVC principles and object-oriented PHP. Educated peers
about software development best practices. Wrote deployment scripts, and
created a test suite ranging from fine-grained unit tests to end-to-end
transactions. Also implemented free-text search, replaced our video player,
managed the transition to a new CDN, and planned for the transition from
Windows/SQLServer to Linux/MySQL. Built an administrative interface, using the
Propel ORM library, HTML5 File and History APIs, jQuery, and the SlickGrid JS
library.

**Software and QA Engineer, ITA Software, Cambridge, Massachusetts (January
2006-December 2008, January 2010-April 2011)**:    Supported developers of
Needlebase, a tool for information gathering and analysis.
(Project [discontinued after acquisition](https://googleblog.blogspot.com/2012/01/renewing-old-resolutions-for-new-year.html),
but [demo video](http://www.youtube.com/watch?v=58Gzlq4zSDk) still available.)
As QA, identified bugs in all layers of the system, documented
reproducers, wrote JUnit tests, and confirmed the fixes. As evangelist, wrote
blog posts and documentation and created demonstrations of the system. As
customer support, helped users understand how the software could solve their
problems, and provided feedback to developers and designers.

**Library Software Developer, University of Pennsylvania Libraries,
Philadelphia, Pennsylvania (2009; funded for one year)**:    For the Penn
Digital Library (http://dla.library.upenn.edu/dla), created new widgets and
applied existing widgets to build new collections. Used Solr for the backend,
WSDLs to connect to outside services, and XLST pipelines in Apache Cocoon for
display. Managed reindexing jobs with Java / Spring and Perl scripts.

**Software Developer VISTA, Community Software Lab, Lowell, Massachusetts (June
2005-December 2005)**:    New features and bug fixes in Perl for
a Merrimack Valley social-services directory. Supported Apache, PostgreSQL,
DHCP, DNS, firewall, and backups on Linux systems. Provided tech support in
person and over the phone. Developed promotional materials for the Lab and
promoted its hosting, email, and custom software services.   

## Education
- Master of Library Science, University of Maryland, College Park, 2005.
- BA, Geology and Mathematics, Carleton College, Northfield, Minnesota, 1999.

## Code Samples

I was the principle developer at the start on each of these: Later contributors have taken the successful ones well beyond what I could have done alone.

- HuBMAP components:
  - [Data Portal](https://portal.hubmapconsortium.org/) ([source](https://github.com/hubmapconsortium/portal-ui)): Flask site with React frontend
  - [ingest-validation-tools](https://github.com/hubmapconsortium/ingest-validation-tools): Data submission guidelines, and tools to check that submissions adhere to those guidelines.
- Visualizations:
  - [Vitessce](https://github.com/vitessce/vitessce): "Visual Integration Tool for Exploration of Spatial Single-Cell Experiments"
  - [heatmap-scatter-dash](https://github.com/refinery-platform/heatmap-scatter-dash): Simple heatmap + scatterplot using Plotly Dash
- Python modules on Pypi:
  - [tableschema-to-template](https://pypi.org/project/tableschema-to-template/): Generate Excel files from Tableschema definitions
  - [django-docker-engine](https://pypi.org/project/django-docker-engine/): Docker engine wrapper + proxy server for containerized visualizations in Django
- Ruby:
  - [American Archive of Public Broadcasting](http://americanarchive.org/) ([source](https://github.com/WGBH-MLA/AAPB2))
  - [WGBH Stock Sales](http://wgbhstocksales.org/) ([source](https://github.com/WGBH-MLA/stock-sales-2))
  - [Open Vault](http://openvault.wgbh.org/) ([source](https://github.com/WGBH-MLA/openvault3))
  - [CMLess](https://github.com/WGBH-MLA/cmless): Rails gem to manage a site's static content as markdown on github
- Java:
  - [FP-DataEntry](https://github.com/mccalluc/FP-DataEntry): “Copy cataloging” tool for natural history collections
