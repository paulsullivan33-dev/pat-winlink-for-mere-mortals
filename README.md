# Pat (Winlink) for Mere Mortals

Email usually needs the internet. Take
the internet away — a storm, a remote
cabin, a boat, a town whose cell towers
are down — and ordinary email stops.
**Winlink** is the system built for
exactly that gap: a worldwide network of
radio gateways and central servers that
moves email over amateur radio. You write
a message on your computer, your computer
talks to a radio, the radio talks to a
gateway station, and the message comes
out the other side as email — or travels
radio-to-radio to another ham.

**Pat** is the program this guide teaches:
a free, open-source **Winlink client** for
your own computer. It holds your mailbox,
lets you write and read messages in a web
browser window or on the command line, and
connects out through whichever path you
have — plain internet, an HF radio with a
sound-card modem, a packet TNC, or a VARA
modem. It runs on Windows, macOS and
Linux, including a Raspberry Pi.

One rule stands in front of everything
else, so here it is on page one: a Winlink
account belongs to a **licensed amateur
radio call sign**, and transmitting on ham
frequencies needs that licence. This guide
uses the placeholder call sign **N0CALL**
in every example. N0CALL is nobody; it has
no account and cannot connect to anything.
Where you see it, picture your own call
sign in its place once you have one. The
lab that wrote this guide used N0CALL too,
which is why the lab's work stops, honestly
and on purpose, at the edge of a real
connection: everything up to the connection
was run and measured; the connections
themselves need a real account and are
taught from the documentation, labelled as
such wherever they appear. `criteria.md`
keeps the full ledger.

What the lab did run is the whole local
life of the program: **Pat 1.0.0**, the
official release binary, installed from
the project's own tarball; the default
config file Pat writes for itself, read
field by field; a mailbox created for
N0CALL; a message composed on the command
line and found again in three places — the
mailbox folder on disk, the `pat read`
listing, and the web mailbox Pat serves on
your own machine; the live gateway
catalogue downloaded from winlink.org and
searched by distance; and the standard
forms library — 13 MB of it — downloaded
and unpacked. The lab also broke things
on purpose: Pat with no call sign answers
*Missing mycall*, and a second copy of the
web server fails with the port already
in use, both quoted exactly in chapter 13.

## What this guide covers

- [**What Winlink and Pat are**](what-winlink-and-pat-are.md) —
  email that works when the internet
  doesn't, the shape of the Winlink
  network, and the licence rule stated
  before anything depends on it
- [**The moving parts**](the-moving-parts.md) —
  the central servers, the gateway
  stations, your mailbox and its four
  folders, the message files themselves,
  and the six ways Pat can carry a
  message — and which part holds what
- [**Installing Pat**](installing-pat.md) —
  the release download, what is inside
  it, and the version check that proves
  it runs
- [**Your account and config**](your-account-and-config.md) —
  how a Winlink account comes to exist,
  and the config file taken field by
  field: call sign, locator, password,
  and the address the web mailbox lives at
- [**The web mailbox**](the-web-mailbox.md) —
  `pat http`: your mailbox in a browser,
  served by your own machine, and a look
  at the small API underneath it
- [**Composing and reading**](composing-and-reading.md) —
  writing mail on the command line and in
  the browser, call signs versus internet
  addresses, attachments, and reading
  what waits in each folder
- [**Connecting by telnet**](connecting-by-telnet.md) —
  the internet path: one command, what a
  session does with your outbox and
  inbox, and why it is the right way to
  learn the ropes (documented)
- [**Connecting by radio**](connecting-by-radio.md) —
  the radio paths: ARDOP, packet radio
  and AX.25, VARA, and Pactor — what each
  needs plugged into what (documented)
- [**Finding a gateway**](finding-a-gateway.md) —
  `rmslist`: the live catalogue of
  gateway stations, sorted by distance
  from your grid square, and how to read
  its frequencies
- [**Forms and position reports**](forms-and-position-reports.md) —
  the standard forms library emergency
  groups actually use, and posting where
  you are
- [**Listening and peer to peer**](listening-and-peer-to-peer.md) —
  letting other stations connect to you,
  mail that never touches the internet,
  and the radio-only mode
- [**Limits**](limits.md) — no account, no
  connection; radio is slow; nothing over
  ham radio is private; and the rest,
  stated plainly
- [**Troubleshooting**](troubleshooting.md) —
  the missing call sign, the busy port,
  the guided setup prompt, and the other
  traps, including the ones this guide's
  lab fell into
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

Getting an amateur radio licence — that
is a course of study of its own, and this
series' Ham Radio guide is the place to
start. Choosing or buying a radio, an
antenna, or a hardware TNC: the guide
names what each connection path needs,
and stops there. Setting up the sound-card
modems themselves in depth — Dire Wolf has
its own guide in this series, and chapter
8 points at it once and completes without
it. Winlink Express, the Windows client
most hams learn first, is mentioned only
as a neighbour; this guide teaches Pat.

## How to use this guide

Read chapter 1 for the model and chapter
2 before installing anything — knowing
which part holds what turns later
confusion into a named problem. Chapters
3 and 4 give you a program and a config;
chapter 5 opens your mailbox in a browser
the same sitting, and chapter 6 puts a
message in it. That much needs no
account, no radio and no licence, and it
is all verified. Chapters 7 and 8 are the
connection chapters: read them with your
account and your station in mind, and
treat them as documentation — the guide
says so inside them too. The lab's
transcripts live in
`pat-winlink-lab/transcripts/`, and its
finished example config is
`pat-winlink-lab/config.example.json`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [Ham Radio for Mere Mortals](https://paulsullivan33-dev.github.io/ham-radio-for-mere-mortals/)
- [Dire Wolf for Mere Mortals](https://paulsullivan33-dev.github.io/dire-wolf-for-mere-mortals/)
- [Fldigi for Mere Mortals](https://paulsullivan33-dev.github.io/fldigi-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/pat-winlink-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/pat-winlink-for-mere-mortals/blob/main/LICENSE-CODE).
