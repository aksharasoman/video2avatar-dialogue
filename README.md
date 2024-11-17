# Transform YouTube Videos into Conversational Avatars with the Sieve API toolkit.

This repository contains the script `pipeline.py` to transform YouTube videos into engaging, conversational avatars using Sieve APIs. The goal is to automate the process of repurposing video content into interactive dialogues between two talking avatars, ideal for storytelling, educational purposes, or creating dynamic presentations.

## Overview

The `pipeline.py` script achieves the following:

1. **Download YouTube Video**: Extracts video content using the Sieve function.
2. **Summarize Content**: Converts the video content into a conversational-style summary between two speakers.
3. **Text-to-Speech Conversion**: Uses Sieve's TTS API to convert the summarized dialogue into speech.
4. **Talking Avatar Generation**: Creates two distinct avatars to narrate the conversation using Sieve's portrait-avatar API.
5. **Merge Video Clips**: Combines individual video segments into a final video using `ffmpeg`.

### Key Benefits
- **Repurpose Content**: Convert lengthy videos into bite-sized, conversational narratives.
- **Interactive Presentations**: Make content more engaging with avatars.
- **Time Efficiency**: Summarization saves time while retaining the core message.
- **Creative Possibilities**: Perfect for storytelling, education, or marketing.

## Installation

### Requirements

- Python 3.7+
- Sieve Python Client
- ffmpeg

1. Clone this repository:

   ```bash
   git clone https://github.com/yourusername/video2dialogue.git
   cd video2dialogue
   ```

2. Install dependencies:

   ```bash
   pip install sievedata
   ```

3. Authenticate with Sieve:

   ```bash
   sieve login
   ```
4. **Run the Script**
   Ensure `pipeline.py` is in your project folder:

   Execute the pipeline with:

   ```bash
   python pipeline.py
   ```
5. **Output**

   The final video featuring talking avatars will be saved in your project directory. Logs and job statuses can be monitored on the Sieve dashboard.

## Example

For a complete working example, see the demo [here](https://www.sievedata.com/jobs/4e76d8e5-3b0c-436e-98fa-c48d310ed60f).

## Explanation of `pipeline.py`

The script follows these steps, with the main part outlined below:

1. **Download YouTube Video**:
   ```python
   youtube_to_mp4 = sieve.function.get("sieve/youtube_to_mp4")
   output_video = youtube_to_mp4.run(url, resolution="highest-available", include_audio=True)
   ```

2. **Summarize as Conversation**:
   ```python
   visual_summarizer = sieve.function.get("sieve/visual-qa")
   summary_as_conversation = visual_summarizer.run(output_video, prompt="Summarize into a dialogue between 2 people.", fps=1)
   ```
   The use of an appropriate prompt is important.

3. **Text-to-Speech and Avatar Generation**:
   ```python
   tts = sieve.function.get("sieve/tts")
   portrait_avatar = sieve.function.get("sieve/portrait-avatar")
   ```
We run these sieve functions iteratively for each turn of the conversation to generate the corresponding avatar videos. For different spekers in the conversation, input different voices for the tts function and different avatar images for the portrait-avatar function .
   
5. **Merge Video Clips**:
   ```bash
   ffmpeg -f concat -safe 0 -i file_list.txt -c copy output.mp4
   ```
## Tutorial
For a detailed explanation, follow the tutorial [here](https://docs.google.com/document/d/1zXoZHmIz-kIjKEnVMis2V6NU3rJo5AaGe-OUDlDf57k/edit?usp=sharing).

## Acknowledgments

Special thanks to [Sieve](https://www.sievedata.com) for their powerful APIs that made this project possible.



