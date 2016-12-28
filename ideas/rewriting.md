## Rewriting
Web routers implement two forms of rewriting of routes. The first of which rewrites with the usage of HTTP status codes 
including, page not found (404) and internal server error (501). The second rewrites requests based upon a specification 
provided by 
the developer. In this research the later of which is not covered as that is worthy of its own paper.
Rewriting using status codes is still a difficult task where by only two (404/501) of which can actively be recognised by most 
implementations. Rewriting in these cases is a simple matter of locating the last route handler that matches the pattern given 
the status code. If an error occurs during the processing of a 501 request, one of two things may occur. 

1. Lookup for status code on path up the tree of path parts
2. Error out and expose this to the client

### Problems
A classic implementation strategy of rewriting mechanisms is to create a new request based upon a set of rewrite rules. This 
requires a new set of lookups which can be extremely costly on cpu time. Assuming one lookup is O(n+1) then for every rewrite 
that is performed the O notation would actually be O(mn+m+1) where m is the number of rewrites that have occured. The +1 
in this notation represents decoding while +m is the cost of rewriting.

