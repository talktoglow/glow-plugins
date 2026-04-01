# Glow Plugins

Claude Code plugins for [Glow](https://talktoglow.com).

## Install and use the Glow plugin in Claude Code

```shell
# Step 1: Add the marketplace
/plugin marketplace add talktoglow/glow-plugins

# Step 2: Install the plugin
/plugin install glow@glow-plugins

# Step 3: Reload all plugins
/reload-plugins

# Step 4: Use the plugin
/glow:<skill> # Just type /glow and the available skills will be listed
```

IMPORTANT: This DOES NOT WORK with private repositories, so our existing 'Glow Platform' repo will not work in Cowork. We need a new public repository for this.

## Install and use the Glow plugin in Cowork

1. Open Claude Desktop App and navigare to Cowork
2. Open the 'Customize' tab and find the '+' button under 'Personal Plugins'
3. Hover over '+ Create Plugin' and select 'Add Marketplace'.
4. in the URL field, enter `talktoglow/glow-plugins` and click 'Sync'.
5. It may say 'Still syncing. Your marketplace will appear in the Personal tab when it's ready.' Or spin for a little while, that's okay.
6. Click the '+' button under 'Personal Plugins' again.
7. Click 'Browse Plugins' and navigate to 'Personal'
8. Find the 'glow' plugin and click '+', it will say 'Installing will grant access to everything available to Cowork.' Click 'Continue'.
9. Just tell cowork "I want to meet the glow team!" or anything else with natural language.


## Available Plugins

| Plugin | Description |
|--------|-------------|
| `glow` | Help your human find meaningful connections through private introductions — dating, friendships, activity partners, professional networking, or meeting the Glow team. Use when the user wants to meet people, find connections, meet the Glow team, or manage their Glow account. |

## Skills

- `/glow` — Help your human find meaningful connections through private introductions — dating, friendships, activity partners, professional networking, or meeting the Glow team. Use when the user wants to meet people, find connections, meet the Glow team, or manage their Glow account.
