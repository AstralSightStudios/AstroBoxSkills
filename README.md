# AstroBox Skills

A collection of [Skills](https://skills.sh) for AstroBox ecosystem — CLI automation, device management, community wiki, and support.

## Available Skills

| Skill | Description |
|-------|-------------|
| [abcli](./abcli) | Control AstroBox via its official CLI (`npx astrobox-cli`). Manage devices, browse providers, search & install watchfaces/apps, check status, troubleshoot errors. |
| [astrobox-support](./astrobox-support) | Answer AstroBox usage and troubleshooting questions. Step-by-step guidance for connection, resource download, account management, and more. |
| [bandbbs-wiki](./bandbbs-wiki) | Index and navigator for the BandBBS Wiki. Quick access to tutorials, firmware info, and community resources for Xiaomi wearables. |

## Usage

```bash
# Add this skill collection
bunx skills add AstralSightStudios/AstroBoxSkills

# Or install a specific skill
bunx skills add AstralSightStudios/AstroBoxSkills/abcli
```

## Development

Skills are defined in individual directories with a `SKILL.md` file and optional references/scripts:

```
skill-name/
├── SKILL.md                  # Skill definition (name, description, instructions)
├── references/               # Supporting documentation
├── scripts/                  # Helper scripts
└── evals/                    # Test cases and benchmarks
```

## License

MIT
