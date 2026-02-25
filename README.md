# MIDI + VVVV Gamma

A VVVV Gamma project that uses **MIDI inputs** and maps them to **triggers** via the [VL.IO.Midi](https://www.nuget.org/packages/VL.IO.Midi/) package.

## What’s in the patch

`MIDICONNECT.vl` already contains a ready-made MIDI → trigger setup:

- **MidiIn** – receives MIDI from the device you choose.
- **ChannelFilter** – restricts to one MIDI channel (0–15).
- **NoteState** – tracks a single note and outputs:
  - **Pressed** – whether the note is currently down (bool).
  - **Velocity** – note velocity (0–1).
  - **On Data** – **trigger**: fires whenever that note receives a note-on or note-off.

Pads on the canvas:

- **Device** – select your MIDI input (dropdown).
- **Is Open** – shows if the device is open.
- **Channel** – MIDI channel (default 0).
- **Note** – note number to watch (default 60 = middle C).
- **Pressed** / **Velocity** / **On Data (trigger)** – connect these to the rest of your patch (e.g. visuals, audio, other logic).

## Setup

1. **Open in VVVV Gamma**  
   Open `MIDICONNECT.vl` in VVVV Gamma and let it restore the **VL.IO.Midi** dependency.

2. **Select your device**  
   In the **Device** pad, choose your hardware or virtual MIDI port (e.g. loopMIDI, virtualMIDI, or your keyboard/controller).

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
