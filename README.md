# Glow Plugin for Claude Cowork and Claude Code

Claude Cowork and Claude Code plugin for [Glow](https://talktoglow.com) — find meaningful connections through private introductions.

## Install

### Claude Desktop (Cowork)

1. Open Claude Desktop and navigate to Cowork.
2. Open the **Customize** tab and find the **+** button under **Personal Plugins**.
3. Hover over **+ Create Plugin** and select **Add Marketplace**.
4. In the URL field, enter `talktoglow/glow-plugins` and click **Sync**.
5. It may say "Still syncing" or spin briefly — that's normal.
6. Click the **+** button under **Personal Plugins** again.
7. Click **Browse Plugins** and navigate to **Personal**.
8. Find the **glow** plugin and click **+**. It will say "Installing will grant access to everything available to Cowork." Click **Continue**.
9. Tell Cowork what you're looking for — "I want to meet people in NYC" or anything else in natural language.

### Claude Code (CLI)

```shell
# Add the marketplace
/plugin marketplace add talktoglow/glow-plugins

# Install the plugin
/plugin install glow-plugins@glow

# Reload plugins
/reload-plugins

# Use it
/glow
```

## What it does

Glow helps your AI assistant find meaningful connections for you through private introduction: friendships, dating, activity partners, professional networking, or even meeting specific people!

The plugin connects to the [Glow Agent API](https://agents.talktoglow.com) via MCP, giving your assistant the ability to:

- Register and manage your Glow profile
- Set up connection intents (what you're looking for)
- Review and respond to introductions
- Message your matches

## Links

- [Glow website](https://talktoglow.com)
- [Agent API docs](https://agents.talktoglow.com)
- [Privacy policy](https://talktoglow.com/privacy-policy)
