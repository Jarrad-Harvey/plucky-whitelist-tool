# plucky-whitelist-tool

A Bash tool to manage an internet whitelist using Plucky.
Supports registering items, unlocking them, listing registered items, and syncing delay commands.

## Features

- `unlock <key> [duration]` — unlock an item.
- `unlock --register <key> (program=<program> | config=<config> | rule=<rule>) [delay=<delay>] [allow=<duration>]` — register a new item.
    - Key: name of the item. (e.g. dev, thesis, spotify)
    - Program: https://docs.pluckeye.net/how-to-allow-a-program
    - Config: https://docs.pluckeye.net/imports
    - Rule: https://docs.pluckeye.net/rules
    - Delay: https://docs.pluckeye.net/delay
    - Allow: default amount of time to allow when unlocking the item.
- `unlock --list` — show all items.
- `unlock --sync` — re-run plucky initialisation commands for all items.

## Installation

1. Clone the repo (or download the script):

    ```bash
    git clone https://github.com/Jarrad-Harvey/plucky-whitelist-tool
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

## Usage Examples

### Unlock items

    unlock dev                # uses stored allow duration
    unlock spotify 45m        # overrides stored allow duration

### Register items

    unlock --register spotify program=spotify delay=30m allow=1h
    unlock --register dev config=71c1fafa-b147-41f0-9cb9-c5724b1a7e00 allow=45m
    unlock --register custom action="program custom_tool --opt" allow=2h

### List all registered items

    unlock --list

### Sync all items (re-run initial delays)

    unlock --sync

## Notes

- The script stores JSON data in `unlock_data/entries.json` relative to the script.  
- You can edit defaults at the top of the script (`DEFAULT_DELAY` and `DEFAULT_ALLOW`).  
- Ensure `jq` is installed: `brew install jq` on macOS.
- There is currently no CLI command to add rules to configs on https://u.pluckeye.net. Go to the website.

## Contributing

1. Fork the repository.  
2. Make your changes (add items, improve output, etc.).  
3. Submit a pull request.
