## Hostnames
The typical method of locating of a website utilises a field called a hostname. Hostnames are defined by the DNS specification. In the case of web development a special form of hostname specified on the webserver itself uses wildcards so that unknown subdomains can be handled by a given method.

The typical form that a hostname will be given will be:

1. ``abc.tld`` or ``def.abc.tld`` and so on
2. ``*.abc.tld``

In the case of the second with wildcard, as per the DNS specification the wildcard component does not necessarily have to be the first element of the hostname specifier. So the case of ``sub.*.abc.tld`` is valid. This complicates a web routers implementation should it be indicative of the website that it is serving for. Nieve implementations will only handle the most basic case of ``*.abc.tld`` however since the DNS specification allows for constant values before and multiple wildcards within a hostname it complicates the matter somewhat.

A wildcard in a hostname is somewhat similar to that of a parameter as a path segment of a URI. It does not match multiple child entries only the one.

Not all web servers support wildcard hostnames to the definition of the DNS specification. IIS did not support wildcards prior to version 10.

https://tools.ietf.org/html/rfc1034
https://tools.ietf.org/html/rfc4592
https://www.iis.net/learn/get-started/whats-new-in-iis-10/wildcard-host-header-support