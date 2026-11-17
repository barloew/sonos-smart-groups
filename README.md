<img src="https://raw.githubusercontent.com/barloew/sonos-smart-groups/main/custom_components/sonos_smart_groups/brand/icon.png" alt="Sonos Smart Groups" width="96" align="right">

# Sonos Smart Groups

[![Release][release-badge]][release-url]
[![HACS][hacs-badge]][hacs-url]
[![Validate][validate-badge]][validate-url]

Rule-based Sonos groups for Home Assistant with per-room volume and EQ.

A Sonos group is a one-time decision: these rooms, right now, at one volume. A smart group is a rule. It knows which room leads, how loud each follower should be relative to the leader, and which group takes precedence when two want the same room.

## Features

- **Volume factors:** each follower keeps a fixed ratio to the leader, such as 1.3 for a room across an open floor.
- **Sound matching:** copies bass, treble, loudness, surround and Sub settings to followers, with a per-room factor for bass and treble.
- **Precedence:** a superior group, such as a home theater, takes rooms over and hands them back afterward. The subordinate group rebuilds itself.
- **Auto-start:** starts a favorite, playlist, station or input on any trigger, at a set volume.
- **Music Assistant support:** works with Sonos and Music Assistant players.
- **Blueprint-based:** every smart group is an automation from one blueprint. The blueprint installs and updates itself.

## Requirements

- Home Assistant 2025.7 or later
- Sonos rooms in Home Assistant through the [Sonos integration](https://www.home-assistant.io/integrations/sonos/) or [Music Assistant][music-assistant]
- TCP port 1400 open between your speakers and Home Assistant, so Sonos can push updates

## Installation

### HACS

[![Open in HACS][my-ha-badge]][my-ha-url]

Or add it manually:

1. In HACS, open the menu and select **Custom repositories**.
2. Add `https://github.com/barloew/sonos-smart-groups` with category **Integration**.
3. Download **Sonos Smart Groups** and restart Home Assistant.

### Manual

Copy `custom_components/sonos_smart_groups` from the [latest release][release-url] to your `config/custom_components` folder and restart Home Assistant.

## Configuration

1. Go to **Settings → Devices & services → Add integration** and select **Sonos Smart Groups**.
2. Optionally, name the situations that can take precedence, such as `Home theater`. Each becomes a switch. You can add them later.
3. Go to **Settings → Automations & scenes → Create automation → Use blueprint** and select **Sonos Smart Group**.
4. Choose a leader and add followers with a volume factor.

| Room | Volume factor | Add to group |
|---|---|---|
| Dining room | 1.0 | yes |
| Living room | 1.3 | yes |

When music starts in the leader's room, the followers join. The living room plays 30% louder. To match sound as well, enable **Bass**, **Treble** and **Loudness** under **Equalizer**. Controls a speaker lacks are skipped.

### Precedence

Create a second smart group with the home theater as leader, set it to **Superior** and select a precedence lock. Set the music group to **Subordinate** with the same lock. When the TV starts, the home theater takes the living room. When it stops, the music group rebuilds itself.

## Documentation

- [Troubleshooting](docs/troubleshooting.md)
- [Advanced guide][advanced]: architecture, Music Assistant, precedence internals, service API

## License

[MIT](LICENSE). Not affiliated with Sonos, Inc.

[release-badge]: https://img.shields.io/github/v/release/barloew/sonos-smart-groups
[release-url]: https://github.com/barloew/sonos-smart-groups/releases
[hacs-badge]: https://img.shields.io/badge/HACS-Custom-41BDF5.svg
[hacs-url]: https://github.com/hacs/integration
[validate-badge]: https://github.com/barloew/sonos-smart-groups/actions/workflows/validate.yml/badge.svg
[validate-url]: https://github.com/barloew/sonos-smart-groups/actions/workflows/validate.yml
[my-ha-badge]: https://my.home-assistant.io/badges/hacs_repository.svg
[my-ha-url]: https://my.home-assistant.io/redirect/hacs_repository/?owner=barloew&repository=sonos-smart-groups&category=integration
[advanced]: docs/advanced.md
[music-assistant]: https://www.music-assistant.io/
