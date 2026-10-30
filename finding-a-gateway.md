# Finding a Gateway

**Outcome: a shortlist of real gateway
stations you could actually reach,
sorted by distance, with frequencies
you can set a radio to.** The check: `pat
rmslist` prints the live catalogue on
your machine, and the lab's capture
(t04) shows the shape of the answer.

## The catalogue is live

Winlink's gateways are volunteers'
stations; they come, go, change
frequency and change modes. Pat does not
ship a stale copy of the list — it
downloads the current catalogue from
winlink.org when asked, then filters it
for you:

```bash
pat rmslist
```

The download takes a few seconds and
happens on any internet connection — no
account, no radio. (On a station with no
internet, the last downloaded copy is
kept and used; the network is helpful
here, not required.) Everything after
this point in the chapter is the lab
working with that real, current
catalogue — transcript t04 is the
evidence, and its gateway rows are the
tool's own download, printed as it
arrived.

## Filtering and sorting

The command takes the filters you would
expect once you know the transports
(chapter 8):

```bash
pat rmslist -m ardop -s
pat rmslist -b 40m -m packet
```

`-m` keeps one mode (ardop, packet,
varahf, pactor and friends). `-b` keeps
one band, written ham-style — `40m`,
`20m`, `2m`. `-s` sorts by distance from
*your* grid square, which is why chapter
4 cared about your `locator`: the sort,
and the distances themselves, are only
as good as that setting. `-q` sorts by
predicted link quality instead, using
propagation modelling (VOACAP) when the
station has it set up — documented here,
not lab-run.

## Reading a row

The lab asked for ARDOP gateways sorted
by distance from the generic square
FN31. The answer's header:

```text
callsign  [gridsq] dist   Az mode(s)       dial freq     center freq  qual url
```

One row per frequency a gateway
listens on — a station with four
channels takes four rows. The columns:

- **callsign / [gridsq]** — the gateway
  and its own grid square.
- **dist** — distance from your locator,
  in kilometres. One wrinkle the lab
  found by checking the arithmetic
  against the map (t04): a four-character
  locator is measured from the square's
  corner, so distances run a little long
  or short by up to the size of the
  square. Give Pat a six-character
  locator (chapter 4) and the numbers
  pin to your actual spot.
- **Az** — the bearing to point a
  directional antenna, in degrees.
- **mode(s)** — the mode and its
  bandwidth: `ARDOP 2000` is ARDOP with a
  2000 Hz signal; your config's
  `arq_bandwidth` must not exceed it.
- **dial freq** — the frequency your
  radio's dial shows, USB dial
  convention. *This is the one you set.*
- **center freq** — the actual centre of
  the signal on the air, 1500 Hz above
  the dial for USB data. It matters when
  reading band plans and other people's
  spots; set the dial, not the centre.
- **qual** — a link-quality figure when
  the modelling is available (the lab's
  run showed `N/A`; the setup for it is
  documented, not run).
- **url** — the prize: a ready-made
  Pat connection string for this channel,
  bandwidth and frequency already filled
  in, shaped like
  `ardop:///<gateway>?bw=2000MAX&freq=<dial>`.
  Copy it to `pat connect` and chapter
  8's machinery does the rest.

## Choosing well

Nearest is not the same as reachable,
and HF is not VHF. For packet and VARA
FM, distance is close to a verdict: if
a gateway is 30 km away and nothing
large is between you, it will probably
work. For HF, the band decides: a
gateway 300 km away may be *too close*
for 20 metres at noon (your signal
lands over its head) and perfect on
40 metres at dusk. Work down the list
with the band in mind, try the
connection, and let the result teach
you your station's real reach — that
table you build yourself, over weeks,
is the gateway knowledge every Winlink
operator ends up keeping.

## The check

`pat rmslist -m <your mode> -s` prints
*your* list, sorted from *your*
locator, and you can pick out the dial
frequency and the ready-made URL in any
row. If your list comes out unsorted or
the distances look like someone else's
geography, the fault is in `locator` —
chapter 4, and the first stop in chapter
13.
