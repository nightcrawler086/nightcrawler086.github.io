---
weight: 999
title: "Duplicate File Finder (dff)"
description: "A cli for find duplicate files in a tree"
icon: "article"
date: "2026-02-16T11:38:35-05:00"
lastmod: "2026-02-16T11:38:35-05:00"
draft: true
toc: true
---

# About

[dff](https://github.com/nightcrawler086/dff) is a cli program to find duplicate files in a tree, written in Go.

It is currently in its most basic form, just printing out any duplicates that it finds. There are a few features that I want to add:

- Arguments
    - extension filter
    - verbose
- Performance
    - Use some concurrency features to test some performance improvements
