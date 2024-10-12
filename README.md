# YouTube MP3 Downloader

A simple Python script to download the audio from YouTube videos and convert them to MP3 format using `yt_dlp`.

## Features

- **Download Audio**: Extracts the best audio quality available from a YouTube video.
- **Convert to MP3**: Converts the downloaded audio to MP3 format with a preferred quality of 192kbps.
- **Easy to Use**: Command-line interface for quick downloads.

## Requirements

- Python 3.6 or higher
- [yt_dlp](https://github.com/yt-dlp/yt-dlp)
- [FFmpeg](https://ffmpeg.org/) installed and added to your system's PATH

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/python_work.git
   cd python_work
   ```

2. **Install Required Python Packages**

   It's recommended to use a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install yt_dlp
   ```

3. **Install FFmpeg**

   - **Windows**:
     - Download FFmpeg from the [official website](https://ffmpeg.org/download.html).
     - Extract the downloaded folder.
     - Add the `bin` folder to your system's PATH.

   - **macOS**:
     ```bash
     brew install ffmpeg
     ```

   - **Linux**:
     ```bash
     sudo apt-get install ffmpeg
     ```

## Usage

Run the script with a YouTube URL as an argument:

```bash
python Youtube.py "https://www.youtube.com/watch?v=your_video_id"
```

If no URL is provided as an argument, the script will prompt you to enter one.

### Example

```bash
python Youtube.py "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
```

This will download the audio from the provided YouTube video and save it as an MP3 file in the current directory.

## Script Overview

```python
import yt_dlp
import sys
import os

def download_youtube_mp3(url):
    ydl_opts = {
        'format': 'bestaudio/best',
        'postprocessors': [{
            'key': 'FFmpegExtractAudio',
            'preferredcodec': 'mp3',
            'preferredquality': '192',
        }],
        'outtmpl': '%(title)s.%(ext)s',
    }

    try:
        with yt_dlp.YoutubeDL(ydl_opts) as ydl:
            ydl.download([url])
        print(f"Successfully downloaded audio from: {url}")
    except Exception as e:
        print(f"An error occurred: {str(e)}")
        print(f"Error type: {type(e).__name__}")
        print(f"Error details: {e.args}")

def main():
    if len(sys.argv) > 1:
        url = sys.argv[1]
    else:
        url = input("Enter the YouTube URL: ")
    
    download_youtube_mp3(url)

if __name__ == "__main__":
    main()
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgements

- [`yt_dlp`](https://github.com/yt-dlp/yt-dlp) for handling YouTube downloads and conversions.
- [FFmpeg](https://ffmpeg.org/) for audio processing.
