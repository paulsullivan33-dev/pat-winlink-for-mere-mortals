# Glossary

**AGWPE** — a protocol by which packet
programs talk to the software TNC that
serves them. Pat reaches Dire Wolf
through it, at `localhost:8000` by
default.

**ARDOP** — Amateur Radio Digital Open
Protocol: the open sound-card mode for
Winlink on HF, run as its own program
and driven by Pat over `localhost:8515`.

**AX.25** — the amateur packet-radio
link protocol: the frames underneath
1200-baud VHF packet, usable through
the Linux kernel, an AGWPE engine, or a
serial TNC.

**B2F** — the protocol of a Winlink
session: the exchange in which client
and far end compare mailboxes and pass
compressed messages, and the extension
(`.b2f`) on every message file in your
mailbox.

**CMS** — Common Message Servers:
Winlink's centre, holding all users'
mail and passing it to and from the
internet and the gateways.

**Grid square / locator** — a Maidenhead
locator: a short code (FN31, or six
characters for finer grain) naming
roughly where a station is. Powers
distance sorting and position stamps.

**Hamlib** — the shared library and
daemon (`rigctld`) by which programs
control radios: frequency, mode,
transmit. Pat uses it when a rig is
named in the config.

**Hybrid / radio-only** — the mode in
which gateways forward mail between
themselves by radio when their internet
is down, toward a message pickup
station. `--radio-only` keeps a client
on that path.

**MID** — message ID: the short unique
code naming one message, and the name
of its file in the mailbox.

**MPS** — message pickup station: a
designated station that holds mail for
collection in the hybrid network.
Managed with `pat mps`.

**P2P** — peer to peer: two stations
exchanging mail directly, radio to
radio, no gateway or CMS in the
session. One end must be listening.

**Pactor** — a family of HF data modes
run by SCS hardware modems (PTC units):
the fast, costly, hardware path.

**RMS** — Radio Message Server: a
gateway station. A volunteer's radios
and computer relaying between the air
and the CMS; listed live by `rmslist`.

**Secure login** — Winlink's
challenge-and-response password check:
the server proves it is itself and you
prove you hold the account password,
without the password crossing in plain
text.

**Service codes** — the config field
naming which Winlink network a station
belongs to; `PUBLIC` is the public
system, and the right answer for almost
everyone.

**Tactical address** — an extra address
(mailbox name) under your call sign,
used by groups in place of a personal
call: set in `auxiliary_addresses`.

**TNC** — terminal node controller: the
modem layer between computer and radio,
whether software (ARDOP, Dire Wolf) or
a box on a serial port.

**VARA** — a closed-source, Windows-
native sound-card modem (HF and FM
builds) prized for speed; Pat drives it
over `localhost:8300`.

**Winlink** — the worldwide email-over-
radio system itself: CMS at the centre,
RMS gateways at the edges, clients like
Pat in operators' hands.
