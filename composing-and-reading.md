# Composing and Reading

**Outcome: a message written by you,
sitting in your outbox, found again by
three different routes — and a clear
picture of how reading works when mail
arrives.** The check is built into the
chapter: the same message ID appears in
the folder listing, in `pat read`, and
in the web mailbox.

## Composing on the command line

`pat compose` has two tempers. With no
arguments it is interactive: it asks for
recipients and a subject, then opens
your editor for the body. With
arguments, it behaves like the classic
Unix `mail`: flags carry the envelope,
and the body arrives on standard input.
Its own help (transcript t06) says so,
and the scripted form is the one this
guide teaches, because it can be checked:

```bash
printf 'Hello,\n\nThis is a test message written in the lab.\n' \
  | pat compose friend@example.com -s "Weekly check-in schedule"
```

Pat's whole reply is `Message posted`.
That modesty hides a complete act: the
message was written into your outbox as
a file (chapter 2's map, made real):

```text
mailbox/N0CALL/out/DDHO73ZWOUYF.b2f
```

Open it and the headers tell the story —
`From: N0CALL`, `Subject:`, `Type:
Private`, and the recipient stored as
`To: SMTP:friend@example.com`. Which
brings up the addressing rule, worth
learning now: **a bare call sign reaches
a Winlink user; an internet address is
stored with `SMTP:` in front**, Winlink's
marker for "deliver this out to the
internet". You type both the same way;
Pat and the CMS sort out the rest.
`--cc` adds carbon copies; `-a` attaches
a file, and may be repeated — remember
chapter 12's arithmetic before attaching
anything large to a radio-bound message.

## Composing in the browser

With `pat http` running (chapter 5), the
Compose button does the same job with a
form: recipients, subject, body,
attachments. It lands in the same
outbox, as the same kind of file,
because there is only one mailbox and
two faces on it. Which face you use is
temperament, not capability.

Forms-based messages — the ICS and
agency forms of chapter 10 — start from
`--template`, or from the forms picker
in the browser. Same outbox again.

## Reading: the folders, honestly

Reading has two halves, and this guide
can only demonstrate one of them.
Messages *you* wrote are here to read
back; messages *for* you arrive only
across a connection, and the lab had
none (chapter 1 explains why). The
machinery is identical either way, and
the lab proved it on the outbox:

```bash
pat read
```

offers the four folders by number —
`0:in  1:out  2:sent  3:archive` — and
inside a folder, a table: subject, from,
date, to. The lab's outbox table
(transcript t02) shows its one message,
`Weekly check-in schedule`, from N0CALL,
to friend@example.com. Choose the
message and Pat prints it in full, then
offers the actions on any message:
reply, reply-all, forward, extract
attachments, delete, quit. (`pat extract`
does the attachment part non-interactively,
straight from a message file.)

The browser route shows the same
folders and the same message — chapter
5's API transcript is the third sighting
of `DDHO73ZWOUYF`. Three faces, one
mailbox, one file. When a real
connection someday fills your **in**
folder, nothing new needs learning: new
mail is read exactly where test mail
was.

## Where messages go when sent

A successful connection (chapters 7 and
8) moves each outbox message to **sent**
as it is accepted by the far end, and
drops arriving mail into **in**. If a
connection fails halfway, what was not
accepted stays in **out** — nothing is
half-sent, and nothing needs unsending.
The folders are the state; the state is
files; the files do not lie. That
plainness is Pat at its best, and it is
why this guide keeps pointing at them.

## The check

Compose one message by the scripted
route. Find its file under
`mailbox/<your call>/out/`, its row in
`pat read`, and its entry in the web
outbox. Same MID in all three: you hold
the whole local life of Winlink mail in
your hands, and only the carrying of it
remains.
