# ansible-ftpd

Setups PureFTPd with SSL. Uses Certbot cerficates if available, generates self-signed if not.

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
