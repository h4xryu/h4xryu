<!-- Intro  -->

<p align="center">
  <samp>On-device AI for wearable biosignals · ECG / PPG · Android · Embedded</samp>
</p>


<br/>


## Featured Project

### [ECG-Realtime-monitor](https://github.com/h4xryu/ECG-Realtime-monitor) — On-device real-time arrhythmia classification on Android

<table>
  <tr>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/personalization.jpeg" alt="1-minute personalization"/></td>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/personalization_history.jpeg" alt="Personalization applied"/></td>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/monitor_calibrated.png" alt="Real-time classification"/></td>
  </tr>
  <tr>
    <td align="center"><sub>① 1-min label-free calibration</sub></td>
    <td align="center"><sub>② Patient vector applied</sub></td>
    <td align="center"><sub>③ Beat-level 5-class result</sub></td>
  </tr>
  <tr>
    <td colspan="3" align="center"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/strip_report.png" width="80%" alt="Strip-view PDF report"/></td>
  </tr>
  <tr>
    <td colspan="3" align="center"><sub>④ Exported clinical strip-view PDF report (25 mm/s)</sub></td>
  </tr>
</table>

A wearable ECG patch (single-lead, 250 Hz) streams over BLE to an Android phone, which classifies every heartbeat on-device in real time — no server round-trip.
On-device implementation of my master's thesis (Yonsei Univ. ISPLAB, Feb 2027).

**What I did**
- Lightweighted ResUMamba [Heo et al.] into ResDSUMamba (depthwise-separable conv) and exported it with ExecuTorch + XNNPACK
- Built the full Android pipeline: BLE frame parsing → filtering / lead-off detection → R-peak alignment → beat classification → clinical-calibrated display (true mV · 25 mm/s)
- Added label-free patient personalization: a 60 s calibration record is encoded into a 256-dim patient vector (CPC) that conditions every beat
- Continuous recording with MAT / NPZ export and a clinical strip-view PDF report

**Results** (Galaxy S21+, FP32, single big core)

| | Before | After |
|---|---:|---:|
| Params / MACs | 2.49 M / 721.5 M | 1.32 M / 331.4 M (−46.9% / −54.1%) |
| Model latency | 1073.6 ms (baseline, portable) | 36.7 ms (ResDSUMamba, XNNPACK) |
| Macro-F1 / Micro-F1 | 42.28% / 79.27% | 44.15% / 83.29% |
| Tab-switch jank (P99) | 2650 ms | 17 ms |

Live 5-minute patch session: 59.4 ms per beat end-to-end (P95 70.3 ms), 7.9% inference-thread CPU.

**Troubleshooting highlights**
- The sensor's on-chip R-peak tag lagged the true QRS by ~340 ms → backward-window realignment on the waveform (98% of beats within 60 ms, unit-tested on real recordings)
- UI froze when switching tabs over many records → async list loading, metadata sidecars, UI-pulse coalescing

