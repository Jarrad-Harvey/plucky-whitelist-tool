# plucky-whitelist-tool

A Bash tool for managing an internet whitelist using Plucky.

- Creates profiles from bundling together Plucky rules
- Unlocks them with a single concise command: `unlock dev`

> Read about Plucky: https://docs.pluckeye.net/overview

## Features

- `unlock <key> [duration]` — activate an profile.
- `unlock --register <key> (program=<program> | config=<config> | rule=<rule>) [delay=<delay>] [allow=<duration>]` — register a new profile.
    - Key: name of the profile. (e.g. dev, thesis, spotify)
    - Program: https://docs.pluckeye.net/how-to-allow-a-program
    - Config: https://docs.pluckeye.net/imports
    - Rule: https://docs.pluckeye.net/rules
    - Delay: https://docs.pluckeye.net/delay
    - Allow: default amount of time to allow after unlocking.
- `unlock --list` — show all profiles.
- `unlock --sync` — re-run plucky delay settings for all profile.

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

### Unlock profiles

    unlock dev                # uses stored allow duration
    unlock spotify 45m        # overrides stored allow duration

### Register profiles

    unlock --register spotify program=spotify delay=30m allow=1h
    unlock --register dev config=71c1fafa-b147-41f0-9cb9-c5724b1a7e00 allow=45m
    unlock --register custom action="program custom_tool --opt" allow=2h

### List all registered profiles

    unlock --list

### Sync all profiles (re-run initial delays)

    unlock --sync

## Notes

- The script stores JSON data in `unlock_data/entries.json` relative to the script.  
- You can edit defaults at the top of the script (`DEFAULT_DELAY` and `DEFAULT_ALLOW`).  
- Ensure `jq` is installed: `brew install jq` on macOS.
- There is currently no CLI command to add rules to configs on https://u.pluckeye.net. Go to the website.

## What is this for?

The goal is to make an internet filter that is both a *whitelist* and *off-by-default*.

### Blacklist vs. Whitelist
- A blacklist filter will *allow* every internet connection except ones that have been labelled as "bad".
- A whitelist filter will *block* every internet connection except ones that have been labelled as "good".

A blacklist is more flexible and less likely to interfere with day-to-day life; a whitelist is stricter, more inconvenient and significantly more effective for controlling temptations & distractions. I personally use a whitelist.

**This is not recommended for beginners!** If you are trying this out for the first time, please use a short delay to avoid causing yourself problems.

### Off by default
Most modern software blockers implement automated scheduling, such as:
- Blocking everything when you should be sleeping
- Allowing gaming only on the weekend

Scheduling blocked/allowed times is a common strategy—and this works very well. However, my personal interest is in factoring *intentionality* into the equation.

My goal is that every time I sit down at my computer, I **choose** what I intend to do—and automatically that becomes the only thing that my computer is capable of doing. I think of it like heading off to a cabin in the woods and bringing nothing with me but a single project.

In my own system, apps/websites are sorted into 4 categories.
- Always allowed
    - general purposes websites. *(notion.com, obsidian.md, maps.google.com)*
    - this list is **very small!**
- Always blocked
    - things that I am addicted to. *(youtube.com, tiktok.com)*
- Pre-approved
    - task-specific tools. *(chatgpt.com, wikipedia.org, discord.com, email, spotify)*
    - grouped into bundles based on the task (software development, thesis work, personal research, making purchases, games with friends)
    - can be activated after a small but noticeable delay (~30m)
- Unknown
    - not yet seen
    - can be approved after a significant delay (~8h)

By default, almost everything is blocked on my computer until I choose to specificaly unblock it.

### Use case
- Wake up in the morning
- Decide to do software development work
- Use command `unlock dev`
- Now my computer is only capable of accessing websites/apps necessary for dev work
- I can work with zero distractions or temptations

Optional:
- At some point during the day, I notice a website that I need—but it's not yet included in the pre-approved dev-specific config
- I go to https://u.pluckeye.net and add it to the relevant config

Note: There is currently no way to edit the user site configs without going directly to the website. The docs loosely suggest that at some point there may be another way: https://docs.pluckeye.net/imports

## Contributing

1. Fork the repository.  
2. Make your changes.
3. Submit a pull request.
