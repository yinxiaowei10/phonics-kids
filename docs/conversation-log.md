# Phonics-Kids 项目对话日志

**项目**: 自然拼读小课堂（Phonics Kids）  
**本地路径**: `/Users/yinyin/projects/phonics-kids/`  
**GitHub 仓库**: `https://github.com/yinxiaowei10/phonics-kids`  
**起始日期**: 2026-06-29

---

## 2026-06-29 | 项目定位确认

### 用户需求（原文整理）

用户明确 phonics 自然拼读项目要作为**独立产品项目**运营，不再放在 `word-challenge` 下面：

> "首先，这个项目我是想做成一个独立的项目，之后能够产品化的，所以你不要放到 Work Challenge 下面，要把它作为一个独立的项目来运营。"

要求用**行业视角**和相关 skill 对项目进行全面 QA：

> "然后，你现在用行业视角还有相关 skill 来 QA 这个项目，针对它目前的所有功能、使用流程，还有音频朗读等等进行测试。"

要求对儿童学习的动画和风格进行全面优化：

> "此外，针对适合孩子学习的动画和风格，你全部都要进行一下优化。"

明确工作步骤：

> "你的工作步骤如下：1. 先去分析 2. 给自己定计划 3. 逐步进行优化"

版本管理要求：

> "另外，每一次优化都要做版本管理，要 push 到 Git 上面。"

对话日志要求：

> "另外，你先把我们刚刚这个'自然拼读'项目的所有的上下文，包括我跟你说的内容，以及你给我的结果分析过程，全部一字不漏地整理成一个对话日志，先把它沉淀下来。后面每做一次修改，你都要增加到那个对话日志里面。项目日志一定要记清楚。"

### 项目名确认

- **GitHub 仓库名**: `phonics-kids`
- **本地路径**: `/Users/yinyin/projects/phonics-kids/`
- **中文名**: 自然拼读小课堂

用户确认：

> "可以啊，你先建立这个仓库，把这个项目建立起来并迁移，作为一个独立项目做好版本管理。先把它弄好，然后再一步一步地去优化。记得每一次修改都要 commit，然后 push 到 Git。"

---

## 2026-06-29 | QA 分析结论

### 项目来源

原文件位于 `/Users/yinyin/projects/word-challenge/phonics.html`，是 word-challenge 仓库中的一个自然拼读扩展页面。已先完成 Level 1 真实数据填充（来自 Oxford Phonics World Level 1 学生用书目录）。

### 当前功能清单

1. **首页**：选择 Level 1-5
2. **单元页**：选择 Unit
3. **模式页**：4 种学习模式
4. **学习模式**：展示字母/组合 + 发音 + keyword + 例词朗读
5. **听音辨音**：播放发音，4 选 1
6. **拼读练习**：展示单词 + 字母拆分
7. **听音写词**：听发音输入单词
8. **进度条**：显示当前进度
9. **面包屑导航**：首页 / 单元 / 模式

### QA 问题汇总

#### 功能流程问题

| 模块 | 状态 | 问题 |
|------|------|------|
| 学习模式 | ⚠️ 可用 | `getPreferredVoice()` 写了但未被 `speak()` 调用，朗读质量依赖系统默认语音 |
| 听音辨音 | ⚠️ 可用 | 选项池仅限当前 Unit 的 phonemes；答对/答错后没有庆祝动画 |
| 拼读练习 | ❌ 逻辑错误 | 使用 `word.split("").join("-")` 按字母拆分，没有真正教拼读。例如 `fox` 拆成 `f-o-x`，但 x 的发音是 /ks/，孩子学到的不是 phoneme 组合 |
| 听音写词 | ⚠️ 可用 | 从整个 Unit 的 words 中随机抽词，可能抽到非当前 phoneme 的单词，难度失控 |
| 完成提示 | ❌ | 使用 `alert()`，打断儿童操作流 |
| 键盘支持 | ❌ | 无键盘快捷键 |
| 进度保存 | ❌ | 无 localStorage |
| 级别锁定 | ❌ | CSS 有 `.locked` 类但逻辑未实现 |

