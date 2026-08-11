# audio-transcribe

Transcribe audio files or YouTube videos locally using whisper.cpp with Apple Silicon acceleration.

## Install

### Homebrew (recommended)

```bash
brew install wimdetroyer/toolz/audio-transcribe
audio-transcribe setup
```

Dependencies (ffmpeg, whisper-cpp, yt-dlp) are installed automatically. The
`setup` step then downloads the whisper large-v3 model (~3 GB), stored in
`~/.whisper/models/`.

### Manual

```bash
git clone https://github.com/wimdetroyer/audio-transcribe.git
cp audio-transcribe/bin/audio-transcribe /usr/local/bin/
audio-transcribe setup
```

Or install the script directly:

```bash
curl -fsSL https://raw.githubusercontent.com/wimdetroyer/audio-transcribe/main/bin/audio-transcribe \
  -o /usr/local/bin/audio-transcribe && chmod +x /usr/local/bin/audio-transcribe
audio-transcribe setup
```

## Usage

```
audio-transcribe [options] <audio-file-or-youtube-url>
audio-transcribe setup
```

### Options

| Flag | Description |
|------|-------------|
| `-l LANG` | Language hint (e.g. `en`, `nl`, `fr`, `de`) |
| `setup` | Download model (and build whisper.cpp if not system-installed) |

### Examples

```bash
# Transcribe a local audio file
audio-transcribe recording.mp3

# Transcribe with a language hint
audio-transcribe -l nl interview.wav

# Transcribe a YouTube video
audio-transcribe https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

## How it works

1. Audio is converted to 16kHz WAV via ffmpeg
2. whisper.cpp transcribes it locally using Metal GPU acceleration
3. No cloud APIs, no usage limits, no internet required after setup

The large-v3 model (~3 GB) is stored in `~/.whisper/models/`.

## Dependencies

- **ffmpeg** (required) - audio conversion
- **whisper-cpp** (required) - install via Homebrew or let `setup` build from source
- **yt-dlp** (optional) - only needed for YouTube URL support

If `whisper-cli` is on your PATH (e.g. from `brew install whisper-cpp`), `setup` skips the build step and only downloads the model.

## License

MIT
