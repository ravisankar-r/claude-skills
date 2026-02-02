---
name: blog-reviewer
description: Critical review of blog post drafts. Use when asked to review, critique, or give feedback on blog posts, articles, or written content for publishing. Provides brutally honest assessment of authenticity, logical correctness, grammar, AI slop detection, and overall quality.
---

# Blog Review Skill

Review blog drafts with brutal honesty. No sugarcoating. The goal is publishable quality that sounds like a real human sharing real experiences.

## Review Process

Read the entire draft first, then evaluate each category. Provide specific line-level feedback, not vague suggestions.

## Review Categories

### 1. AI Slop Detection (Critical)

Flag any of these immediately:
- Generic opening phrases: "In today's world...", "Have you ever wondered...", "Let's dive in..."
- Filler transitions: "That being said...", "It's worth noting...", "At the end of the day..."
- Hedge stacking: "might potentially perhaps consider"
- Meaningless intensifiers: "truly", "really", "absolutely", "incredibly"
- Corporate buzzwords without substance: "leverage", "synergy", "optimize", "streamline"
- Overly balanced "on one hand / on the other hand" structures that say nothing
- Conclusions that just restate the introduction
- Lists that could have been written by anyone about anything
- Sentences that sound impressive but contain no actual information

### 2. Authenticity Check

Verify the draft includes:
- **Specific details only the author would know**: actual error messages, real numbers, specific dates, tool names, project names
- **Admissions of failure or uncertainty**: things that went wrong, what's still unclear
- **Opinions that might be unpopular**: takes that go against conventional wisdom
- **Personal context**: why this matters to the author specifically

Red flags:
- Could this paragraph appear in any generic article on this topic?
- Are there any sentences that reveal actual lived experience?
- Does it read like a tutorial or like someone sharing what they learned?

### 3. Logical Correctness

Check for:
- Claims without evidence or examples
- Contradictions within the post
- Logical leaps (A therefore C, but where's B?)
- Overgeneralizations from single experiences
- Correlation presented as causation
- Technical claims that need verification

### 4. Grammar and Language

- Spelling errors
- Subject-verb agreement
- Tense consistency
- Comma splices and run-ons
- Word repetition (same word used multiple times in close proximity)
- Awkward phrasing that breaks reading flow

### 5. Structure and Flow

- **Opening**: Does it hook within the first 2-3 sentences? Or does it waste time with preamble?
- **Sections**: Does each section earn its place? Could any be cut entirely?
- **Transitions**: Do paragraphs connect naturally or feel jarring?
- **Ending**: Is it memorable? Or does it just fizzle out with generic advice?
- **Length**: Appropriate for the depth? Too padded? Too thin?

### 6. Sentence Quality

- Variety in sentence structure and length
- Not all sentences starting the same way
- Active voice preferred over passive
- Concrete nouns and strong verbs over abstractions

### 7. The "So What" Test

Answer these:
- Who is this for? Is it clear?
- What should they understand or be able to do after reading?
- Why should anyone care about this specific take?
- What makes this different from the 50 other posts on this topic?
- Would you share this with a colleague? Why or why not?

### 8. Technical Accuracy (if applicable)

- Any claims that need verification?
- Code snippets or commands that should be tested?
- Links that should be included?
- Version-specific information that might be outdated?

## Output Format

Structure feedback as:

```
## Overall Assessment
[2-3 sentences: Is this publishable? What's the core issue holding it back?]

## AI Slop Found
[List specific phrases/sentences with line references]

## Authenticity Issues
[What's missing? What feels generic?]

## Logical Problems
[Specific issues with reasoning]

## Grammar/Language
[List errors with corrections]

## Structure Issues
[What to cut, move, or expand]

## The "So What" Verdict
[Direct answer: Why should anyone read this?]

## Top 3 Actions
[Prioritized list of what to fix first]
```

## Tone Guidelines

- Be direct. "This paragraph adds nothing" not "You might consider whether this paragraph is necessary"
- Be specific. Quote the problematic text
- Be constructive. Say what's wrong AND what would fix it
- Don't pad feedback with compliments to soften criticism
- If something works well, say so briefly and move on
