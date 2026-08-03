# Git & GitHub CLI Setup Cheat Sheet

## Git Setup: Step 1

Check install:

```bash
$ git --version
# 2.x.x       -> good
# not found   -> install at git-scm.com
```

Set your identity (stamped on every commit you make):

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Git Setup: Step 2

```bash
$ gh auth login
```

```text
? What account do you want to log into?
> GitHub.com

? What is your preferred protocol?
> HTTPS

Opens browser for auth
```

Claude Code uses this same CLI.

## Line Endings (Windows)

If on Windows, create a `.gitattributes` file at your project root.

**Problem:** `core.autocrlf` adds noise to diffs when the SDK regenerates TypeScript.

**Fix:** add `.gitattributes` at root (explicit beats automatic):

```text
# .gitattributes
* text=auto eol=lf
src/fluent/generated/*.ts  lf
```

## New Repo Setup

If it's a brand new repo:

```bash
$ gh repo create my-app --private
$ git remote add origin <url>
$ gh repo view
# -> Shows repo info (perfect)
```

## Source

[ServiceNow Developer Advocate Blog: Building ServiceNow Apps via Claude Code and the ServiceNow SDK](https://www.servicenow.com/community/developer-advocate-blog/building-servicenow-apps-via-claude-code-and-the-servicenow-sdk/ba-p/3525677#ep-3-16)
