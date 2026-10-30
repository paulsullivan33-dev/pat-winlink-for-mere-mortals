# The Moving Parts

**Outcome: for every piece of a Winlink
exchange, you can name the part that
holds it — the server, the gateway, the
mailbox, the modem, the config file.**
The check: after reading, look at the
mailbox folder layout in the last
section and say where an unsent message
lives, and in what form.

## The far end: CMS and RMS

Two kinds of station do the carrying,
and neither is on your desk.

The **CMS** (Common Message Servers) are
Winlink's centre: a small set of servers
that hold every Winlink user's mail,
route between users, and pass mail to
and from the ordinary internet. When Pat
connects "to Winlink", the CMS is the
destination of the journey, even when a
radio carries the first hop.

An **RMS gateway** (Radio Message
Server) is the on-ramp. Each is a
volunteer's station — radios, antennas,
a computer running gateway software —
listening on published frequencies in a
published mode. Your client connects to
a gateway; the gateway's internet link
passes your mail to the CMS; replies
come back down the same chain. There are
hundreds of gateways, on VHF for local
reach and on HF for regional and
oceanic reach. Chapter 9 is about
finding the right one: Pat downloads the
whole catalogue and sorts it by distance
from you.

Some gateways also run in **hybrid**
mode, forwarding mail radio-to-radio
between gateways when the internet at
their end is down. Chapter 11 covers
that and the *radio-only* setting it
pairs with.

## Your end: the mailbox

Pat keeps your mail the way a careful
clerk would: as files, in a folder, in
the open. By default the mailbox lives
at `~/.local/share/pat/mailbox`, with one
subfolder per call sign, and inside it
four folders whose names are their jobs:

- **in** — messages that arrived and are
  waiting to be read
- **out** — messages composed and
  waiting for the next connection
- **sent** — messages a connection has
  carried away
- **archive** — messages you have filed
  for keeping

Each message is a single file named by
its **MID** (message ID), a short code
like `DDHO73ZWOUYF`, with the extension
`.b2f`. Open one and it is mostly
readable text — headers first, then the
body. The lab's transcript t02 shows one
in full:

```text
Mid: DDHO73ZWOUYF
From: N0CALL
Subject: Weekly check-in schedule
To: SMTP:friend@example.com
Type: Private

Hello, ...
```

Two details in that header carry weight
later. `Type: Private` marks ordinary
user mail (position reports and
bulletins have their own types). And the
`SMTP:` in front of the internet address
is how Winlink says "this one leaves the
system for the internet"; a bare call
sign means "another Winlink user".

**B2F** is the name of the exchange
protocol — the conversation Pat holds
with a gateway or server during a
connection: who has mail for whom,
compressed message bodies passed in
turn, receipts confirmed. You never
speak it by hand, but the file format
wears its name, and chapter 13's errors
sometimes speak it too.

## The carriers: six transports

A **transport** is how Pat reaches the
far end. `pat help connect` lists them,
and the lab's transcript t06 keeps the
list verbatim:

- **telnet** — plain TCP over the
  internet, straight to a CMS. No radio.
  Chapter 7.
- **ardop** — ARDOP, a sound-card mode
  for HF: your computer's audio becomes
  the modem, your radio carries it.
- **ax25** — AX.25 packet radio, the
  classic VHF data mode, through one of
  three engines (next section).
- **varahf** and **varafm** — the VARA
  modem programs for HF and VHF/UHF:
  fast, popular, and separate software
  Pat drives.
- **pactor** — Pactor through an SCS
  hardware modem: the expensive,
  capable, hardware path.

Every connection is named by a small
URL-like string: `ardop:///CALLSIGN`,
`telnet` (a built-in alias), or a full
address like the one sitting in the
default config for the telnet alias,
`telnet://{mycall}:CMSTelnet@cms.winlink.org:8772/wl2k`
— your call sign, the shared telnet
password `CMSTelnet`, the CMS host, port
8772, and the `wl2k` service name.
Chapter 7 unpacks it; chapter 8 handles
the radio forms.

## The modem layer: TNCs and sound cards

Between Pat and a radio there is always
a **TNC** (terminal node controller):
the thing that turns data into tones and
tones back into data. Three shapes:

- **Software, through a sound card.**
  ARDOP runs as its own program (Pat's
  config expects it at `localhost:8515`).
  For packet, **Dire Wolf** is a software
  TNC that talks to Pat through the
  **AGWPE** protocol (config default
  `localhost:8000`). This series has a
  whole guide to Dire Wolf.
- **The Linux kernel's AX.25 stack** —
  Pat can use an AX.25 port you have
  configured in the operating system
  (config names the port `wl2k`).
- **Hardware.** A serial TNC for packet
  (config default `/dev/ttyUSB0`, 9600
  baud, 1200 baud on air, Kenwood-style
  commands) or an SCS PTC modem for
  Pactor.

Rig control — making the radio change
frequency and key up by itself — is a
separate thread: Pat can drive radios
through **Hamlib**, which is why the
config has a `hamlib_rigs` section and
this series has a Hamlib guide. Manual
tuning and a finger on the microphone's
transmit button also work; automation is
a convenience, not a requirement.

## The config file, GPS, and forms

Three supporting parts finish the map.
The **config file** (default
`~/.config/pat/config.json`) is one JSON
text file holding your call sign,
locator, password, and every transport's
settings; chapter 4 walks it. **GPS**:
Pat can ask a **GPSd** daemon where you
are (config default `localhost:2947`) to
stamp your **locator** — your grid
square — and to post position reports
(chapter 10). And the **forms library**
(default `~/.local/share/pat/Standard_Forms`)
holds the HTML form templates Winlink's
emergency groups use, so a message can
be a filled-in ICS or Red Cross form
rather than free text (chapter 10).

## The check

An unsent message lives in
`mailbox/<your call>/out/`, as one
`.b2f` file named by its message ID,
waiting for a connection over one of
the six transports to carry it — through
a gateway's radio, or straight up the
internet — to the CMS. If you can point
at each noun in that sentence and say
which part of this chapter it came from,
the map is yours.
