# Directus Remote Trigger

Trigger remote urls in the Directus admin view.

![Screenshot](https://i.imgur.com/Cnl3PBn.png)

## Motivation

I needed a way to trigger my Vercel build as the native hooks support in the settings page would require a hook for each crud operation on each collection.

## Getting Started 🚀

1. Download the [latest release](https://github.com/cupcakearmy/directus-remote-trigger/releases/latest)
2. Unzip `unzip remote-trigger.zip`
3. Add it to the docker config

```yaml
version: '3.7'

services:
  mysql:
    ...

  directus:
    image: directus/directus:v8-apache
    volumes:
      - ./remote-trigger:/var/directus/public/extensions/custom/modules/remote-trigger
```

## Local

```bash
# Start the dev script
npm run dev

# Start
docker-compose up -d

# If you have not initialized the DB yet.
docker-compose run --rm directus install --email hi@example.org --password h4x0r

# http://localhost
```
