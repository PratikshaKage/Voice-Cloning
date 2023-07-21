# Tortoise TTS: Text-to-Speech Voice Cloning

Tortoise TTS is an open-source project that provides a simple and efficient way to perform text-to-speech (TTS) voice cloning. With this project, you can generate speech in the voice of a specified speaker, clone an existing voice, and even modify speech attributes such as pitch, voicing, and more.

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#installation)
3. [Installation](#installation)
4. [Usage](#usage)



## Introduction

Tortoise TTS is built on top of PyTorch and provides an easy-to-use API for generating speech with customizable voice attributes. It uses pre-trained models and embeddings to clone a given voice, and you can also modify conditioning latents to change pitch, voicing, and other speech characteristics.

## Features

Tortoise TTS provides a range of powerful features for text-to-speech voice cloning and customization:

1. **Text-to-speech conversion:** Easily convert text into natural-sounding speech using customizable conditioning latents.

2. **Adjustable voice attributes:** Modify various speech characteristics, such as:
   - Pitch: Change the pitch of the generated speech to make it sound higher or lower.
   - Voicing: Control the voicing of the speech to increase or decrease its clarity.
   - Rounding of vowels: Adjust the rounding of vowels in the speech.
   - Aspiration of consonants: Modify the aspiration level of consonant sounds.
   - Speech rate: Speed up or slow down the generated speech to match specific requirements.
   - Intonation: Customize the intonation pattern of the speech.
   - Syllabic rate: Change the syllabic rate of the speech.
   - Word stress: Adjust the stress on words during speech generation.
   - Breath intake: Control the breath intake during speech synthesis.
   - Accent: Customize the accent of the generated speech.

3. **Audio format support:** Tortoise TTS supports various audio formats, including WAV and MP3, allowing you to save and export the generated speech in the desired format.

4. **Easy integration:** The library provides a simple and user-friendly API, making it easy to integrate Tortoise TTS into your Python projects.

With these features, Tortoise TTS empowers you to create natural and expressive speech with customizable voice characteristics, making it a versatile tool for voice cloning, voice modification, and other text-to-speech applications.

## Installation

To install Tortoise TTS, use the following pip command:

```python
pip install -U scipy
pip install -U torch torchaudio
pip install git+https://github.com/jnordberg/tortoise-tts.git
```

## Usage

Tortoise TTS is built on top of PyTorch and provides an easy-to-use API for generating speech with customizable voice attributes. It uses pre-trained models and embeddings to clone a given voice, and you can also modify conditioning latents to change pitch, voicing, and other speech characteristics.

### 1. Import the required modules:

```python
import torch
import torchaudio
from tortoise.api import TextToSpeech
from tortoise.utils.audio import load_audio, load_voice
```

### 2.Load the pre-trained TTS model:

```python
tts = TextToSpeech()

```

### 3.Load the custom voice samples (if available):



#### Gather Audio Clips:

1. Find audio clips of your speaker(s) from various sources like YouTube interviews, audiobooks, or podcasts.
2. Use tools like youtube-dl to fetch audio from YouTube videos.
3. Aim for good quality clips with clear and natural speech.

#### Prepare Audio Clips:

1. Cut the audio clips into approximately 10-second segments. It's recommended to have at least 3 clips for each speaker, but having more segments will lead to better results.
2. Save the clips as WAV files with a floating-point format and a 22,050 sample rate. This is crucial for compatibility with Tortoise TTS.

#### Create Custom Voice Folder:

1. Organize the prepared audio clips for each speaker in a folder named after the custom voice. For example, if the custom voice is named "my_custom_voice", create a folder named "my_custom_voice" and place the WAV files inside.

#### Load Custom Voice Samples:

1. Use the `load_voice` function from Tortoise's `utils.audio` module to load the custom voice samples and conditioning latents.

```python
custom_audio, = load_audio('audiosample.wav', sampling_rate=44100)

```
#### Adjust Conditioning Latents (Optional)

If you want to customize the voice attributes, you can adjust the conditioning latents. You have the flexibility to increase or decrease pitch, voicing, rounding of vowels, aspiration of consonants, and more.

Example code (as shown in the previous code provided):
```python
conditioning_latents = tensor.clone()
conditioning_latents[0, 0] *= 1.5   # Increase the pitch
conditioning_latents[0, 1] *= 0.5   # Decrease the voicing
conditioning_latents[0, 2] *= 1.25  # Increase the rounding of vowels
conditioning_latents[0, 3] *= 0.5   # Decrease the aspiration of consonants
# Add more adjustments as needed to customize the voice
```

#### Generate Speech:

Use Tortoise TTS to generate speech with the modified conditioning latents.
```python
text = "Your desired text goes here."
gen = tts.tts_with_preset(text, voice_samples=voice_samples, conditioning_latents=conditioning_latents, preset='standard')
```

#### Save and Play Generated Speech:

Save the generated speech as a WAV file and play it.

```python
torchaudio.save('generated_audio.wav', gen.squeeze(0).cpu(), 24000)
# Play the generated speech using IPython.display.Audio or any other audio player of your choice.
```


By following these steps, you can add new voices to Tortoise TTS and customize them as needed for your specific application. Enjoy experimenting with different voices and voice attributes!





