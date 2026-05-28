# SKILL: Daily Tech Brief and Quiz Generation

## GOAL
Generate a high-quality, personalized daily tech brief for a user and send it via Telegram. The brief must include exactly 5 interview questions and 3–5 technical tidbits, tailored to the user's stored preferences.

## CONTEXT
This skill is triggered by a cron job (scheduled at 21:00 daily in the user's timezone) and receives the user's ID. It must read the user's profile from memory and use `web_search` to collect fresh content relevant to the user's domains.

## GENERATION WORKFLOW
1. Retrieve the user's profile from persistent memory using key `user_profile_{{user.id}}`.
2. For each domain listed in `domains`, perform a `web_search` with queries emphasizing recent/fresh content. Example queries:
   - "latest [domain] developer news 2025"
   - "2025 tutorials [domain] performance tips"
   - "best practices [domain] 2025"
   Use any available freshness parameter to prioritize recent articles.
3. Read top results using `web_fetch` as needed and synthesize 3 to 5 short technical tidbits — concise, useful facts or insights derived from recent sources.
4. Generate exactly 5 interview questions tailored to the user's `domains` and `level`:
   - Ensure relevance to domains.
   - Match difficulty to the user's level (do not present senior-level system design to juniors).
   - Include a mix of conceptual, coding/algorithmic, system-design, and behavioral questions.
   - Avoid repeating questions asked recently; use memory to track topics if possible.
5. Format the final message using Telegram Markdown as follows:

```
🦞 *Your Daily Tech Brief* — [Date]

━━━━━━━━━━━━━━━━━━━━
🧠 *Interview Questions*
━━━━━━━━━━━━━━━━━━━━

*Q1 [Type — Domain]*
[Question 1 Text]

*Q2 [Type — Domain]*
[Question 2 Text]

*Q3 [Type — Domain]*
[Question 3 Text]

*Q4 [Type — Domain]*
[Question 4 Text]

*Q5 [Type — Domain]*
[Question 5 Text]

━━━━━━━━━━━━━━━━━━━━
💡 *Today's Tidbits*
━━━━━━━━━━━━━━━━━━━━

• [Tidbit 1]

• [Tidbit 2]

• [Tidbit 3]

(Optional • [Tidbit 4])

━━━━━━━━━━━━━━━━━━━━
Reply *answers* to get feedback, or *more* for extra questions.
```

## CONSTRAINTS
- Exactly 5 questions must be generated.
- 3–5 tidbits only.
- Use `web_search` and prefer recent content.
- Message must be Markdown-formatted for readability on mobile.
- The skill must run autonomously when triggered by cron.
