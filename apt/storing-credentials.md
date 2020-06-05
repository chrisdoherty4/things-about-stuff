# Storing credentials

Ubuntu Apt lets you configure package source lists in `/etc/apt/sources.list.d`. When you list
a source you can include the username and password/token used to authenticate with the
server but it's considered bad practice.

Instead, we can configure a file under `/etc/apt/auth.conf.d` to contain the credentials in a `.netrc` file fashion.

#### Example

In the `/etc/apt/sources.list.d/source.list` file.

```
 deb https://apt:debian@example.org/debian buster main
```

The credentials above can be removed and placed in a `/etc/apt/auth.conf.d/source.conf` file.

```
machine https://example.org/debian login apt password debian
```
