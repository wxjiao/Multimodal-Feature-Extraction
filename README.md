# Multimodal-Feature-Extraction
A detailed description on how to extract and align text, audio, and video features at word-level.

## Text
###  Pretrained Embeddings from BERT

## Audio
### Extract Audio Track from Video
[FFmpeg](https://ffmpeg.org/): A complete, cross-platform solution to record, convert and stream audio and video.

**FFmpeg** is used to extract the audio track from video, merge voice channels, and resample the audio. 

To extract the audio track from video in Windows `cmd`:
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
[COVAREP](https://github.com/covarep/covarep): A cooperative voice analysis repository for speech technologies.

**COVAREP** is built on Matlab ( compatible with Octave), requiring the toolbox [*Voicebox*](http://www.ee.ic.ac.uk/hp/staff/dmb/voicebox/voicebox.html). 
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

## Video
### Facial Feature Extraction
[OpenFace](https://github.com/TadasBaltrusaitis/OpenFace):  A state-of-the art tool intended for facial landmark detection, head pose estimation, facial action unit recognition, and eye-gaze estimation.

**OpenFace** can be installed on Windows, MacOS, and Linux, here we run the code on Windows in `cmd`:
```
# Extract features from videos
FeatureExtraction.exe -f "./Dataset/video/video_1.mp4"

# Videos with multiple faces
FaceLandmarkVidMulti.exe -f "./Dataset/video/video_1.mp4"

# Extract all videos
# Test: for %f in (./Dataset/MUStARD/*.mp4) do echo %f
for %f in (./Dataset/video/*.mp4) do FaceLandmarkVidMulti.exe -f "./Dataset/video/%f"
```


