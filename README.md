# ansible-ftpd

Configures Pure-FTPd with TLS using the `community.crypto` Ansible collection.
The role installs `python3-cryptography` on the managed host.

Passive connections use ports 6000–6100 by default. Override
`pure_passive_port_range` with a space-separated range, for example `"30000 30100"`,
and allow those ports in the server firewall.

Certbot takes precedence when both `privkey.pem` and `fullchain.pem` are
available under `/etc/letsencrypt/live/<host FQDN>/`. The role installs a
Certbot deploy hook to update the bundle after renewal. The combined PEM is
stored at `pure_certificate_path` (`/etc/ssl/private/pure-ftpd.pem` by default)
with mode `0600`.

Without a complete Certbot pair, the role keeps an existing PEM unless it is a
self-signed certificate using the role-managed key. If no bundle exists, the
role generates a self-signed certificate and stores its key and certificate
next to the bundle in `.key` and `.crt` files. New and renewed certificates
are valid for 3650 days. Managed certificates are renewed when a role run
finds that they expire within 30 days.

The role generates `pure_dhparams_path` for Pure-FTPd 1.0.38 through 1.0.49.
With other installed versions, it removes the unused file without restarting
the service.

The PureDB backend initializes missing password and database files before
starting the service. Existing accounts and databases are preserved.

## Requirements

- `ansible-core` 2.19 or newer.
- The `ansible.mysql` collection when using the MySQL backend.

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
