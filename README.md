# ansible-ftpd

Setups PureFTPd with SSL. Uses Certbot cerficates if available, generates self-signed if not.

Passive connections use ports 6000–6100 by default. Override
`pure_passive_port_range` with a space-separated range, for example `"30000 30100"`,
and allow those ports in the server firewall.

Certbot certificates are read from `/etc/letsencrypt/live/<host FQDN>/`.
The role maintains a renewal deploy hook even when the FTP certificate already
exists. The combined certificate is stored at `pure_certificate_path`
(`/etc/ssl/private/pure-ftpd.pem` by default) with mode `0600`.

The PureDB backend initializes missing password and database files before
starting the service. Existing accounts and databases are preserved.

### Example playbook
```yaml
---
- hosts: myserver
  roles:
    - role: sunfoxcz.ftpd
      pure_user_database: mysql # or puredb
```

## License

Licensed under MIT license. See [LICENSE](LICENSE.md) for details.
