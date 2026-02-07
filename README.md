# Mashup Generator

A command-line Python program that creates an audio mashup by downloading songs of a given singer from YouTube, trimming them, and merging them into a single output file.

## Part 1 - CLI Mashup (102303185.py)

### What it does

1. Searches YouTube for N videos of a given singer
2. Downloads them as audio
3. Converts all downloads to MP3
4. Cuts the first Y seconds from each audio file
5. Merges all trimmed clips into a single output MP3 file

### Prerequisites

- Python 3.7+
- ffmpeg (`brew install ffmpeg` on macOS)

### Setup

```bash
python -m venv venv
source venv/bin/activate
pip install -r part1/requirements.txt
```

### Usage

```
python part1/102303185.py <SingerName> <NumberOfVideos> <AudioDuration> <OutputFileName>
```

| Parameter       | Description                              | Constraint     |
|-----------------|------------------------------------------|----------------|
| SingerName      | Name of the singer to search on YouTube  | Any string     |
| NumberOfVideos  | Number of videos to download             | >= 10          |
| AudioDuration   | Seconds to cut from each audio           | >= 20          |
| OutputFileName  | Name of the final merged file            | Must end in .mp3 |

### Example

```bash
python part1/102303185.py "Sharry Maan" 20 20 102303185-output.mp3
```

This will download 20 Sharry Maan songs, trim the first 20 seconds of each, and merge them into `102303185-output.mp3`.

### Dependencies

- [yt-dlp](https://pypi.org/project/yt-dlp/) - YouTube video/audio downloading
- [pydub](https://pypi.org/project/pydub/) - Audio conversion, cutting, and merging
