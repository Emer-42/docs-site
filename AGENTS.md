# Pocket Timer docs

The user documentation of Pocket Timer, a small command-line focus timer, as Markdown pages in `docs/`.
Readers are developers who live in the terminal. The docs ship offline.

## Precedence
When instructions conflict, follow the first that applies:
1. Factory rules and gates (enforced by factory.sh; you cannot override them).
2. This file.
3. The approved `.factory/plan.md`.
4. The issue, then human feedback on the plan.
If you cannot satisfy the issue within these rules, deliver the closest version that complies and say why
in your phase's output file. Never stop without writing that file.

## Facts
- Product facts (commands, flags, keys, defaults, paths, versions, platforms) come only from the issue
  and the existing pages in `docs/`. Never invent one.
- If the issue omits a fact a reader needs (for example a prerequisite), leave it out and list it under
  Assumptions in the plan as an open gap. Do not fill it with a plausible guess.
- A new page must not contradict an existing page. If the existing pages already contradict each other,
  report it; do not fix it unless the plan says so.

## Language
- Pages are in English. An issue written in another language still produces English pages.
- A translation is a separate file, `<page>.<lang>.md` (e.g. `installation.es.md`), only when the issue
  or the approved plan asks for it. Commands, keys and file paths are never translated.

## Writing conventions
- One `# Title` per page, then `##` sections; `###` only inside a `##`. Sentence case for headings.
- No two headings on one page may have the same text (anchors would collide).
- Short paragraphs, second person ("you"), present tense.
- Commands in backticks: `pocket start`. Config keys as `key = value`.

## Links
- Only relative links to pages in `docs/`, e.g. `faq.md` or `configuration.md#daily-goal`.
- No `http://` or `https://` links. `gates/no-external-links.sh` rejects them. `docs/allowed-links.txt` is
  edited only by a human, even though it is under `docs/`. If an issue asks for an external link, plan
  the page without it and flag the conflict under Assumptions so the human sees it at plan approval.
- Anchor slug = heading lowercased, punctuation removed, spaces → `-` (`## Where is my history stored?`
  → `#where-is-my-history-stored`). Check the real heading before linking to it.
- Every page is listed in `docs/index.md` as `- [Title](page.md): one-line description.`, in reading
  order (install → start → configure → reference).
- Every page except `index.md` ends with `Back to [the index](index.md).`

## Check
- `python3 tools/check_links.py` must print `0 broken link(s)`. Run it exactly as written, one command
  per Bash call.
- Already enforced by the factory, so don't re-verify by hand: SCOPE, the gates, the link check.

## Finding severity (checker assigns, reviewer rejects on any high)
- high: broken link or anchor, page not in the index, invented fact, contradiction with another page,
  external URL, change outside the plan.
- medium: a reader-blocking gap (missing prerequisite, step that cannot be followed) or a convention breach.
- low: wording, ordering, style.

## Factory rules
- Phase state lives in `.factory/`: planner → `plan.md`, builder → `build.md`, checker → `report.md`,
  reviewer → `review.md`. Each phase writes only its own file plus, for the builder and checker,
  pages under `docs/`.
- Only the paths in SCOPE (factory.conf) may change. Do not touch factory.sh, lib/, gates/, .claude/,
  tools/, docs/allowed-links.txt or this file.
- Report only on the diff and the docs. Repo infrastructure (factory.conf telemetry, scripts) is out of
  scope for findings.
