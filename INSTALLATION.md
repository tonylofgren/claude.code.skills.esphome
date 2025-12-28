# ESPHome Code Assistant - Installation Guide

Complete guide to installing the ESPHome Code Assistant skill for Claude Code.

## Prerequisites

1. **Claude Code** installed and working
   - Download from [claude.ai/code](https://claude.ai/code)
   - Verify with `claude --version`

2. **Basic ESPHome knowledge** (recommended)
   - Understand YAML syntax
   - Know what ESP32/ESP8266 boards are

---

## Installation (Recommended)

Install directly in Claude Code using the plugin system:

**1. Add the marketplace:**
```
/plugin marketplace add tonylofgren/claude.code.skills.esphome
```

**2. Install the skill:**
```
/plugin install esphome-code-assistant
```

**Done!** Start using the skill immediately.

---

## Updating

To update to the latest version:

```
/plugin marketplace update tonylofgren-claude.code.skills.esphome
```

---

## Uninstalling

```
/plugin uninstall esphome-code-assistant
```

To also remove the marketplace:
```
/plugin marketplace remove tonylofgren-claude.code.skills.esphome
```

---

## Alternative: Manual Installation

If you prefer manual installation or need to modify the skill locally:

### All Platforms

```bash
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git
```

Then copy to your skills folder:

| Platform | Path |
|----------|------|
| macOS/Linux | `~/.claude/skills/esphome-code-assistant` |
| Windows | `%USERPROFILE%\.claude\skills\esphome-code-assistant` |

Restart Claude Code after installation.

---

## Verification

Test the skill by saying:

```
Create a simple ESP32 temperature sensor config
```

**Expected:** A complete ESPHome YAML configuration.

---

## Configuration

### Secrets File

The skill generates configs using `!secret` references. Create your secrets file in your ESPHome config directory:

```yaml
# secrets.yaml
wifi_ssid: "YourWiFiName"
wifi_password: "YourWiFiPassword"
wifi_ap_password: "FallbackAPPassword"
api_encryption_key: "your-32-byte-base64-key"
ota_password: "your-ota-password"
```

### Generate API Key

```bash
openssl rand -base64 32
```

---

## Troubleshooting

### Skill Not Triggering

1. Verify the skill is installed: `/plugin list`
2. Restart Claude Code
3. Try reinstalling the skill

### Generated Config Has Errors

1. Check ESPHome version compatibility
2. Verify pin assignments for your specific board
3. Ask Claude: "Fix this ESPHome error: [paste error]"

---

## Getting Help

- **Usage examples:** See [USAGE-GUIDE.md](USAGE-GUIDE.md)
- **600+ prompts:** See [PROMPT-IDEAS.md](PROMPT-IDEAS.md)
- **GitHub Issues:** [Report bugs or request features](https://github.com/tonylofgren/claude.code.skills.esphome/issues)

---

## Version History

| Version | Changes |
|---------|---------|
| v1.0.0 | Initial release - 17 templates, 22 reference docs, 600+ example prompts |
