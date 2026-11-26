# 第三方许可 · Third-party licences

Paristay 的“自然语音包”（可选下载，按引擎分两个：学法语、英语的下 Supertonic，学中文的下 Melo）用到下面这些东西。

## Supertonic 3（法语、英语合成语音）

- 作者：Supertone Inc.。原始模型：https://huggingface.co/Supertone/supertonic-3/tree/3cadd1ee6394adea1bd021217a0e650ede09a323
- Paristay 用的是 MulTape 做的 int8 版本（四个 `.onnx` 模型的大权重存成 int8，计算不变；`tts.json`、`unicode_indexer.json`、`voice_styles/` 没改），从 MulTape 的网站下载：`https://aarynyan-cell.github.io/OoFR/voices/supertonic-3-int8/`。设置里的女声 / 男声：法语 F3、M4，英语 F2、M5——MulTape 用 Whisper 听写挑出的听错最少的几个；镇上不同的人还会用到同一测试里也听得清的几个预设（清单见 `voice.js` 的 POOLS）。模型不会读中文。

## MeloTTS（中文合成语音）

- 作者：MyShell.ai（https://github.com/myshell-ai/MeloTTS）。许可：**MIT**，全文见 `melotts/LICENSE`，说明见 `melotts/NOTICE.md`。
- 用的是 sherpa-onnx 项目转成 ONNX 的中英模型 `csukuangfj/vits-melo-tts-zh_en`（固定版本 `a0d5c6a264c0ef92d70d8661d8cc502d79627cd6`，和 MulTape 一样，从 Hugging Face 下载，Paristay 不改它）：手机、平板 `model.int8.onnx`（53.5 MB），电脑 `model.onnx`（170.4 MB），加上 `tokens.txt`、`lexicon.txt`（6.8 MB 的词表，管多音字）。sherpa-onnx 的许可：**Apache-2.0**，见 `sherpa-onnx/`。
- 只有一个声音（女声）。中文的拼音、变调、数字读法是 MulTape 自己写的代码，移植进了 `voice.worker.js`。
- 许可：**BigScience OpenRAIL-M**，全文见 `supertonic-3/LICENSE`，说明见 `supertonic-3/NOTICE.md`。
- 这份许可带有**使用限制**（第 5 段和附件 A），对这份副本和每一个使用它的人都有效，转发时也要把它和这些限制一起交给对方。其中一条：**用模型生成的内容不能当作人做的来呈现**（附件 A (e)）。所以游戏里凡是用这个声音读的地方都标明“AI 合成”，并附上这份许可的链接。
- 许可证还禁止用它冒充真人、生成违法或伤害他人的内容等，详见附件 A。

## ONNX Runtime Web 1.30.0（在浏览器里运行模型）

- 作者：Microsoft Corporation。许可：**MIT**，全文见 `onnxruntime-web/LICENSE`。
- 文件在 `vendor/ort/`（见那里的 README）。它的 WebAssembly（约 14 MB）不是打开页面就下载，而是和语音包一起下载、存进浏览器。

## 离线词典的数据（用的时候从 MulTape 网站取，不在 Paristay 里）

`multape.js` 查词、分词、拼音、变位、语法点、查词联想用的是 MulTape 公开网站上的数据：`https://aarynyan-cell.github.io/OoFR/dictionary/`。来源和许可（MulTape 的 `THIRD_PARTY_NOTICES.md`、`dictionary/*-manifest.json`）：

- 法语：Wiktionary（经 Kaikki.org / wiktextract，CC BY-SA 4.0 / GFDL）、FreeDict（CC BY-SA 3.0）、Morphalou / LEFFF（LGPL-LR）；中文释义由 AI 依据英文释义写成。
- 英语：Open English WordNet 2025（CC BY 4.0）、ECDICT（skywind3000，MIT；中文释义和词形变化）；常用词的中文释义由 AI 写成。
- 中文：CC-CEDICT（MDBG，CC BY-SA 4.0；拼音、英文释义）、CFDICT（Chine Informations，CC BY-SA；法文释义）。
- 语法点（法、英、中各一百多个，中英法三种说明）：MulTape 写的。

测试用的 `tests/fixtures/assets.json` 是这些文件的一小部分（只留测试碰到的键），许可同上。

---

Paristay's optional natural-voice packs use Supertonic 3 for French and English (Supertone Inc., BigScience OpenRAIL-M — the licence and its use-based restrictions, paragraph 5 and Attachment A, travel with every copy; synthetic speech must not be presented as human: Paristay labels it “AI 合成”), MeloTTS for Chinese (MyShell.ai, MIT; ONNX conversion by sherpa-onnx, Apache-2.0, downloaded unchanged from Hugging Face) and ONNX Runtime Web 1.30.0 (Microsoft, MIT). Dictionary data is fetched at run time from MulTape's public site: Wiktionary/Kaikki (CC BY-SA), FreeDict (CC BY-SA 3.0), Morphalou/LEFFF (LGPL-LR), Open English WordNet (CC BY 4.0), ECDICT (MIT), CC-CEDICT (CC BY-SA 4.0), CFDICT (CC BY-SA).
