---
tags:
  - article
  - Astro
  - JavaScript
  - sharrowvale
  - technology/programming
title: Astro Pagefind
date: 2025-02-23
---

# Astro Pagefind

## Requirements

Pagefind API support for on Astro SSR

Potential Existing support for SSR with template UI.[^1] Upon further reading, this component renders the required code to run pagefind client side.

We need to be able to call the static pagefind api from the Astro backend. This would let us render search components in Astro and send responses [[htmx]] style.

## Research

You can run pagefind as a separate server. Could this be used to easily connect two services?

You can also run pagefind on node.[^2] Its unclear if this is just for indexing, or for searching too. Will need to test this with astro.

Found a GitHub issue for running pagefind in node.[^3] This is pretty clearly what would be needed before an Astro version of pagefind was possible. It would certainly be the required step for working on this.

Found a further github discussion for running pagefind in node by faking the browser object on the server.[^4] They outline 3 responsibilities for successfully running pagefind server side:

1. Importing `pagefind.js` from file rather than from a web request
2. Faking some browser global objects
3. Running imported pagefind and returning results

This discussion concludes with a working version of pagefind. Good news!

## Proposal

1. Run pagefind search api within Node.js
2. Run this pagefind search api within an Astro component
3. Make use of pagefind search api within Astro component to serve search in Astro SSR
4. Support Astro features such as pagination in pagefind queries

## Concerns

### Partial Builds of Pagefind

Because pagefind will be run during site build, and the subsequent pages will be scanned by pagefind to build a new pagefind directory, it is possible to keep outdated items in the search engine when results or pagefind are recorded into the engine.

[^1]: https://github.com/shishkin/astro-pagefind?tab=readme-ov-file#pre-filled-search-query
[^2]: https://pagefind.app/docs/node-api/
[^3]: https://github.com/CloudCannon/pagefind/issues/519
[^4]: https://github.com/CloudCannon/pagefind/discussions/175
