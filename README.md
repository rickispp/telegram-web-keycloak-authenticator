# Telegram Web Keycloak Authenticator

![Keycloak-with-telegram-logo.png](docs/Keycloak-with-telegram-logo.png)

## Contents

*   [What is this?](#what-is-this)
*   [Getting started](#getting-started)
    *   [Requirements](#requirements)
    *   [Install](#install)
    *   [Usage](#usage)
*   [Contribute](#contribute)

## What is this?

The goal of this project is to implement seamless Keycloak authorization via [Telegram Login Widget](https://core.telegram.org/widgets/login).

There are several projects that implement a similar feature but all of them require either user interaction with the bot in the Telegram interface (going to the Telegram application and entering code or generating a link to an external application). Such solutions are good, but a process is inconvenient in many cases and often requires the implementation of additional logic outside Keycloak.

This project, on the other hand, provides the ability to log in without leaving the browser in just a few clicks and does not require the user to perform any special actions.

In addition, the possibilities are not limited only to Browser Flow. You can easily set up authorization through external applications using Implicit Flow with data validation on the Keycloak side.

## Getting Started

For a quick introduction to the features, you can deploy a demo project from this repository using docker-compose. This will deploy Keycloak with this plugin and import a demo realm with pre-configured flows.

### Requirements

* Java 17 or higher installed
* Docker and docker-compose
* You have a Telegram bot and you know its username and token

### Install

Use git to clone this repository into your computer.

```shell
git clone https://github.com/rickispp/telegram-web-keycloak-authenticator
```

Build project

```shell
./gradlew build
```

Run docker compose

```shell
docker-compose up
```

Send to [@BotFather](https://t.me/BotFather) command for install domain
```shell
/setdomain http://keycloak.localhost
```

Then configure authenticator in Keycloak
* Go to the page http://keycloak.localhost/admin/master/console/#/demo/authentication and log in with the `admin/admin` credentials.
* Select a flow named `Copy of browser`
* Find the `Telegram Web Login Widget` and click on the `Settings` button
* Fill in the fields `Alias`, `Bot Token` and `Bot username` without `@` (e.g. `sample_bot`, not `@sample_bot`) and save configuration

![Bot config](./docs/bot-config.png)

### Usage

* After deployment and configuration, you can go to the page http://keycloak.localhost/realms/demo/account/

* You will see an authorization page that should have an authorization button via Telegram.

![Login page](./docs/login-page.png)

* When you click on the button, the Telegram authorization process will start

![Login page](./docs/telegram-auth-popup.png)

* After successful authorization, Keycloak will prompt you to enter your email (because this parameter is required in the demo realm settings).

![required-email-action.png](docs/required-email-action.png)

* Finally, by entering an email, you will be redirected to a page with user data. The authorization process has been completed, and a new user has been created in keycloak based on the data received from Telegram.

![authorized-user.png](docs/authorized-user.png)

## Contribute

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.