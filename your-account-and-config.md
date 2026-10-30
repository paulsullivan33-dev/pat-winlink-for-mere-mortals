# Your Account and Config

**Outcome: a config file that names your
call sign, your locator, and your
password — and Pat agreeing it has read
it.** The check: `pat env` prints your
call sign back at you, as it does in
transcript t01.

## First, the account itself

A Winlink account is not a username you
invent. It *is* your call sign, and it
comes to exist in one of two ways: you
create it on winlink.org, or it is
created for you the first time you
connect successfully with that call sign
and a password. Either way, the password
you set is the password Pat must present
every time it connects — the servers
check it with a challenge-and-response
handshake called **secure login**, so
the password itself never crosses the
air or the wire in plain text, but Pat
must know it to answer the challenge.

Set a password recovery address early:
if the password is ever lost, the
account is recovered by email, and an
account with no recovery address on file
is an account you can lose. Pat can read
and set it once you can connect:
`pat account password.recovery.email`
(transcript t06 has the command's own
help). This account section is taught
from the project's documentation — the
lab's call sign, N0CALL, has no account
and never will, so no transcript shows
an account being made. The mechanics
below, everything on your own machine,
are all lab-verified.

## Two ways to a first config

Run any Pat command with no config file
present and Pat notices. The lab ran
`pat configure` and was greeted
(transcript t01):

```text
Hello there! Do you want to be guided through the basic setup?
Run 'pat init'? (Y/n):
```

Answer yes and `pat init` walks you
through the basics — call sign,
password, locator — with account
verification as part of the flow. That
is the right door for a real station.

Answer no — the lab did — and Pat writes
a complete **default config file** and
opens it in your editor (`pat configure`
reopens it any time). The lab's route is
the transparent one, so this guide takes
it: the file Pat writes is plain JSON
text, and every field has a default you
can read. Nothing about your station is
magic or hidden; it is a page of
settings you own.

## The config file, field by field

The default file lives at
`~/.config/pat/config.json`. Transcript
t01 prints the lab's copy in full, as
generated. The fields that matter first:

- **`mycall`** — your call sign. Empty
  at birth; until it is set, Pat answers
  `Missing mycall` and stops (t07).
- **`secure_login_password`** — your
  Winlink account password, as above.
- **`locator`** — your **grid square**
  (Maidenhead locator): a short code,
  four or six characters, that says
  roughly where on Earth you are. It
  powers the distance sorting in chapter
  9 and the position stamping in chapter
  10. The lab used `FN31`, a generic
  square, because N0CALL lives nowhere.
- **`service_codes`** — `["PUBLIC"]`.
  Leave it alone; other codes belong to
  specific served-agency networks.
- **`http_addr`** — where the web
  mailbox listens, `localhost:8080` by
  default. The lab moved to
  `localhost:18080` because 8080 was
  spoken for on its machine — chapter 13
  shows the error you get when a port
  is, in Pat's words, *already in use*.
  Keep the `localhost` part: chapter 5
  explains why the web mailbox has no
  lock of its own.
- **`auxiliary_addresses`** — extra
  addresses mail can arrive under your
  call sign (tactical addresses, in
  emergency-group language). Empty to
  start.
- **`connect_aliases`** — named
  shortcuts. The default file carries
  one, `telnet`, and chapter 7 unpacks
  the address it points at.
- **`motd`** — the line Pat greets with.
  Harmless; leave it or make it yours.

Below those sit the transport sections —
`ardop`, `ax25`, `agwpe`, `serial-tnc`,
`pactor`, `varahf`, `varafm`, `telnet`,
`gpsd`, `hamlib_rigs` — each a small
block of settings with sane defaults
(the modem addresses from chapter 2 live
here). Chapter 8 touches the few fields
a radio path actually makes you visit.
You do not need to understand them yet;
you need to know they are *here*, in
this file, when you do.

## The check

With the three fields set — call sign,
password once you have one, locator —
ask Pat what it loaded:

```bash
pat env
```

`PAT_MYCALL="N0CALL"` and
`PAT_LOCATOR="FN31"` head the lab's
output in t01, along with every path
Pat is using. If your call sign is not
in that list, Pat is reading a different
config file than the one you edited —
the `--config` flag in t01's commands is
how the lab made sure, and chapter 13
starts there too.
