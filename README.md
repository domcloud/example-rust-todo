# Example Project: Rust Example

This example makes use of rocket.rs TODO App complete with GitHub actions pushed to DOM Cloud server.

But instead of pulling code changes, we build the binary in GitHub CI and push it to server, 
avoiding extra storage cost by installing rust feature and compiling depedencies compared to 
classic webhook mentioned in the documentation.

## Add server ID Key

This CI used SSH identifier keys instead of SSH password, so there's extra step you need to do in the server SSH:

```
ssh-keygen -t rsa -b 4096 -C youremail@example.com
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600  ~/.ssh/authorized_keys
```

Examine the secret key by `cat ~/.ssh/id_rsa` then add it to `SSH_KEY` action secrets.
