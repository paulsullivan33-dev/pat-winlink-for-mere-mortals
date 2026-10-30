# Listening and Peer to Peer

**Outcome: you understand the three ways
mail moves without you dialling the CMS
yourself — being listened *for*, talking
station to station, and the radio-only
network.** *Documented chapter: each
mode here is a way of connecting, and
the lab made no connections
(chapter 1). The flags and settings
quoted are Pat's real ones, from its
help (t00, t06) and the config it writes
(t01).*

## Listening: Pat as a door

Ordinarily Pat connects *out*. The
`--listen` flag reverses the arrow:

```bash
pat --listen ardop,telnet http
```

Pat now *accepts* connections on the
listed transports — the flag is a
comma-separated list from the same
family as chapter 8's transports —
while the web mailbox serves as the
operator's chair. Another station that
connects exchanges mail with you
directly, using your machine as its
far end.

Who uses this? A station set up as a
local hub for a group; an operator who
wants their home station to collect
mail from their portable station; and
the second mode, below, which needs one
end to be listening. A listening Pat is
a station making an offer to the band,
and the obvious caution applies: an open
telnet listener is an open door on the
internet too — the config's `telnet`
section carries a `password` field and a
`listen_addr` (default `:8774`) for
exactly this reason. Set both thinking
like chapter 5.

## Peer to peer: no centre at all

Two Winlink stations can exchange mail
directly, radio to radio, with no
gateway and no CMS in the session at
all. That is **peer to peer** (P2P): one
station connects, the other must be
listening on the same frequency and
mode, and the outboxes and inboxes trade
places' contents. Mail a message is
marked for with `--p2p-only` (there is a
matching switch in the browser) will
travel *only* this way — it will not be
left with a gateway for the CMS.

P2P is the most resilient shape Winlink
has — two stations and the ionosphere,
no infrastructure anywhere in the loop —
and the least convenient: both ends,
same frequency, same mode, same time,
one of them listening. Nets and
exercises schedule such things; the
software just has to be told.

## Radio-only and the hybrid network

Between "the CMS by any road" and "P2P
only" sits the hybrid design (chapter 2
mentioned its gateways). Some RMS
stations run as **hybrid** gateways:
when their internet is down, they
forward mail *by radio*, gateway to
gateway, toward one that still has a
link — and ultimately to a **message
pickup station** (MPS), a designated
station holding mail for collection.

Pat's side of this is one flag and one
command. `--radio-only` (a global
option, in t00's help) tells Pat to use
only the radio/hybrid path and not
deliver through the internet side of
the system; `pat mps` manages which
pickup stations serve you. Groups whose
doctrine is "the internet is what's
broken; plan for it" run this way by
policy. The mode exists for the day
everything in chapter 7 is pointless —
and using it well means arranging it,
with your group, before that day.

## The check

You have this chapter when you can sort
three situations to their modes: the
club hub that accepts everyone's
connections is *listening*; the two
tents trading mail with the county net
down are *peer to peer*; the region
whose gateways relay radio-to-radio
until one finds a working uplink is the
*hybrid, radio-only* network. Same
mailbox, same messages — three different
agreements about what "connected" means.
