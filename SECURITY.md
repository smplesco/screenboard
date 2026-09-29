# Security Policy

Screenboard is a drawing board that runs entirely in your browser. It has no
accounts and no server of its own. Boards live on your device (in files you
save and in your browser's storage), and live sessions connect people's
browsers directly to each other.

## Supported Versions

Screenboard doesn't publish numbered releases. The copy on GitHub Pages always
runs the latest code from the `main` branch, and installed copies update
themselves the next time they're opened online.

| Version                                          | Supported          |
| ------------------------------------------------ | ------------------ |
| Latest (GitHub Pages / `main` branch)            | :white_check_mark: |
| Older copies (downloaded HTML files, forks, installs that haven't updated) | :x: |

If you're reporting a problem, please check it on the live site first.

## Reporting a Vulnerability

**Please don't open a public issue for security problems.**

Report it privately through GitHub instead:

1. Go to the repository's **Security** tab.
2. Click **Report a vulnerability**.
3. Describe what you found, how to reproduce it, and what someone could do
   with it. A sample `.screenboard` file or a short screen recording helps a lot.

What to expect:

- **Acknowledgement within 7 days.** This is a one-person hobby project, so
  replies aren't instant, but every report gets read.
- **Updates at least every 14 days** until the report is closed.
- **If it's accepted:** I'll work on a fix, aiming for 30 days or less for
  serious issues, and let you know when it's live. With your permission,
  you'll be credited in the fix's commit message.
- **If it's declined:** I'll explain why (for example, it's out of scope below,
  or it can't be reproduced), and you're welcome to follow up with more detail.

Please give me a reasonable chance to fix a problem before sharing it publicly.

## What's in scope

Things I especially want to hear about:

- A `.screenboard` file, pasted content or dropped file that runs code, reads
  data it shouldn't, or makes the app contact another website when opened.
- Anything a person in a live session can send that runs code on someone
  else's screen, gets around watch-only mode, pausing, pinned items or removal,
  or lets them draw after the host has made new links.
- Exported files (SVG, PDF, PNG, board files) that carry hidden scripts or
  personal data.
- Problems with how boards are kept in your browser's storage.

## How live sessions work (security model)

- **Links are the keys.** Anyone with the "Can draw" link can draw on the board,
  and anyone with the "View only" link can watch. Share them like you would a
  meeting link. The host can make new links at any time, which stops the old
  draw link from giving drawing rights.
- **The host is in charge.** Every change passes through the host's browser,
  which ignores changes from people who are only allowed to watch, and can
  remove people. The session ends when the host closes their board.
- **Direct connections.** Browsers connect to each other with WebRTC, which
  encrypts traffic between them. A free public matchmaking service
  ([PeerJS](https://peerjs.com)) introduces the browsers, and, on strict
  networks, may relay the already-encrypted traffic. That service can see
  connection details such as IP addresses and the random session ID, but not
  what's drawn.
- **Nothing is stored online.** When a session ends, each person keeps their
  own copy of the board on their device. Nothing is kept on a server.

## Out of scope

- Availability of third-party services (the PeerJS matchmaking and relay
  servers, and the CDNs that serve libraries).
- People you've given a link to doing what the link allows, such as drawing
  something unwanted with a "Can draw" link. The host can switch them to watch
  only, erase their drawings or remove them.
- Flooding a live session you've been invited into with large amounts of
  drawing, or other denial-of-service within a session.
- Issues that need someone to already control your device or browser.
- Social engineering, or reports based only on automated scanner output.

## Third-party code

Screenboard loads a few libraries on demand from public CDNs: MathJax (math
rendering, from jsDelivr), PeerJS (live sessions, from unpkg), and jsPDF, JSZip
and PDF.js (exporting, zipping and opening PDFs, from cdnjs). Vulnerabilities in
those libraries should be reported to their own projects, but let me know too
if one affects Screenboard.
