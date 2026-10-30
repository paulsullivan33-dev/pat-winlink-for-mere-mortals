# What Winlink and Pat Are

**Outcome: you can say what Winlink is,
what Pat does inside it, and the one rule
that governs both — before touching a
command.** The check is the last section
of this chapter: three sentences you
should be able to say out loud.

## The problem Winlink solves

Email rests on an assumption so ordinary
we forget it is one: somewhere nearby
there is a working internet connection.
Remove it — the hurricane took the
cables, the boat is two days from shore,
the field station is a tent — and the
assumption fails. But radio does not
need the local infrastructure. A radio
signal crosses a county or an ocean on
its own.

**Winlink** (short for Winlink 2000) is
a worldwide system that carries email
over amateur radio. It has three kinds
of parts. **Central servers**, called
**CMS** (Common Message Servers), hold
mail the way an internet mail provider
does. **Gateway stations**, called
**RMS** (Radio Message Server) stations,
are run by licensed volunteers: each one
is a computer with radios, listening on
published frequencies, ready to relay
between the airwaves and the servers.
And **clients** — programs like Pat —
sit on your computer, hold your mailbox,
and connect to a gateway by radio, or to
the servers directly when the internet
still works.

Write a message in Pat and it waits in
your outbox. Connect — to a gateway over
HF radio, say — and Pat hands the message
up. The gateway passes it to the servers;
if the person you wrote to is another
Winlink user, they collect it on their
next connection, from whichever gateway
they can reach. If you wrote to an
ordinary internet address, the servers
deliver it as ordinary email. Replies
come back the same road in reverse.
Chapter 2 names each part and what it
holds.

## Where Pat fits

Several clients can speak to Winlink.
The best known is Winlink Express, a
Windows program with a long history in
emergency-communications groups. **Pat**
is the open-source one: a single program,
written in Go, released for Windows,
macOS and Linux by its maintainers (the
project lives at getpat.io), and happy
on machines as small as a Raspberry Pi.
It gives you two faces for the same
mailbox — a **web mailbox** you open in a
browser, and a **command line** that
scripts well — and it is unusually
honest machinery: your mailbox is a
folder of readable files, its settings
are one text file, and everything this
guide's lab claims, it shows from those
files directly.

Pat is a client only. It is not a
gateway, not a server, and not a radio
modem: for radio paths it drives other
programs — a sound-card modem such as
ARDOP, a packet program such as Dire
Wolf — and chapter 8 explains that
division of labour.

## The rule, stated early

Winlink accounts are issued to **call
signs**, and a call sign is issued to a
**licensed amateur radio operator**. To
transmit on the ham bands you must hold
that licence yourself; there is no guest
mode. Sending through Winlink by
internet (chapter 7) needs the account
but no transmission; every radio path
(chapter 8) needs both.

Two consequences shape this whole guide.
First, the examples use **N0CALL**, the
standard placeholder call sign. N0CALL
has no account, so no example here can
show a live connection — and none
pretends to. Second, amateur radio is a
public medium with public rules: traffic
must not be obscured or encrypted, and
it cannot carry commercial business.
Winlink mail over the radio is therefore
*carried openly*, like everything else
on the air. Email you would not read
aloud on a repeater does not belong on a
radio path. Chapter 12 returns to this.

## A first taste

Installed and configured (chapters 3 and
4), Pat's everyday shape is short. Run
the web mailbox:

```bash
pat http
```

and Pat answers with the line the lab's
transcript t03 records:

```text
Starting HTTP service (http://localhost:18080)...
```

Open that address and your mailbox is a
web page — inbox, outbox, a compose
button. Nothing has left your machine.
Or stay on the command line and file a
message into the outbox without any
connection at all:

```bash
printf 'First test message.\n' \
  | pat compose friend@example.com -s "Hello"
```

`Message posted` — and there it sits,
patiently, until a connection sends it.
Chapter 6 takes that apart.

## The check

You have this chapter if you can say:
Winlink is email carried by a network of
radio gateways and central servers for
when the internet is absent. Pat is one
client for it — the open-source,
cross-platform one — holding a mailbox on
my machine and driving whatever
connection path I have. And the account
is my call sign, so the radio paths wait
until I am licensed.
