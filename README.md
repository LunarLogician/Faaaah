
# Installing Faah Sound Extension from .vsix

If you downloaded the `.vsix` file for the Faah Sound extension from GitHub (e.g., `faah-sound-error-1.0.0.vsix`):

1. Open VS Code
2. Go to Extensions (`Ctrl+Shift+X`)
3. Click the `...` menu (top right) → `Install from VSIX...`
4. Select the `.vsix` file you downloaded
5. The extension will install and activate automatically

You do **not** need to package or publish the extension yourself if you have the `.vsix` file.

# Faah Sound on Terminal Error 🔊

A VS Code extension that plays a "faah" sound whenever an error appears in your terminal. Perfect for catching errors when you're multitasking!


## Features

- 🎵 Automatically plays a sound when terminal errors are detected
- ⚙️ Configurable error patterns to match
- 🔊 Adjustable volume control
- 🎮 Easy toggle on/off
- 🧪 Test sound command to verify it's working


## Installation

1. Open VS Code
2. Press `Ctrl+P` to open Quick Open
3. Paste the following command and press Enter:
   ```
   ext install Zubair.faah-sound-error
   ```
4. Done! The extension will activate automatically.


## Commands

- **Faah Sound: Toggle Error Sound** - Enable/disable the sound
- **Faah Sound: Test Sound** - Play the sound to test it's working

Access commands via Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`)


## Configuration

Open VS Code settings and search for "Faah Sound" to configure:

### `faahSoundError.enabled`
- **Type:** `boolean`
- **Default:** `true`
- **Description:** Enable/disable the faah sound on terminal errors

### `faahSoundError.volume`
- **Type:** `number`
- **Default:** `0.5`
- **Range:** `0.0` to `1.0`
- **Description:** Volume level for the faah sound

### `faahSoundError.errorPatterns`
- **Type:** `array`
- **Default:** 
   ```json
   [
      "error:",
      "Error:",
      "ERROR:",
      "fail:",
      "FAIL:",
      "Failed",
      "fatal:",
      "FATAL:",
      "Exception",
      "Traceback"
   ]
   ```
- **Description:** Patterns to detect errors in terminal output


## Audio Player Requirements

The extension uses system audio players to play sounds:

- **Linux:** Requires `paplay` (PulseAudio), `aplay` (ALSA), or `ffplay` (FFmpeg)
- **macOS:** Uses built-in `afplay` (✅ Works out of the box)
- **Windows:** Uses PowerShell's SoundPlayer (✅ Works out of the box with WAV format)

sudo apt-get install pulseaudio-utils

### Installing Audio Players (Linux)

If you don't have an audio player installed:

```bash
# For Ubuntu/Debian (PulseAudio)
sudo apt-get install pulseaudio-utils

# For ALSA
sudo apt-get install alsa-utils

# For FFmpeg
sudo apt-get install ffmpeg
```


## Packaging the Extension

To package and install the extension:

1. Install vsce (VS Code Extension Manager):
   ```bash
   npm install -g @vscode/vsce
   ```

2. Package the extension:
   ```bash
   vsce package
   ```

3. Install the `.vsix` file:
   - Open VS Code
   - Go to Extensions (`Ctrl+Shift+X`)
   - Click the "..." menu → "Install from VSIX"
   - Select the generated `.vsix` file


## Publishing (Optional)

To publish to the VS Code Marketplace:

1. Create a publisher account at https://marketplace.visualstudio.com/
2. Update `publisher` in `package.json`
3. Run:
   ```bash
   vsce publish
   ```


## How It Works

1. The extension monitors all terminal output using VS Code's `onDidWriteTerminalData` event
2. When terminal data is written, it checks against configured error patterns
3. If an error pattern is matched, it plays the sound file
4. The sound is played using system audio players (platform-specific)


## Troubleshooting

### Sound not playing?

1. **Check the sound file exists:** Make sure `sounds/faah.mp3` exists
2. **Test the sound:** Use the "Faah Sound: Test Sound" command
3. **Check audio player:** Ensure you have a compatible audio player installed (see requirements)
4. **Check system volume:** Make sure your system volume is not muted
5. **Check extension logs:** Open Output panel → select "Faah Sound Error"

### Too many false positives?

Adjust the `faahSoundError.errorPatterns` setting to be more specific to your needs.

### Sound too loud/quiet?

Adjust the `faahSoundError.volume` setting (0.0 to 1.0).


## Development

### Project Structure

```
Faah extension/
├── extension.js          # Main extension code
├── package.json          # Extension manifest
├── sounds/
│   ├── faah.mp3         # Your sound file
│   └── README.txt       # Instructions
└── README.md            # This file
```


### Testing

1. Open the extension folder in VS Code
2. Press `F5` to start debugging
3. Test in the Extension Development Host window


## License

MIT License - Feel free to use and modify!


## Contributing

Contributions are welcome! Feel free to:
- Add new features
- Improve error detection
- Add support for more audio formats
- Report bugs or issues


## Changelog

### 1.1.1
- **Fixed:** Added `terminalDataWriteEvent` to API proposals to resolve activation error
- **Fixed:** Extension now properly declares all required proposed APIs
- **Improved:** Better compatibility with VS Code stable releases

### 1.1.0
- **New:** Windows support added! Now works on Windows, macOS, and Linux
- **New:** Includes WAV audio file for Windows compatibility (PowerShell SoundPlayer requires WAV format)
- **Improved:** Automatically selects correct audio format based on platform (MP3 for Linux/Mac, WAV for Windows)
- **Fixed:** Resolved audio playback issues on Windows systems

### 1.0.0
- Initial release
- Terminal error detection
- Configurable error patterns
- Volume control
- Toggle command
- Test sound command

---

Made with ❤️ for developers who want audible error notifications!
