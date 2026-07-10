# MIDI + VVVV Gamma

A VVVV Gamma project that uses **MIDI inputs** and maps them to **triggers** via the [VL.IO.Midi](https://www.nuget.org/packages/VL.IO.Midi/) package.

## What’s in the patch

`MIDICONNECT.vl` already contains a ready-made MIDI → trigger setup:

- **MidiIn** – opens the **WinMM** input at **`Port index`** (see **`GetInputDeviceNames`** order). **`Name contains`** only drives the **Substring hit** / **Found** hint pads. All channels pass through unless you add a **ChannelFilter**.
- **NoteState** – tracks a single note and outputs:
  - **Pressed** – whether the note is currently down (bool).
  - **Velocity** – note velocity (0–1).
  - **On Data** – **trigger**: fires whenever that note receives a note-on or note-off.

Pads on the canvas:

- **WinMM inputs** – how many MIDI **inputs** the classic Windows MIDI (“WinMM”) stack sees for this patch. **`0`** means the controller is **not** visible to VL’s MIDI backend at all (often driver, cable, powered hub, asleep device, Bluetooth without paired route, etc.). **`> 0`** but still dead → wrong **Port index**, another app hogging the device, or the controller not sending notes on the MIDI channel/note numbers you wired.
- **Port index** – which entry in **`GetInputDeviceNames`** opens **`MidiIn`** (`0 … WinMM inputs − 1`). If renaming broke substring matching, change this until **`Is Open`** is true (compare names in **MIDIBerry** /**MIDI‑OX** ordering if needed).
- **Name contains** / **Substring hit** / **Found** – optional hint (“does any port name contain this text?”); **opening** uses **Port index**, not substring.
- **Is Open** – `MidiIn` opened the port resolved by index.
- **Note** – note number to watch (set per pad; default 60 = middle C).
- **Pressed** / **Velocity** / **On Data (trigger)** – connect these to the rest of your patch (e.g. visuals, audio, other logic).

## Setup

1. **Open in VVVV Gamma**  
   Open `MIDICONNECT.vl` in VVVV Gamma and let it restore the **VL.IO.Midi** dependency.

2. **Pick the right port**  
   Check **WinMM inputs**: if it is **0**, Windows is not exposing any MIDI‑In to this API (fix USB/driver first). If **`> 0`**, set **`Port index`** until **`Is Open`** is **true**. Use **`Name contains`** as a sanity check (**Substring hit** / **Found**), not as the gate for opening.

3. **Use the trigger**  
   Connect **On Data (trigger)** to whatever should run on each note event (e.g. a ForEach, a bang, or a state update). Use **Pressed** and **Velocity** for continuous control.

## Useful tools (Windows)

- [loopMIDI](https://www.tobias-erichsen.de/software/loopmidi.html) – virtual MIDI ports.
- [virtualMIDI](https://www.tobias-erichsen.de/software/virtualmidi.html) – virtual MIDI cable.
- [MIDI Monitor](https://www.midimonitor.com) – inspect MIDI traffic.

## Optional package

For extra MIDI helpers (e.g. music-oriented utilities), you can add **VL.MiDi.Music.Utils** via NuGet in Gamma (Quad → Manage NuGet Packages).

## Docs

- [Audio & MIDI – Gray Book](https://thegraybook.vvvv.org/reference/libraries/audio.html)
- [VL.IO.Midi (GitHub)](https://github.com/vvvv/VL.IO.Midi)
