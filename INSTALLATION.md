# ESPHome Code Assistant - Installation Guide

Complete guide to installing the ESPHome Code Assistant skill for Claude Code.

## Prerequisites

1. **Claude Code** installed and working
   - Download from [claude.ai/code](https://claude.ai/code)
   - Verify with `claude --version`

2. **Git** (for cloning the repository)

3. **Basic ESPHome knowledge** (recommended)
   - Understand YAML syntax
   - Know what ESP32/ESP8266 boards are

---

## Installation by Platform

### macOS

```bash
# Clone the repository
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git
cd claude.code.skills.esphome

# Create skills folder and copy
mkdir -p ~/.claude/skills
cp -r . ~/.claude/skills/esphome-code-assistant

# Restart Claude Code and verify
```

### Linux / WSL

```bash
# Clone the repository
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git
cd claude.code.skills.esphome

# Create skills folder and copy
mkdir -p ~/.claude/skills
cp -r . ~/.claude/skills/esphome-code-assistant

# Restart Claude Code and verify
```

### Windows (PowerShell)

```powershell
# Clone the repository
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git
cd claude.code.skills.esphome

# Create skills folder and copy
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude\skills" -Force
Copy-Item -Recurse . "$env:USERPROFILE\.claude\skills\esphome-code-assistant"

# Restart Claude Code and verify
```

### Windows (Command Prompt)

```cmd
:: Clone the repository
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git
cd claude.code.skills.esphome

:: Create skills folder and copy
mkdir "%USERPROFILE%\.claude\skills"
xcopy . "%USERPROFILE%\.claude\skills\esphome-code-assistant" /E /I /H

:: Restart Claude Code and verify
```

---

## Alternative: Project Installation

Install for a specific project only (team members get the skill automatically).

```bash
# In your project root
mkdir -p .claude/skills
git clone https://github.com/tonylofgren/claude.code.skills.esphome.git .claude/skills/esphome-code-assistant
```

---

## Alternative: Symlink (For Development)

Keep the skill synced with the repo for easy updates.

**macOS / Linux / WSL:**
```bash
ln -s /full/path/to/claude.code.skills.esphome ~/.claude/skills/esphome-code-assistant
```

**Windows (Admin PowerShell):**
```powershell
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.claude\skills\esphome-code-assistant" -Target "C:\full\path\to\claude.code.skills.esphome"
```

---

## Verification

After installation, test the skill:

### Quick Test

Say to Claude:

```
Create a simple ESP32 temperature sensor config
```

**Expected:** A complete ESPHome YAML configuration with core settings, WiFi, API, OTA, and a temperature sensor.

### Verify All Features

| Test Command | Expected Result |
|--------------|-----------------|
| "Create ESP32 with DHT22" | DHT sensor YAML config |
| "Convert Shelly 1PM to ESPHome" | Shelly-specific config with GPIO mappings |
| "Add SSD1306 OLED display" | Display component with example pages |
| "Troubleshoot WiFi connection" | Diagnostic steps and config checks |

---

## Configuration

### Secrets File

The skill generates configs using `!secret` references. Create your secrets file:

**Location:** Same directory as your ESPHome configs

```yaml
# secrets.yaml
wifi_ssid: "YourWiFiName"
wifi_password: "YourWiFiPassword"
wifi_ap_password: "FallbackAPPassword"
api_encryption_key: "your-32-byte-base64-key"  # Generate with: openssl rand -base64 32
ota_password: "your-ota-password"
```

### Generate API Key

```bash
# Generate a random 32-byte base64 key
openssl rand -base64 32
```

Or use Python:

```python
import secrets, base64
print(base64.b64encode(secrets.token_bytes(32)).decode())
```

---

## Updating

### Pull Latest Changes

If installed via clone:

```bash
cd ~/.claude/skills/esphome-code-assistant
git pull
```

If installed via copy, re-copy from updated source.

### Restart Claude Code

After updating, restart Claude Code to load changes.

---

## Troubleshooting

### Skill Not Triggering

**Symptom:** Claude doesn't recognize ESPHome-related requests

**Solutions:**
1. Verify installation path is correct:
   - Personal: `~/.claude/skills/esphome-code-assistant/SKILL.md`
   - Project: `.claude/skills/esphome-code-assistant/SKILL.md`
2. Restart Claude Code
3. Check folder contains `SKILL.md` file

### Skill Folder Structure

The skill must have this structure:

```
esphome-code-assistant/
├── SKILL.md              ← Required (main skill file)
├── references/           ← Supporting documentation
│   ├── sensors.md
│   ├── displays.md
│   └── ...
└── assets/templates/     ← Ready-to-use templates
    ├── base-esp32.yaml
    └── ...
```

### Generated Config Has Errors

**Symptom:** ESPHome compilation fails

**Solutions:**
1. Check ESPHome version compatibility
2. Verify pin assignments for your specific board
3. Ask Claude: "Fix this ESPHome error: [paste error]"

### Clear Plugin Cache

If skills aren't updating:

```bash
# macOS/Linux
rm -rf ~/.claude/plugins/cache

# Windows
rmdir /s /q %USERPROFILE%\.claude\plugins\cache
```

---

## Uninstalling

Remove the skill folder:

```bash
# macOS/Linux
rm -rf ~/.claude/skills/esphome-code-assistant

# Windows
rmdir /s /q %USERPROFILE%\.claude\skills\esphome-code-assistant
```

---

## Skill Locations Reference

| Location | Path | Scope |
|----------|------|-------|
| Personal | `~/.claude/skills/` | All your projects |
| Project | `.claude/skills/` | This repo only |

If multiple skills have the same name, project skills take precedence over personal skills.

---

## Directory Structure

```
esphome-code-assistant/
├── SKILL.md                    # Main skill instructions
├── INSTALLATION.md             # This file
├── USAGE-GUIDE.md              # Detailed usage examples
├── README.md                   # Overview and quick start
├── references/
│   ├── sensors.md              # 200+ sensor platforms
│   ├── binary-sensors.md       # PIR, touch, NFC, buttons
│   ├── lights.md               # LED strips, effects
│   ├── displays.md             # OLED, TFT, E-Paper
│   ├── climate.md              # Thermostat, PID, AC
│   ├── covers-fans.md          # Blinds, garage doors
│   ├── motors.md               # Stepper, servo
│   ├── remote-rf-ir.md         # IR/RF protocols
│   ├── communication.md        # I2C, SPI, UART, CAN
│   ├── automations.md          # Triggers, actions
│   ├── home-assistant.md       # HA integration
│   ├── device-guides.md        # Shelly, Sonoff, Tuya
│   ├── troubleshooting.md      # Common issues
│   ├── external-components.md  # Community components
│   ├── solar-energy.md         # MPPT, inverters, BMS
│   ├── popular-devices.md      # AirGradient, VINDRIKTNING
│   ├── power-management.md     # Deep sleep, battery
│   ├── bluetooth.md            # BLE tracker, proxy
│   ├── buttons-inputs.md       # Number, Select, Text
│   ├── outputs.md              # GPIO, PWM, DAC
│   ├── cookbook.md             # Complete projects
│   └── arduino-conversion.md   # Arduino to ESPHome
└── assets/templates/
    ├── base-esp32.yaml
    ├── base-esp8266.yaml
    ├── shelly-1pm.yaml
    ├── sonoff-basic.yaml
    ├── voice-assistant.yaml
    └── (12 more templates...)
```

---

## Getting Help

- **Usage examples:** See [USAGE-GUIDE.md](USAGE-GUIDE.md)
- **Quick reference:** See [README.md](README.md)
- **GitHub Issues:** [Report bugs or request features](https://github.com/tonylofgren/claude.code.skills.esphome/issues)

---

## Version History

| Version | Changes |
|---------|---------|
| v1.0.0 | Initial release - Complete ESPHome skill with 18 triggers, 22 reference docs, 17 templates |
