# Pantheon Advanced Page Cache

[![CircleCI](https://circleci.com/gh/pantheon-systems/pantheon_advanced_page_cache.svg?style=svg)](https://circleci.com/gh/pantheon-systems/pantheon_advanced_page_cache)

Pantheon Advanced Page Cache module is a bridge between [Drupal cache metadata](https://www.drupal.org/docs/8/api/cache-api/cache-api) and the [Pantheon Global CDN](https://pantheon.io/docs/global-cdn/).

Just by turning on this module your Drupal site will start emitting the HTTP headers necessary to make the Pantheon Global CDN aware of data underlying the response. Then, when the underlying data changes (nodes and taxonomy terms are updated, user permissions changed) this module will clear only the relevant pages from the edge cache.

This module has no configuration settings of its own, just enable it and it will pass along information already present in Drupal 8 to the Global CDN.

If you want to take finer grain control of how Drupal is handling it's cache data (in ways that will interact with both the Global CDN and internal Drupal caches) consider using [Views Custom Cache Tags](https://www.drupal.org/project/views_custom_cache_tag) and [Cache Control Override](https://www.drupal.org/project/cache_control_override).

### Debugging

By default, Pantheon's infrastructure strips out the `Surrogate-Key` response header before responses are served to clients. The contents of this header can be viewed as `Surrogate-Key-Raw` by adding on a debugging header to the request.

A direct way of inspecting headers is with `curl -I`. This command will make a request and show just the response headers. Adding `-H "Pantheon-Debug:1"` will result in `Surrogate-Key-Raw` being included in the response headers. The complete command looks like this:

 `curl -IH "Pantheon-Debug:1" https://dev-cache-tags-demo.pantheonsite.io/`

 Piping to `grep` will filter the output down to just the `Surrogate-Key-Raw` header:

`curl -IH "Pantheon-Debug:1" https://dev-cache-tags-demo.pantheonsite.io/ | grep -i Surrogate-Key-Raw`

### Feedback and collaboration

For real time discussion of the module find Pantheon developers in our [Power Users Slack channel](https://pantheon.io/docs/power-users/). Bug reports and feature requests should be posted in [the drupal.org issue queue.](https://www.drupal.org/project/issues/pantheon_advanced_page_cache?categories=All) For code changes, please submit pull requests against the [GitHub repository](https://github.com/pantheon-systems/pantheon_advanced_page_cache) rather than posting patches to drupal.org.
