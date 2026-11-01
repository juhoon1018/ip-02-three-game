# 像素猎手 · PIXEL HUNTER 3D

《互动编程》课程 · 作业二（互动艺术与电子媒介）作品
作者：郑可滢 · 技术栈：Three.js（WebGL）· 纯前端 3D 小游戏

一个俯视角竞技场的 **3D Roguelike 生存射击游戏**。打开网址即可玩：用 WASD 移动、鼠标瞄准射击、空格冲刺，撑过一波波敌人，击杀掉经验宝石升级强化。

## 玩法 / 操作

| 操作 | 功能 |
|---|---|
| **WASD / 方向键** | 移动 |
| **鼠标** | 瞄准（射线投射到地面） |
| **左键** | 射击 |
| **空格** | 冲刺闪避（短暂无敌） |
| **右键拖拽** | 旋转视角（轨道控制） |
| **滚轮** | 缩放 |
| **P / Esc** | 暂停 |
| **1 / 2 / 3** | 升级时选择强化 |

击杀敌人掉落经验宝石 → 升级 → 从 3 张强化卡选 1 张（力量 / 速射 / 散射 / 疾行 / 体质 / 穿透 / 影步 / 磁力 / 高速弹 / 急救 / 弹匣）。
游戏规则：有开始（标题页）→ 实时计分 / 连击 / 波次 → 失败（游戏结束）→ 可重开一局。

## 技术说明

| 项目 | 实现 |
|---|---|
| 渲染 | Three.js（`WebGLRenderer`），场景含雾、网格地面、竞技场边界 |
| 3D 物体与材质 | 玩家（锥体+头+枪）、4 类敌人（球/二十面体/盒，各带 `MeshStandardMaterial` 自发光）、子弹、经验宝石（八面体）、粒子（盒） |
| 光照 | 环境光 + 平行光 + 跟随玩家的点光源 |
| 相机 | `OrbitControls` 轨道控制（右键拖拽旋转、滚轮缩放），并自动跟随玩家 |
| 游戏循环 | `requestAnimationFrame` + 固定步长 `dt` 更新（帧率稳定 ≥30fps） |
| 音效 | Web Audio API 即时合成（无音频文件） |
| 交互 | 鼠标射线拾取地面求瞄准方向、键盘移动、点击/数字键升级、暂停 |
| 依赖 | 本地 `libs/three.module.js`，**离线可用**，无需联网 |

## 目录结构

```
ip-02-three-game/
├── index.html                 # 游戏主文件（Three.js 场景 + 玩法）
├── libs/
│   ├── three.module.js        # Three.js 本地副本（离线运行）
│   └── jsm/controls/OrbitControls.js
└── README.md
```

## 本地预览（必须用本地服务器）

本作使用 ES Module + importmap，**不能直接双击 `index.html` 打开**（浏览器会拦截模块加载），需起一个本地服务器：

```bash
python -m http.server 8001
# 浏览器访问 http://localhost:8001
```

## 提交到 GitHub + 开启 Pages

1. 在 GitHub 新建**公开**仓库，命名为 **`ip-02-three-game`**。
2. 在本目录执行：

```bash
git remote add origin https://github.com/<你的用户名>/ip-02-three-game.git
git branch -M main
git add .
git commit -m "作业二：像素猎手 PIXEL HUNTER 3D (Three.js)"
git push -u origin main
```

3. 仓库 **Settings → Pages** → Source 选 `main` 分支、`/ (root)` → 保存。
4. 几分钟后访问 `https://<用户名>.github.io/ip-02-three-game/` 即可在线游玩。

## 录屏要求（作业通用）

录制 `学号_姓名_作业2.mp4`（mp4 / H.264，≥1280×720），流程包含：
1. 打开项目目录
2. 打开 `index.html`（或 GitHub Pages 链接）
3. 本地运行游戏
4. 完整玩一局（移动 / 射击 / 升级 / 撑过几波 / 失败重开）
5. 展示仓库提交记录（GitHub 仓库页或 `git log`）

## 创作说明

以「在发光网格竞技场中独自对抗无尽敌潮」为核心意象：用冷色调网格地面 + 暖色自发光敌人形成对比，强化「猎手 vs 兽群」的紧张感。4 类敌人对应不同形状与行为（史莱姆追击、蝙蝠蛇形游走、射手远程、坦克高血），配合升级卡牌构成 Roguelike 循环。技术上全程用 Three.js 原生 API 搭建，未引入游戏框架，便于老师查看场景/物体/逻辑分块。
