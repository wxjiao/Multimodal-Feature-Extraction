# Multimodal-Feature-Extraction
A detailed description on how to extract and align text, audio, and video features at word-level.

## 1. Text
### Pre-trained Word Embeddings from GloVe
The first and also convenient way to obtain textual feature is to fetch the pre-trained word embeddings from publicly available sources, such as Word2Vec, and GloVe. To do so, we follow the strategies below:
  - **Vocabulary**: Build a vocabulary based on the output of **Forced Alignment**, as it performs the first step of tokenization. Some abbrevations need to be taken care of, such as `i'm`, `i've`, and `what's`.
  - **Embedding Matrix**: Assign the GloVe vectors to the built **Vocabulary**, and initialize unknown word by random vectors.
  - **Embedding Matching**: To be consistent with the audio segments, we get the embeddings for abbrevations like `what's` by summing the embeddings of `what`,`'`, and `s`. Other single tokens just fetch their embeddings from the **Embedding Matrix** directly.

###  Pretrained Embeddings from BERT

## 2. Audio
### Extract Audio Track from Video
[FFmpeg](https://ffmpeg.org/) \[C/C++\]: A complete, cross-platform solution to record, convert and stream audio and video.

**FFmpeg** is used to extract the audio track from video, merge voice channels, and resample the audio. 

To extract the audio track from video in Windows `cmd`:
```ruby
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
[P2FA](https://web.sas.upenn.edu/phonetics-lab/) \[Python\]: Penn Phonetics Lab Forced Aligner for English.

**Requisites**:
- [HTK](http://htk.eng.cam.ac.uk/) \[C/C++\]: About the compiling of HTK on Windows please refer to [HTK on Windows](https://github.com/JoFrhwld/FAVE/wiki/HTK-on-Windows). You need to set up the `win32` environment in `cmd` for compiling. Note that you may encounter errors when compling due to the incompatibility of `.mkf` syntax. To solve the problem, you have to remove all the unnecessary **space line** in related `.mkf` files. 
- [SoX](http://sox.sourceforge.net/) \[C/C++\]: To install SoX on Windows, you may refer to [SoX on Windows](https://github.com/JoFrhwld/FAVE/wiki/Sox-on-Windows).

We use a modified version from [p2fa-vislab](https://github.com/ucbvislab/p2fa-vislab), which could take the `.json` schema for the input and the output. The `.wav` audio file must be 16 bit mono. More details please refer to the repository. 

Here, we run the Python scripts in Windows `cmd`:
```ruby
# Align for all videos
for %f in (./Dataset/alignment/*.wav) do \
python align.py ./Dataset/alignment/%f \
./Dataset/alignment/%~nf.json \
./Dataset/alignment/%~nf_aligned.json
```

> TODO: radiotool package; mis-alignment; phase;

### Audio Feature Extraction
[COVAREP](https://github.com/covarep/covarep) \[MATLAB/Octave\]: A cooperative voice analysis repository for speech technologies.

**Requisites**
- [Voicebox](http://www.ee.ic.ac.uk/hp/staff/dmb/voicebox/voicebox.html) \[MATLAB\]: **COVAREP** is built on MATLAB ( compatible with Octave), requiring the *Voicebox* toolbox. Unzip the *Voicebox* package and move the '/voicebox' folder to the MATLAB toolbox folder. Use **Set Path** in Matlab to add '/voicebox' to MATLAB Search Path.
- [Deep Learning Toolbox](https://www.mathworks.com/products/deep-learning.html) should be installed in MATLAB for extracting the *Voice Activity Detection* (VAD) feature.

To extract the audio feature in MATLAB:
```ruby
# Run startup.m at the home dir of COVAREP to set up the paths
>> startup;

# Put your audio data in in_dir='Dataset/audio', set your sample_rate=0.04 (s)
# the COVAREP_feature_formant_extraction.m script will extract features of each frame 
# and save them in separate .mat/.csv files for each audio
>> COVAREP_feature_formant_extraction('./Dataset/audio', 0.04);
```

> **Note:** The called function `COVAREP_feature_formant_extraction_perfile.m` should report errors when handling very short audios, limited by `filtfilt.m`. To address the problem, we keep doubling the input audio until the number of samples exceeds the original sampling rates (16000 Ours).


## 3. Video
### Facial Feature Extraction
[OpenFace](https://github.com/TadasBaltrusaitis/OpenFace) \[C/C++\]:  A state-of-the art tool intended for facial landmark detection, head pose estimation, facial action unit recognition, and eye-gaze estimation.

**OpenFace** can be installed on Windows, MacOS, and Linux, here we run the code in Windows `cmd`:
```ruby
# Extract features from videos
FeatureExtraction.exe -f "./Dataset/video/video_1.mp4"

# Videos with multiple faces
FaceLandmarkVidMulti.exe -f "./Dataset/video/video_1.mp4"

# Extract all videos
# Test: for %f in (./Dataset/MUStARD/*.mp4) do echo %f
for %f in (./Dataset/video/*.mp4) do FaceLandmarkVidMulti.exe -f "./Dataset/video/%f"
```
> TODO: distinguish multiple faces;


