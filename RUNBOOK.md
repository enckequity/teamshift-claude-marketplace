# "Claude for your team" rollout (#6261)

$1,500 setup + $250/month care (`/services/team-ai-rollout`). Delivered in a week: 5 company
skills, 1 connector, a company `CLAUDE.md` with the company-brain starter, and a private plugin
marketplace the whole team gets automatically.

## 1. Intake (30 minutes, recorded with consent)
Ask the owner for the five tasks people repeat most, how each is done today, what "good" looks like,
what must never happen, and which app holds the data (that picks the connector). Transcribe it.

## 2. Build the skills from the transcript
For each task, write `plugins/<company>/skills/<task>/SKILL.md` the way the reference skills here
do: when to use it, the steps in order, the rules (prices, approvals, consent), and the finish
format. Only what the owner said; anything unclear is a question back to them.
For each skill write one eval case in `evals/<task>/case.yaml` from a real example in the intake:
a `tool_used: Skill` grader (the skill fires), a `regex` grader for a must/must-not phrase, and an
`llm` grader stating the owner's definition of good. Then:

```bash
claude plugin validate . --strict
claude plugin eval plugins/<company> --trust-plugin --no-publish --max-cost-usd 5 --ablation none
```
Fix the skill (not the grader) until every case passes 3 of 3 runs; change a grader only when it
misjudges a correct output.

## 3. Connector and company brain
Add the one connector the intake picked (the app's official MCP server in the plugin's `.mcp.json`,
or the claude.ai connector the admin enables). Copy `starter/` into the company repo: `CLAUDE.md`,
`company-map.md`, `learnings.md` and the folders it names.

## 4. Ship it to the team
- Put the marketplace in the client's **private** GitHub repo (relative `./plugins/...` sources).
- **Claude.ai Team/Enterprise:** an Owner goes to Organization settings > Plugins & skills > Add >
  Sync from GitHub, picks the repo, leaves Sync automatically on, and sets the plugin to installed
  by default.
- **Claude Code:** an Owner adds managed settings (claude.ai Organization settings > Claude Code >
  Managed settings):
  ```json
  {"extraKnownMarketplaces": {"<company>-marketplace": {"source": {"source": "github", "repo": "<org>/<repo>"}, "autoUpdate": true}},
   "enabledPlugins": {"<company>@<company>-marketplace": true}}
  ```
- Check one teammate's install with `claude plugin list`.

## 5. Care ($250/month)
Monthly: read `learnings.md`, fold repeated corrections into the skills, add an eval case for each,
rerun the suite, bump the plugin `version`, and push.

## Reference marketplace (this folder)
`teamshift-reference` with the `teamshift-small-business` plugin (quote follow-up, review replies,
SOP from a narrated recording). Verified locally on 2026-10-10: `claude plugin validate --strict`
passes for the marketplace and the plugin; `claude plugin marketplace add` + `install` succeed with
all 3 skills; `claude plugin eval` passes every case 3 of 3 (about $0.31 a run).

## Public listing
Submit through the directory portal (https://claude.ai/directory/manage) from an Owner account after
`claude plugin validate --strict`; track the review status on the issue.
