# Forms and Position Reports

**Outcome: the standard forms library
downloaded onto your machine, and a
clear picture of the two special message
kinds — form messages and position
reports.** The check: your forms folder
holds the same named collections the
lab's does (transcript t05); one part of
this chapter (posting a report) needs a
connection and is labelled documented
where it stands.

## Why forms at all

Emergency communications runs on forms.
When a served agency — a county, a
hospital network, the Red Cross — takes
a message, it takes it on *their* form:
fixed fields, fixed order, no prose to
misread at 3 a.m. over a fading channel.
Winlink's answer is a library of HTML
forms that travel with the system. A
sender fills in the form; what crosses
the radio is a compact text rendering
plus the small data file that lets the
receiving end redraw the same filled
form. Pat carries the whole library as
the **Standard Forms**, and composes
with them natively.

## Getting the library: verified live

```bash
pat templates update
```

That is the whole procedure, and the
lab ran it for real (transcript t05).
Pat fetched `Standard_Forms_1.1.22.0`
from the project's forms service —
about 13 MB — and unpacked it into the
forms folder. The top level is a map of
the world the library serves: **ARC
Forms** (Red Cross), **FEMA Forms**,
**ICS USA Forms** (the incident-command
set: the ICS-213 general message form
lives here), **General Forms**, **General
Medical Forms**, state and regional
collections, and more. Run the update
again whenever you like; the library is
versioned, and chapter 12 notes the one
drift that matters — sender and receiver
on very different library versions can
render a form differently, so groups
update together.

Composing with a form is chapter 6 with
one flag: `pat compose --template
<path-to-form>` — or, in the browser,
the forms picker — and the message that
lands in the outbox is the form's data,
ready for any transport. The lab did not
send a form anywhere (no account, no
connection) and does not pretend
otherwise; the library download and the
file layout are the verified parts.

## Position reports

A **position report** is a tiny message
that says *I am here*, stamped with your
locator or exact coordinates and an
optional comment, which the Winlink
system plots for anyone who looks up
your call sign. Boats, travellers and
event stations live on them.

```bash
pat position -c "QRV 145.500MHz"
pat position --latlon 40.704,-73.945
```

The first takes coordinates from GPSd
*if* you run it (chapter 2: Pat's config
points at `localhost:2947`, and its
`gpsd` section can even keep your
`locator` fresh as you move); the second
states them by hand, decimal degrees,
as in the command's own help
(transcript t06, whose example comment
the first line borrows). What happens
next is the documented part: the report
is posted as a message over your next
connection, so it inherits chapter 7's
and 8's machinery whole — and the lab,
having no connection, posted none. The
*command's shape and the config behind
it* are verified; the posting is not,
and this guide keeps the two apart
deliberately.

## The check

`ls` your forms folder: the named
collections of t05 should be there, 13 MB
of other people's careful standardisation.
And you can say how each special message
is born — a form from the library, filled
in and filed like any message; a position
report from the `position` command,
waiting for a connection like any
message — because in Pat there is no
second machinery for them. There is only
the mailbox, and messages of different
types in it.
