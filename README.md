# Claude Skills

Personal Claude Code and claude.ai skills, synced across machines via this repo.

## Repo structure

Each skill is a top-level folder containing a `SKILL.md` with YAML frontmatter (`name`, `description`). Folder name matches the destination folder name under `~/.claude/skills/` on each machine.

```
claude-skills/
  README.md                       <- this file
  live-session-cache/
    SKILL.md
  another-skill/                  <- future skills follow the same pattern
    SKILL.md
```

To add a new skill: create a new top-level folder with a `SKILL.md` inside, commit, push. Run the sync command on each machine to pick it up.

## Installation

Same on every machine. Clone the repo into a working directory, then sync the skill folders into `~/.claude/skills/`.

### Windows (PowerShell)

```powershell
# One-time clone
git clone https://github.com/SchnappAPI/claude-skills.git $HOME\dev\claude-skills

# Sync (run after the initial clone and after every git pull)
$src = "$HOME\dev\claude-skills"
$dst = "$HOME\.claude\skills"
New-Item -ItemType Directory -Force -Path $dst | Out-Null
Get-ChildItem -Path $src -Directory | Where-Object { $_.Name -ne '.git' } | ForEach-Object {
    Copy-Item -Path $_.FullName -Destination $dst -Recurse -Force
}
```

### macOS and Linux (bash or zsh)

```bash
# One-time clone
git clone https://github.com/SchnappAPI/claude-skills.git ~/dev/claude-skills

# Sync (run after the initial clone and after every git pull)
mkdir -p ~/.claude/skills
for d in ~/dev/claude-skills/*/; do
  name=$(basename "$d")
  [ "$name" = ".git" ] && continue
  rsync -a --delete "$d" "$HOME/.claude/skills/$name/"
done
```

## Updating

```
cd ~/dev/claude-skills      # or the Windows equivalent
git pull
```

Then re-run the sync command for the OS you are on. The sync overwrites the skill folder under `~/.claude/skills/` with the latest content.

## Why copy instead of symlink

Copying works everywhere with no admin rights and no developer-mode toggle. Symlinks on Windows need elevation; junctions work but are filesystem-specific. Copy is the lowest-friction pattern for cross-platform sync.

## Why a working directory instead of cloning straight into `~/.claude/skills/`

Cloning into the skills directory pollutes it with git state and conflicts with any other skills installed there from other sources. Keeping the repo in a working directory keeps git operations separate from the active skills directory.
