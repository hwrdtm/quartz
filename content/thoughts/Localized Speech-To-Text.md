---
title: Localized Speech-To-Text
---

I am looking for an offline-first, privacy-preserving tool that can help me:
1. Transcribe audio to text
2. Perform speaker diarization so I know who's saying which words
3. To a good degree of accuracy.

I came across https://github.com/MahmoudAshraf97/whisper-diarization
- Installing requirements using Python `3.11.0a7` didn't work.
- Using Python `3.9.9` works for the most part, but not in offline mode.

Tweaks:
- When running in `--prepare-offline-mode` without having previously set any HuggingFace environment parameters, by default it downloads to `~/.cache/huggingface/hub/models--guillaumekln--faster-whisper-medium.en`. I can pass a particular snapshot directly after the `--whisper-model-path` option, eg. as 

```
python diarize.py -a <AUDIO_FILE> --whisper-model-path ~/.cache/huggingface/hub/models--guillaumekln--faster-whisper-medium.en/snapshots/83a3b718775154682e5f775bc5d5fc961d2350ce
```
- I'm getting segmentation faults when I try to load the alignment model.
	- Am I just running out of space on my machine?
- I'm downloading the alignment model to here:
```
Downloading: "https://download.pytorch.org/torchaudio/models/wav2vec2_fairseq_base_ls960_asr_ls960.pth" to ~/.cache/torch/hub/checkpoints/wav2vec2_fairseq_base_ls960_asr_ls960.pth
```


## MacWhisper
Changing up the strategy, I came across this app called [MacWhisper](https://github.com/ggerganov/whisper.cpp/discussions/420) and decided to give it a shot. It handled my audio file to a great degree of accuracy, **even better than Otter.ai's AI**. 
- This app uses a [C/C++ implementation of the Whisper framework](https://github.com/ggerganov/whisper.cpp).
- So, using the same audio file, there's definitely discrepancies in results between MacWhisper and the following:
	- Using [openai/whisper](https://github.com/openai/whisper) directly to parse, eg. `whisper <AUDIO_FILE> --model medium --language en`
		- Lower accuracy than MacWhisper but still good.
	- Using [MahmoudAshraf97/whisper-diarization](https://github.com/MahmoudAshraf97/whisper-diarization) to parse
		- This just did not parse any words from my audio at all.

## Solution
The best solution that I have so far that prioritizes speaker segmentation is to use a tiny model against the whisper.cpp project, but it doesn't work on Intel graphics card unfortunately.


1. Turn any non-`.wav` files into `.wav` files using `ffmpeg`:
	- `ffmpeg -i <AUDIO_FILE_NON_WAV> -acodec pcm_s16le -ac 1 -ar 16000 output.wav`
2. We will be using the [whisper.cpp](https://github.com/ggerganov/whisper.cpp) project. Download the model that supports speaker segmentation (not diarization?).
	 - `./models/download-ggml-model.sh small.en-tdrz`
3. Make the main
	- `./make`
4. Run the inference
	- `./main -m models/ggml-small.en-tdrz.bin -tdrz -f <AUDIO_FILE_WAV> -otxt`


