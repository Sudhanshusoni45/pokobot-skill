# Pokobot skill

An agent skill that sets WhatsApp reminders with [Pokobot](https://www.pokobot.com), a reminder bot that lives in WhatsApp.

Ask your coding agent to remind you about something. It gives you a WhatsApp link with the reminder already typed in. Open it, press Send, and Pokobot pings you at the right time.

## Install

```bash
npx skills add Sudhanshusoni45/pokobot-skill
```

## Example

> **You:** Remind me on WhatsApp tomorrow at 10am to call the bank.
>
> **Agent:** Open this link and press Send. Pokobot will confirm in WhatsApp.
>
> https://wa.me/919407606251?text=Remind%20me%20tomorrow%20at%2010am%20to%20call%20the%20bank

## What it does

- One-time reminders: `Remind me in 2 hours to check the deploy`
- Repeating reminders: `Remind me every Monday at 9am to send the report`
- Any language you write in

The skill builds the link and nothing else. You list, change, or cancel reminders by texting Pokobot in the same chat.

## Security

The skill is one instruction file. It has no scripts, no API keys, and makes no network calls. Nothing happens until you press Send in WhatsApp, and you can read the whole message first.

## Cost

The skill is free. Pokobot is free for 7 days, then a paid plan that depends on your country. See [pricing](https://www.pokobot.com/pricing).
