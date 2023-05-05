---
title: "dependabot: code analysis and dependency management"
date: 2023-06-05
draft: false
categories:
  - "devops"
tags:
  - "ci-cd"
  - "devops"
---

# what is dependabot?  

dependabot is a github tool that automates the process of updating dependencies in your code base. it analyzes your project's dependencies and alerts when it finds new versions available.

it can update dependencies for a wide range of package managers, mine include:

[source, yaml]
----
rust: cargo
go: gomod
python: pip
svelte: npm
----

# how does dependabot work?

when you enable dependabot for your repository, it starts by scanning your codebase for outdated dependencies. it then creates a pull request with the updated dependencies, which you can review and merge into your codebase.
dependabot uses a set of default update strategies for each package manager it supports. these strategies include:

* version updates: dependabot updates the dependency to the latest available version.
* range updates: dependabot updates the dependency to the latest version within a specific range.
* lockfile updates: dependabot updates the lockfile to ensure that all dependencies are up-to-date.
* how to apply dependabot to your repository
* make a `.github/workflows/dependabot.yaml` and add the below yaml

[source, yaml]
----
version: 2
updates:
  - package-ecosystem: "package-manager-name"
    directory: "/"
    schedule:
      interval: "weekly"
----

in this example we put dependabot to search in the root of the repo for dependencies once every week.
note: avoid daily interval unless it’s absolutely necessary


# how to enable dependabot

on github.com, navigate to the main page of the repository. under your repository name, click
settings. 

image::https://docs.github.com/assets/cb-28266/mw-1440/images/help/repository/repo-actions-settings.webp[]

if you cannot see the "settings" tab, select the dropdown menu, then click settings.
in the "security" section of the sidebar, click code security and analysis, enable dependancy graph, and after that enable what you wish to use. 

# when do we upgrade

taking to account that your main branch is on a working state, making a new branch and testing dependabot's pr should probably be enough.

