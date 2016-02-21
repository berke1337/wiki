# Apache Cheatsheet
* Default process name: `httpd`. Config usually in `/etc/apache2/httpd.conf`.

### Setup as reverse proxy
* `a2enmod proxy` or `LoadModule proxy_module modules/mod_proxy.so`
* Configure the Proxy
```
<VirtualHost *:*>
ProxyPass /app1/ http://localhost:81/
</VirtualHost>
```

#### Default configuration
FreeBSD `pkg install apache24`, excluding comments, with __mod_php__ installed
```
ServerRoot "/usr/local"
Listen 80
LoadModule authn_file_module libexec/apache24/mod_authn_file.so
LoadModule authn_core_module libexec/apache24/mod_authn_core.so
LoadModule authz_host_module libexec/apache24/mod_authz_host.so
LoadModule authz_groupfile_module libexec/apache24/mod_authz_groupfile.so
LoadModule authz_user_module libexec/apache24/mod_authz_user.so
LoadModule authz_core_module libexec/apache24/mod_authz_core.so
LoadModule access_compat_module libexec/apache24/mod_access_compat.so
LoadModule auth_basic_module libexec/apache24/mod_auth_basic.so
LoadModule ratelimit_module libexec/apache24/mod_ratelimit.so
LoadModule reqtimeout_module libexec/apache24/mod_reqtimeout.so
LoadModule filter_module libexec/apache24/mod_filter.so
LoadModule mime_module libexec/apache24/mod_mime.so
LoadModule log_config_module libexec/apache24/mod_log_config.so
LoadModule env_module libexec/apache24/mod_env.so
LoadModule headers_module libexec/apache24/mod_headers.so
LoadModule unique_id_module libexec/apache24/mod_unique_id.so
LoadModule setenvif_module libexec/apache24/mod_setenvif.so
LoadModule version_module libexec/apache24/mod_version.so
LoadModule mpm_prefork_module libexec/apache24/mod_mpm_prefork.so
LoadModule unixd_module libexec/apache24/mod_unixd.so
LoadModule status_module libexec/apache24/mod_status.so
LoadModule autoindex_module libexec/apache24/mod_autoindex.so
LoadModule dir_module libexec/apache24/mod_dir.so
LoadModule alias_module libexec/apache24/mod_alias.so
LoadModule php5_module        libexec/apache24/libphp5.so

IncludeOptional etc/apache24/modules.d/[0-9][0-9][0-9]_*.conf

<IfModule unixd_module>
User www
Group www
</IfModule>

ServerAdmin you@example.com

ServerName bsd.local #insert your hostname here

<Directory />
    AllowOverride none
    Require all denied
</Directory>

DocumentRoot "/usr/local/www/apache24/data"
<Directory "/usr/local/www/apache24/data">
    Options FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>

<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>

<Files ".ht*">
    Require all denied
</Files>

ErrorLog "/var/log/httpd-error.log"
LogLevel warn

<IfModule log_config_module>
    LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined
    LogFormat "%h %l %u %t \"%r\" %>s %b" common

    <IfModule logio_module>
      LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" %I %O" combinedio
    </IfModule>
    CustomLog "/var/log/httpd-access.log" common
</IfModule>

<IfModule alias_module>
    ScriptAlias /cgi-bin/ "/usr/local/www/apache24/cgi-bin/"
</IfModule>

<Directory "/usr/local/www/apache24/cgi-bin">
    AllowOverride None
    Options None
    Require all granted
</Directory>

<IfModule mime_module>
    TypesConfig etc/apache24/mime.types
    AddType application/x-compress .Z
    AddType application/x-gzip .gz .tgz
</IfModule>

<IfModule proxy_html_module>
Include etc/apache24/extra/proxy-html.conf
</IfModule>

<IfModule ssl_module>
SSLRandomSeed startup builtin
SSLRandomSeed connect builtin
</IfModule>

Include etc/apache24/Includes/*.conf


<FilesMatch "\.php$">
    SetHandler application/x-httpd-php
</FilesMatch>
<FilesMatch "\.phps$">
    SetHandler application/x-httpd-php-source
</FilesMatch>

```
