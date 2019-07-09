# ansible-composer

Setups PureFTPd.

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
