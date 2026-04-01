# Claude Code Skills (Public)

Reusable skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Each folder contains a `SKILL.md` that Claude Code can use as a slash command.

## Skills

| Skill | Trigger | Description |
|-------|---------|-------------|
| [architecture-diagram](architecture-diagram/) | `/architecture-diagram` | Generate Mermaid architecture diagrams by analyzing any codebase |
| [decision-crucible](decision-crucible/) | `/decide` | Multi-framework decision-making with adversarial reasoning passes |
| [first-principles](first-principles/) | `/first-principles` | First principles deconstructor for decisions, problems, and stuck situations |
| [security-audit](security-audit/) | `/security-audit` | Comprehensive security audit for any codebase (OWASP, deps, secrets, AI code) |
| [VC-Due-Dil](VC-Due-Dil/) | `/VC-Due-Dil` | Angel investor due diligence for early-stage startup evaluation |

## Usage

1. Clone this repo (or symlink individual skills) into your Claude Code skills directory
2. Invoke any skill with its trigger command in Claude Code

## License

MIT
