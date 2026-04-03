# PR for daymade/claude-code-skills

## Title
add mindbreak skill (work break reminder)

## Body
Hi, I made a skill that reminds you to take breaks when you've been working with Claude Code for too long.

I noticed I kept skipping lunch and working late into the night when using Claude for coding — the back-and-forth is so fast you lose track of time. So I built this to fix that for myself, and figured others might want it too.

How it works:
- A hook logs a timestamp every time you send a message
- The skill reads those timestamps and figures out how long you've been working continuously
- If you've been at it for 45+ minutes, it adds a short reminder at the end of the response
- It also catches meal times and late-night sessions
- If you step away for 15+ minutes, the timer resets so it won't bug you when you come back

It's not a pomodoro timer — no forced breaks, just a gentle nudge. You can say "don't remind me" to turn it off for the session.

Tested it for a few days on my own setup, works well. Repo: https://github.com/ZKXSparke/mindbreak-skill

---

# PR for mhattingpete/claude-skills-marketplace

## Title
add mindbreak (break reminder skill)

## Body
A skill that tracks how long you've been working with Claude Code and reminds you to take breaks.

Uses a hook to log message timestamps, then calculates continuous work time. Reminds you after 45min, at meal times, and late at night. Won't nag you after a break.

Repo: https://github.com/ZKXSparke/mindbreak-skill
