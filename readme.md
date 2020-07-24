# Directus Remote Trigger

Trigger remote urls in the Directus admin view.

## Motivation

I needed a way to trigger my Vercel build as the native hooks support in the settings page would require a hook for each crud operation on each collection.

## Getting Started 🚀

![Screenshot](https://i.imgur.com/Cnl3PBn.png)

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
