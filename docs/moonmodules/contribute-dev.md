---
title: Contribute to WLED MM Development
hide:
  # - navigation
  # - toc
---

This page Work In Progress

## Setup

<img width="400" alt="Screenshot 2022-10-25 at 17 40 14" src="https://user-images.githubusercontent.com/91013628/197819274-b2e318ba-9039-4de1-8296-6673a09d08e9.png">

## Core branches
* **mdev**: Main development branch. [merge from upstream](#Merge-from-upstream)
* **dev/acmain/main**: Do not commit or merge directly to this branch -> easier to keep up to date with upstream

### General coding standards
* Use WLEDMM in comments so our changes can be found back
* Add 🌜character on UI items which are MM specific so users can see where MM differs from AC

## Work from other repos:
* Fork
* submit PR

## Access to repo

### Additional coding standards
* Always update date in wled.h
* Sometimes update version: Find and replace old version (e.g. 0.14.0-b15.21) by new version (e.g. 0.14.0-b15.22)

### Feature branches
* Only use for new features. Branch from dev/acmain/main if intended to merge in upstream using PRs, otherwise branch from mdev

### Merge from upstream
* Merge with care: add a commit that will create a conflict. Merge (with conflicts). Resolve conflicts. Unstage all files so you see the differences. Undo changes you do not want in (most often conflicts but can be others too) and stage files. Do that with each file one-by-one. Commit. Undo if you doubt else push to remote.
* If WLEDMM comments have been added consequently this will help with merging from uptream. However you can't rely on this for 100% so merging always need to be done very precisely, knowing what you will merge.

