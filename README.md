# clabot-config

Org-wide configuration for [cla-bot](https://colineberhardt.github.io/cla-bot/), which checks that every committer on a pull request to a `crabtalk` repository has signed the CLA.

cla-bot reads `.clabot` from this repository for **every** repo in the org, in preference to any `.clabot` in the repo itself. There is one config and one contributor list; individual projects carry neither.

## Signing

The agreement is [`CLA.md`](CLA.md). One signature covers every CrabTalk, LLC project, MIT and Apache-2.0 alike — the CLA is the inbound grant to the company, and each repository's LICENSE is what we distribute under.

A contributor comments on their pull request:

> I have read the CLA document and I hereby sign the CLA.

A maintainer adds their GitHub username to `contributors.json` and comments `@cla-bot check` on the pull request. The comment on the pull request is the record of assent; `contributors.json` is the ledger the bot checks against.

## contributors.json

A JSON array. An entry is matched case-insensitively against each committer and may be:

- a GitHub username — `"octocat"`
- a git commit email — `"octocat@example.com"`
- an email domain — `"@example.com"`, matching any committer whose commit email is at that domain

## Operational notes

- The status check is `verification/cla-signed`. Make it a required check on branches that receive pull requests.
- The `cla-signed` label must exist in a repository before the bot can apply it there.
- cla-bot resolves `.clabot` from this repository's default branch. A change takes effect on `main`, not on a branch.
