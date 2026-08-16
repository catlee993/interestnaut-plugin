# Interestnaut plugin for Claude

Connects Claude to your [Interestnaut](https://interestnaut.com) account so recommendations are
grounded in what you have actually reacted to and rated — across films, TV, books, games, music,
podcasts and creators — instead of being guessed from genre labels.

This repository contains only the plugin wrapper. The MCP server itself is hosted at
`https://api.interestnaut.com/mcp`.

## What it does

Claude gets read access to your taste history and, if you approve it, the ability to record
reactions and ratings for you. A typical exchange:

> **You:** I've got a free evening and I want something like *Annihilation* but not as bleak.
>
> **Claude:** *(reads your ratings and taste profile)* You rated *Arrival* 9 and *Under the Skin* 6,
> and your profile leans cerebral but away from despairing…

Because it can write as well as read, you can also keep your library up to date without leaving the
conversation — "mark that one as a 7", "I've seen this, it was fine".

## Tools

| Tool | What it does |
|---|---|
| `search_catalog` | Find an item by title across all seven media types |
| `get_item_details` | Descriptive metadata for specific items |
| `get_my_reactions` | Your reaction history, newest first, with ratings |
| `get_my_ratings` | Only the things you have scored 1–10, highest first |
| `get_taste_profile` | Your five taste axes and archetype |
| `react_to_item` | Record a reaction (write) |
| `rate_item` | Record a 1–10 rating (write) |

Reactions are `favorited`, `liked`, `watchlisted`, `meh`, `disliked` and `skipped`. They are not
interchangeable: **meh** means you consumed something and felt nothing, while **skipped** means you
passed without engaging and carries no opinion at all.

## Requirements

An Interestnaut account. You do not need one before installing — the sign-in screen can create one
from just an email address, and it will be waiting for you in the app afterwards.

## Authentication and privacy

Sign-in uses OAuth 2.1 with PKCE. You approve a consent screen listing exactly what you are granting,
and you can disconnect at any time from Claude's own connector settings without signing out of the
Interestnaut app.

What the connector deliberately does **not** send to Claude:

- Cover art or any image
- Plot summaries and synopses
- Your email address or password
- Anything from a private list
- Adult titles — excluded from this surface regardless of your in-app setting

Items come back as links to `app.interestnaut.com`, so the artwork and full detail stay on the page
where they belong.

Full policy: <https://interestnaut.com/privacy>

## Install

Claude Code or Cowork, via the official directory once listed. To add it directly meanwhile:

```
/plugin marketplace add catlee993/interestnaut-plugin
/plugin install interestnaut@interestnaut
```

If the install summary says `Run /reload-plugins to activate.`, run that too.

For Claude on the web or desktop, add the MCP server as a custom connector instead:

<https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Interestnaut&connectorUrl=https%3A%2F%2Fapi.interestnaut.com%2Fmcp>

## Support

<support@interestnaut.com>

## Licence

MIT for this wrapper. Catalog data comes from providers including TMDB, IGDB, Open Library and
MusicBrainz. This product uses the TMDB API but is not endorsed or certified by TMDB.
