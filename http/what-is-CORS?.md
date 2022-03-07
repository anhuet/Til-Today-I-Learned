# CORS?

When it comes to HTTP, an [origin](https://developer.mozilla.org/en-US/docs/Glossary/origin) is defined by several different aspects of the URL. This is important for understanding what qualifies as same and cross-origin when dealing with [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) (Cross-Origin Resource Sharing).

For something to be same-origin, it must have the same scheme (HTTP/HTTPS), the same host, and the same port. If any one of the scheme, host (including subdomains), or port is different, then it is not same-origin.

Here are some examples of different origins:

- https://example.com vs http://example.com (different scheme)
- https://example.com vs https://sub.example.com (different host)
- https://example.com:3000 vs https://example.com:5000 (different port)

As long as the scheme, host, and port match, they are the same origin. The path (everything following the origin) doesn't factor into the question of same origin.  
More: [Deep dive in CORS](https://ieftimov.com/posts/deep-dive-cors-history-how-it-works-best-practices/)
