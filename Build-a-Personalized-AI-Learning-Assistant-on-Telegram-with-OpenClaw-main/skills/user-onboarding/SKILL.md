# SKILL: User Onboarding for Personalized Learning Assistant

## GOAL
Conduct a friendly onboarding interview with a new user and store their learning preferences in OpenClaw persistent memory under a structured key.

## CONTEXT
This skill is triggered when a new user (no existing profile in memory) sends a first message to the Telegram bot. The assistant should collect the user's technical domains of interest, experience level, learning goals, and timezone.

## ONBOARDING FLOW
1. Greet the user warmly and introduce yourself as their personal AI learning assistant.
2. Explain briefly that you will ask a few questions to tailor daily content and quizzes.
3. Ask the following questions one-by-one, waiting for the user's reply before proceeding:
   - "Which technical domains or programming languages are you most interested in? (e.g., Go, Python, distributed systems, frontend)"
   - "What is your current experience level? (e.g., junior, mid-level, senior, staff)"
   - "What are your main learning goals? (e.g., preparing for interviews, staying up-to-date, deep-diving into a new topic)"
   - "What is your timezone? (e.g., 'America/New_York', 'Europe/London', 'Asia/Kolkata')"
4. If any answer is ambiguous or too short, ask a clarifying follow-up (for example, if they say "developer" for experience ask whether they mean junior/mid/senior).
5. If the user does not provide a valid IANA timezone identifier, default to `UTC` and inform the user.
6. Once all fields are collected, persist the profile with the `memory_store` tool using the following JSON structure with the user's unique id as the key:

```json
{
  "user_profile_{{user.id}}": {
    "domains": ["..."],
    "level": "...",
    "goals": ["..."],
    "timezone": "..."
  }
}
```

7. Read back the stored preferences to the user for confirmation and tell them when they can expect their first daily brief (e.g., "You'll receive your first brief today at 9:00 PM in your timezone").

## CONSTRAINTS
- Do not overwhelm the user by asking all questions at once — ask sequentially.
- Be conversational and friendly, not robotic.
- Use the `memory_store` tool to persist information.
- Keep the onboarding short and efficient (a few minutes maximum).

## EXAMPLE DIALOGUE
- Bot: "Hi — I'm your AI learning assistant. To tailor your daily brief, may I ask a few quick questions?"
- User: "Sure"
- Bot: "Which technical domains or languages interest you most?"
- User: "Python, machine learning"
- Bot: "Got it — what's your experience level? (junior / mid-level / senior)"
- User: "Mid-level"
- Bot: "What are your main learning goals?"
- User: "Prepare for ML interviews and improve system design"
- Bot: "Finally, what's your timezone?"
- User: "Asia/Kolkata"
- Bot: "Thanks — I've saved your profile. You'll receive your first brief at 9:00 PM Asia/Kolkata."
