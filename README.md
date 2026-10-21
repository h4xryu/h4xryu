<!-- Intro  -->
<h3 align="center">
        <samp>&gt; Hey There!, I am
                <b><a target="_blank" href="https://blog.naver.com/hies8875">Ryuha</a></b>
        </samp>
</h3>

<p align="center">
  <samp>On-device AI for wearable biosignals · ECG / PPG · Android · Embedded</samp>
</p>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=h4xryu&color=grey" alt="View"/>
</p>

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

## Featured Project

### 🫀 [ECG-Realtime-monitor](https://github.com/h4xryu/ECG-Realtime-monitor) — On-device real-time arrhythmia classification on Android

<table>
  <tr>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/portfolio/01_personalize_calibration.png" alt="1-minute personalization"/></td>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/portfolio/02_personalize_history.png" alt="Personalization applied"/></td>
    <td align="center" width="33%"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/portfolio/03_monitor_classification.png" alt="Real-time classification"/></td>
  </tr>
  <tr>
    <td align="center"><sub>① 1-min label-free calibration</sub></td>
    <td align="center"><sub>② Patient vector applied</sub></td>
    <td align="center"><sub>③ Beat-level 5-class result</sub></td>
  </tr>
  <tr>
    <td colspan="3" align="center"><img src="https://github.com/h4xryu/ECG-Realtime-monitor/raw/main/docs/img/portfolio/04_strip_report.png" width="80%" alt="Strip-view PDF report"/></td>
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

## Other Projects

[![ECG-Potassium-Estimation](https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=ECG-Potassium-Estimation&border_color=7F3FBF&bg_color=0D1117&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF)](https://github.com/h4xryu/ECG-Potassium-Estimation)
[![PPG-serial-monitor](https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=PPG-serial-monitor&border_color=7F3FBF&bg_color=0D1117&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF)](https://github.com/h4xryu/PPG-serial-monitor)
[![SignalPlot](https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=SignalPlot&border_color=7F3FBF&bg_color=0D1117&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF)](https://github.com/h4xryu/SignalPlot)
[![Dataset-for-ECG-Paper-detection](https://github-readme-stats.vercel.app/api/pin/?username=h4xryu&repo=Dataset-for-12-lead-ECG-Paper-detection&border_color=7F3FBF&bg_color=0D1117&title_color=C9D1D9&text_color=8B949E&icon_color=7F3FBF)](https://github.com/h4xryu/Dataset-for-12-lead-ECG-Paper-detection)

<p align="left">
  <a href="https://github.com/h4xryu?tab=repositories" target="_blank"><img alt="All Repositories" title="All Repositories" src="https://img.shields.io/badge/-All%20Repos-2962FF?style=for-the-badge&logo=koding&logoColor=white"/></a>
</p>

<br/>
<hr/>
<br/>

<p align="center">
  <a href="https://github.com/h4xryu">
    <img src="https://github-readme-streak-stats.herokuapp.com/?user=h4xryu&theme=radical&border=7F3FBF&background=0D1117" alt="Ryuha's GitHub streak"/>
  </a>
</p>

<p align="center">
  <a href="https://github.com/h4xryu">
    <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=h4xryu&theme=radical" alt="Ryuha's GitHub Contribution"/>
  </a>
</p>

<a> 
    <a href="https://github.com/h4xryu"><img alt="Ryuha's Github Stats" src="https://denvercoder1-github-readme-stats.vercel.app/api?username=h4xryu&show_icons=true&count_private=true&theme=react&border_color=7F3FBF&bg_color=0D1117&title_color=F85D7F&icon_color=F8D866" height="192px" width="49.5%"/></a>
  <a href="https://github.com/h4xryu"><img alt="Ryuha's Top Languages" src="https://denvercoder1-github-readme-stats.vercel.app/api/top-langs/?username=h4xryu&langs_count=8&layout=compact&theme=react&border_color=7F3FBF&bg_color=0D1117&title_color=F85D7F&icon_color=F8D866" height="192px" width="49.5%"/></a>
  <br/>
</a>


![Ryuha's Graph](https://github-readme-activity-graph.vercel.app/graph?username=h4xryu&custom_title=Ryuha's%20GitHub%20Activity%20Graph&bg_color=0D1117&color=7F3FBF&line=7F3FBF&point=7F3FBF&area_color=FFFFFF&title_color=FFFFFF&area=true)
