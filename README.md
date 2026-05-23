# VITS-VI vs. F5-TTS Side-by-Side Audio Demos

This repository showcases side-by-side audio quality comparisons between ground truth recordings, our VITS-VI synthesis, and F5-TTS baseline synthesis.

## Demo Sentences & Transcripts

Below are the 5 selected sentences from `test_list.tsv` (Speaker_10, FOSD dataset). For each sentence, we provide:
1. **GT**: Ground Truth original human recording.
2. **VITS**: Synthesized by our VITS-VI model.
3. **F5TTS**: Synthesized by F5-TTS-Vietnamese-ViVoice baseline.

| # | Transcript | GT WAV File | VITS-VI WAV File | F5-TTS WAV File |
|---|------------|-------------|------------------|-----------------|
| 01 | **tôi xin một tách cà phê** | [01_FPTOpenSpeechData_Set001_V0.1_014093_GT.wav](01_FPTOpenSpeechData_Set001_V0.1_014093_GT.wav) | [01_FPTOpenSpeechData_Set001_V0.1_014093_VITS.wav](01_FPTOpenSpeechData_Set001_V0.1_014093_VITS.wav) | [01_FPTOpenSpeechData_Set001_V0.1_014093_F5TTS.wav](01_FPTOpenSpeechData_Set001_V0.1_014093_F5TTS.wav) |
| 02 | **tôi có thể tìm bảng tin ở đâu** | [02_FPTOpenSpeechData_Set001_V0.1_000128_GT.wav](02_FPTOpenSpeechData_Set001_V0.1_000128_GT.wav) | [02_FPTOpenSpeechData_Set001_V0.1_000128_VITS.wav](02_FPTOpenSpeechData_Set001_V0.1_000128_VITS.wav) | [02_FPTOpenSpeechData_Set001_V0.1_000128_F5TTS.wav](02_FPTOpenSpeechData_Set001_V0.1_000128_F5TTS.wav) |
| 03 | **cảm ơn rất nhiều tôi đã có một chuyến bay tốt đẹp** | [03_FPTOpenSpeechData_Set001_V0.1_007201_GT.wav](03_FPTOpenSpeechData_Set001_V0.1_007201_GT.wav) | [03_FPTOpenSpeechData_Set001_V0.1_007201_VITS.wav](03_FPTOpenSpeechData_Set001_V0.1_007201_VITS.wav) | [03_FPTOpenSpeechData_Set001_V0.1_007201_F5TTS.wav](03_FPTOpenSpeechData_Set001_V0.1_007201_F5TTS.wav) |
| 04 | **xin vui lòng uống thuốc này khi anh cảm thấy đau rất nhiều** | [04_FPTOpenSpeechData_Set001_V0.1_011755_GT.wav](04_FPTOpenSpeechData_Set001_V0.1_011755_GT.wav) | [04_FPTOpenSpeechData_Set001_V0.1_011755_VITS.wav](04_FPTOpenSpeechData_Set001_V0.1_011755_VITS.wav) | [04_FPTOpenSpeechData_Set001_V0.1_011755_F5TTS.wav](04_FPTOpenSpeechData_Set001_V0.1_011755_F5TTS.wav) |
| 05 | **anh phải gọi cho tôi trước tiên trước khi anh đến đây lần sau** | [05_FPTOpenSpeechData_Set001_V0.1_002985_GT.wav](05_FPTOpenSpeechData_Set001_V0.1_002985_GT.wav) | [05_FPTOpenSpeechData_Set001_V0.1_002985_VITS.wav](05_FPTOpenSpeechData_Set001_V0.1_002985_VITS.wav) | [05_FPTOpenSpeechData_Set001_V0.1_002985_F5TTS.wav](05_FPTOpenSpeechData_Set001_V0.1_002985_F5TTS.wav) |

## System Descriptions

* **VITS-VI (Our System)**: Vietnamese VITS TTS model adapted and trained on a subset of FOSD Speaker_10 containing 2,685 utterances (~4 hours of clean speech).
* **F5-TTS-Vi**: The baseline F5-TTS-Vietnamese-ViVoice model (trained on approximately 1,000 hours of multi-speaker Vietnamese speech, fine-tuned/zero-shot inferred for this speaker context).

## VITS-VI v2 Samples

We have also generated speech samples using the fine-tuned **VITS-VI v2** model (`checkpoint_final.pth` at step 115,000). You can find the audio files and transcripts in the [output_v2/](output_v2) directory.

See [output_v2/README.md](output_v2/README.md) for more details.

## MOS Survey

A blind, randomized Mean Opinion Score survey is available at:
**https://nguyen220905.github.io/tts-audio-oke/survey/**

If you are a native Vietnamese speaker, please consider participating (takes ~15-20 minutes, requires headphones). Results contribute to academic research on Vietnamese text-to-speech.

System details and survey methodology described in the main paper: [nguyen220905/project_tts](https://github.com/nguyen220905/project_tts).

## Links & Licensing

* **Main Repository**: [nguyen220905/project_tts](https://github.com/nguyen220905/project_tts)
* **License**: Audio files generated/derived from the F5-TTS baseline are subject to the **CC-BY-NC-SA-4.0** license, in accordance with the F5-TTS-Vietnamese-ViVoice project terms.
