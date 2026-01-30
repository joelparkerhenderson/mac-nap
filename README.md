# mac-nap

This is a simple command line script to use the Apple macOS
power management settings command `pmset` to go to sleep now,
then wake at a given datetime.

Syntax:

```sh
mac-nap <yyyy-mm-dd hh:mm:ss> [command]
```

Example to sleep until 2026 new year's day eight in the morning:

```sh
mac-nap 2026-01-01 08:00:00
```

Example to sleep until tonight 11 p.m., then wake, then run Claude AI on your existing tasks file:

```sh
mac-nap +%Y-%m-%d 23:00:00 "claude $HOME/tasks.md"
```

## pmset options

The command `pmset` has many options; here are the most-relevant.

```sh
pmset schedule {sleep | wake | poweron | shutdown | wakeorpoweron} "MM/dd/yy HH:mm:ss" [owner]
pmset schedule [cancel] [cancelall]
```

```sh
pmset repeat {sleep | wake | poweron | shutdown | wakeorpoweron} weekdays "HH:mm:ss"
pmset repeat cancel
```

Examples:

- `pmset -g sched`: See the current schedule.

You may want to know about similar pmset options:

- `wake`: wake up a Mac that is sleeping e.g. by inactivity or sleep command.

- `poweron`: turn on a Mac that is powered off e.g. by shut down command.

- `wakeorpoweron`: both wake and poweron.

Examples that use repeat:

- `sudo pmset repeat wake M 8:00:00`: Schedule wake at 8:00 am every Monday.

- `sudo pmset repeat cancel`: Cancel the current schedule.

Weekdays:

- `MTWRFSU`: Monday Tuesday Wednesday Thursday Friday Saturday Sunday

## Run a command

To run a command when the mac wakes up, you can use the command `at`.

Example that runs a program named `foo` a minute after eight in the morning:

```sh
echo "foo" | at 08:01
```

Example that runs Claude AI with your home directory tasks file:

```sh
echo "claude $HOME/tasks.md" | at 08:01
```

If you prefer other ways to schedule, then see the commands `cron` and `anacron`.
