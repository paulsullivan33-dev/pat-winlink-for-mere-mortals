# Connecting by Telnet

**Outcome: you understand the internet
path to Winlink end to end — and why it
is the best first connection to make.**
*This chapter is documented, not
lab-run: the lab's call sign, N0CALL,
has no Winlink account, so no live
connection was attempted or is
pretended. The commands are Pat's own
documented forms, grounded in its help
text (transcript t06).*

## Why telnet first

Telnet here is not the vintage remote-
login program; it is Pat's name for the
internet transport — a TCP connection
from Pat to the Winlink central servers,
with no radio involved. Every operator
should make one early, for three
reasons. It needs no station at all:
computer, internet, account, done. It
exercises exactly the same mailbox
machinery as a radio connection, so
when a radio path fails later, the
mailbox is already a known quantity.
And it validates the account — call sign
and password — which is the one piece a
radio connection cannot debug by itself.

If you are licensed but radio-less, or
your radio is still in a box, telnet is
also simply how you use Winlink. Plenty
of operators do most of their mail this
way, and there is no shame in it:
the network serves both roads equally.

## The one command

```bash
pat connect telnet
```

`telnet` is the built-in alias in the
default config. It expands to the
address Pat ships with:

```text
telnet://{mycall}:CMSTelnet@cms.winlink.org:8772/wl2k
```

Read it right to left of the `@` first:
`{mycall}` becomes your call sign, and
`CMSTelnet` is the shared password for
the telnet service — the same for
everyone, which is why your *account*
password matters elsewhere. Then the
host, `cms.winlink.org`, port 8772, and
the service name `wl2k`. You can write
aliases of your own in `connect_aliases`
for the same shape — a second CMS host,
a personal gateway — but the default is
the front door, and it is enough.

## What a session does

Connect, and Pat and the server hold a
B2F exchange: the two sides compare
mailboxes. Pat offers every outbox
message (and, with `-s`/`--send-only`,
uploads before anything else is even
considered); the server accepts each in
turn and Pat moves it to **sent**. Then
the direction reverses: mail waiting for
you is downloaded into **in**, any
bulletins you are subscribed to arrive,
and receipts are confirmed both ways.
Pat prints the session as it goes — the
status line in the web mailbox, or the
terminal log — and then the connection
closes. Nothing is left half-done: a
message is **out** until the far end has
accepted it, and only then **sent**.

For a first session, compose one small
message to yourself first (chapter 6's
shape, addressed to your own call sign)
and one to an internet address you can
check. Send, wait a little, connect
again, and watch the inbox fill from the
other end. That round trip is the
certificate for everything else in this
guide.

## When it does not work

*Wrong password*: the handshake fails
before any mail moves — check
`secure_login_password` in the config
and the account's password recovery
address (chapter 4). *No route to the
host*: the telnet service lives at a
single host and port, so a firewall that
blocks outbound 8772 is the usual
culprit; a plain `nc -zv cms.winlink.org
8772` tells you whether the road is
open (this is a network check, not a
connection, and it asks nothing of your
account). *Mail stuck in out*: a
message the server rejects — an address
Winlink will not deliver to, or a
message over the size the system accepts
— stays put, and Pat's log says why.
Chapter 13 gathers the local errors the
lab met; the server's own refusals live
in the session log, and that is where
you look.

## The check

You have this chapter when you can say
what `pat connect telnet` does without
looking: opens the alias to the CMS on
port 8772, uploads your outbox, downloads
your inbox, and reports — and when you
know that a successful first telnet
session is the proof your account works,
before any radio enters the story.
