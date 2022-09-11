<p align="leftr"><img src="docs/assets/logomark.png" alt="Mailu" height="200px"></p>


Mailu is a simple yet full-featured mail server as a set of Docker images.
It is free software (both as in free beer and as in free speech), open to
suggestions and external contributions. The project aims at providing people
with an easily setup, easily maintained and full-featured mail server while
not shipping proprietary software nor unrelated features often found in
popular groupware.

> **NOTE:** This fork is extended by an OpenID Connect implementation to enable user session handling (single sign-on) and authentication using OpenID standard. The fork is maintained by [Heviat](https://heviat.com), a German cloud computing company based in Potsdam. Feel free to contribute to this repository!

Features
========

Main features include:

- **Standard email server**, IMAP and IMAP+, SMTP and Submission with autoconfiguration profiles for clients
- **Advanced email features**, aliases, domain aliases, custom routing
- **Web access**, multiple Webmails and administration interface
- **User features**, aliases, auto-reply, auto-forward, fetched accounts
- **Admin features**, global admins, announcements, per-domain delegation, quotas
- **Security**, enforced TLS, DANE, MTA-STS, Letsencrypt!, outgoing DKIM, anti-virus scanner
- **Antispam**, auto-learn, greylisting, DMARC and SPF
- **Freedom**, all FOSS components, no tracker included
- **Compatibility**, OpenID Connect support for user authentication

![Domains](docs/assets/screenshots/domains.png)

Installation
============

The installation process is currently not automated by an addtional fork of the Mailu setup utility. Therefore, you can use the [mailu setup utility](https://setup.mailu.io/1.9/) as you would with the normal mailu server. But after the generation of the required files, you need to update them:

You need to change every used Docker image delivered from the Dockerhub _mailu_ organization to the similar named image from Dockerhub _heviat_ - e.g. _mailu/admin_ must be _heviat/admin_.
Moreover, to enable OpenID Connect authentication, the following configuration properties are needed in _mailu.env_:

- *OIDC_ENABLED*: **True** or **False**
- *OIDC_PROVIDER_INFO_URL*: the OpenID Connect provider information url (also known as _well-known_ url) e.g. <http://keycloakhost:keycloakport/auth/realms/{realm}/.well-known/openid-configuration>
- *OIDC_CLIENT_ID*: Client ID for mailu OpenID client
- *OIDC_CLIENT_SECRET*: Client secret for mailu OpenID client
- *OIDC_BUTTON_NAME*: Name for the "login-with-OpenID"-button. Default: **OpenID Connect**

After that, the installation process should be working as expected.

Contributing
============

Mailu-OpenID is free software, open to suggestions and contributions. All
components are free software and compatible with the MIT license. All
specific configuration files, Dockerfiles and code are placed under the
MIT license.