`Kotlin` `Android` `BLE` `ExecuTorch` `XNNPACK` `PyTorch` `Mamba (SSM)` · [Design spec & UML](https://github.com/h4xryu/ECG-Realtime-monitor/blob/main/docs/DESIGN_SPEC.md)

<br/>

### [12-Lead ECG Dataset Utils](https://github.com/h4xryu/12-Lead-ECG-Dataset-Utils-For-Real-Time-Lead-Detection-Using-YOLO) — For Real-Time YOLO-Based ECG Lead Detection

Utilities for preparing and augmenting 12-lead ECG image datasets for YOLOv7-based lead detection.

<p align="center">
  <img
    src="https://github.com/h4xryu/12-Lead-ECG-Dataset-Utils-For-Real-Time-Lead-Detection-Using-YOLO/raw/main/images/before1.jpeg"
    width="48%"
    alt="ECG lead detection before refinement"
  />
  <img
    src="https://github.com/h4xryu/12-Lead-ECG-Dataset-Utils-For-Real-Time-Lead-Detection-Using-YOLO/raw/main/images/after1.jpeg"
    width="48%"
    alt="ECG lead detection after refinement"
  />
</p>

<p align="center">
  <sub>ECG lead detection results before and after bounding-box refinement.</sub>
</p>

<p align="center">
  <img
    src="https://raw.githubusercontent.com/h4xryu/12-Lead-ECG-Dataset-Utils-For-Real-Time-Lead-Detection-Using-YOLO/main/images/lead_roi_detection.gif"
    width="85%"
    alt="Real-Time Lead ROI Detection"
  />
</p>

<p align="center">
  <sub>Real-time detection and localization of ECG lead regions.</sub>
</p>

**Key areas**
- ECG image preprocessing and dataset preparation
- Image augmentation with background textures, shadows, and geometric distortions
- ROI extraction and lead-region organization

`Python` `YOLOv7` `OpenCV` `Computer Vision`


### [ECG Signal Generation Using TCWGAN-GP](https://github.com/h4xryu/ECG-Signal-Generation-Using-TCWGAN-GP) — Transformer-Based ECG Signal Generation

A Transformer-based generator trained using the Wasserstein GAN with Gradient Penalty (WGAN-GP) framework.

<p align="center">
  <img
    src="https://github.com/h4xryu/ECG-Signal-Generation-Using-TCWGAN-GP/raw/main/images/gen_example.gif"
    width="85%"
    alt="Generated ECG waveforms across training epochs"
  />
</p>

<p align="center">
  <sub>Synthetic ECG waveforms generated during training.</sub>
</p>

**Key areas**
- Transformer encoder-based signal generation
- WGAN-GP training framework
- One-dimensional ECG waveform synthesis

`Python` `PyTorch` `Transformer` `GAN` `ECG`


<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=PPG-serial-monitor&theme=transparent&border_color=7F3FBF&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=PPG-serial-monitor&theme=transparent&border_color=7F3FBF&title_color=24292F&text_color=57606A&icon_color=7F3FBF"
  />
  <img
    src="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=PPG-serial-monitor&theme=transparent&border_color=7F3FBF&title_color=24292F&text_color=57606A&icon_color=7F3FBF"
    alt="PPG-serial-monitor"
  />
</picture>

<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=SignalPlot&theme=transparent&border_color=7F3FBF&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF"
  />
  <source
    media="(prefers-color-scheme: light)"
    srcset="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=SignalPlot&theme=transparent&border_color=7F3FBF&title_color=24292F&text_color=57606A&icon_color=7F3FBF"
  />
  <img
    src="https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=SignalPlot&theme=transparent&border_color=7F3FBF&title_color=24292F&text_color=57606A&icon_color=7F3FBF"
    alt="SignalPlot"
  />
</picture>


<p align="left">
  <a href="https://github.com/h4xryu?tab=repositories" target="_blank"><img alt="All Repositories" title="All Repositories" src="https://img.shields.io/badge/-All%20Repos-2962FF?style=for-the-badge&logo=koding&logoColor=white"/></a>
</p>

<br/>
<hr/>
<br/>

## Use To Code & Library, IDEs

![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&labelColor=black&logo=kotlin&logoColor=7F52FF)
![Android](https://img.shields.io/badge/Android-34A853?style=for-the-badge&labelColor=black&logo=android&logoColor=34A853)
![ExecuTorch](https://img.shields.io/badge/ExecuTorch-EE4C2C?style=for-the-badge&labelColor=black&logo=pytorch&logoColor=EE4C2C)
![Torch](https://img.shields.io/badge/Torch-black?style=for-the-badge&logo=pytorch&logoColor=orange)
![Python](https://img.shields.io/badge/Python-white?style=for-the-badge&labelColor=&logo=python&logoColor=black)
![C](https://img.shields.io/badge/C-007acc?style=for-the-badge&labelColor=black&logo=c&logoColor=007acc)
![C++QT](https://img.shields.io/badge/C++QT-6EA94B?style=for-the-badge&labelColor=black&logo=qt&logoColor=6EA94B)
![Java](https://img.shields.io/badge/-Java-F0DB4F?style=for-the-badge&labelColor=black&logo=openjdk&logoColor=F0DB4F)
![OpenCV](https://img.shields.io/badge/OpenCV-000000?style=for-the-badge&logo=opencv&logoColor=)
![Tensorflow](https://img.shields.io/badge/Tensorflow-white?style=for-the-badge&logo=tensorflow&logoColor=orange)
![Ubuntu](https://img.shields.io/badge/ubuntu-E34F26?style=for-the-badge&logo=Ubuntu&logoColor=white)
![CLion](https://img.shields.io/badge/CLion-50C878?style=for-the-badge&labelColor=50C878&logo=Clion&logoColor=black)
![VSCode](https://img.shields.io/badge/Visual_Studio-black?style=for-the-badge&logo=visual%20studio&logoColor=0078d7)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

<br/>

<p align="center">
  <a href="https://github.com/h4xryu">
    <picture>
      <source
        media="(prefers-color-scheme: dark)"
        srcset="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=h4xryu&theme=github_dark"
      />
      <source
        media="(prefers-color-scheme: light)"
        srcset="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=h4xryu&theme=github"
      />
      <img
        src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=h4xryu&theme=github"
        alt="Ryuha's GitHub Contribution"
      />
    </picture>
  </a>
</p>

<p align="center">
  <a href="https://github.com/h4xryu">
    <picture>
      <source
        media="(prefers-color-scheme: dark)"
        srcset="https://denvercoder1-github-readme-stats.vercel.app/api?username=h4xryu&show_icons=true&count_private=true&theme=react&border_color=7F3FBF&bg_color=00000000&title_color=F85D7F&icon_color=F8D866"
      />
      <source
        media="(prefers-color-scheme: light)"
        srcset="https://denvercoder1-github-readme-stats.vercel.app/api?username=h4xryu&show_icons=true&count_private=true&theme=default&border_color=7F3FBF&bg_color=00000000&title_color=7F3FBF&icon_color=BF8700"
      />
      <img
        height="192px"
        width="49.5%"
        src="https://denvercoder1-github-readme-stats.vercel.app/api?username=h4xryu&show_icons=true&count_private=true&theme=default&border_color=7F3FBF&bg_color=00000000&title_color=7F3FBF&icon_color=BF8700"
        alt="Ryuha's GitHub Stats"
      />
    </picture>
  </a><a href="https://github.com/h4xryu">
    <picture>
      <source
        media="(prefers-color-scheme: dark)"
        srcset="https://denvercoder1-github-readme-stats.vercel.app/api/top-langs/?username=h4xryu&langs_count=8&layout=compact&theme=react&border_color=7F3FBF&bg_color=00000000&title_color=F85D7F&icon_color=F8D866"
      />
      <source
        media="(prefers-color-scheme: light)"
        srcset="https://denvercoder1-github-readme-stats.vercel.app/api/top-langs/?username=h4xryu&langs_count=8&layout=compact&theme=default&border_color=7F3FBF&bg_color=00000000&title_color=7F3FBF&icon_color=BF8700"
      />
      <img
        height="192px"
        width="49.5%"
        src="https://denvercoder1-github-readme-stats.vercel.app/api/top-langs/?username=h4xryu&langs_count=8&layout=compact&theme=default&border_color=7F3FBF&bg_color=00000000&title_color=7F3FBF&icon_color=BF8700"
        alt="Ryuha's Top Languages"
      />
    </picture>
  </a>
</p>


