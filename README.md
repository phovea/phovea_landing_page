# Phovea Landing Page [![Phovea][phovea-image]][phovea-url]

This repository contains the Dockerfile for creating the caleydoapp.org landing page nginx server. In addition, this server also proxies to the various caleydoapp.org pages based on environment variables.

A Docker image is available at [Docker Hub](https://hub.docker.com/r/caleydo/phovea_landing_page).

## Configuration

The ngnix server can be configured using the following environment variables (ENV):

* [`PHOVEA_ENABLE_SSL_LANDING_PAGE`](#enable-ssl-for-landing-page)
* [`PHOVEA_APP_*`](#add-phovea-app)
* [`PHOVEA_APPFORWARD_*`](#add-phovea-app-forward)
* [`PHOVEA_FORWARD_*`](#add-caleydo-subdomain-forward)


### Enable SSL for landing page

If the variable `PHOVEA_ENABLE_SSL_LANDING_PAGE` exists a SSL certificate for caleydoapp.org is added. By default no SSL certificate is added.


### Add phovea app

The variable `PHOVEA_APP_*` adds an app to the landing page and creates a ngnix configuration and a SSL certificate for this app automatically.

`PHOVEA_APP_<NAME>=<name>;<domain>;<forward>;<release-channel>`

* `<name>`: Name of the app that is visible in the landing page
* `<domain>`: Subdomain of the app only (e.g., `lineup`)
* `<forward>`: Target requests are forwarded to (e.g., `cluster:12345`)
* `<release-channel>`: Release channel can be `stable`, `daily`, or `development` and is indicated on the landing page

Example: `PHOVEA_APP_LINEUP=LineUp;lineup;cluster:12345;stable`


### Add phovea app forward

The variable `PHOVEA_APPFORWARD_*` adds an app to the landing page only. No ngnix configuration and SSL certificate is created.

`PHOVEA_APPFORWARD_<NAME>=<name>;<domain>;<forward>;<release-channel>`

* `<name>`: Name of the app that is visible in the landing page
* `<domain>`: Subdomain of the app only (e.g., `lineup`)
* `<forward>`: *Not used.*
* `<release-channel>`: Release channel can be `stable`, `daily`, or `development` and is indicated on the landing page

Example: `PHOVEA_APPFORWARD_LINEUP=LineUp;lineup;cluster:12345;stable`


### Add Caleydo subdomain forward

The variable `PHOVEA_FORWARD_*` adds a forward for caleydo.org subdomains.

`PHOVEA_FORWARD_<NAME>=<name>;<domain>;<forward>`

* `<name>`: Name of the forward
* `<domain>`: Full source domain (e.g., `lineup.caleydo.org`)
* `<forward>`: Full target domain (e.g., www.caleydo.org/tools/lineup)

**Note**: Do not add a protocol (http or https) to the domains!

Example: `PHOVEA_FORWARD_LINEUP=LineUp;lineup.caleydo.org;www.caleydo.org/tools/lineup`


## Build Docker image

The official [Docker image](https://hub.docker.com/r/caleydo/phovea_landing_page) is build continuously by Docker Hub. Locally you can run `docker build -t phovea_landing_page .` to build a Docker image.

***

<a href="https://caleydo.org"><img src="http://caleydo.org/assets/images/logos/caleydo.svg" align="left" width="200px" hspace="10" vspace="6"></a>
This repository is part of **[Phovea](http://phovea.caleydo.org/)**, a platform for developing web-based visualization apps. For tutorials, API docs, and more information about the build and deployment process, see the [documentation page](http://caleydo.org/documentation/).


[phovea-image]: https://img.shields.io/badge/Phovea-DevTools-lightgrey.svg
[phovea-url]: https://phovea.caleydo.org
