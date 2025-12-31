---
description: >-
  Here are some quality settings for OBS that worked for me. I will update
  overtime as I test and experience more.
---

# My looking into of OBS Settings.

**OBS**

This is mainly for **recording** and not for live streaming, please keep that in mind :) \[ ] **Recording Formats**: \[ ] There are quite a few but I am just going to go through the most used ones. =-=

* **Matroska Video (.mkv)**
  * This is quite often used for recording to prevent corrupted recordings in case your system crashes or anything like that.
  * Deef uses this and this is honestly probably the best container to use if you do not want to test others :)
  * Keep in mind you will have to remux this (Obs -> File -> Remux)
  * Another thing to note if you are just clipping. You won't be able to view it directly in discord. The person you send it to would have to download the file. =-=
* **MPEG-4 (.mp4)**
  * This is a modern video container/recording format and one of the most supported.
  * Offers good compression and access to hard acceleration.
  * Not good for recording as if a crash happens the recording could be corrupted.
  * Good format, but not ideal for recording your videos in. =-=
* **QuickTime (.mov)**
  * I have not looked that much into this one to be honest as I believe there are better options.
  * Does have larger file size.
  * Again, did not do a lot of research in to this one. =-=
* **Hybrid MP4 (.mp4)**
  * !_This is in BETA_!
  * This is what I have been testing with and has been working well in my experience.
  * Has the benefits of MP4 as well as fragmented MP4.
  * Further information can be found here: [Native Hybrid MP4 Muxer by derrod · Pull Request #10608 · obsproject/obs-studio · GitHub](https://github.com/obsproject/obs-studio/pull/10608)
  * **Something to note**:
    * Fragmented MP4 would struggle with audio imports into Davinci. But, Hybrid MP4 did not have that issue. =-=
* **Fragmented MP4 (.mp4)**
  * Is supposed to give the benefit of MP4, but to help with the issue of corrupted recordings on crash.
  * I tried using this for a bit, but the audio import issue made me stop using this.
  * I personally believe "Hybrid MP4" is better if it works for you. =-=
* **Fragmented MOV (.mov)**
  * Thought I would just include this. Basically MOV, but to help with corrupted recordings on crash. =-=
* **Recording Formats Summary**:
  * Use **MKV**. If you are willing to test out others, I would suggest **Hybrid MP4** if possible.
  * From my system specs, it does not look like this limits Video or Audio encoding formats.
  * MKV may need to be remuxed only if you're not editing in Davinci Resolve, which recognizes MKV as an editable format. (Thank you Deef for this info)

\[ ] **Video Encoders**: \[ ] I won't go into all of them, mainly just what looks like to be the most used ones. =-=

* **Quickly there are some things to clear up.**
  * AMD HW = AMD Hardware based encoding.
  * NVIDIA NVENC = NVIDIA Hardware encoding.
  * There are some other forms, but I did not look into those. =-=
* **x264**
  * This is CPU based encoding. Avoid if possible, it is good just uses a _lot_ of CPU resources.
  * One of the originals. Good quality, but less efficient compression compared to newer codecs like H.265 or AV1, resulting in larger files for the same quality.
  * Widely supported. =-=
* **NVIDIA NVENC**
  * **HEVC**
    * Basically H.265, good compression.
    * Potentially better quality than H.264 for the same bitrate.
    * Generally good efficiency.
    * Heavier hardware load.
  * **AV1**
    * Newest, and most efficient codec.
    * Really good compression.
    * From my testing, this seems better for streaming due to codec efficiency. For my goals quality does not seem there for recording yet.
    * Heaviest hardware load.
  * **H.264**
    * Oldest and most supported codec.
    * It is a great codec, just not as efficient compared to other codecs.
    * Quality is really good (probably the best) for it as well, again file size will just be a lot bigger.
    * Lightest hardware load. =-=
* **AMD HW**
  * **H.264**
    * Quality is not as refined as NVENC.
    * The rest is the same as described for NVIDIA NVENC encoding.
  * **H.265 (HEVC)**
    * The same as described for NVIDIA NVENC encoding.
  * **AV1**
    * Might be better than NVENC AV1.
    * The rest is the same as described for NVIDIA NVENC encoding. =-=
* **Video Encoders Summary**:
  * Try hardware before software (NVIDIA NVENC or AMD HW).
  * I use HEVC as the quality looks really good and the file size is not crazy.
    * I may test H.264 but wanting to be cautious of file size.
  * **Quality**:
    * H.264 -> H.265(HEVC) -> AV1
  * **Efficiency:**
    * AV1 -> H.265(HEVC) -> H.264 =-= \[ ] **Audio Encoders** \[ ] For the most part there are really only 2 good audio encoders (from my understand and research) that will work best for recording. =-=
  * **FFmpeg AAC**
    * Overall this is what _most_ people will be using.
    * It offers high quality audio that is **lossy**.
    * It is efficient, compatible, and smaller file size compared to FFmpeg PCM (32-bit float). =-=
  * **FFmpeg PCM (32-bit float)**
    * Lossless audio
    * Basically keeps all details and full dynamic range of audio
    * File size is a _**lot**_ bigger than FFmpeg AAC =-=
* **Audio Encoders Summary**:
  * **FFmpeg AAC** will give high quality audio and will work for mostly everyone. It also has great compression so file size is quite low.
  * **FFmpeg PCM (32-bit float)** will give you the highest form of audio (Lossless) and I would suggest it if you really care about high quality audio and editing afterwards.
    * **Real example**: Your mic peaks during recording and clip. You could recover the clipped audio and essentially bring down the peak.
      * Good explanation here @ 1:43 ([OBS 29.1 - Lossless Audio - YouTube](https://www.youtube.com/watch?v=c44-UIRCQ08))
  * I am personally using **FFmpeg PCM (24-bit float)**.

\[ ] **Rate Control**: \[ ] I have only looked into two of the options personally especially since I am only using. =-=

* **Constant Bitrate**
  * A way to make sure the recording is _always_ hitting a certain bitrate.
  * This will increase file size overall but can be good for maintaining higher quality.
  * Usually better for streaming =-=
* **Constant QP**
  * The encoder keeps the same compression level throughout the whole recording.
  * Lower QP = Higher Quality (Less Compression), Higher QP = Lower Quality (Higher Compression)
  * Usually better for recording =-=
* **Rate Control Summary**:
  * For recording use Constant QP
  * For streaming use Constant Bitrate
    * I am not going to give the best settings as a lot of this is personal preference.
    * But a good starting point at least for QP is 17 or 18 for really high quality. I could not find the graph, but 18 is where it starts to drop quality more. Just test around as I know some people do 22.
  * Watch for file size, and quality. Do what works best for what you like :

\=-=-=-= I am going to be going pretty quick for the next settings due to the nature of them as well as it can get quite complex. =-=-=-=

\[ ] **Keyframe interval**: \[ ]

* I will be honestly this can get a little complicated in this document as it is long already.
* I would suggest 2 frames every 2 seconds. (120 frames for 60fps)
* YouTube prefers it, it has good quality and compression.
* I do not stream but Twitch streamers I have seen use it.

\[ ] **Preset**: \[ ]

* This essentially sets how fast the encoder process frames
  * Slow presets = better compression efficiency:
    * Higher Quality but GPU has to work harder
* For recording P4-P7. Depending on your system specs.

\[ ] **Tuning**: \[ ]

* Basically how the encoder looks into prioritizing certain aspects of the recording/streaming.
* How they are named is pretty self explanatory.
  * High Quality = Would suggest for recording for YouTube Vids
  * Low Latency = Good for streaming, sacrifices some efficiency for compression.
  * Ultra Low Latency = Good for competitive gaming or broadcasting. =-= \[ ] **Multipass Mode**: \[ ]
* This is basically where the encoder goes through the whole video and stores information about where more bitrate may be needed (first pass).
* The second pass will actually encode the video with what was found during the first pass.
* **Disabled** = Fasted but not efficient quality for the same bitrate
* **Quarter** = Very light Multipass, improved efficiency for the bitrate.
  * I use this for recording, but Full for rendering.
* **Full** = Best for high quality recordings, will take longer to render. =-= \[ ] **Profile**: \[ ]
* How your video is recording for color profiles.
  * **Main** = 8bit color, less head room for colors, and smaller color range.
  * **Main10** = 10bit color, higher colors range, more head room for editing.
* If your GPU supports it, use **Main10** for better color depth and reduced banding — great for YouTube or any post-processing work. =-= \[ ] **Look-ahead**: \[ ]
* The codec will look ahead in your recording by a few frames to see if more bitrate is needed.
* This will help transition during scene changes and makes things smoother.
* Better bit allocation as well.
* I suggest enabling look-ahead, and enable it myself. =-= \[ ] **Adaptive Quantization**: \[ ]
* This is a kind of strange thing and I am testing what I like personally.
* What this does is will add more compression things that are like a background. But, for things that are foreground it will use less compression to make it look better.
* Test for yourself, but usually keeping it enabled _should_ help with file size. =-= \[ ] **B-Frames**: \[ ]
* This is a form of compression that will look at the frame <- before and -> after the current one it is one to determine the best bitrate.
* Helps a lot with file size and is the best form of compression while keeping video quality.

\--

\[ ] **TL;DR**: \[ ]

* These are good starting settings for high quality recordings. Adjust and test per your liking and what works best for you as that is what matters in the end.&#x20;

\=-= \[ ] **Key Settings Summary:** \[ ]

* **Recording Format**: `.MKV` (safe from crashes, remux to `.MP4` if needed)
  * You can try out `Hybrid MP4` if you want, but this is in BETA. Safe from crashes from my testing as well.
* **Video Encoder**: `AV1 (NVIDIA)` or `HEVC/H.265 (NVIDIA)` for modern GPUs
  * `AV1` is really good on AMD cards, might be better than NVIDIA AV1 encoding.
  * `H.264` is really good as well but has a bigger file size. I am fairly certain this is what Deef uses as well :)
* **Audio**: `FFmpeg PCM 32-bit float` for lossless, high-fidelity audio
  * If you want good quality, but not the file size of lossless `FFmpeg PCM (24-bit)` is really good and what I am using at the time of writing this.
* **Rate Control**: `Constant QP` for max quality (lower QP = better quality, and bigger file size)
  * Start at `18` and adjust from there.
* **Preset**: `Slow` for best balance of quality vs performance
* **Tuning**: `High Quality` (prioritizes visual fidelity)
* **Profile**: `Main`
  * `Main10` for 10-bit color, better gradients and less banding. Higher file size.
* **Lookahead**: `Enabled`
* **B-Frames**: `Enabled` set to `2`
* **Keyframe Interval**: `2 seconds` (good for YouTube and editing)
* **Adaptive Quantization (AQ)**: `Enabled` =-= :bulb: **Tips**:
* **AV1 is cutting edge** — amazing quality at lower bitrates, but not all editors support it yet.
* Constant QP gives the best quality for recording, especially for high-motion games.
* Lower QP values = larger file sizes, but visibly better quality.
*   Always test your settings on a few clips before doing long sessions.

    \--
