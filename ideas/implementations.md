## Implementations

The implementations of the web routers are classified into two groups: rooted and unrooted. A rooted router is one which devides the registered routes into its own websites.

The web routers being tested are rooted except for the list web router. It sorts the registered routes into one big array, based upon:

- HTTP status code
- Website (address/port)
- Path
- SSL

With preference for non-wildcards to go first.
