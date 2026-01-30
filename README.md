# nap

This is a simple command line script to use the Apple macOS
power management settings command `pmset` to go to sleep now,
then wake at a given datetime, and optionally run a command.

Syntax:

```sh
nap <n hours> [command]
nap <hh:mm:ss | description> [command]
```

## Examples

Nap until noon:

```sh
nap today 12:00
```

Nap until noon then run a command:

```sh
nap today 12:00 say hello
```

Nap until 2027 new year midnight then run a command:

```sh
nap 2027-01-01 00:00 say happy new year
```

Nap for five hours then run Claude AI on a tasks file:

```sh
nap "5 hours" say happy new year
```

5-hour basis.

## Date descriptions

If your system has a command `gdate` or command `date` that
supports the option `--date=` for a date description string,
then you can create a date or time such as:

```sh
nap today "3 hours"
nap tomorrow 12:00
nap "3 days" 12:00
nap "next saturday" 12:00
```

If you want to install GNU coreutils which has the GNU command `gdate`,
and you use brew, then you can run:

```sh
brew install coreutils
```

## Command

If you specify a command, then nap will schedule it for one minute
after the wake time, because this helps the machine have time to spin up.

Because of this timing increment, please choose a minute from 00 to 58, not 59.

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

- `sudo pmset repeat wake M 8:00:00`: Schedule wake at 8:00 am every Monday.

- `sudo pmset repeat cancel`: Cancel the current schedule.

You may want to know about similar pmset options:

- `wake`: wake up a Mac that is sleeping e.g. by inactivity or sleep command.

- `poweron`: turn on a Mac that is powered off e.g. by shut down command.

- `wakeorpoweron`: both wake and poweron.

Weekdays:

- `MTWRFSU`: Monday Tuesday Wednesday Thursday Friday Saturday Sunday

## at command

<https://en.wikipedia.org/wiki/At_(command)>

On Unix-like operating systems, at reads a series of commands from standard
input and collects them into one "at-job" which is carried out at a later
date. The job inherits the current environment, so that it is executed in the
same working directory and with the same environment variables set as when it
was scheduled.

If you prefer other ways to schedule, you may want to read about more options
for the `at` command, or about other commands such as `cron`, `anacron`, etc.
