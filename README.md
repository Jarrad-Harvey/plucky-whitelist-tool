# plucky-whitelist-tool

Interfaces with Plucky to configure whitelist software blocking systems with concise commands.

A flexible Bash tool to manage “unlockable” items and programs using Plucky.  
Supports registering items, unlocking them, listing registered items, and syncing delay commands.

---

## Features

- `unlock <key> [duration]` — unlock a subject or program with optional override duration.  
- `unlock --register <key> (program=<name> | config=<config> | action=<action>) [delay=<delay>] [allow=<duration>]` — register a new item.  
- `unlock --list` — show all registered items with colors and aligned formatting.  
- `unlock --sync` — re-run initial delay commands for all registered items.  

---

## Installation

1. Clone the repo (or download the script):

    ```bash
    git clone https://github.com/yourusername/unlock.git
    ```

2. Copy the script to `~/bin` (or `/usr/local/bin` for global):

    ```bash
    mkdir -p ~/bin
    cp plucky-whitelist-tool/unlock ~/bin/
    chmod +x ~/bin/unlock
    ```

3. Ensure `~/bin` is in your PATH:

    ```bash
    echo 'export PATH="$PATH:$HOME/bin"' >> ~/.zshrc
    source ~/.zshrc
    ```

> `unlock` is now callable from any terminal session.

---

## Usage Examples

### Unlock items

    unlock dev                # uses stored allow duration
    unlock spotify 45m        # overrides stored allow duration

### Register items

    unlock --register spotify program=spotify delay=30m allow=1h
    unlock --register dev config=1234 allow=45m
    unlock --register custom action="program custom_tool --opt" allow=2h

### List all registered items

    unlock --list

### Sync all items (re-run initial delays)

    unlock --sync

---

## Notes

- The script stores JSON data in `unlock_data/entries.json` relative to the script.  
- You can edit defaults at the top of the script (`DEFAULT_DELAY` and `DEFAULT_ALLOW`).  
- Ensure `jq` is installed: `brew install jq` on macOS.

---

## Contributing

1. Fork the repository.  
2. Make your changes (add items, improve output, etc.).  
3. Submit a pull request.
