SimpleCombat

SimpleCombat adds a basic PvP combat tag to Paper servers. When one player damages another, both players are tagged for the configured time. Player-fired projectiles count, and each new hit resets the timer.

## Requirements

- Paper 26.3
- Java 25
- No other plugins are required.

LuckPerms or another permissions plugin is optional. It can be used to give the SimpleCombat permissions to non-operators. SimpleCombat does not provide commands such as `/home`, `/spawn`, or `/tpa`; those are only names in the default command-block list. They do nothing unless another plugin or server feature provides matching commands.

## Install

1. Put `SimpleCombat-1.0.0.jar` in the server's `plugins` folder.
2. Start or restart the server.
3. Edit `plugins/SimpleCombat/config.yml` if you want different defaults.
4. Run `/combat reload` after editing the file in game.

The plugin creates `config.yml` the first time it starts. Settings changed with `/combat set` are saved to that file.

## What it does

- Tags both players after a player-versus-player hit. Direct attacks and projectiles shot by players count.
- Refreshes both players' timers after each qualifying hit.
- Shows a countdown in the action bar when enabled.
- Blocks only the command names listed in the config while a player is tagged.
- Kills a player who leaves during combat when the logout penalty is enabled.

Combat tags are kept in memory and clear when the server restarts. When logout punishment is disabled, leaving clears the player's tag.

## Commands

`/ctag` is an alias for `/combat`.

| Command | Access | Description |
| --- | --- | --- |
| `/combat` or `/combat help` | Everyone | Show commands available to you. |
| `/combat status` | Everyone | Show your remaining tag time. From the console, show the number of tagged players. |
| `/combat options` | `simplecombat.admin` | Show current settings. |
| `/combat set tag-seconds <1-600>` | `simplecombat.admin` | Change the tag duration. |
| `/combat set block-commands <true\|false>` | `simplecombat.admin` | Turn command blocking on or off. |
| `/combat set blocked-commands <names\|none>` | `simplecombat.admin` | Set comma-separated command names, or use `none` to clear the list. |
| `/combat set action-bar <true\|false>` | `simplecombat.admin` | Turn the countdown on or off. |
| `/combat set punish-logout <true\|false>` | `simplecombat.admin` | Turn the logout penalty on or off. |
| `/combat reload` | `simplecombat.admin` | Reload `config.yml`. |

For example, `/combat set blocked-commands home,spawn,tpa` sets three blocked command names. Do not put spaces between the names.

## Permissions

| Permission | Default | Description |
| --- | --- | --- |
| `simplecombat.admin` | Operators | Use `/combat options`, `/combat set`, and `/combat reload`. |
| `simplecombat.bypass` | Operators | Use commands in the blocked list while tagged. |

The bypass permission only skips command blocking. It does not prevent combat tags or the logout penalty.

## Configuration

The default `config.yml` contains:

```yaml
combat:
  tag-seconds: 15
  block-commands: true
  blocked-commands:
    - home
    - spawn
    - tpa
    - tpaccept
  action-bar: true
  punish-logout: true
```

- `tag-seconds`: how long a tag lasts after the latest hit.
- `block-commands`: whether the list below is blocked during combat.
- `blocked-commands`: command names only, without `/` or arguments.
- `action-bar`: whether tagged players see the countdown.
- `punish-logout`: whether leaving during combat kills the player.

The `messages` section controls the prefix and player messages. Message colors use ampersand codes such as `&c` for red and `&a` for green.

## Build from source

With Maven and JDK 25 installed, run `mvn package` from the project folder. The jar is written to `target/SimpleCombat-1.0.0.jar`.
