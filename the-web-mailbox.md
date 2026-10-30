# The Web Mailbox

**Outcome: your mailbox open in a
browser — inbox, outbox, compose — served
entirely by your own machine.** The
check: the browser tab's title reads
*Pat - Mailbox*, and the lab's curl
transcript (t03) proves the same page
answers even with no browser involved.

## Starting the server

One command:

```bash
pat http
```

Pat answers with the line from
transcript t03:

```text
Starting HTTP service (http://localhost:18080)...
```

(the lab's config points at port 18080;
yours says 8080 unless you changed it —
chapter 4). Pat is now a small web
server. It stays in the foreground of
that terminal, logging as it works;
Ctrl-C stops it. Leave it running and
open the address in a browser. The bare
address redirects to `/ui`, and the page
that loads is your mailbox: folder list
on one side — in, out, sent, archive —
messages in the middle, and buttons to
compose, reply, and connect.

Nothing about this page lives anywhere
else. The HTML, the scripts and your
mail all come from the Pat process on
your machine; you could pull the network
cable and the mailbox would still open.
That is the point of the design, and
also its warning, next section but one.

## What you can do in it

Everything the command line does, this
page does friendlier: read a message,
compose one (chapter 6), attach a file,
watch a connection happen — the Connect
dialog takes the same transport
addresses chapter 2 introduced, and the
status line shows the session as Pat
sees it. For many operators this page is
Pat, full stop; the command line matters
when you script, or when a browser is
more computer than the station has.

## The warning: it has no lock

The web mailbox does not ask who you
are. Anyone who can reach that port can
read your mail and send as you. That is
a reasonable design **only** because the
default address is `localhost` — the
same machine, where "anyone" is you.
Keep it that way. Do not change
`http_addr` to expose the port on your
network, and doubly not on the internet,
unless you have put real access control
in front of it yourself. The config will
let you; this guide will not help. Treat
the mailbox like the radio it drives:
your call sign, your responsibility.

## Under the page: a small API

The browser page is a skin over a plain
HTTP API, and the lab used it as a
measuring instrument — what the API
reports is what the program believes.
Three stops, all in transcript t03:

```bash
curl -s http://localhost:18080/api/status
```

```json
{"active_listeners":[], "connected":false, "dialing":false, ...}
```

Status: not connected, not dialing, no
listeners — the machine at rest.

```bash
curl -s http://localhost:18080/api/mailbox/out
```

lists the outbox as JSON: one entry per
waiting message, with its MID, subject,
sender and recipients. And
`/api/mailbox/out/<MID>` returns one
message in full, body included — the
very message chapter 6 composes, which
is how the lab knew, from a second and
third direction, that the message really
was in the mailbox. You may never need
the API; scripts and curious minds both
like knowing it is there.

## The check

`pat http` running, the page open, title
*Pat - Mailbox*, outbox showing the
folders of chapter 2 — that is the whole
claim of this chapter, and all of it
happens without an account, a radio, or
a network. If the page does not load,
chapter 13 has the port error, quoted
word for word.
