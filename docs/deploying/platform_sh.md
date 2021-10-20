---
id: platform_sh
title: Deploy with Platform.sh
description: "Deploying with Platform.sh"
slug: /platform_sh
---

## Why Platform.sh

Platform.sh is currently the quicker way to get a production Papercups environment up and running!

If you've never heard of [Platform.sh](https://platform.sh) or what it does, feel free to check out this page that provides a quick gist of the product: https://platform.sh/product/

## Prerequisites

None, really. If you don't have a Platform.sh account one will be created for you in the setup wizard.

## Step By Step Installation

<a href=
  "https://console.platform.sh/projects/create-project/?template=https://github.com/papercups-io/papercups&amp;utm_campaign=deploy_on_platform?utm_medium=button&amp;utm_source=affiliate_links&amp;utm_content=https://github.com/papercups-io/papercups"
  target="_blank" title="Deploy with Platform.sh"><img src=
  "https://platform.sh/images/deploy/deploy-button-lg-blue.svg" /></a>

1. Click on the button above to go to the app creation screen.
2. Follow the steps in the wizard.
3. **Wait**. Note that this may take a few minutes, so resist the urge to refresh the page or restart the process :)
4. Once completed, you will be forwarded to the management console where you'll get a link to the actual Papercups environment.

## Adding Redis

If you want to add a Redis instance to your installation, simply uncomment in `.platform/services.yaml`:
```
cache:
    type: redis:6.0
```
And `.platform/applications.yaml` uncomment the line for the relationship:
```
  relationships:
    cache: 'cache:redis'
```
and the environment variable:
```
  variables:
    env:
      REDIS_URL: redis://cache.internal
``` 

## Upgrading Papercups on Platform.sh

It is always better to do this on a development environment rather than directly on production so if you have the `platform` CLI installed:
```
platform branch upgrade
platform source-operation:run upstream-update
```
and after you tested the development environment 
```
platform merge upgrade
```
Otherwise you can also simply use git to pull changes from the upstream and push them to your Platform.sh git remote.
