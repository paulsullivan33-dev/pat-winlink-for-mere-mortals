# Installing Pat

**Outcome: a `pat` program on your
machine that runs and states its
version — before any account or radio
enters the picture.** The check is the
last command on this page: `pat version`
prints one line, and the lab's is quoted
below so you can compare shapes.

## The release download

Pat is distributed from its GitHub
releases page (`github.com/la5nta/pat`).
The lab installed **Pat 1.0.0** — the
current release as this guide was
written — as the archive
`pat_1.0.0_linux_amd64.tar.gz`, about
6.4 MB. There is one asset per platform:
`.tar.gz` and `.deb` packages for Linux
on amd64, arm64, armhf and i386; a `.pkg`
for macOS; a `.zip` for Windows. On a
Raspberry Pi you want an ARM build
(arm64 for a 64-bit OS, armhf for 32-bit).
Pick the archive unless your system
prefers the package; the program inside
is the same single file.

```bash
curl -LO https://github.com/la5nta/pat/releases/download/v1.0.0/pat_1.0.0_linux_amd64.tar.gz
sha256sum pat_1.0.0_linux_amd64.tar.gz
```

Check the sum against the one published
with the release. The lab's download
hashed to
`331e4700c9e8b44098d7173e448da53204f59720c6c19ebc903685666aa377f7`
(transcript t00) — yours should match
the release page for the file you took,
which is the same number if you took the
same file. This is the piper chapter's
lesson in new clothes: a download that
failed quietly still leaves a file
behind, sometimes a 9-byte one saying
*Not Found*. The hash is how you know.

## What is inside

Unpack it anywhere you keep programs:

```bash
tar -xzf pat_1.0.0_linux_amd64.tar.gz
```

The archive holds one folder,
`pat_1.0.0_linux_amd64`, and inside it
one file that matters: `pat` itself, a
single self-contained binary (plus, on
some platforms, small files macOS adds
that you can ignore). No installer, no
dependencies to chase: Go programs carry
their world with them. Copy `pat`
somewhere on your path — `~/bin` or
`/usr/local/bin` are the usual homes —
or just run it where it lies, as the lab
did. The `.deb` package, if you chose
it, puts it on the path for you.

## The version check

```bash
pat version
```

The lab's answer, from transcript t00:

```text
Pat v1.0.0 (2e6a8d1) linux/amd64 - go1.26.2
```

Version, build commit, platform, and
the Go it was built with — one line that
proves the binary runs on your machine.
Then take the tour the guide will keep
returning to:

```bash
pat --help
```

Eighteen commands, from `init` to
`version`, plus the global options. Two
options matter from the start, because
every later chapter leans on them:
Pat's places are flags — `--config`,
`--mbox`, `--forms`, `--log` — so a
script (or a lab) can point Pat at a
self-contained set of folders instead of
the defaults in your home directory.
Chapter 4 uses the defaults; the lab
used the flags to keep its work in one
corner, and said so.

That is the whole install. What Pat
cannot do yet is anything at all: with
no config file it answers most commands
with two words, `Missing mycall`. That
is not a defect — it is the subject of
the next chapter.
