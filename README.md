# Relative Keyboard

A web-based musical keyboard using relative intervals, designed for composition with a numpad as the Cantus Firmus and top row number keys as fugal counterpoint. Supports customizable intervals, key/mode selection, MIDI output, and polyphony. Future goal: standalone hardware on Teensy with small keypad.

## Features

- **Numpad Notes**: Keys `0`–`9` (`Numpad0`–`Numpad9`, `0`–`9`) play notes relative to the tonic in the current mode (e.g., C4, A3, F3, E3, D3, C4, D4, E4, F4, A4 in C major, Ionian).
- **Top Row Notes**: Keys `0`–`9` (`Digit0`–`Digit9`) play notes relative to the last numpad note, with a configurable octave offset (+1/-1).
- **Intervals**: Configurable via `-` + `0` (random, monotonic), `1` (original: 6th -1, 4th -1, 3rd -1, 2nd -1, Last Note, 2nd, 3rd, 4th, 6th), `5` (with 5th).
- **Key Selection**: `/` + `1`–`7` for keys (C, D, E, F, G, A, B).
- **Mode Selection**: Shift + `3`–`9` or `*` + `1`–`7` for modes (Ionian, Dorian, Phrygian, Lydian, Mixolydian, Aeolian, Locrian).
- **Tone Cycling**: `+` or `NumpadAdd` cycles tones (sine, organ, buzz1, buzz2, ting).
- **Octave Offset**: `=` + `1` (+1 octave for top row), `2` (-1 octave).
- **MIDI Output**: Supports multiple MIDI ports with a dropdown selector.
- **Chord Detection**: Displays chords (e.g., “C major”) for multiple held notes.
- **Range Limiting**: Notes clamped to MIDI 24–108 (C1–C8).
- **UI**: Displays Current Note, Tonic, Mode, Chord, Intervals, Top Row Octave Offset, MIDI Status.

## Setup

### Prerequisites
- **Browser**: Chrome (for Web MIDI) or Safari 18.5+ (for Web Audio).
- **HTTPS**: Serve over HTTPS (e.g., GitHub Pages, Netlify) for Web MIDI.
- **MIDI**: MIDI device or virtual port (e.g., IAC Driver on macOS).

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/relative-keyboard.git
   cd relative-keyboard
   ```
2. Serve `index.html` over HTTPS:
   - Use a local server like `http-server`:
     ```bash
     npm install -g http-server
     http-server -p 8080 --ssl
     ```
   - Or deploy to GitHub Pages/Netlify (see below).
3. Enable MIDI in Chrome:
   - Go to `chrome://settings/content/midiDevices`.
   - Set “Sites can ask to use MIDI devices” to enabled.
4. Set up MIDI on macOS:
   - Open Audio MIDI Setup (Applications > Utilities > Audio MIDI Setup).
   - Enable IAC Driver (MIDI Studio > IAC Driver > Online).
   - Or connect a MIDI device/DAW (e.g., GarageBand).

### Deploy to GitHub Pages
1. Create a GitHub repository:
   - Go to [GitHub](https://github.com) and create a new repository (e.g., `relative-keyboard`).
   - Push the code:
     ```bash
     git init
     git add index.html README.md LICENSE
     git commit -m "Initial commit"
     git remote add origin https://github.com/your-username/relative-keyboard.git
     git push -u origin main
     ```
2. Enable GitHub Pages:
   - Go to repository Settings > Pages.
   - Set Source to “Deploy from a branch,” select `main` branch, `/ (root)` folder.
   - Save and access the HTTPS URL (e.g., `https://your-username.github.io/relative-keyboard`).
3. Test in Chrome/Safari via the GitHub Pages URL.

## Usage

- **Numpad (Cantus Firmus)**:
  - `0`: Plays tonic (e.g., C4) and resets degree.
  - `1`–`4`: Descending intervals (e.g., A3, F3, E3, D3 in C major).
  - `5`: Last note (e.g., C4).
  - `6`–`9`: Ascending intervals (e.g., D4, E4, F4, A4).
- **Top Row (Fugal Counterpoint)**:
  - `0`–`9`: Play notes relative to the last numpad note with octave offset.
- **Controls**:
  - `/` + `1`–`7`: Select key (C, D, E, F, G, A, B).
  - `*` or Shift + `3`–`9`: Select mode (Ionian, Dorian, etc.).
  - `+` or `NumpadAdd`: Cycle tones (Sine → Organ → Buzz1 → Buzz2 → Ting).
  - `-` + `0`/`1`/`5`: Set random/original/with-5th intervals.
  - `=` + `1`/`2`: Set top row octave offset (+1/-1).
- **MIDI**: Select port from dropdown if multiple devices detected.
- **Displays**: Monitor Current Note, Tonic, Mode, Chord, Intervals, Top Row Octave Offset, MIDI Status.

### Example
- In C major (Ionian):
  - Press numpad `7` (E4): “Current Note: E4”, “Tonic: C4”.
  - Press top row `5`: Plays E4 (if offset=0).
  - Press numpad `0` (C4): “Current Note: C4”, “Tonic: C4”.
  - Press `-` + `0`: Random intervals (e.g., “Tonic, 7th -1, 3rd -1, 2nd -1, Last Note, 2nd, 4th, 5th, 6th”).
  - Press `=` + `1`: “Top Row Octave Offset: 1”, top row `5` plays E5.
  - Hold numpad `5` (C4), `7` (E4): “Chord: C major (partial)”.

## Troubleshooting

- **MIDI Issues**:
  - Ensure HTTPS (e.g., GitHub Pages, Netlify).
  - Check Chrome MIDI settings (`chrome://settings/content/midiDevices`).
  - Enable IAC Driver or connect a MIDI device.
  - Check console logs for `MIDI Access Error` or `MIDI Note On error`.
- **Note Repetition**:
  - If a numpad has poor repetition, test with another keypad or USB port.
  - Check console logs for rapid `Keydown` events.
- **Top Row Keys**:
  - Verify `Digit0`–`9` work on laptops without numpad.
  - Check logs for `isNumpad=false` events.
- **Sound**:
  - Web Audio uses 5ms fade-in/out. Report clipping issues.

## Hardware Plans
- **Goal**: Standalone Raspberry Pi with USB keypad.
- **Next Steps**: Specify RPi model (e.g., Pi 4) and keypad for Python/C++ port.
- **Features**:
  - Numpad: Cantus Firmus with CV output (e.g., 0V for C4).
  - Top Row: Counterpoint via second keypad or GPIO buttons.
  - Map `/`, `*`, `+`, `-`, `=` to keypad combinations.

## Contributing
- Fork the repository and submit pull requests for enhancements.
- Report issues via GitHub Issues.
- Potential improvements: enhanced chord detection, Python audio fixes, hardware integration.

## License
MIT License (see [LICENSE](./LICENSE)).
