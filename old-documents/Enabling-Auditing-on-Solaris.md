On older Solaris boxes, you may need to run
`/etc/security/bsmconv/`.

After that, `audit -s` (re)starts auditing and `audit -t` stops it.

You can check if auditing is running with `auditconfig -getcond`.

To enable auditing of network, process management, and logins, the command is `auditconfig -setflags lo,nt,ps`

To enable forwarding to syslog, type `auditconfig -setplugin audit_syslog active p_flags=lo,nt,ps`

Audit logs can be viewed with `auditreduce | praudit`