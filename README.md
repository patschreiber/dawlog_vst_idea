# DAW LOG (vst)

## Problem:

> You're tired, and you're getting creative, and you accidentally fiddle with a setting and forget about it. You listen later, and it's shit. Or you just come back later and it sounds like shit even if you didn't touch anything. There's no easy way to "retrace your steps" and see if you did somethign stupid after coming home from the bar and fiddling with the project.

## Solution:

> It's a VST that writes major events to a simple log file, which you can go back and audit later.

## Example

> _You open Ableton late at night and accidentally set the gain on Track 3 to `0`, add then a key map to toggle the compressor plugin on the master bus._
>
> The next day Track 3 isn't producing signal. What do?


### Here's an example of the textfile that would be written:

```
Jul 15 00:00:01 Opened project POP_ROCK2021_remix
Jul 15 00:01:01 Unfreeze Track 3
Jul 15 00:01:31 Highlighted Utility Rack
Jul 15 00:01:31 Gain value now 0
Jul 15 00:01:59 Freeze Track 3
Jul 15 00:02:01 Keypress W
Jul 15 00:02:02 Keypress H
Jul 15 00:02:10 Highlighted Track Master
Jul 15 00:02:23 Added "Compressor" to Track Master
Jul 15 00:02:27 Keypress Ctrl + K
Jul 15 00:02:41 Clicked I/O button on Compressor Rack
Jul 15 00:02:43 Keypress 7
Jul 15 00:02:51 Keypress Ctrl + K
Jul 15 00:02:52 Keypress Ctrl + S
Jul 15 07:00:00 Quit project POP_ROCK2021_remix
```

Now you can follow through the events of what happened on the commute to your
job or whatever so you don't have to fuck around with it when you actually just
want to work on music when you get off.

## Reasoning

1. It sucks when you make a lot of work for your future self.
2. Text file can be versioned.
3. Text file can be shared.
4. Text file can be parsed quickly with `Ctrl + F`
5. Text file can be filtered easily. Maybe you only want to see "Freeze" and "Unfreeze" events for tracks, for example.

## Problems

1. Can you hook into DAW events at that level?
2. What I/O do you log?
  - Just user interface devices?
  - MIDI control messages?
  - Ext. In signal?
  - Could get noisy and messy
3. How hard is it to log chord keypresses so you're not logging stuff like:
  ```
  Keypress Ctrl
  Keypress K
  ```
  when it should really be a single event?


## Design

### Proposed file structure

```
├── dawlog/
│   └── logs/
│       └── Fri Jul 15/
│           ├── current.log
│           ├── dawlog_09:39:25.log
│           └── dawlog_11:01:05.log
```
