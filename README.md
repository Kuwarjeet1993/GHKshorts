# GHKshorts

A Claude skill that turns long videos into social-ready clips.

![GHKshorts turns long videos into 9:16 social clips](assets/preview.png)

Point it at any video and it will:

1. **Find clip-worthy moments**
   - *Dialogue mode*: transcribes with [Whisper](https://github.com/openai/whisper) and scans for punchlines, reversals, awkward pauses and audio peaks.
   - *Action mode*: detects repeated impact sounds (axe chops, hits, drumbeats) and cuts on each one.
2. **Reframe 16:9 → 9:16**: hard-cut pans that follow whoever is speaking, or a split-screen with both faces.
3. **Speed-ramp slow reveals** so they're tighter but keep the whole arc.
4. **Burn word-by-word captions** in three presets: opus, karaoke or minimal.

Everything runs locally with no cloud APIs and no OpenCV.

## Requirements

- `ffmpeg` with `libx264`
- [`whisper`](https://github.com/openai/whisper) (`pip install openai-whisper`)
- Python 3 with `numpy`
- On macOS, `-hwaccel videotoolbox` speeds up decoding. Remove it on Linux or Windows.

## Install

**Claude Code**

```bash
git clone https://github.com/Kuwarjeet1993/GHKshorts.git ~/.claude/skills/ghkshorts
```

Restart Claude Code, then run `/ghkshorts`.

**Claude app**: upload `ghkshorts.zip` (the repo folder zipped) in Settings → Capabilities → Skills.

## Usage

```
/ghkshorts
```

Give it a video. It proposes 3–5 candidate clips, then asks for the aspect ratio (9:16, 16:9 or 1:1), pan or split-screen, and a caption style. Finished clips are saved to `<source-video-dir>/ghkshorts_out/`.

## Files

```
SKILL.md                     # the skill instructions
scripts/analyze.py           # speaker timeline from ROI motion energy
scripts/build_pan.py         # ffmpeg crop expression for hard-cut pans
scripts/build_ass.py         # opus/karaoke/minimal ASS captions
scripts/audio_align.py       # locate a sub-clip in a longer source (FFT)
scripts/detect_transients.py # impact detection for action montages
```

## Credits

Based on [louisedesadeleer/clipify](https://github.com/louisedesadeleer/clipify), MIT licensed. The original copyright notice is kept in [LICENSE](LICENSE).
