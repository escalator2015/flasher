# Project Instructions

## Project

This repository is a self-contained browser-based ESP Web Flasher. The application, styles, UI markup, bundled `esptool.js`/`pako` code, and app logic all live in [espflash.html](espflash.html). `dsp24u.bin` is a firmware binary asset.

## Working Conventions

- Keep the single-file distribution shape unless the task explicitly asks for a build system or source split.
- Preserve the bundled flasher library and its public globals (`ESPLoader`, `Transport`, and related reset helpers); do not replace or regenerate the bundle casually.
- Keep UI behavior and DOM ids aligned with the event handlers in `espflash.html`.
- Treat serial transport state, stream ownership, reconnect behavior, baud-rate changes, and stub-loader lifetime as sensitive code paths. Make cleanup and error handling explicit when changing them.
- Avoid logging firmware contents, serial data, or device identifiers into new persistent storage.
- Preserve the existing inline style and script organization; make focused edits and avoid unrelated formatting churn.

## Runtime Constraints

- The app requires a browser with Web Serial support and a secure context, such as `https://` or an appropriate localhost origin.
- Real flash, read, erase, and monitor validation requires a compatible Espressif device and firmware. Do not claim hardware behavior was tested without hardware.
- The bundled library is compressed/minified and difficult to review line-by-line. Prefer changes in the readable application script near the end of the file unless the bundled implementation is the demonstrated source of the bug.

## Validation

- There is no package manager, build script, or automated test suite in this repository.
- For markup or script changes, first use a lightweight syntax/static check available in the environment, then open [espflash.html](espflash.html) in a Web Serial-capable browser and exercise the affected UI path when hardware is available.
- For serial changes, test connect, disconnect, failed-connect cleanup, baud-rate fallback, and the affected flash/read/erase/monitor operation as applicable.
- Check browser-console errors and verify that progress, logs, and button disabled states recover after failures.

## Change Scope

- Do not add dependencies or generated project metadata for a narrow fix.
- Update this file only when project structure, commands, or durable conventions change.
