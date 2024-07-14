# Example Project: Rust Example

This example makes use of rocket.rs TODO App complete with GitHub actions pushed to DOM Cloud server.

But instead of pulling code changes, we build the binary in GitHub CI and push it to server, 
avoiding extra storage cost by installing rust feature and compiling depedencies compared to 
classic webhook mentioned in the documentation.

This project demo live here: http://rocket-rs-todo-app.domcloud.dev/ (note the db is lives in mem)

## Add server ID Key

This CI used SSH identifier keys instead of SSH password, so there's extra step you need to do in the server SSH:

```
ssh-keygen -t rsa -b 4096 -C youremail@example.com
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600  ~/.ssh/authorized_keys
```

Examine the secret key by `cat ~/.ssh/id_rsa` then add it to `SSH_KEY` action secrets.

Try checking [this repo CI scripts](.github/workflows/domcloud.yml)

## NGINX Setup

The NGINX setup would be like this:

```yaml
nginx:
  root: public_html/public
  passenger:
    enabled: 'on'
    app_start_command: env ROCKET_PORT=$PORT ./todo
```

## Caveats when using this method

### Shared libraries

When building from CI, note the differences between our servers and CI servers. If you find yourself unable to run due to lack of required shared library, then you also need to compile the given shared library and push it too to the server.

For example in this example, the project [require to have libsqlite3 library](https://diesel.rs/guides/getting-started#:~:text=A%20note%20on%20installing%20diesel_cli) in the system but since DOM Cloud servers [having this shared library already](https://domcloud.co/docs/integration/self-host#package-installs-rhel), we don't need to copy this shared library.

See our guide for [installing shared libraries](https://domcloud.co/docs/features/linux#installing-shared-libraries)

### Embedding paths

Avoid embedding or hardcoding paths that evalues at build time, e.g. `relative!` macro originally used in this example [are removed](https://github.com/domcloud/example-rust-todo/commit/36af73c) to make this example works.
