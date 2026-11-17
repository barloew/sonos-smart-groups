# Troubleshooting

### Followers respond only on the second button press

The volume tolerance is too high. Set it to `0.5` in section 6 of the blueprint. With a factor of 1.2, one volume step differs by only 1.2 points, which a tolerance of 2 ignores.

### Nothing happens

Open the automation trace. Every condition is named, so the trace shows which one stopped the run. Common causes: an entity under **Only when these are on** is off, or the leader is a follower in a larger group.

### Everything is about 30 seconds late

Sonos push updates are not reaching Home Assistant, so it falls back to polling every 30 seconds. Look for `Subscription renewal failed` in the log and check firewalls and VLANs for TCP port 1400.

### Groups reassemble after the TV stops

Check the Sonos **TV autoplay** and **Ungroup on autoplay** switches for each room. They act independently of this integration.

### Equalizer settings are not copied

Both speakers need the control. A Play:1, for example, has no surround level or Sub gain. With Music Assistant only, the equalizer entities do not exist; install the Sonos integration alongside it.

### Followers get the volume but do not join the group

The leader and followers come from different integrations, such as Sonos and Music Assistant. Grouping only works within one integration. The log notes this.

### Groups made in the Sonos app are undone

A smart group rebuilds itself as configured, not as you left it. This is by design; see [Why rebuilding beats snapshots](advanced.md#why-rebuilding-beats-snapshots).

Still stuck? See [Reading a trace](advanced.md#reading-a-trace) or open an [issue](https://github.com/barloew/sonos-smart-groups/issues).
