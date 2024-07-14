# Rocket Todo Example

This example makes use of a SQLite database via `diesel` to store todo tasks. As
a result, you'll need to have `sqlite3` and its headers installed:

  * **OS X:** `brew install sqlite`
  * **Debian/Ubuntu:** `apt-get install libsqlite3-dev`
  * **Arch:** `pacman -S sqlite`

## Add server ID Key

```
ssh-keygen -t rsa -b 4096 -C youremail@example.com
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600  ~/.ssh/authorized_keys
```

Examine the secret key by `cat ~/.ssh/id_rsa`
