# Skill: Create or Update User Profile

**Trigger:** User says "create my profile", "who am I", "update my user file", "user.md", or this is their first session and no `artifacts/user.md` exists yet.

## What This Skill Does

Interviews the user to build a comprehensive profile that gives the Jarvis deep context on who they are, what they care about, and what is blocking them. Saves the result to `artifacts/user.md`.

If `artifacts/user.md` already exists, read it first and ask what has changed.

## Interview Flow

Ask these questions **one at a time**. Wait for the user to answer each one before moving to the next. Do not dump all questions at once. Keep a conversational, warm tone. If the user gives a short answer, ask a follow-up to go deeper.

### Part 1: Who You Are

1. "What is your name and what do you do? Give me the real version, not the LinkedIn version."
2. "What are you most excited about right now in your work or life?"
3. "What are your core values or non-negotiables? The things that, if violated, would make you walk away from a deal or opportunity."
4. "How do you make decisions? Are you gut-first, data-first, advice-first? What is your process when something big is on the line?"

### Part 2: Your Operation

5. "Describe your business or career situation right now. What is the honest state of things?"
6. "Who are the most important people in your professional life right now? (Partners, clients, team members, mentors, investors)"
7. "What tools and systems do you currently use to stay organized? (Even if the answer is 'nothing,' that is useful information.)"

### Part 3: Your Strategic Blocker

8. "What is the single biggest thing blocking you right now? The thing that, if you solved it, would unlock the most progress."
9. "Why is it blocked? What have you tried? What is actually in the way?"
10. "If you had a brilliant advisor sitting next to you right now who knew everything about your situation, what would you ask them?"

### Part 4: Where You Are Going

11. "What does success look like for you in 90 days? Be specific."
12. "What is the scariest thing you are not saying right now, or will not admit to yourself?"

## Output

After the interview, compile everything into `artifacts/user.md` with the following structure:

```markdown
# User Profile

*Last updated: YYYY-MM-DD*

## Who I Am
[Name, role, background from questions 1-2]

## Values and Decision-Making
[From questions 3-4]

## Current Situation
[From questions 5-7]

## Strategic Blocker
[From questions 8-10]

## 90-Day Vision
[From questions 11-12]
```

After saving, tell the user: "Your Jarvis now knows who you are. Every future conversation will be informed by this context. You can update this any time by saying 'update my profile.'"

Then ask: "Would you like me to help you think through your strategic blocker right now? I can draft a plan based on what you just told me."

If they say yes, create a second artifact at `artifacts/YYYY-MM-DD-strategic-blocker-plan.md` that breaks their blocker into actionable steps.
