---
layout: page
permalink: /publications/
title: publications
description: Peer-reviewed publications are listed in reverse chronological order. † indicates co-first authorship.
nav: true
nav_order: 1
---

<!-- _pages/publications.md -->

See also my [Google Scholar](https://scholar.google.com/citations?user=jsDXz44AAAAJ&hl=en) profile.

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

<h3 class="mt-4">Peer-reviewed articles</h3>

{% bibliography --query @article %}

<h3 class="mt-5">Under review</h3>

{% bibliography --query @unpublished --group_by none %}

<h3 class="mt-5">Reports and commentary</h3>

{% bibliography --query @misc --group_by none %}

</div>
