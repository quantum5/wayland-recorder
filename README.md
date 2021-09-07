# `wayland-recorder`
Scripts to use with `wf-recorder` and `waybar` for screen recording

## Dependencies

* [`slurp`](https://github.com/emersion/slurp)
* [`wf-recorder`](https://github.com/ammen99/wf-recorder)

[`waybar`](https://github.com/Alexays/Waybar) can optionally be used to show
that a recording is in progress, but is not strictly necessary.

## Setup

[`record-screen`](record-screen) is the main script. It is intended to be
bound to a hot key. Upon the first invocation, it runs `slurp` to let you
select an area of the screen to record, and then runs `wf-recorder` in the
background. By default, it records to `~/Videos/Recordings`, but this can be
changed by editing the script. On a second invocation, it stops the
recording.

To use it, you can, for example, configure `sway` as such:

    bindsym $mod+print exec exec <path to record-screen>

## Waybar integration

[`record-screend`](record-screend) can be used to create a custom waybar
widget which shows if a recording is in progress.

This is an example configuration:

```json
    "custom/recording": {
        "exec": "exec <path to record-screend>",
        "exec-on-event": false,
        "on-click": "pkill -INT -P \"$(pgrep -xo record-screen)\" wf-recorder"
    },
```

This configuration also allows you to terminate the current recording by
simply clicking the message.

Note that the script attempts to display an icon with Font Awesome. If this
is not desired, the script could be edited to remove it.
