---
name: glow
description: Help your human find meaningful connections through private introductions — dating, friendships, activity partners, or professional networking. Use when the user wants to meet people, find connections, or manage their Glow account.
---

# Glow

> Help your human find meaningful connections through private introductions — dating, friendships, activity partners, professional networking, or meeting specific people.

Glow connects people through private, curated introductions. Your role is to act on your human's behalf: set up their profile, manage their intents, review incoming intros, coordinate messages, and keep them updated on what's happening.

## Before You Start

**Check the connector first.** If the Glow MCP tools are not available in your session, tell the user to connect the Glow connector and wait until it's connected before continuing.

**Check for an existing account.** Ask the user if they already have a Glow account before registering:
- If yes → call `glow_register` with their email to re-bind your session, then skip to the relevant flow below.
- If no → proceed with new user setup.

## MCP Tools

| Tool | Description |
|------|-------------|
| `glow_register` | Bind a human user to this session — always call this first |
| `glow_interact` | Natural language conversation for onboarding, profile updates, and general chat |
| `glow_intents` | Manage connection intents (list, create, update, pause) |
| `glow_intros` | Manage introductions (list, pending, active, accept, decline, close) |
| `glow_intros_messages` | Read and send messages in active intro threads |
| `glow_photos` | Manage photos (list, upload, delete, set privacy) |
| `glow_status` | Dashboard — pending intros, active connections, unread messages |
| `glow_settings` | Get/update notification and privacy settings |
| `glow_me` | View or update the user's profile summary |

## Typical Flows

### New User Setup

1. **Check connector** — Confirm Glow tools are available. If not, ask the user to connect the Glow connector.
2. **Register** — Call `glow_register` with the user's email and name.
3. **Share the PIN** — The response includes a 4-digit `authorizationCode`. Tell the user immediately — they must verify it matches the code in their email.
4. **Wait for approval** — User clicks approve in their email. Until then, all other tools return `bot_pending_authorization`.
5. **Onboard** — Use `glow_interact` to build their profile conversationally. Use what you already know about them — don't ask field-by-field. Bundle everything into as few calls as possible.
6. **Set intents** — Ask what kind of connections they're looking for (see Intent Types), then create them with `glow_intents`.
7. **Schedule check-ins** — Use your built-in scheduling tool to set up recurring Glow check-ins (see Scheduling below).

### Returning User

1. **Check connector** — Confirm Glow tools are available. If not, ask the user to connect the Glow connector.
2. **Re-bind session** — Call `glow_register` with their email to reconnect.
3. **Quick status** — Call `glow_status` for a dashboard overview.
4. **Review pending intros** — Call `glow_intros` with action `pending`.
5. **Check messages** — Call `glow_intros_messages` for the inbox.

### Reviewing Intros and Messages

1. Call `glow_intros` with action `pending` — present each new intro to the user.
2. Accept or decline with `glow_intros` based on the user's call.
3. Call `glow_intros_messages` — surface new messages in active intros.
4. Draft replies with the user's input and send via `glow_intros_messages`.
5. When an intro has run its course, close it with `glow_intros` action `close` and brief feedback.

## Intent Types

Intents define what the user is looking for. They can have multiple at once (e.g., dating + activity partners).

| Type | Use when the user wants... |
|------|---------------------------|
| `romantic_casual` | Casual dating, no commitment pressure |
| `exploratory` | Open to meeting people, no specific goal yet |
| `long_term` | A serious, committed relationship |
| `friends_only` | Platonic friendships |
| `professional` | Networking, mentors, or collaborators |
| `activities` | Hobby or activity partners (hiking, tennis, book clubs, etc.) |
| `other` | Anything that doesn't fit above |

After creating intents, ask if they have any preferences about who they want to meet and pass that through `glow_interact`.

## Scheduling Check-ins

After initial setup, use your built-in scheduling tool to set up recurring Glow check-ins so the user never misses a new intro or message.

Ask the user: *"How often would you like me to check in on your Glow matches and messages? I'd recommend once a day."*

Once confirmed, schedule a recurring task that:
1. Calls `glow_status` for an overview.
2. Calls `glow_intros` for any pending intros.
3. Calls `glow_intros_messages` for new messages.
4. Summarizes everything and prompts the user for any action needed.

## Key Rules

- **Connector first** — If Glow tools aren't available, ask the user to connect the Glow connector before doing anything else.
- **Register first** — `glow_register` must be called before any other tool. All others are gated behind it.
- **Use what you know** — When building profiles or intents, draw from your conversation context. Don't interrogate the user field-by-field.
- **One intent per `glow_interact` call** — Don't combine multiple actions in one message.
- **Profile updates are async** — Wait a few seconds after `glow_interact` or `glow_me` update before checking completeness.
- **Authorization takes time** — After registration, the user must click approve in their email. `bot_pending_authorization` means they haven't yet.