#### 音频朗读问题

- `getPreferredVoice()` 函数未接入 `speak()`
- 未预加载语音，首次朗读可能失败或延迟
- 无对错音效反馈
- 语速固定 0.8，对儿童无调节入口
- 无自动朗读开关
- 无音频降级方案

#### 儿童体验 / 视觉问题

- 界面干净但偏成人化
- 缺少 mascot / 角色陪伴
- 缺少星星、奖杯、连击等正向激励
- 缺少答对庆祝动画（confetti、弹跳、闪光）
- 缺少声音可视化（朗读时按钮无波纹）
- 配色（紫色为主）可以更具童趣
- 卡片动效偏简单

#### 产品化问题

- 单文件架构，后续难扩展
- 和 word-challenge 同仓库，不符合独立产品定位
- 无 README / 品牌说明
- 无 PWA / 离线能力
- 无版本号 / CHANGELOG
- 无用户引导 / onboarding

### 行业对标观察

参考 Duolingo、ABCmouse、Khan Kids 等儿童学习应用：

- 有 mascot 全程陪伴和情绪反馈
- 即时正向反馈（星星、音效、动画）
- 课程短、可完成、有成就感
- 高质音频 + 可视化提示
- 离线可用、启动快
- 进度可保存、有连续学习激励

---

## 2026-06-29 | 分版本优化计划

| 版本 | 目标 | 关键改动 |
|------|------|---------|
| **v0.1.0** | 独立项目搭建 | 新建 `phonics-kids` 仓库，迁移 `phonics.html`，建立 README、CHANGELOG、版本管理、对话日志 |
| **v0.2.0** | 音频系统重做 | 接入 preferred voice、语音预加载、对错音效、语速设置、自动朗读开关 |
| **v0.3.0** | 核心逻辑修复 | 修复拼读练习拆分逻辑、听音写词题目范围、替换 alert、加键盘支持 |
| **v0.4.0** | 儿童视觉升级 | mascot 角色、童趣配色、卡片动效、声音波纹、答题反馈动画 |
| **v0.5.0** | 激励与进度系统 | 星星、奖杯、连击、完成庆祝、localStorage 进度保存 |
| **v0.6.0** | PWA 化 | manifest、service worker、离线可用、应用图标 |
| **v0.7.0+** | 内容扩展 | Level 2-5 真实数据填充 |

---

## 2026-06-29 | v0.1.0 执行记录

### 已完成

- [x] 创建 GitHub 仓库 `https://github.com/yinxiaowei10/phonics-kids`
- [x] 初始化本地项目 `/Users/yinyin/projects/phonics-kids/`
- [x] 将 `/Users/yinyin/projects/word-challenge/phonics.html` 迁移为 `/Users/yinyin/projects/phonics-kids/index.html`
- [x] 编写 `README.md`
- [x] 编写 `CHANGELOG.md`
- [x] 初始化 Git 并 push v0.1.0

### 提交信息

```
feat: v0.1.0 独立项目搭建

- 从 word-challenge 迁移 phonics.html 为 index.html
- 添加 README.md 和 CHANGELOG.md
- 添加 docs/conversation-log.md 项目日志
- Level 1 保留牛津自然拼读真实数据
```

### 项目结构

```
phonics-kids/
├── index.html              # 主应用
├── README.md               # 项目说明
├── CHANGELOG.md            # 版本日志
└── docs/
    └── conversation-log.md # 项目对话日志
```

---

## 待执行

- [ ] v0.2.0 音频系统重做
- [ ] v0.3.0 核心逻辑修复
- [ ] v0.4.0 儿童视觉升级
- [ ] v0.5.0 激励与进度系统
- [ ] v0.6.0 PWA 化
- [ ] v0.7.0+ Level 2-5 内容扩展

---

*本日志会在每次修改后追加记录。*
