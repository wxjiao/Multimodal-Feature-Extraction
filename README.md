# Multimodal-Feature-Extraction
A detailed description on how to extract and align text, audio, and video features at word-level.

## Text Feature Extraction: Pretrained Embeddings from BERT
xxx

## Audio Feature Extraction
### Extract Audio Track from Video
Tool: **FFmpeg** run in windows `cmd`:
```
# extract from one videos
ffmpeg -i 1_60.mp4 -f mp3 -vn 1_60.mp3

# extract all videos
# for %f in (*.mp4) do echo %f
for %f in (*.mp4) do ffmpeg -i "%f" -f mp3 -vn "%{f%.mp4}.mp3"; done
```

P2FA: audio aligns with transcript.

## Video Feature Extraction: Pretrained Embeddings from ResNet
xxx
