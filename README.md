# Multimodal-Feature-Extraction
A detailed description on how to extract and align text, audio, and video features at word-level.

## Text Feature Extraction
###  Pretrained Embeddings from BERT

## Audio
### Extract Audio Track from Video
[FFmpeg](https://ffmpeg.org/) is used to extract the audio track from video. 

We run it in windows `cmd`:
```
# Extract from one videos
ffmpeg -i 1_60.mp4 -f wav -vn 1_60.wav

# Extract all videos
# test: for %f in (*.mp4) do echo %f
for %f in (*.mp4) do ffmpeg -i "%f" -f wav -vn "%~nf.wav"

# Convert stereo to mono: -ac
# Resample to 16000: -ar
ffmpeg -i 1_60.wav -ac 1 -ar 16000 1_60_.wav
```

### Forced Alignment
P2FA: audio aligns with transcript.

### Audio Feature Extraction
[COVAREP](https://github.com/covarep/covarep): A Cooperative Voice Analysis Repository for Speech Technologies.

The COVAREP tool is built on Matlab ( compatible with Octave), requiring the toolbox [*Voicebox*](http://www.ee.ic.ac.uk/hp/staff/dmb/voicebox/voicebox.html). 
Unzip the *Voicebox* package and move the '/voicebox' folder to the Matlab toolbox folder. Use **Set Path** in Matlab to add '/voicebox' to Matlab Search Path.

To extract the audio feature in Matlab:
```
# Run startup.m at the home dir of COVAREP to set up the paths
>> startup

# Put your audio data in in_dir='Dataset/audio', set your sample_rate=0.04 (s)
# the COVAREP_feature_extraction.m script will extract features of each frame 
# and save them in separate .mat files for each audio
>> COVAREP_feature_extraction('./Dataset/audio', 0.04);
```

## Video Feature Extraction
### Pretrained Embeddings from ResNet
xxx
