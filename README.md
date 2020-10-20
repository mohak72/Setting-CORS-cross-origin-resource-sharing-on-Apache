# Setting-CORS-cross-origin-resource-sharing-on-Apache
# In  virtualhost config
Header set Access-Control-Allow-Origin "*"
Restart server, reload page, and I was greeted with the normal cross-domain error.

# Chrome developer tools
OPTIONS http://my.example.dev/setting/1316 405 (Method Not Allowed) 

# Firefox developer tools
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://my.example.dev/setting/1316. This can be fixed by moving the resource to the same domain or enabling CORS.
Header set Access-Control-Allow-Origin "*"
Header set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
Header set Access-Control-Max-Age "1000"
Header set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"

with a 200 SUCCESS on every OPTIONS request.

Header set Access-Control-Allow-Origin "*"
Header set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
Header set Access-Control-Max-Age "1000"
Header set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"

# Added a rewrite to respond with a 200 SUCCESS on every OPTIONS request
RewriteEngine On
RewriteCond %{REQUEST_METHOD} OPTIONS
RewriteRule ^(.*)$ $1 [R=200,L]
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Chrome developer tools
XMLHttpRequest cannot load http://my.example.dev/setting/1316. No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://mydevsite.dev' is therefore not allowed access. 

# Firefox developer tools
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://my.example.dev/setting/1316. This can be fixed by moving the resource to the same domain or enabling CORS.
Solution for above errors:-
Add following in virtual host files:-
# Always set these headers.
Header always set Access-Control-Allow-Origin "*"
Header always set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
Header always set Access-Control-Max-Age "1000"
Header always set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"
 
# Added a rewrite to respond with a 200 SUCCESS on every OPTIONS request.
RewriteEngine On
RewriteCond %{REQUEST_METHOD} OPTIONS
RewriteRule ^(.*)$ $1 [R=200,L]
