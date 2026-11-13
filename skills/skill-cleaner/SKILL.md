---
name: skill-cleaner
description: Cleans, deduplicates, unifies, and installs raw or downloaded agent skills into the global OpenCode and Antigravity environments. Use when the user downloads new skills, imports skill packs from GitHub/online repos, or asks to clean, rebrand, sanitize, or integrate incoming skills.
---

# Skill Cleaner & Integrator

A pipeline for sanitizing, deduplicating, merging, and installing third-party agent skills into your local environment.

## When to Use
- User downloads skills into a folder (e.g. `Downloads/`, `myskills/`, `uncleaned/`).
- User asks to import skills from online sources or GitHub repositories.
- User wants to clean skills of vendor-specific branding, licenses, or creator footprints.
- User asks to merge overlapping skills or delete duplicate skill files.

---

## 4-Step Processing Pipeline

### Step 1: Sanitize & Rebrand ("Make Them Clean")
Strip all third-party branding, external attribution, and proprietary locks:
1. **Remove License Metadata**:
   - Delete all lines matching `license: Complete terms in LICENSE.txt` or `license: ...` from YAML frontmatter.
   - Delete standalone `LICENSE.txt` or `LICENSE` files inside skill folders.
2. **Remove External Attribution & Links**:
   - Strip out lines like `> Inspired by [plugin](https://...)` or author setup commands (e.g., `/setup-...`).
3. **Generalize Model & Tool Branding**:
   - Replace `CLAUDE.md` with `AGENTS.md`.
   - Replace `Claude Code` with `OpenCode`.
   - Replace `Claude` / `claude` with `Agent` / `agent`.
   - Replace `claude.ai` with `web-artifacts` or `workspace`.
   - Replace `claude -p` with `opencode run`.
4. **Preserve Functionality**:
   - Do NOT delete functional code, helper scripts (`scripts/`), schemas (`schemas/`), or templates (`assets/`). Clean scripts in-place.

---

### Step 2: Exact Duplicate Detection & Deletion
Before installing:
1. Compare SHA256 checksums or exact file content between incoming files and existing skills.
2. If two files have identical content (e.g. `SKILL.md` and `SKILL(1).md`):
   - Keep the canonically named file.
   - Delete the duplicate file immediately.
   - Report the duplicate to the user.

---

### Step 3: Semantic Similarity & Intelligent Combination
If an incoming skill provides a capability that already exists under a slightly different name:
- **Do not overwrite** the existing skill blindly.
- **Do not keep both** as confusing duplicates (e.g. `code-review` vs `code-review-and-quality`, or `frontend-design` vs `frontend-ui-engineering`).
- **Combine them**:
  1. Merge the YAML frontmatter description into a comprehensive summary.
  2. Keep the existing skill's canonical folder name.
  3. Append the new skill's unique checklists, protocols, or guidelines as distinct sections inside the canonical `SKILL.md`.
  4. Merge any unique scripts or assets into the skill folder.

---

### Step 4: Installation & Global Sync
Once cleaned and resolved:
1. **Target Directories**:
   - OpenCode Global: `~/.config/opencode/skills/<skill-name>/SKILL.md`
   - Antigravity Global: `~/.gemini/config/skills/<skill-name>/SKILL.md`
2. **Folder Structure**:
   Ensure every skill follows the standard layout:
   ```text
   <skill-name>/
   ├── SKILL.md
   ├── scripts/     (if present)
   └── references/  (if present)
   ```
3. **Consolidated Backup**:
   - Maintain a unified, cleaned copy in `~/Github/skills/<skill-name>/` (or project repo).
   - Delete the temporary incoming uncleaned directory once installation is verified.
4. **Summary Report**:
   Display a clear Markdown table showing:
   - Skills added as new
   - Skills merged/combined
   - Duplicates discarded
