# Multimodal-Feature-Extraction
A detailed description on how to extract and align text, audio, and video features at word-level.

## Text Feature Extraction: Pretrained Embeddings from BERT
xxx

## Audio Feature Extraction
### Extract Audio Track from Video
Tool: **FFmpeg** run in windows `cmd`:
```
# extract from one videos
ffmpeg -i 1_60.mp4 -f wav -vn 1_60.wav

# extract all videos
# test: for %f in (*.mp4) do echo %f
for %f in (*.mp4) do ffmpeg -i "%f" -f wav -vn "%~nf.wav"

# convert stereo to mono: -ac
# resampling to 16000: -ar
ffmpeg -i 1_60.wav -ac 1 -ar 16000 1_60_.wav
```

P2FA: audio aligns with transcript.

## Video Feature Extraction: Pretrained Embeddings from ResNet
xxx
