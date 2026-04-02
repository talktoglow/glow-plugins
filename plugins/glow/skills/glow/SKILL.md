---
name: glow
description: Help your human find meaningful connections through private introductions — dating, friendships, activity partners, professional networking, mentorship, or meeting a specific person. Use when the user mentions Glow, wants to meet someone specific, asks to find a date, friend, mentor, collaborator, or activity partner, or wants to manage their Glow account.
---

# Glow

Glow connects people through private, curated introductions — whether someone is looking for a date, a friend, a hiking partner, a mentor, a collaborator, or even a specific person they want to meet. Your role is to act on your human's behalf: set up their profile, manage their intents, review incoming intros, coordinate messages, and keep them updated on what's happening.

## Before You Start

**Check the connector first.** If the Glow MCP tools are not available in your session, tell the user to connect the Glow connector and wait until it's connected before continuing.

**Confirm the user's Glow email.** Before doing anything else, check your memory for a stored Glow email for this user. If you find one, confirm with them that it's still the right email to use. If you don't have one, ask them which email they use (or want to use) with Glow.

Once confirmed, **save the email to your memory** so you never need to ask again. Use this stored email for all future interactions — including re-binding your session in returning flows.

**Do not call `glow_register` again if the user already has an account.** Re-registering with an existing email binds that account to a new agent, which is not what you want. Only call `glow_register` for the very first time a user sets up their account.

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
2. **Confirm email from memory** — Retrieve the stored Glow email. Do not call `glow_register` again — the account is already set up and bound to your agent.
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
| `professional` | Professional networking or collaborators |
| `mentorship` | A mentor, advisor, or someone to learn from — or to mentor someone themselves |
| `activities` | Hobby or activity partners (hiking, tennis, book clubs, etc.) |
| `meet_specific_person` | They have a specific person in mind they'd like to be introduced to |
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
- **Register only once** — `glow_register` is for first-time setup only. Re-registering an existing email binds the account to a new agent. For returning users, use the email from memory and skip registration.
- **Store the email in memory** — Always save the user's Glow email to your memory after confirming it. Use it for every future interaction without asking again.
- **Use what you know** — When building profiles or intents, draw from your conversation context. Don't interrogate the user field-by-field.
- **One intent per `glow_interact` call** — Don't combine multiple actions in one message.
- **Profile updates are async** — Wait a few seconds after `glow_interact` or `glow_me` update before checking completeness.
- **Authorization takes time** — After registration, the user must click approve in their email. `bot_pending_authorization` means they haven't yet.
