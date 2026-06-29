# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0] - 2026-06-29

### Added
- 完成庆祝页面，替代原生的 `alert()`
- "再来一次"功能：完成练习后可立即重玩当前模式
- 全局键盘支持：
  - 学习/拼读模式：空格/回车进入下一步
  - 听音辨音：按 1-4 选择答案
  - 听音写词：回车提交
  - 任意学习页：按 ESC 返回
- 学习模式进入后自动朗读当前 phoneme 和例词
- 听音写词输入框自动聚焦和禁用状态管理

### Fixed
- 修复拼读练习的拆分逻辑：从按字母拆分（`f-o-x`）改为按 phoneme 拆分（`/k/ + at`）
- 修复 v0.2.0 中意外丢失的 `switchScreen()` 函数
- 移除所有 `alert()` 弹窗

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
