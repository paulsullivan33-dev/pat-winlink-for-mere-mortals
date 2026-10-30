# Connecting by Radio

**Outcome: for each radio path — ARDOP,
packet AX.25, VARA, Pactor — you can say
what software or hardware it needs, what
Pat expects of it, and how a connection
is addressed.** *This chapter is
documented, not lab-run: a radio
connection needs a licensed station and
a Winlink account, and the lab had
neither. No transcript in the lab shows
a radio session, because none happened.
The settings quoted are Pat's real
defaults, read from the config Pat
writes (transcript t01) and its help
(transcript t06).*

## The shape of every radio connection

However it works, a radio connection has
three layers, and keeping them separate
turns confusion into a named layer.
**Pat** holds the mailbox and drives.
**The modem layer** — a program or a box
— turns Pat's data into tones and back,
and keys the radio. **The radio** puts
the tones on a frequency where a gateway
is listening. Pat never talks to the
radio's audio directly; it talks to the
modem layer over the addresses in its
config, and the modem layer owns the
sound card and the transmit key. Rig
control, when used, is the side thread
from chapter 2: Hamlib telling the radio
which frequency to sit on.

Every connection is addressed with the
URL-like string from chapter 2 — for
example `ardop:///CALLSIGN?freq=7101.3`
(read it: ARDOP, no host part, target is
the gateway CALLSIGN, set frequency
7101.3). Chapter 9's catalogue prints
one of these per gateway, ready to use.

## ARDOP: the open HF workhorse

**ARDOP** is a sound-card mode designed
for Winlink on HF: adaptive, narrow, and
openly specified. The modem is a separate
program (on Linux, usually `ardopcf`);
it listens for Pat at `localhost:8515`,
which is exactly the address Pat's
default config carries in its `ardop`
section. That section also caps the
signal bandwidth (`arq_bandwidth` Max
500 Hz by default; gateways also offer
1000 and 2000 Hz modes — the `bw=` in
chapter 9's URLs) and leaves CW
identification on, as the rules like.

The station needs: an HF radio with a
sound-card interface (a USB sound dongle
or the radio's built-in USB audio), the
ARDOP program running, and Pat told the
radio's frequency — typed into the
connection string, or set by Hamlib.
Speeds are honest HF numbers: hundreds
to a few thousand bits per second when
the band is kind. Chapter 12 prices
messages against that.

## Packet and AX.25: the VHF classic

**AX.25** packet at 1200 baud is how
local Winlink moves: gateway within
radio reach, a VHF or UHF radio, and a
TNC between it and Pat. Pat names three
engines in the address itself —
`ax25+agwpe`, `ax25+linux`,
`ax25+serial-tnc` — and the config's
`ax25` section picks the default
(`engine: linux` as generated).

- **Through Dire Wolf** (`agwpe`): Dire
  Wolf, the software TNC, runs as its
  own program and speaks the AGWPE
  protocol; Pat's config expects it at
  `localhost:8000`. This is the usual
  modern answer, and the Dire Wolf guide
  in this series builds the modem itself.
- **Through the Linux kernel** (`linux`):
  the operating system's own AX.25 stack,
  with a port (default name `wl2k`)
  configured at the system level. Pat
  simply uses the port.
- **Through a serial TNC**
  (`serial-tnc`): a real hardware TNC on
  a serial port — the config's defaults
  (`/dev/ttyUSB0`, 9600 baud to the TNC,
  1200 baud on air, `kenwood` command
  style) fit the common Kenwood-shaped
  boxes.

Packet paths can hop: an AX.25 address
may carry a digipeater path between Pat
and the gateway call sign, which is the
`[/digi]` in the address grammar. Local,
simple, and line-of-sight: packet is
where most in-county emergency traffic
actually lives.

## VARA: the fast guest

**VARA** (in two builds, `varahf` and
`varafm`) is a modem program written by
one author, EA5HVK: closed-source,
Windows-native, and by broad agreement
the fastest of the sound-card modes —
on a good HF path it outruns ARDOP by a
wide margin, and VARA FM is quicker
still. Pat drives it like ARDOP: VARA
listens at an address (`localhost:8300`
in the config, with a default bandwidth
of 2300 Hz for HF), and Pat connects
there. On Linux, VARA runs under Wine;
that is a known, trodden path, but it is
a guest in the house, and chapters of
other guides have been written about
keeping it happy. The free build and
the paid licence differ in speed; the
protocol is the same either way.

## Pactor: the hardware path

**Pactor** through an SCS PTC modem is
the old professional road: a dedicated
box (config: a serial path,
`/dev/ttyUSB0` at 57600 baud), a real
price tag, and a mode that maritime and
long-haul users have trusted for
decades. Pat's support is there in the
`pactor` section of the config and the
transport list; everything else about
the mode lives in the modem. Few new
stations start here, but many proven
ones are here already.

## Which one should a new station run?

HF, starting out: ARDOP — open,
included, and every gateway chapter 9
lists speaks it. Local VHF: packet
through Dire Wolf. Speed once the
station works: VARA. Pactor if the box
is already on the shelf. All of them end
at the same B2F exchange chapter 7
described; the mailbox neither knows
nor cares which road carried it.

## The check

You have this chapter when, shown any
`connect` string, you can name its three
layers and what plugs into what — and
when you remember that the lab verified
every *setting* on this page and
transmitted nothing at all.
