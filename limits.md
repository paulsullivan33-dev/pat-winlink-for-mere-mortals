# Limits

What Pat and Winlink cannot do, stated
plainly. The lab met some of these
itself; the rest are properties of the
system, labelled as such.

**No account, no connection.** Everything
past the mailbox — every transport,
every gateway — requires a Winlink
account, and the account requires a
licensed call sign. There is no trial
mode and no guest band. The lab's whole
existence proves the boundary from the
inside: with N0CALL it could install,
configure, compose, serve, download the
gateway catalogue and the forms library
— and connect to nothing.

**Radio is slow. Plan like it.** The
transports of chapter 8 move hundreds
to a few thousand bits per second on HF,
1200 baud on ordinary packet. A page of
text is nothing; a photograph is an
event; a large attachment is an
imposition on a shared, volunteer-run
network, and the system has message
size limits besides. Winlink is email
for the message that matters, at the
length that matters needs.

**Nothing on the air is private.**
Amateur rules forbid obscuring traffic,
so Winlink over radio is open by design:
anyone with a receiver and the software
can read what passes, and the system
keeps no secrets for you. The telnet
path is ordinary internet email, with
ordinary internet email's privacy —
which is to say, plan accordingly in
both worlds. Do not put in Winlink mail
what you would not say on the air,
because on the radio paths you *are*
saying it on the air.

**The network is volunteers.** Gateways
are hams' stations, run at hams'
expense, on hams' schedules. A gateway
in chapter 9's live catalogue today may
be silent next month; frequencies move;
the CMS is a small set of servers
maintained for a niche worldwide
service. It has run for decades and is
sturdier than it sounds — but no one's
job depends on your message arriving,
including, in the end, yours. Emergency
plans that name Winlink name it as one
layer among several, never the layer.

**One mailbox, one call sign, at a time.**
A Pat process serves the config it was
started with. Auxiliary addresses let a
station receive under tactical names,
but a second call sign is a second
config — the lab's flag-based setup
(chapter 3) shows the shape of running
several, and it is plumbing you build
yourself.

**Pat drives modems; it is not one.**
Every radio path needs its modem layer
alive first — ARDOP or Dire Wolf or
VARA already running and listening
where the config says. When a
connection fails, the modem layer is
as likely to be the story as Pat is,
and Pat's log cannot always tell you
which (chapter 13).

**VARA is a guest.** The fastest
sound-card path is closed-source,
single-author, Windows-native software.
Pat's support for it is real, but the
mode's future, licence and Linux-under-
Wine comforts are outside this project's
gift — and outside this guide's
verification.

**The web mailbox has no lock.** Restated
from chapter 5 because it belongs in
any honest limits list: `pat http` does
not authenticate its user. Localhost
only, by design and by your discipline.

**Forms drift.** The forms library is
versioned (the lab's download was
1.1.22.0), and a form's rendering
depends on the receiver having a
compatible library. The tooling handles
the common cases; groups that exchange
forms keep their libraries updated
together, because the failure mode —
the same message, two readings — is
quiet.

**This guide's edge.** No live
connection, no transmission, no radio,
and no listening were done by its lab:
chapters 7, 8 and 11 are the
documentation's account, checked against
Pat's own help and defaults, and are
labelled where they stand. What a real
station sounds like at 300 baud through
a bad night on 40 metres, this guide
cannot tell you. It can only make sure
that when you get there, the mailbox
part is already boring.
