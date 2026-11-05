# Photon Lab

A test bench for a screen-to-camera optical channel: a transmitter draws symbol
grids on one screen, a receiver reads them with a camera, and every run is
measured, logged and exportable.

## Why it exists

Screen-to-camera links fail in ways that are hard to argue about: rolling
shutter, moire, tearing, focus, exposure, ambient light. To say anything useful
about a coding scheme you need the same bench every time: known symbols, known
framing, recorded results. Photon Lab is that bench, built from a single-file
prototype and split into modules so each stage can be tested.

## What you can do

- **Transmit** symbol grids from the TX tab, on a second screen or a second
  device.
- **Receive** on the RX tab with a camera, and read the symbols back.
- **Auto-calibrate** by detecting the magenta corner markers, so the receiver
  finds the frame without being told where it is.
- **Run experiments** from the experiment panel, with parameters recorded per run.
- **Inspect** the live dashboard, heatmaps and FFT of the received signal.
- **Export sessions** so results can be compared across runs.

## Running it

```bash
# no build step
open index.html     # Chrome recommended
```

Or serve the directory:

```bash
python3 -m http.server 8000
```

Then: TX on one screen or device, RX on another with a camera, calibrate, and run
an experiment. The receiver needs camera permission, which needs a secure origin
(`localhost` counts, plain HTTP on a LAN address does not).

## What is not here

- No result is a promise about throughput. The bench characterises a channel; it
  does not claim a bitrate.
- Calibration assumes the four magenta markers are visible. Occlude a corner and
  the frame is not found.
- `legacy/` holds the original single-file prototype, kept for comparison, not
  maintained.
- `android/` and `native/` are the platform experiments; the browser bench is the
  part in daily use.

## How it is built

```
index.html      the bench: TX, RX, calibration, dashboard, experiments
src/            the modules behind it
native/         platform receivers
android/        the Android experiment
legacy/         the original single-file prototype
docs/           brief, notes and results
```
