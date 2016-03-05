# Tomcat

Apache Tomcat is a Java based web-server.

In most default installations, Tomcat includes a "manager"
application, which allows uploading arbitrary JARs to run on the
server (e.g. a web shell).

![Tomcat manager UI](https://db.apache.org/derby/images/TomcatDeploy.gif)

## Securing Tomcat

* Check if the host-manager and manager applications are running.
    * By default the URLs are `/manager` and `/host-manager`
    * To disable these managers
        * move or change the extension of ```/etc/tomcat7/Catalina/localhost/{host-manager.xml,manager.xml}```
    * If you need to keep these managers running, check the credentials for the users with access to them in `/etc/tomcat7/tomcat-users.xml`

* Tomcat uses a port (defaults to 8005) as a remote shutdown port.
  * Make sure this port is firewalled.
  * Disable it by changing shutdown port to `-1` in `/etc/tomcat7/server.xml`.

## More info

* https://www.owasp.org/index.php/Securing_tomcat
* https://tomcat.apache.org/tomcat-7.0-doc/manager-howto.html
* https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-7-on-ubuntu-14-04-via-apt-get
* http://www.tomcatexpert.com/blog/2011/11/02/best-practices-securing-apache-tomcat-7
