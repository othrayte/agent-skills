---
name: clarity
description: "Write or edit text so a human reader gets the point from the first words: key topic first in each sentence, one fact per sentence, related facts in one paragraph, and only terms the reader already knows. Use when writing or reviewing anything people read: code comments, commit messages, PR descriptions and comments, changelog entries, specs, plans, proposals, reports, Jira comments, status updates and stored memory facts. Also use when asked to make text clearer, shorter, simpler or human friendly, to 'remove AI slop', 'unsloppify', 'simplify this comment' or 'reduce to just' something."
---

# Clarity

Clear text puts the point in the first words and gives each fact its own sentence. Every word earns its place, and nothing the reader needs is dropped.

## Sentences

- **Key topic first.** Start each sentence with its core subject, the thing the sentence is about. In a code comment, the core subject is usually what the code controls. In a proposal or changelog, it is often the action or change. State the main fact next, then work sequentially from there.
- **One fact per sentence.** Start a new sentence for each new fact. If a fact doesn't fit in one sentence, it is not one fact.
- **Complete grammar.** Keep sentences self-contained and minimal, but in complete English. Write "Should I go ahead?", not "Go ahead?".
- **Minimal freestanding form.** State the fact plainly. Leave out reinforcing words ("exactly", "genuinely", "simply", "the one thing") and emphasis capitals.

## Paragraphs

- **Related facts together.** Keep each topic in one paragraph. Split a paragraph that covers two topics.
- **Most important first.** Open with the most important sentence: the answer, issue, change or result. Detail follows in the order the reader needs it.
- **Questions stand alone.** State each question plainly and separately, never buried in other prose.

## Words

- **Reader's terms only.** Use terms the reader already knows. Introduce any new term as concisely as possible before using it.
- **No invented names.** Use the established term or glossary. Ask before coining a name; past coinages like "notch", "fold" and "tube" confused the reader.
- **No bare IDs.** Pair an issue, task or question number with its name: "PROJ-123 (export dialog)", not "PROJ-123".
- **Plain words.** Prefer everyday words to academic ones.
- **Detail only where it matters.** Use the general term when the specifics don't change what the reader needs to know: "the build agent runs out of memory", not "the link.exe processes use all 32 GB of RAM on the Windows build agent".
- **Names say what a thing is.** Name a thing after what it is or how it is defined. "EnvelopeSurface" fails because every surface forms part of an envelope.

## Cut

Remove text that doesn't help the reader ("AI slop"):

- Negatives that add nothing: "as a plain CSS file, not a Rust API".
- What the reader would assume anyway: "runs on every push to `main`, and on nothing else".
- Reasons that don't matter or aren't the real reason.
- Hypotheticals about processes that don't exist.
- How we got here: earlier attempts, previous claims, task numbers from past iterations.
- Why one option was chosen over another. That belongs in commit messages or design docs.
- Anything already stated elsewhere in the same text or spec.

Concise is not incomplete. Keep what the reader needs to act: new defaults, how to switch a feature on, upgrade steps and numbers.

## By kind of text

- **Code comments.** Write for a future reader of the code as it is now. Drop any comment that only states what can be read from the code. Lead with what the code does and the problem it prevents, then the cause, then why it is safe. Leave change history and task IDs to commit messages. Delete a useless comment rather than expanding it. Keep comment edits small so the diff is easy to review.
- **Commit messages and PR text.** Lead with the change. Put rationale and history here, such as where a binary came from. Show small relevant code changes as fenced `diff` blocks.
- **Specs.** Describe only the behaviour wanted and, where not obvious, why. "Content is HTML-escaped" is enough; don't explain how escaping works.
- **Changelogs and other user-facing text.** Write for the user or operator, never the developer. Describe what the user observes, in their language and context.
- **Proposals and plans.** Describe the final state, with numbers. Start sentences with the action or change. Keep background to the minimum.
- **Stored facts and memories.** Write one fact as one sentence, in its minimal freestanding form.
- **Replies to the user.** Follow any reply structure the user's own instructions give.

## Before and after

| Before | After |
|---|---|
| Because the stamp raced between projects under /m, only the patch project now deletes it on Clean. | The patch project deletes the stamp on Clean. No other project deletes it, so parallel builds can't race on it. |
| `# Increased from 60 s to 600 s. The package manager takes a machine-wide lock during configure, so a second build waits for it, which looked like a hang and got killed.` | `# The configure timeout is 10 minutes to prevent waiting builds being killed. When another build holds the package manager's machine-wide lock, configure waits for it. A real hang still fails within 10 minutes.` |
| `# Admin-install Product.msi so we test the product as it is actually shipped, rather than relying on the app being installed on the host.` | `# Admin-install Product.msi` |
| The red dot marking a denied tool call now sits on the command line it belongs to rather than floating against the middle of a multi-line entry. | Aligned the denied tool call red dot with the first line of the command. |
| Close or abbreviated names find an existing thread; `#+name` always starts a new one. | Automatically fixes minor typos. Use `#+Name` to bypass typo handling and make a new thread. |
| `Drop the stamp on Clean so the patch re-runs on the next build. Safe here because only this one project deletes it; the same hook in the shared props file raced between projects under /m (PROJ-456).` | The comment is deleted. Its history goes in the commit message. |

## Reviewing text

When asked to review or tidy text:

1. Check each sentence. It should start with its core subject, carry one fact and use only known terms.
2. Check each paragraph. It should hold one topic, with the most important sentence first.
3. Cut anything on the Cut list, and any comment that only restates the code. Keep what the reader needs.
4. Make the smallest edit that fixes each problem, and keep the author's meaning.
