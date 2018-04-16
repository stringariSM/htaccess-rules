# htaccess-rules

<?php
/*
    HTACCESS DA RAÍZ
 */
'
Options +FollowSymlinks -MultiViews -Indexes

RewriteEngine On
RewriteBase /

RewriteCond %{HTTP_HOST} !^www\. [NC]
RewriteRule ^(.*)$ http://www.%{HTTP_HOST}/$1 [R=301,L]

# URL with no path
RewriteCond %{REQUEST_URI}  ^/?$        [NC]
RewriteCond %{REQUEST_URI}  !index\.php [NC]
RewriteRule .*  /2015/  [NC,L]

# URL with path
RewriteCond %{REQUEST_URI}  !^/2015     [NC]
RewriteRule ^(.+)  /2015/$1             [NC,L]
'
    /*
        HTACCESS DA 2015
     */
'
#Regras para dominio
RewriteEngine on
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?/$1 [L]
'
'
#Força o www com https (deve ficar na raiz)
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteCond %{HTTP_HOST} !^www\..+$ [NC]
RewriteRule ^ https://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]


#Força o https (deve ficar na raiz)
RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
'

git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT {commit id} | xargs tar -rf mytarfile.tar


git archive -o update.zip HEAD $(git diff --name-only COMMIT~ COMMIT)
