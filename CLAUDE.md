# CLAUDE.md

## About this repo

Portfolio of hands-on AWS labs from my cloud computing course (AWS Cloud Practitioner prep).
Each lab is documented as a real case: what was built, what broke, how I diagnosed it and how I fixed it.

Audience: recruiters and engineers (including international ones) skimming my GitHub.
They should understand each lab in under a minute and see my reasoning, not a copy of the course instructions.

- **All repo content in English.**
- **Talk to me in Portuguese** in the chat.

## Repo structure

```
.
├── README.md                     # index: intro + table of all labs
├── CLAUDE.md
├── .gitignore
├── _raw/                         # my raw material per lab (git-ignored, never published)
│   └── <lab-slug>/
└── NN-<lab-slug>/                # one folder per documented lab, NN = 01, 02, 03...
    ├── README.md
    ├── scripts/                  # fixed scripts, user data, *.diff (only if the lab has them)
    └── images/                   # architecture diagram, screenshots (only if provided)
```

If `README.md` or `.gitignore` don't exist yet, create them following the templates below.

## Workflow

I drop raw material for a lab into `_raw/<lab-slug>/`: lab instructions (.txt / .md / .pdf), terminal output,
diffs, scripts, screenshots, the architecture diagram and my own notes about what I did.

When I ask you to document a lab:

1. Read **everything** in `_raw/<lab-slug>/`.
2. Pick the next number `NN` by checking the existing `NN-*` folders.
3. Create `NN-<lab-slug>/` with `README.md` (template below), plus `scripts/` and `images/` only if there is material for them.
   - Copy fixed scripts and `.diff` files into `scripts/`.
   - Copy images into `images/` with descriptive kebab-case names (`architecture.png`, `nmap-before-fix.png`).
4. Add a row for the lab to the table in the root `README.md`.
5. Run the sanitization check (see Rules).
6. Reply with a short summary in Portuguese: what you created, and a list of **anything missing or unclear** that I need to fill in.

Do not `git commit` or `git push` unless I ask. When I do, use messages like `docs(lab-NN): add <lab title>`.

## Lab README template

Not every lab is a troubleshooting lab. For "build" labs, skip **Issues found** and use **What I built** instead.

````markdown
# <Lab title>

> One-sentence summary of what this lab builds and what skill it shows.

**AWS services:** EC2, VPC, Security Groups, AWS CLI, ...
**Tools:** bash, nmap, ...

## Objective
2–3 sentences in my own words. What is being built and why.

## Architecture
![Architecture](images/architecture.png)
One or two sentences explaining the diagram.

## What I built
Short numbered summary of the main steps (not a copy of the instructions). Only for build labs.

## Issues found

### Issue 1 — <short name>
- **Symptom:** what I saw (error message, page not loading...)
- **Diagnosis:** how I investigated (commands, what the output told me)
- **Root cause:** what was actually wrong
- **Fix:** what I changed

```bash
# key commands, trimmed to what matters
```

(repeat per issue)

## What I tried first
Optional. Wrong turns or workarounds before the proper fix, and why the proper fix is better.
These are good: they show real reasoning. Only include if my notes mention them.

## Key takeaways
- 3–5 bullets with concepts I learned (e.g. nmap `closed` vs `filtered`).

## Files
- `scripts/...` — what each file is
````

## Root README template

```markdown
# AWS Cloud Labs

AWS hands-on labs documented as real troubleshooting cases: symptom, diagnosis, root cause and fix.
EC2, networking, security groups and AWS CLI.

Each lab folder has its own README with the architecture, the issues I hit and how I solved them.

| # | Lab | AWS services | What was built / fixed |
|---|-----|--------------|------------------------|
| 01 | [Lab title](01-lab-slug/) | EC2, AWS CLI | One line |
```

## Rules

**Never invent.** Only document what is in `_raw/`. If the material doesn't show how an issue was diagnosed or fixed,
or what I actually ran, leave a `<!-- TODO: ... -->` in the README and list it in your reply. Don't fill gaps with
what the "expected" answer probably is.

**Own words, no copying.** The course instructions are copyrighted course material. Don't paste them into the repo
or reproduce them step by step. Summarize objectives and steps briefly in your own words.
`_raw/` must stay in `.gitignore`.

**Sanitize before finishing.** Replace with placeholders:
- AWS access keys, secret keys, session tokens → remove entirely
- 12-digit account IDs (also inside ARNs) → `<ACCOUNT_ID>`
- Public IPs → `<PUBLIC_IP>`; private IPs can stay
- Emails, usernames, lab-specific URLs with tokens → remove
- Key pair names and resource IDs (`i-...`, `sg-...`, `vpc-...`) → `<INSTANCE_ID>`, `<SG_ID>`, etc.

Then grep the new folder for `AKIA`, `ASIA`, `aws_secret`, `aws_session_token` and `\b[0-9]{12}\b` and
report the result. You can't edit images, so if a screenshot looks like it shows an IP, account ID or key, tell me
which one so I can crop it.

**Formatting.**
- Commands in fenced `bash` blocks; terminal output in plain fenced blocks, trimmed to the relevant lines.
- Concise: a recruiter should get the gist from the summary line and the Issues section.
- Use consistent naming: folder slugs in kebab-case, e.g. `01-troubleshooting-ec2-cli`.

## .gitignore template

```
_raw/
*.pem
*.ppk
.aws/
.env
credentials
```
