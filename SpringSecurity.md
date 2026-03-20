owasp -open world application security project
owasp releaes security vulnerablity every 4 years and the user has to make sure all the things are enforced
CSRF -Cross site Request Forgery
A reviw of filters
- Every HTTP request passes through a series of filter chain 
![[Pasted image 20260320101900.png]]
1. The client send request to the application and the spring container creates a Filter Chain wich contain filters and servelte that should process the httpservlet request
2. 