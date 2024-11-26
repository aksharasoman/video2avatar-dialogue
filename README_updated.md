# video2dialogue

This is a Sieve pipeline that converts a YouTube video into an interactive dialogue between two talking avatars. It consists of the following steps:
* Download YouTube Video with the [youtube_to_mp4](https://sievedata.com/functions/sieve/youtube_to_mp4) Sieve function.
* Summarize the downloaded video into conversational-style text using [visual-qa](https://sievedata.com/functions/sieve/visual-qa) Sieve function (employ suitable prompt).
* Summary text is converted into speech using [tts](https://sievedata.com/functions/sieve/tts) Sieve function.
* Talking avatars are generated with [portrait-avatar](https://sievedata.com/functions/sieve/portrait-avatar) Sieve function.

**Note:** This function is a demo. To use it in production, please deploy it to [your own Sieve account](#deploying-video2dialogue-to-your-own-sieve-account).

The pipeline completes jobs quickly by running each step (audio enhancement, background removal, eye contact correction) in parallel.

You can try it here: [https://sievedata.com/functions/sieve/video2dialogue](https://sievedata.com/functions/sieve/video2dialogue)

Or see [Calling `video2dialogue` via the Sieve SDK](#calling-video2dialogue-via-the-sieve-sdk) to learn how to call the function via the Sieve Python SDK.

## Options

* `youtube_url`: url of the youtube video 
* `voice1` and `voice2`: voice for speakers in the generated dialogue (choose a non-cloning voice compatible with sieve-tts. See [sieve/tts](https://sievedata.com/functions/sieve/tts) readme).
* `image1` and `image2`: Input images for the talking avatars.


## Calling `video2dialogue` via the Sieve SDK
You can install `sieve` via pip with `pip install sievedata`.
Be sure to set `SIEVE_API_KEY` to your Sieve API key. 
You can find your API key at [https://www.sievedata.com/dashboard/settings](https://www.sievedata.com/dashboard/settings).

```python
import sieve

# get the video2dialogue function
video2dialogue = sieve.function.get("sieve/video2dialogue")

# get input video url, avatar images, and speaker voice options.
url = "https://www.youtube.com/watch?v=AKJfakEsgy0"
voice1 = "cartesia-commercial-man"
voice2 = "cartesia-sweet-lady"
image1 = sieve.File("path/to/portrait-man.png")
image2 = sieve.File("path/to/portrait-lady.png")

# generate a video of two talking avatars
out = video2dialogue.run(url, voice1, voice2, image1, image2)
```

## Deploying `video2dialogue` to your own Sieve account
First ensure you have the Sieve Python SDK installed: `pip install sievedata` and set `SIEVE_API_KEY` to your Sieve API key.
You can find your API key at [https://www.sievedata.com/dashboard/settings](https://www.sievedata.com/dashboard/settings).

Then deploy the function to your account:
```bash
git clone https://github.com/sieve-community/video2dialogue
cd video2dialogue
sieve deploy pipeline.py
```

You can now find the function in your Sieve account and call it via API or SDK.
