# Syncthing With TLS Secrets Export

This is a version of Syncthing identical to the upstream code with the single addition of one tiny patch (just two lines of code) that causes the application to export its TLS secrets to a file (currently hard-coded to `tls-secrets.txt` in the directory from which the application is run), which can then be provided to [Wireshark](https://www.wireshark.org/) in order to enable the dissection of the various [Syncthing protocols](https://docs.syncthing.net/specs/index.html) that utilize TLS. (A Wireshark Syncthing dissector is available [here](https://github.com/tmo1/wireshark-syncthing-dissector); it is a WIP, and so far only [Local Discovery Protocol v4](https://docs.syncthing.net/specs/localdisco-v4.html) [which does not utilize TLS] has been implemented.)

**Important:** Note that [as the Go documentation warns](https://pkg.go.dev/crypto/tls#example-Config-KeyLogWriter),

```
"WARNING: Use of KeyLogWriter compromises security and should only be used for debugging.
```

To build this patched version, just follow [upstream's simple build instructions](https://docs.syncthing.net/dev/building.html), replacing upstream's git URL (`https://github.com/syncthing/syncthing.git`) with this repository's (`https://github.com/tmo1/syncthing.git`).

When using this patched version of Syncthing, automatic upgrades should be disabled (e.g., via `Actions / Settings / Automatic upgrades` from the GUI), since if this is not done, the application will eventually "upgrade" itself to a vanilla, unpatched version.

The upstream Syncthing `README` follows.

---

[![Syncthing][14]][15]

---

[![Latest Linux & Cross Build](https://img.shields.io/teamcity/https/build.syncthing.net/s/Syncthing_BuildLinuxCross.svg?style=flat-square&label=linux+%26+cross+build)](https://build.syncthing.net/viewType.html?buildTypeId=Syncthing_BuildLinuxCross&guest=1)
[![Latest Windows Build](https://img.shields.io/teamcity/https/build.syncthing.net/s/Syncthing_BuildWindows.svg?style=flat-square&label=windows+build)](https://build.syncthing.net/viewType.html?buildTypeId=Syncthing_BuildWindows&guest=1)
[![Latest Mac Build](https://img.shields.io/teamcity/https/build.syncthing.net/s/Syncthing_BuildMac.svg?style=flat-square&label=mac+build)](https://build.syncthing.net/viewType.html?buildTypeId=Syncthing_BuildMac&guest=1)
[![MPLv2 License](https://img.shields.io/badge/license-MPLv2-blue.svg?style=flat-square)](https://www.mozilla.org/MPL/2.0/)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/88/badge)](https://bestpractices.coreinfrastructure.org/projects/88)
[![Go Report Card](https://goreportcard.com/badge/github.com/syncthing/syncthing)](https://goreportcard.com/report/github.com/syncthing/syncthing)

## Goals

Syncthing is a **continuous file synchronization program**. It synchronizes
files between two or more computers. We strive to fulfill the goals below.
The goals are listed in order of importance, the most important one being
the first. This is the summary version of the goal list - for more
commentary, see the full [Goals document][13].

Syncthing should be:

1. **Safe From Data Loss**

   Protecting the user's data is paramount. We take every reasonable
   precaution to avoid corrupting the user's files.

2. **Secure Against Attackers**

   Again, protecting the user's data is paramount. Regardless of our other
   goals we must never allow the user's data to be susceptible to
   eavesdropping or modification by unauthorized parties.

3. **Easy to Use**

   Syncthing should be approachable, understandable and inclusive.

4. **Automatic**

   User interaction should be required only when absolutely necessary.

5. **Universally Available**

   Syncthing should run on every common computer. We are mindful that the
   latest technology is not always available to any given individual.

6. **For Individuals**

   Syncthing is primarily about empowering the individual user with safe,
   secure and easy to use file synchronization.

7. **Everything Else**

   There are many things we care about that don't make it on to the list. It
   is fine to optimize for these values, as long as they are not in conflict
   with the stated goals above.

## Getting Started

Take a look at the [getting started guide][2].

There are a few examples for keeping Syncthing running in the background
on your system in [the etc directory][3]. There are also several [GUI
implementations][11] for Windows, Mac and Linux.

## Docker

To run Syncthing in Docker, see [the Docker README][16].

## Vote on features/bugs

We'd like to encourage you to [vote][12] on issues that matter to you.
This helps the team understand what are the biggest pain points for our users, and could potentially influence what is being worked on next.

## Getting in Touch

The first and best point of contact is the [Forum][8].
If you've found something that is clearly a
bug, feel free to report it in the [GitHub issue tracker][10].

## Building

Building Syncthing from source is easy. After extracting the source bundle from
a release or checking out git, you just need to run `go run build.go` and the
binaries are created in `./bin`. There's [a guide][5] with more details on the
build process.

## Signed Releases

As of v0.10.15 and onwards release binaries are GPG signed with the key
D26E6ED000654A3E, available from https://syncthing.net/security.html and
most key servers.

There is also a built in automatic upgrade mechanism (disabled in some
distribution channels) which uses a compiled in ECDSA signature. macOS
binaries are also properly code signed.

## Documentation

Please see the Syncthing [documentation site][6] [[source]][17].

All code is licensed under the [MPLv2 License][7].

[1]: https://docs.syncthing.net/specs/bep-v1.html
[2]: https://docs.syncthing.net/intro/getting-started.html
[3]: https://github.com/syncthing/syncthing/blob/main/etc
[5]: https://docs.syncthing.net/dev/building.html
[6]: https://docs.syncthing.net/
[7]: https://github.com/syncthing/syncthing/blob/main/LICENSE
[8]: https://forum.syncthing.net/
[10]: https://github.com/syncthing/syncthing/issues
[11]: https://docs.syncthing.net/users/contrib.html#gui-wrappers
[12]: https://www.bountysource.com/teams/syncthing/issues
[13]: https://github.com/syncthing/syncthing/blob/main/GOALS.md
[14]: assets/logo-text-128.png
[15]: https://syncthing.net/
[16]: https://github.com/syncthing/syncthing/blob/main/README-Docker.md
[17]: https://github.com/syncthing/docs
