---
date: '2026-07-13'
title: 'From GPT Chat to Live'
draft: true
categories: ["AI"]
tags: ["LLM"]
---


## Cascaded voice systems

STT(whisper) -> LLM (GPT) -> TTS(Fish Audio?)
VAD (silero VAD)
编排系统 (把上述子系统串起来、管理打断/流式, Pipecat, LiveKit Agents)

每个模块独立运行，都有独立的benchmark，没有端到端交互体验，端到端的体验靠编排系统

## Turn-based voice models system

GPT-4o (Advanced Voice Mode)
Mini-Omni2, AudioPaLM, AudioLM, SpeechGPT, (Valle?)

依赖的工具 (Meta-EnCodec, Google-SoundStream) RVQ
多模态Continue pretrain + 后训练（SFT+RLHF）
也依赖VAD做打断和静音检测

评测：VoiceBench

### 离散化



## Full-duplex system

GPT-Live, Gemini iLive, Moshi(Hibiki 同声传译)
