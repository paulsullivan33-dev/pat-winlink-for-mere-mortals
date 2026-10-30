# Troubleshooting

**Outcome: the failures you are most
likely to meet, each with its cause
named and its check given.** The first
three are the lab's own, quoted exactly
from transcript t07; the rest are the
documented traps, marked as such.

## `Missing mycall`

```text
$ pat env
Missing mycall
```

Two words and a full stop to everything.
**Cause:** the config Pat read has an
empty `mycall` — either Pat found no
config at all, or the one it found was
never filled in. **Check:** `pat env`
itself, once a config exists, prints
`PAT_MYCALL` plus `PAT_CONFIG_PATH` —
the path line is the confession. If the
path is not the file you have been
editing, you have been editing a
different config than Pat is reading;
the `--config` flag exists for settling
that (the lab used it in every command).

## The greeting that looks like an error

```text
Hello there! Do you want to be guided through the basic setup?
```

**Cause:** none — Pat found no config
file and is offering the guided setup.
Answer `Y` for `pat init`, or `n` and
Pat writes the default file for you to
edit (chapter 4). It appears once, on
the first run, in whichever command you
happened to start with.

## `bind: address already in use`

```text
Starting HTTP service (http://localhost:18080)...
listen tcp 127.0.0.1:18080: bind: address already in use
```

**Cause:** something already holds the
web mailbox's port — very often another
copy of Pat you left running (the lab
produced this exact error by starting a
second server on purpose, t07), or, on
the default 8080, another program
entirely. **Check:** stop the other
copy, or give this one a different port
with `http_addr` in the config (chapter
4). Note Pat prints the *Starting* line
first and the failure second: a log that
ends at *Starting* is a server that did
not, in fact, start.

## Pat reads a different world than you set up

Mail, config or forms are not where you
left them. **Cause:** the default paths
(`~/.config/pat`, `~/.local/share/pat`,
`~/.local/state/pat`) versus flags
pointing elsewhere — Pat happily runs
with several sets of folders, and your
two terminals may be using different
ones. **Check:** `pat env` prints every
path in force: `PAT_CONFIG_PATH`,
`PAT_MAILBOX_PATH`, `PAT_FORMS_PATH`,
`PAT_LOG_PATH`. Compare them with where
you have been looking. This one trap
explains most "my message vanished"
reports: it was posted to the other
mailbox.

## Compose hangs, or eats the terminal

**Cause:** `pat compose` *with no
arguments* is interactive — it is
waiting, politely, for you. In a script,
always pass at least a recipient and
`-s`; with flags present, compose reads
the body from standard input and exits
with `Message posted` (t02, t06).
Symmetrical trap: piping a body to the
interactive form accomplishes nothing;
the flags are the switch between the
two tempers.

## The gateway list is from the wrong place

`rmslist -s` sorts, but the distances
are another continent's. **Cause:** your
`locator` is empty, wrong, or somebody
else's leftover — the sort is honest
arithmetic on a wrong input. **Check:**
`pat env` shows `PAT_LOCATOR`; chapter 4
shows where it lives. A subtler variant
(documented): with no internet, rmslist
uses its last download, so a stale list
wears a fresh face — `rmslist -d` forces
a new download when the road is open.

## A connection fails before it starts (documented)

The modem layer is not there. Pat's
config promises ARDOP at
`localhost:8515`, Dire Wolf's AGWPE at
`localhost:8000`, VARA at
`localhost:8300` — if the modem program
is not running and listening there, the
connection cannot begin, and the error
is about addresses, not radios.
**Check:** start the modem first, then
Pat; and when an address in the config
was edited, confirm the modem's own
settings moved with it. Frequency and
rig complaints, by contrast, come from
the Hamlib thread: a rig name in the
config that the running rigctld does
not know fails politely but firmly, and
chapter 8's answer stands — automation
is a convenience; set the dial by hand
and connect without it while you sort
the rig control out.

## Mail that will not leave the outbox (documented)

Stays in `out` across connections that
otherwise succeed. **Cause:** the far
end refused *that message* — an address
it cannot deliver, a size it will not
carry. **Check:** the session log names
the refusal; the message file itself
(chapter 2) shows the exact headers Pat
offered. Fix the message or set it
aside into `archive` by hand — the
folders are yours to move files in,
which is the quiet superpower of the
whole design.
