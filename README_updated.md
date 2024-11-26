# video2dialogue

This is a Sieve pipeline that converts a YouTube video into an interactive dialogue between two talking avatars. It consists of the following steps:
* Download YouTube Video with the [youtube_to_mp4](https://sievedata.com/functions/sieve/youtube_to_mp4) Sieve function.
* Summarize the downloaded video into conversational-style text using [visual-qa](https://sievedata.com/functions/sieve/visual-qa) Sieve function (employ suitable prompt).
* Summary text is converted into speech using [tts](https://sievedata.com/functions/sieve/tts) Sieve function.
* Talking avatars are generated with [portrait-avatar](https://sievedata.com/functions/sieve/portrait-avatar) Sieve function.

**Note:** This function is a demo. To use it in production, please deploy it to [your own Sieve account](#deploying-speaker-enhance-to-your-own-sieve-account).

The pipeline completes jobs quickly by running each step (audio enhancement, background removal, eye contact correction) in parallel.

You can try it here: [https://sievedata.com/functions/sieve/speaker-enhance](https://sievedata.com/functions/sieve/speaker-enhance)

Or see [Calling `speaker-enhance` via the Sieve SDK](#calling-speaker-enhance-via-the-sieve-sdk) to learn how to call the function via the Sieve Python SDK.

## Options

* `background_img`: A background image to use for the background replacement. Overrides `background_color_rgb`.
* `background_color_rgb`: A comma-separated string representing the RGB color to use for the background replacement.
* `blur_background`: If true, blurs the background.
    * If `background_img` is provided, blurs the background image.
    * Otherwise, blurs the background of the input video.
* `blur_strength`: Size of blurring kernel. Larger values blur the background more. A value of 0 means no blurring. Defaults to 19.

## Calling `speaker-enhance` via the Sieve SDK
You can install `sieve` via pip with `pip install sievedata`.
Be sure to set `SIEVE_API_KEY` to your Sieve API key. 
You can find your API key at [https://www.sievedata.com/dashboard/settings](https://www.sievedata.com/dashboard/settings).

```python
import sieve

# get the speaker-enhance function
speaker_enhance = sieve.function.get("sieve/speaker-enhance")

# get input video, background image, and options
video = sieve.File("path/to/video.mp4")
background_img = sieve.File("path/to/background.png")
blur_background = True

# create a corrected video with the new background
out = speaker_enhance.run(video, background_img=background_img)

# create a corrected video with the original background blurred
out = speaker_enhance.run(video, blur_background=True)

# create a corrected video with a custom background color
out = speaker_enhance.run(video, background_color_rgb="255,255,255")
```

## Deploying `speaker-enhance` to your own Sieve account
First ensure you have the Sieve Python SDK installed: `pip install sievedata` and set `SIEVE_API_KEY` to your Sieve API key.
You can find your API key at [https://www.sievedata.com/dashboard/settings](https://www.sievedata.com/dashboard/settings).

Then deploy the function to your account:
```bash
git clone https://github.com/sieve-community/speaker-enhance
cd speaker-enhance
sieve deploy app.py
```

You can now find the function in your Sieve account and call it via API or SDK.
