# Mashup Generator

A Python project that creates audio mashups by downloading songs of a given singer from YouTube, trimming them, and merging them into a single output file. Available as both a CLI tool and a web service.

**Live Demo:** https://mashup-xwsv.onrender.com

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

---

## Part 2 - Web Service (Flask App)

A web interface for the mashup generator. Users fill a form, get the result on screen with an audio player + download links, and receive the output as a ZIP via email.

**Deployed at:** https://mashup-xwsv.onrender.com

### What it does

1. User submits a form with singer name, number of videos, duration, and email
2. Server downloads and processes the videos into a mashup
3. Result is displayed on screen with an audio player and download links
4. ZIP file is sent to the user's email

### Setup

```bash
source venv/bin/activate
pip install -r part2/requirements.txt
```

### SMTP Configuration (for sending emails)

Set these environment variables before running:

```bash
export SMTP_EMAIL="youremail@gmail.com"
export SMTP_PASSWORD="your-gmail-app-password"
```

To get a Gmail App Password:
1. Go to https://myaccount.google.com/apppasswords
2. Select "Mail" and your device
3. Copy the 16-character password and use it as `SMTP_PASSWORD`

### Running

```bash
cd part2
python app.py
```

Then open http://localhost:5000 in your browser.

### Features

- Web form: singer name, number of videos, duration, email
- Input validation (email format, min videos/duration)
- Audio preview player on the results page
- Direct MP3 and ZIP download links
- Sends ZIP to the provided email via SMTP

### Deployment Options

Since many cloud providers block SMTP port 25, use port 587 (TLS) which is open on most platforms:

| Platform          | SMTP 587 | Free Tier | Notes                        |
|-------------------|----------|-----------|------------------------------|
| **Render**        | Open     | Yes       | Best free option, easy setup |
| **Railway**       | Open     | Yes       | Simple deploy from GitHub    |
| **PythonAnywhere**| Open     | Yes       | Python-focused hosting       |
| **DigitalOcean**  | Open     | No        | Full VPS, no SMTP blocks     |
| **AWS EC2**       | Open*    | Yes       | Request needed for port 25, 587 works |

### Dependencies

- [Flask](https://pypi.org/project/Flask/) - Web framework
- [yt-dlp](https://pypi.org/project/yt-dlp/) - YouTube downloading
- [pydub](https://pypi.org/project/pydub/) - Audio processing
