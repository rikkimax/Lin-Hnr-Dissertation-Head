Routes in isolation are easy to confirm that they match the request. In some cases with the mixture of parameters, catch all and constant path parts this can cause errors in the routing process.

To illestrate this, the following set of routes can be used (hostname:*port*/path):

* some.site.acl:*80*/part
* some.site.acl:*80*/:var
* some.site.acl:*80*/*

In the given order these routes will not intefere with each other. This is because the constant goes first, then the variable (for any other path part), lastly the catch all hits which takes into account any path that has multiple path parts after the fact.

If the path parts for the parameter and catch all are swapped, the catch all will always execute and the catch all will never be executed. If the constant is swapped with the variable instead, the constant route will never be the given route but the catch all will be hit as the constant will fall under the variable if it does not have any following path parts.

The solution to this problem is given a path segment (i.e. /path/part where /path would be the scope for /path/party) would be sorted with all constant path parts going first, then the parameter, and finally the catch all. Note for one segment it is not possible to have multiple variables without giving some form of condition.

A multiple sort to alleviate these issues can be implemented in D using the code:

```D
	void doSort() {
		import std.algorithm : multiSort;

		multiSort!(
			(Route a, Route b){ return a.code < b.code},
			(Route a, Route b){ return isRouteLess(a.path, b.path); },
			(Route a, Route b){ return isAddressesLess(a.website.addresses, b.website.addresses); },
			)(allRoutes);
	}
```

Where allRoutes, is a dynamic array of type ``Route`` and the functions ``isRouteLess``/``isAddressesLess`` implement a comparison against a route path and address(es) as a dynamic array to determine which should go first in the array.

The above code was written for the purposes of sorting a list based router implementation. For a tree graph depending on at which point in the tree the addition of nodes is at, it may be possible to only do one or two of these in total instead of all three.