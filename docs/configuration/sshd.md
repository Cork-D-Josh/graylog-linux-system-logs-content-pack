## 🔐 SSH Server Configuration

To get clean SSH logs (`Accepted password` / `Failed password` only),
disable keyboard-interactive authentication in `/etc/ssh/sshd_config`:

```conf
# /etc/ssh/sshd_config
KbdInteractiveAuthentication no
```

Then restart the SSH service:

```bash
sudo systemctl restart sshd
```

> ⚠️ Without this setting, SSH logs authentication events as
> `keyboard-interactive/pam` instead of `password`, which will
> **break the parsing rules** of this content pack.
