> [!WARNING]
> We are currently migrating this fork to `mailu 2024.06`. Some things might be broken, such as `notls`. We are sorry for the inconveniences caused.

<p align="leftr"><img src="docs/assets/logomark.png" alt="Mailu" height="200px">&nbsp;<img src="docs/assets/openid-logo.svg" alt="OpenID" height="200px"></p>


Mailu is a simple yet full-featured mail server as a set of Docker images.
It is free software (both as in free beer and as in free speech), open to
suggestions and external contributions. The project aims at providing people
with an easily setup, easily maintained and full-featured mail server while
not shipping proprietary software nor unrelated features often found in
popular groupware.

> [!NOTE]
> This fork is extended by an OpenID Connect implementation to enable user session handling (single sign-on) and authentication using OpenID standard. The fork is maintained by [Heviat](https://heviat.com), a German cloud computing company based in Potsdam. Feel free to contribute to this repository!

Features
========

Main features include:

- **Standard email server**, IMAP and IMAP+, SMTP and Submission with auto-configuration profiles for clients
- **Advanced email features**, aliases, domain aliases, custom routing, full-text search of email attachments
- **Web access**, multiple Webmails and administration interface
- **User features**, aliases, auto-reply, auto-forward, fetched accounts, managesieve
- **Admin features**, global admins, announcements, per-domain delegation, quotas
- **Security**, enforced TLS, DANE, MTA-STS, Letsencrypt!, outgoing DKIM, anti-virus scanner, [Snuffleupagus](https://github.com/jvoisin/snuffleupagus/), block malicious attachments
- **Antispam**, auto-learn, greylisting, DMARC and SPF, anti-spoofing
- **Freedom**, all FOSS components, no tracker included
- **Compatibility**, OpenID Connect support for user authentication

![Domains](docs/assets/screenshots/domains.png)

Installation
============

The automated installation process of the Mailu Setup Utility currently does not support the OpenID Connect extension this fork brings. You can still use the [Mailu Setup Utility](https://setup.mailu.io/1.9/) as usual, but you have perform some steps manually after downloading.

> [!WARNING]
> The setup utility allows selecting features which are not yet present in this fork. An update will follow soon.

Every Docker image from the organization [`mailu`](https://hub.docker.com/u/mailu) must be replaced with an image from the organization [`heviat`](https://github.com/orgs/heviat/packages) at GitHub Container Registry - e.g. [`mailu/admin`](https://hub.docker.com/r/mailu/admin) becomes [`ghcr.io/heviat/admin`](https://ghcr.io/heviat/admin). To do so, you can simply place a `.env` file in the project directory and set `DOCKER_ORG` and `MAILU_VERSION` environment variables matching our Docker images:

Example `.env` file:

```
DOCKER_ORG=ghcr.io/heviat
MAILU_VERSION=master
```

Moreover, to enable OpenID Connect authentication, the following additional configuration properties are needed in `mailu.env`:

|             Property Name               |                                                      Description                                                    |           Example         |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `OIDC_ENABLED`                          | Enable OpenID Connect                                                                                               | `True` \| `False`         |
| `OIDC_PROVIDER_INFO_URL`                | OpenID Connect provider configuration url (aka. _well-known_ url)                                                   | [https://`host`:`port`/auth/realms/`realm`/.well-known/openid-configuration]() |
| `OIDC_REDIRECT_URL`                     | OpenID Connect custom redirect URL if HOSTNAME not matching your login url                                          | [https://`host`]()        |
| `OIDC_CLIENT_ID`                        | OpenID Connect Client ID for Mailu                                                                                  | `6779ef20e75817b79602`    |
| `OIDC_CLIENT_SECRET`                    | OpenID Connect Client Secret for Mailu                                                                              | `3d66bbd6d0a69af62de7...` |
| `OIDC_BUTTON_NAME`                      | Display text for the "login-with-OpenID" button                                                                     | `OpenID Connect`          |
| `OIDC_VERIFY_SSL`                       | Disable TLS certificate verification for the OIDC client                                                            | `True` \| `False`         |
| `OIDC_CHANGE_PASSWORD_REDIRECT_ENABLED` | If enabled, OIDC users will have an button to get redirect to their OIDC provider to change their password          | `True` \| `False`         |
| `OIDC_CHANGE_PASSWORD_REDIRECT_URL`     | Defaults to provider issuer url appended by `/.well-known/password-change`.                                         | `https://oidc.example.com/pw-change`         |

Here is a snippet for easy copy paste:

```properties
###################################
# OpenID Connect settings
###################################

# Enable OpenID Connect. Possible values: True, False
OIDC_ENABLED=True
# OpenID Connect Provider configuration URL
OIDC_PROVIDER_INFO_URL=https://<host>:<port>/auth/realms/.well-known/openid-configuration
# OpenID redirect URL if HOSTNAME not matching your login url
OIDC_REDIRECT_URL=https://mail.example.com
# OpenID Connect Client id
OIDC_CLIENT_ID=<CLIENT_ID>
# OpenID Connect Client secret
OIDC_CLIENT_SECRET=<CLIENT_SECRET>
# Display text for OpenID Connect login button. Default: OpenID Connect
OIDC_BUTTON_NAME=OpenID Connect
OIDC_VERIFY_SSL=True
OIDC_CHANGE_PASSWORD_REDIRECT_ENABLED=True
OIDC_CHANGE_PASSWORD_REDIRECT_URL=https://oidc.example.com/pw-change

```

After that, the installation process should be working as expected.

Contributing
============

Mailu-OpenID is free software, open to suggestions and contributions. All
components are free software and compatible with the MIT license. All
specific configuration files, Dockerfiles and code are placed under the
MIT license.
