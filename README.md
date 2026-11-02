# ojizero/skills

> My agent skills I use day-to-day.

This repo retains the skills that I found I needed to do in order to codify common patterns I do. They are shared here primarily as means for synching them and versioning them more than anything, but also as means for other that may find them useful or maybe inspired by them.

## Install

Skills are grouped by topic. Each `<group>/<skill>` folder is one skill, such as `delivery/pull-request`.

<details>
<summary><strong>dotagents (recommended)</strong></summary>
If you use [dotagents by Sentry](https://dotagents.sentry.dev): 

```bash
# Using The Forge as the source
npx @sentry/dotagents add git:git@ssh-forge.ojizero.dev:ojizero/skills.git <skill-name> <skill-name>

# Using GitHub as the source
npx @sentry/dotagents add ojizero/skills <skill-name> <skill-name>
```

Swap the names for `--all` to take everything, and add `--project` before `add` to install into the current repo instead of `~/.agents/`.
</details>

<details>
<summary><strong>skills.sh</strong></summary>
[skills.sh](https://skills.sh) is the other option:

```bash
# Using The Forge as the source
npx skills add git@ssh-forge.ojizero.dev:ojizero/skills.git --skill <skill-name> --skill <skill-name>

# Using GitHub as the source
npx skills add ojizero/skills --skill <skill-name> --skill <skill-name>
```

Remove all `--skill <skill-name>` to install all skills.
</details>

Or if you want to tinker clone the repo and copy (or symlink) the skill folder into `~/.agents/skills/` or a project's `.agents/skills/`.
