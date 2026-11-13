# OpenCode Skills & Commands

A curated collection of skills and custom commands for [OpenCode](https://github.com/opencode-org/opencode) that I personally use in my daily development workflow.

> [!NOTE]
> **Disclaimer:** These skills and commands are collected and adapted from various community sources and experiments. Please review the instructions and scripts inside each skill before running them in your projects.

## Structure

- `skills/` – Agent skills and workflows (design systems, TDD, debugging, planning, optimization, and code review).
- `commands/` – Quick prompt shortcuts and commands.

## Installation / Usage

Copy the skills or commands into your local OpenCode configuration directory:

```bash
# Clone the repository
git clone https://github.com/<your-username>/Opencode.git

# Copy skills to OpenCode configuration
cp -r Opencode/skills/* ~/.config/opencode/skills/

# Copy commands to OpenCode configuration
cp -r Opencode/commands/* ~/.config/opencode/commands/
```

Or symlink specific skills you want to try:

```bash
ln -s "$(pwd)/skills/<skill-name>" ~/.config/opencode/skills/
```

## Contributing / Credits

Contributions, tweaks, and credits to original authors are welcome! Feel free to open an issue or pull request.

## License

MIT (or whichever open-source license applies to respective upstream sources).
