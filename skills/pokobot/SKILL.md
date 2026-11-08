---
name: pokobot
description: Sets a reminder that arrives on the user's WhatsApp, using Pokobot. Use when the user wants to be reminded, pinged, or nudged on WhatsApp or on their phone, including one-time reminders, repeating reminders, deadlines, follow-ups, or a nudge to come back to something later. Creates a WhatsApp link with the reminder already typed in. The user taps it and presses Send.
---

# Pokobot WhatsApp reminders

[Pokobot](https://www.pokobot.com) is a reminder bot that lives in WhatsApp. People text it in plain language and it messages them at the right time. There is no app to install.

This skill turns a request into a WhatsApp link. The link opens a chat with Pokobot with the reminder already typed in. The user presses Send and Pokobot sets the reminder.

The skill makes no API calls and needs no API key. Nothing is set until the user presses Send, and you cannot see the chat afterwards.

## When to use

- "Remind me on WhatsApp to call the bank tomorrow at 10am"
- "Ping me in 2 hours to check this deploy"
- "Nudge me every Monday at 9am to send the report"

Do not use it for:

- Reminders for another person. The link sets a reminder for whoever presses Send.
- Listing, changing, or cancelling reminders. The user does that by texting Pokobot in the same chat.

## Steps

### 1. Work out what and when

You need a task and a time. If the time is missing, ask one short question.

Pokobot reminds at a time. It cannot watch for an event such as "when the build finishes", so ask the user what time to use instead.

### 2. Write the message

Write one reminder per message, starting with "Remind me".

- Keep the time exactly as the user said it: `tomorrow at 10am`, `in 2 hours`, `every Monday at 9am`. Do not convert it to another timezone.
- Make the task make sense on its own, because the user will read it later without this conversation. Write `review the checkout PR in the billing repo`, not `look at this`.
- Use the user's language. Pokobot understands and replies in any language.
- Never include passwords, API keys, or other secrets. The text passes through WhatsApp and Pokobot.

If the user wants several reminders, make one link for each.

### 3. Build the link

```
https://wa.me/919407606251?text=<message>
```

Percent-encode the message the same way JavaScript's `encodeURIComponent` does. Spaces become `%20`, not `+`. Characters such as `&`, `#`, and `?` must be encoded too, or the message gets cut off.

| Message | Encoded |
| --- | --- |
| `Remind me tomorrow at 10am to call the bank` | `Remind%20me%20tomorrow%20at%2010am%20to%20call%20the%20bank` |
| `Remind me at 5pm to review PR #42 & merge it` | `Remind%20me%20at%205pm%20to%20review%20PR%20%2342%20%26%20merge%20it` |

### 4. Give it to the user

Show the full link as a plain URL, so it is clickable in a terminal, and show the message it will send. Reply in this shape:

> Open this link and press Send. Pokobot will confirm in WhatsApp.
>
> https://wa.me/919407606251?text=Remind%20me%20tomorrow%20at%2010am%20to%20call%20the%20bank
>
> It will send: `Remind me tomorrow at 10am to call the bank`

Do not say the reminder is set. It is only set once the user presses Send and Pokobot confirms.

## More Pokobot facts

Share these only when they help.

- **First message:** Pokobot says hello, names the timezone it guessed from the phone number, and acts on the reminder. To fix the timezone, the user texts `timezone <their city>`.
- **Repeats:** daily, weekly, monthly, or more often, such as every 2 hours. Fast repeats can pause overnight: `Remind me every 2 hours between 9am and 8pm to drink water`.
- **Managing reminders:** the user can list, change, snooze, or cancel by texting Pokobot in the same chat. Texting `help` shows the commands.
- **Cost:** 7 days free, then a paid plan that depends on the country. When the trial ends, reminders stop until the user subscribes. Current prices are at https://www.pokobot.com/pricing.
