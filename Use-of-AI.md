# Use of AI, LLMs, and Code Generation Tools in LandSandBoat

```
* This post was written by hand, zhuzhed up by AI, and then manually proofread, fact-checked, and
polished by hand, exactly how it should be.

Even with careful oversight, I still had to alter the tone, correct statements, remove ligatures,
remove outright lies and hallucinations, replace the telltale "em dashes"'s that AI is so fond
of (—), etc.

It's unknown if it would have been faster for me to write the document entirely by hand, or if using
AI forced me to spend much more time in editing and verification than I otherwise would have...

Worth thinking about.
```

## Introduction

AI-assisted coding tools like ChatGPT, Claude, Copilot, and Cursor are now a part of most developers'
workflows. Their use is inevitable in an open-source project like LandSandBoat.

However, these tools are not a substitute for understanding what you're doing, and they cannot be 
trusted to write, test, or reason about code on your behalf. If you submit code written or heavily 
influenced by AI, you are still responsible for the result. That means understanding it, testing it, 
and verifying that it's correct and appropriate for the project. The code you submit is still going
to be read many times over by reviewers and future contributors, and it should be of sufficient
quality that it can stand up to this scrutiny. 

We've started to see submissions that clearly came straight from AI with minimal oversight, which 
we'll bluntly call **AI slop**. This wastes reviewers' time and degrades the quality of the codebase. 
If you're using AI, please do so carefully and responsibly.

## When is AI suitable?

### Enhanced Auto-Complete / IntelliSense

AI tools that provide inline suggestions, such as Copilot or Cursor, can be very effective when used 
as smart autocomplete.

When they assist you in filling in small patterns, repetitive code, or documentation, they can boost 
productivity without sacrificing correctness - provided you understand what's being inserted.

### Generating well-documented, boilerplate code

It's fine to let AI help you lay out template code, data structures, or simple glue logic - as long 
as you review, test, and annotate it yourself.

Think of AI as a very enthusiastic intern, not a competent developer. It can save you time on setup,
but you still need to ensure everything is correct, idiomatic, and fits within LSB's conventions and
expectations.

### Turning bullet points into prose

AI is a decent writing assistant. If you use it to expand notes or ideas into sentences (like 
documentation or design notes), make sure to proofread for:

**Truth**: Is what it says actually correct?

**Clarity**: Does it make sense and say what you mean?

**Tone**: Does it match the project's communication style?

The final words and ideas should always be yours, not the model's.

## When is AI not suitable?

### Writing new or novel logic

AI has no genuine understanding of your codebase or game systems. It guesses patterns based on text 
it has seen before - often wrong, often dangerously so.

If you're implementing something new (for example, an unimplemented quest or unique gameplay
mechanic), AI will produce plausible-sounding nonsense. These "confidently wrong" outputs cause
subtle bugs that waste time and break things down the line, leading us to have to manually fix your 
submission ourselves, or remove it entirely.

### FFXI-specific logic

AI doesn't understand FFXI's game rules, quirks, client interactions, or behaviors. It doesn't know 
how retail behaves, what our packet flow looks like, or why things are implemented the way they are.

Quite obviously, AI doesn't have access to retail or the FFXI client in general.

At best, it can and will produce vague approximations that seem like they could be right but are
completely wrong in-game.

### LSB-specific logic and patterns

These models were not trained on LandSandBoat. LandSandBoat moves at a very fast pace and these
models are often many months or years out of date for their training context. The closest they
might have seen is the DarkStar Project, which is long outdated and architecturally very different
in many places.

They may also have drawn patterns from more popular but unrelated projects that have C++/Lua interop
or different Lua versions; like Windower, Ashita, Roblox, Luau, Lua 5.3, WoW Addons with Eluna, etc.
all of which demonstrate very different qualities, idioms, runtime behaviors, and use different
internal/external structures and libraries, etc.

If you ask AI for help with something deeply tied to LSB's internals, it will almost certainly give 
you incorrect or obsolete code. You can use it to brainstorm, but the real work: testing, 
validation, and understanding - must be yours.

## Final Thoughts

AI tools can be useful assistants, but they're not developers. They don't read and understand the 
codebase, they're unable to correctly verify their work, and they don't care about breaking changes 
or incorrect logic - you do.

If you choose to use AI, that's fine - just use it responsibly:

* Always read what it outputs.
* Always test what it changes.
* Always understand what it does.

**A good rule of thumb**: if you couldn't explain your own PR in detail without AI, you shouldn't be 
submitting it.
