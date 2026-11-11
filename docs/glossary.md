# Glossary

The four terms Pocket Timer uses everywhere, in one place.

## Session

A session is a countdown you start with `pocket start`. Pocket Timer counts down in the terminal and rings when it ends. Its length is set by `session_minutes`; see [session length](configuration.md#session-length).

## Break

A break is a rest you start with `pocket break`. Breaks never count toward your daily goal. See [taking a break](getting-started.md#taking-a-break).

## Daily goal

The daily goal is how many sessions make a full day, set with `daily_goal = 8`. Run `pocket today` to see your progress. See [daily goal](configuration.md#daily-goal).

## History

The history is the record of your sessions and breaks, kept in `~/.pocket/history.jsonl`, one line per session or break. See [where your history is stored](faq.md#where-is-my-history-stored).

Back to [the index](index.md).
