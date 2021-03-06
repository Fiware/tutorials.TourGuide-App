# FIWARE Tour Guide Application

[![License: MIT](https://img.shields.io/github/license/FIWARE/tutorials.TourGuide-App.svg)](https://opensource.org/licenses/MIT)
![](https://nexus.lab.fiware.org/static/badges/statuses/deprecated.svg)
[![Support badge](https://img.shields.io/badge/tag-fiware-orange.svg?logo=stackoverflow)](https://stackoverflow.com/questions/tagged/fiware)


> This repository is now archived. Since this application was created, a series of self-contained tutorials on each
> generic enabler have been created and are maintained separately for **NGSI-v2** and **NGSI-LD**.
>
> -   The [Step-by-Step Tutorials](https://github.com/FIWARE/tutorials.Step-by-Step) Complete collection of tutorials for the FIWARE ecosystem 
>     for **NGSI-v2** developers
> -   The [Linked Data Tutorials](https://github.com/FIWARE/tutorials.NGSI-LD)  Complete collection of tutorials for the FIWARE ecosystem 
>     for **NGSI-LD** developers
>
> More links and information can be found within the [FIWARE Catalogue](https://github.com/FIWARE/catalogue)

[FIWARE Tour Guide App](https://github.com/Fiware/tutorials.TourGuide-App) was a Node.js sample application used in the
[FIWARE Tour Guide](http://www.fiware.org/tour-guide/) to show real code working with the Generic Enablers integrated.

This application is a smart, context-aware application which allows to manage large Restaurant chains which are
operating worldwide. Is intended to both franchise managers and to customers. To this aim, the main functionalities
provided by the application are:

-   Admit Customer reservations
-   Register customer reviews
-   Real-time control of different parameters at each restaurant location (temperature and humidity)
-   Restaurant geo-location
-   Short time historic data of the different parameters monitored
-   Publication of open data concerning the most relevant information about the different restaurant locations, grouped
    by different properties

**Table of Contents**

-   [Architecture](#architecture)
-   [How to build and install](#how-to-build-and-install)
    -   [Installation and Administration Guide](#installation-and-administration-guide)
    -   [Deploying on a Cloud Fiware Lab Instance](#deploying-on-a-cloud-fiware-lab-instance)
-   [User and Programmers Manual](#user-and-programmers-manual)
    -   [Miscellaneous configuration](#miscellaneous-configuration)
        -   [How to configure a Context Provider in Orion](#how-to-configure-a-context-provider-in-orion)
        -   [How to configure Cygnus in TourGuide](#how-to-configure-cygnus-in-tourguide)
        -   [How to generate a new restaurant data image](#how-to-generate-a-new-restaurant-data-image)
        -   [How to run Feeders for the data image generation](#how-to-run-feeders-for-the-data-image-generation)
        -   [How to retrieve an Oauth Token to use the API](#how-to-retrieve-an-oauth-token-to-use-the-api)
-   [API Overview](#api-overview)
-   [End to End tests](#end-to-end-tests)
-   [Feedback](#feedback)

## Architecture

![Architecture diagram](https://github.com/Fiware/tutorials.TourGuide-App/blob/develop/doc/img/archDiagram.png?raw=true "Architecture diagram")

It includes (for the moment) the following components:

-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/core.svg)](./core/README.md) [Orion Context Broker](https://github.com/telefonicaid/fiware-orion/),
    providing the NGSIv2 interfaces.
-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/iot-agents.svg)](./iot-agents/README.md) [Backend Device Management - IDAS](https://github.com/FIWARE/catalogue/blob/master/iot-agents/README.md), to connect
    IoT devices (temperature & humidity).
-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/core.svg)](./core/README.md) [Cygnus](https://github.com/telefonicaid/fiware-cygnus) for the
    [Cosmos ecosystem](https://github.com/ging/fiware-cosmos) to give persistance to the context
    data (using its sinks).
-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/security.svg)](./security/README.md) [Authorization PDP - AuthZForce](https://github.com/authzforce/server), to get
    authorization decisions based on authorization policies.
-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/security.svg)](./security/README.md) [PEP Proxy - Wilma](https://github.com/ging/fiware-pep-proxy), to add authentication and authorization security to
    the application.
-   [![](https://nexus.lab.fiware.org/repository/raw/public/badges/chapters/security.svg)](./security/README.md) [IDM KeyRock](https://github.com/ging/fiware-idm), covering the user profile management, authorization and
    authentication among others.

## How to build and install

This project integrates a set of Generic Enablers using those enablers inside [docker](https://github.com/docker/docker)
containers. It also comes with restaurants, reviews and reservations loaded to start working out of the box, as well as
users and organizations to play with it.

For that purpose, [docker](https://github.com/docker/docker) and [docker-compose](https://docs.docker.com/compose/) are
required.

![Compose Diagram](https://github.com/Fiware/tutorials.TourGuide-App/blob/develop/doc/img/composeDiagram.png?raw=true "Compose Diagram")

### Installation and Administration Guide

Detailed information of how to start this environment can be found
[here](https://github.com/Fiware/tutorials.TourGuide-App/tree/develop/docker/images/tutorials.tourguide-app).

### Deploying on a Cloud Fiware Lab Instance

You can deploy an instance of the Fiware TourGuide App in a cloud instance using
[Docker-machine](https://docs.docker.com/machine/). Detailed information of this process can be found in the following
documentation:

-   [Installing Docker on FIWARE Cloud](http://simple-docker-hosting-on-fiware-cloud.readthedocs.io/)

## User and Programmers Manual

The complete user guide of this environment is available at
[Readthedocs](http://fiwaretourguide.readthedocs.org/en/latest/fiware-tour-guide-application-a-tutorial-on-how-to-integrate-the-main-fiware-ges/fiware-tour-guide-application-a-tutorial-on-how-to-integrate-the-main-fiware-ges/).

### Miscellaneous configuration

#### How to configure a Context Provider in Orion

[Here](https://github.com/Fiware/tutorials.TourGuide-App/blob/develop/doc/ContextProvider.md) you can find a simple
example of how to configure a Context Provider using Orion.

#### How to configure Cygnus in TourGuide

As Cygnus can publish in several third-party storages,
[here](https://github.com/Fiware/tutorials.TourGuide-App/blob/develop/docker/cygnus/README.md) we explain where you
should add your credentials for each source to publish the TourGuide data.

#### How to generate a new restaurant data image

The image provided is based on
[Euskadi Open Data information](http://opendata.euskadi.eus/contenidos/ds_recursos_turisticos/restaurantes_sidrerias_bodegas/opendata/restaurantes.json).
The image is already loaded, but we provide information on
[how to generate it yourself](https://github.com/Fiware/tutorials.TourGuide-App/blob/develop/docker/images/tutorials.tourguide-app.restaurant-data/Readme.md).

#### How to run Feeders for the data image generation

Find out how to load information into a new image using the
[Tourguide feeders](https://github.com/Fiware/tutorials.TourGuide-App/tree/develop/server/feeders).

#### How to retrieve an Oauth Token to use the API

Every TourGuide API request must be authenticated. For that purpose, we provide
[a simple script](https://github.com/Fiware/tutorials.TourGuide-App/tree/develop/server/misc) to generate an Oauth Token
based on a username and password of the
[preloaded data](https://github.com/Fiware/tutorials.TourGuide-App/tree/develop/docker/images/tutorials.tourguide-app#idm-users-organizations-apps-roles-and-permissions).

## API Overview

The application provides a RESTful API with different routes and functions that covers the functionalities described
above:

-   [FIWARE TourGuide RESTful API](http://docs.tourguide.apiary.io)

## End to End tests

To run the end to end tests, you will need to first download the repository, then browse to `server` folder and run:

```console
$ npm install
$ grunt
```

[Grunt](https://github.com/gruntjs/grunt) will run `jshint` and `jscs` linters as well as start a full TourGuide
environment and run the End to End [jasmine-node](https://github.com/mhevery/jasmine-node) tests.

