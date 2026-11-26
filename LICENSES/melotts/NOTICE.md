# MeloTTS (Chinese natural voice), as used by Paristay

- Model: MeloTTS, https://github.com/myshell-ai/MeloTTS, Copyright (c) 2024 MyShell.ai, MIT licence (`LICENSE` here).
- Converted copy: `csukuangfj/vits-melo-tts-zh_en` on Hugging Face, converted to ONNX by the sherpa-onnx project
  (https://github.com/k2-fsa/sherpa-onnx, Apache License 2.0, `../sherpa-onnx/LICENSE`), fixed at revision
  `a0d5c6a264c0ef92d70d8661d8cc502d79627cd6` — the same files and revision MulTape uses (`v2/src/speech/piper/voices.ts`).
- Files Paristay downloads (only when a learner of Chinese asks for the natural voice; nothing is bundled):
  - phones and tablets: `model.int8.onnx` (53,517,430 bytes); computers: `model.onnx` (170,429,550 bytes)
  - `tokens.txt` (655 bytes): the model's phone ids
  - `lexicon.txt` (6,837,671 bytes): the model's word list (word → phones and tones), used for words without a reading
- Paristay does not change these files. They are checked by size (and `.onnx` by its header byte) before they are kept;
  MulTape has no SHA-256 for them, so neither does Paristay yet.
- One voice (a woman's), 44.1 kHz. The Chinese text front end (pinyin, tone changes, numbers) is MulTape's own code,
  ported into `voice.worker.js`.

Synthetic speech: Paristay labels this voice “AI 合成”.
