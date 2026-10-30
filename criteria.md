# Writing criteria for this guide

Every "for Mere Mortals" guide is written to the same nine-point
standard, so a reader who trusts one can trust the rest. Here it
is, with the verification notes for this particular guide below.

1. **Fix it first.** Reader outcomes lead, not action items: each
   chapter opens by naming the outcome it delivers, shows a check
   the reader can run to confirm they got it, and a reasonable
   reader finishes able to state what was done, what it means,
   and what to try next.
2. **Plain language.** Short sentences, everyday vocabulary,
   technical terms defined on first use. No slang, and no
   idioms that only make sense in one country — the reader may
   be translating as they go.
3. **No dead ends.** A guide never tells the reader to do
   something it cannot show them how to verify. Every claim a
   reader relies on — an install, a command, an output — is
   something this guide demonstrates or clearly labels
   documented-only below.
4. **Live-verified where it matters.** Procedures are run for
   real in the guide's lab wherever the build machine allows it,
   and the transcripts kept in the repository are the evidence.
   What could not be run is listed honestly below, never
   presented as if it had been.
5. **General audiences.** Nothing in this guide — examples,
   fixtures, names, addresses — is modelled on any particular
   reader or author's real life, network, or organisations.
   The lab's call sign is the placeholder N0CALL, its
   correspondent is at example.com, and its locator is a
   generic grid square.
6. **Standalone.** A reader needs this guide, its lab, and
   nothing else. Where another guide would genuinely help, it
   is pointed to once, by name, and the chapter still completes
   without it.
7. **Honest about limits.** Chapter 12 names what the system
   cannot do: no account means no connection, radio speeds are
   slow, nothing over ham radio is private, the network is
   volunteers, the web mailbox has no lock of its own, and this
   guide's own lab never connected to anything.
8. **The ethics rule is in the text, early.** Winlink accounts
   belong to licensed call signs and transmitting needs the
   licence; Winlink traffic over radio is open by rule and
   cannot carry commercial business. Chapter 1 and the README
   state this before any procedure depends on it, and the
   guide's lab operated inside it throughout: a placeholder
   call sign, no account, no transmission.
9. **Builds clean.** The site builds with MkDocs in strict mode
   with no warnings, and a fresh reader following the chapters
   in order reaches the stated outcome of each.

## Verification notes for this guide

The lab ran in a shared Linux sandbox with no radio hardware,
no sound devices in use, no Winlink account, and no licence to
transmit — limits this guide treats as the subject, not an
embarrassment: everything Pat does *before* a connection is
fully exercisable without one, and everything that needs one is
taught from documentation and labelled. Pat **1.0.0** was
installed from the official release archive
`pat_1.0.0_linux_amd64.tar.gz` (SHA-256
`331e4700c9e8b44098d7173e448da53204f59720c6c19ebc903685666aa377f7`)
and run unmodified, with its config, mailbox, forms and logs
pointed by flags into one lab folder. All transcripts live in
`pat-winlink-lab/transcripts/`; the lab's finished example
config is `pat-winlink-lab/config.example.json`.

Run for real, with transcripts as evidence:

- The release tarball's hash and contents, `pat version`
  (v1.0.0, build 2e6a8d1) and the full `--help` command list
  (t00).
- First run with no config: the guided-setup greeting, answered
  `n`; Pat's complete default `config.json` written by Pat
  itself and read field by field (t01). The lab then changed
  exactly three fields — `mycall` to the placeholder N0CALL,
  `locator` to the generic square FN31, `http_addr` to
  localhost:18080 — and `pat env` confirmed what was loaded.
- A message composed by the scripted route (flags plus body on
  standard input) answered `Message posted` and produced
  `mailbox/N0CALL/out/<MID>.b2f`; the stored file's headers —
  including the `SMTP:` prefix Pat adds to an internet
  address — are quoted whole (t02). `pat read` listed the
  message in the outbox and printed it in full (t02).
- `pat http` serving the web mailbox on loopback: the startup
  line, `/` answering 302 to `/ui`, the page loading with the
  title *Pat - Mailbox*, and the JSON API — `/api/status`,
  `/api/mailbox/out`, and the single-message endpoint returning
  the lab's message with its body (t03).
- `pat rmslist -m ardop -s` downloading the live gateway
  catalogue from winlink.org and printing ARDOP gateways
  sorted by distance from FN31 (t04). The gateway rows in t04
  are the tool's own public catalogue output, reproduced as
  evidence; they are data Pat fetched, not fixtures, and the
  guide's prose names no gateway. Checking t04's distances
  against the map also produced a finding the guide reports:
  a four-character locator is measured from the square's
  corner, verified by recomputing three rows' distances and
  bearings to the printed values.
- `pat templates update` downloading Standard_Forms 1.1.22.0
  (about 13 MB) and unpacking its named collections (t05).
- Failures, on purpose: `pat env` with no call sign answers
  exactly `Missing mycall`; a second `pat http` on the same
  port prints the startup line then fails with `listen tcp
  127.0.0.1:18080: bind: address already in use` (t07).
- The documented surfaces themselves: `pat help connect`,
  `help compose`, `help position`, `help rmslist`,
  `help templates` and `help account` were read and are the
  grounding for the connection chapters' command forms (t06).

Documented only — described from the project's documentation
and Pat's own help text, not run, and the text says so in each
chapter it touches:

- Creating a Winlink account (on winlink.org or on first
  connection), secure login in a live session, and the
  `pat account` settings commands, which need the account.
- Every connection: the telnet session to the CMS (chapter 7),
  and all radio paths — ARDOP, AX.25 through Dire Wolf, the
  Linux kernel or a serial TNC, VARA HF/FM, and Pactor
  (chapter 8). No transmission of any kind was made.
- Listening for incoming connections, peer-to-peer exchange,
  the hybrid network, `--radio-only` and `pat mps`
  (chapter 11).
- Posting a position report: the `position` command's shape,
  flags and config are verified from its help and the config
  file, but no report was posted, since posting rides a
  connection.
- Link-quality sorting in `rmslist -q`, which needs a VOACAP
  setup the lab did not build.
- Filling and sending an actual form message: the library
  download is verified; composing with `--template` is
  described from the help, and no form was sent.

Fixtures are this guide's own and deliberately generic: the
placeholder call sign N0CALL (which has no account and cannot
connect), a correspondent at the reserved example.com domain,
a generic grid square (FN31), and one stock message about a
weekly check-in. No real person's call sign is used as any
party in this guide, and nothing was transmitted, posted, or
connected at any point in the lab.
