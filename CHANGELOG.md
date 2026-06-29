# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-06-29

### Added
- 音频系统重做
- 朗读音色自动优选（Google US English / Samantha / Microsoft David 等）
- 语音预加载与音色选择器
- 对错音效反馈（Web Audio API 生成）
- 设置面板：自动朗读开关、语速调节、音效开关、音色选择
- 首页设置入口（齿轮按钮）

### Changed
- 默认朗读语速从 0.8 调整为 0.7，更适合儿童
- `speak()` 优先使用优选的英文语音

## [0.1.0] - 2026-06-29

### Added
- 从 `word-challenge` 仓库独立出来，建立 `phonics-kids` 项目
- 迁移自然拼读应用 `index.html`
- 添加 `README.md` 项目说明
- 添加 `docs/conversation-log.md` 项目对话日志
- Level 1 真实数据：8 个 Unit，26 个字母发音、keyword 和例词
- 4 种学习模式：学习模式、听音辨音、拼读练习、听音写词
