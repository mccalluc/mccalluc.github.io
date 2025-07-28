---
layout: default
title: Writing
---


## Public history

### Scripts

These are scripts and fragments of scripts which assume a particular setting. I'll say at the start that the questions that visitors have are what I look forward to in a tour, so I hope these invite questions rather than seeming to be self-contained.

- [Cooper-Frost-Austen](cfa)
- [Music at Old North](music)

### Sources

For now, this is just a place to keep transcriptions from documents. Hope to pull it into a more coherent essay.

- [Old North 1912 Restoration](on-1912)


## Software

For me, writing is central to the software development process. While documentation is one output, other, more ephemeral notes are necessary along the way.
- Meeting agendas: What questions need to be answered, and what are the answers?
- Design notes: Before we start sketching UIs, who are the users, and what actions are we trying to support?
- Issues: Make sure to record enough information to record a bug, or enough background information to motivate a feature request.

Software documentation needs to address different audiences. Think about how we deepen our engagement with a particular tool over time: First assessing whether a particular package does what we need, then learning how to use the tool, and perhaps at some point even contributing to its development. In DP Wizard I created a small, nested set of documentation to serve these different needs:
- For the active user, documentation of the command-line interface.
- For the shopper, documentation on [PyPI](https://pypi.org/project/dp_wizard/) provides some motivation, and also quotes the command-line documentation.
- Finally, for the developer, the [README](https://github.com/opendp/dp-wizard#readme) provides all of the above information, and extends with infomation on the development process.

Finally, software documentation exists as part of a software project, so we can use software tools to help produce it, and ensure its consistency. In the case of DP Wizard, there are checks on the consistency of the nested documentation, and the software itself generates Jupyter notebooks to explain the underlying computations. Other documentation tools may include link checking, API documentation generation, and using doctests for any examples to ensure their consistency.