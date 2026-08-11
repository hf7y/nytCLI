## NYTimes CLI

Read the latest stories from the New York Times directly in the terminal.

```
-s      Section, e.g. world, business, technology (defaults to home)
-l      Limit (number of items, defaults to all returned)
-a      Your NYTimes API key

Usage example: nytcli -s world -l 10 -a your_nyt_api_key_here
```

Go to [New York Times Developers](https://developer.nytimes.com/) to get your own API key
(enable the **Top Stories API** for it).

`-a` is optional if the key is available another way, checked in this order:

1. `-a` flag
2. `NYTCLI_API_KEY` environment variable
3. `~/.config/nytcli/api_key` (or `$XDG_CONFIG_HOME/nytcli/api_key`), one line, `chmod 600`

### 2026-08 repair

NYT retired the News API (`api.nytimes.com/svc/news/v3`) that this script
originally used, and `xmlstarlet` was a dependency for parsing its XML.
The script now calls the **Top Stories API v2** (JSON) instead and parses
the response with `jq`. Requires: `curl`, `jq`, `awk`, `fmt`.

Section names come from the Top Stories API, not the old News API — see
[the section list](https://developer.nytimes.com/docs/top-stories-product/1/overview).
