# V0.26 小游戏规则与开源研究

核查时间：2026-10-19。实现归属：`src/v2/minigames/engine.ts`；逻辑验证：`tests/v26-minigames.test.ts`。本文件记录实际打开的上游仓库、代码和许可证，不以记忆代替规则核查。所有小游戏是独立休闲内容，没有金币、物品、体力、时间或剧情奖励接口。

## 查阅的一手来源

| 项目与固定版本 | 实际查阅文件 | 许可证 | 采纳的设计依据 |
| --- | --- | --- | --- |
| [Gabriele Cirulli / 2048](https://github.com/gabrielecirulli/2048/tree/478b6ec346e3787f589e4af751378d06ded4cbbc) | [game_manager.js](https://github.com/gabrielecirulli/2048/blob/478b6ec346e3787f589e4af751378d06ded4cbbc/js/game_manager.js)、[LICENSE.txt](https://github.com/gabrielecirulli/2048/blob/478b6ec346e3787f589e4af751378d06ded4cbbc/LICENSE.txt) | MIT，Copyright 2014 Gabriele Cirulli | 初始两块；新块90%为2、10%为4；同一轮每块只能参与一次合并；加上合并后数值作为得分；仅有效移动后出块；2048达成后可明确选择继续；无空格且无相邻相同数字才结束。 |
| [Emrys Muhammad / snake-game](https://github.com/Emrysmuhammad/snake-game/tree/ab34ad21bbabcd4bcd762aec631e40f86a9842dc) | [README](https://github.com/Emrysmuhammad/snake-game/blob/ab34ad21bbabcd4bcd762aec631e40f86a9842dc/README.md)、[snake.js](https://github.com/Emrysmuhammad/snake-game/blob/ab34ad21bbabcd4bcd762aec631e40f86a9842dc/js/snake.js)、[food.js](https://github.com/Emrysmuhammad/snake-game/blob/ab34ad21bbabcd4bcd762aec631e40f86a9842dc/js/food.js)、[LICENSE](https://github.com/Emrysmuhammad/snake-game/blob/ab34ad21bbabcd4bcd762aec631e40f86a9842dc/LICENSE) | MIT，Copyright 2026 Emrys Muhammad | 以已完成移动方向判断反向输入；空格候选集合避免满盘时无限重试；允许进入本轮释放的尾格；撞墙/撞身结束；食物加10分；满盘获胜。 |
| [Rob McGuire-Dale / sudoku.js](https://github.com/robatron/sudoku.js/tree/4362a13510925f03a2f749b4657a8e4c5f36a869) | [sudoku.js](https://github.com/robatron/sudoku.js/blob/4362a13510925f03a2f749b4657a8e4c5f36a869/sudoku.js)、[README](https://github.com/robatron/sudoku.js/blob/4362a13510925f03a2f749b4657a8e4c5f36a869/README.md)、[LICENSE](https://github.com/robatron/sudoku.js/blob/4362a13510925f03a2f749b4657a8e4c5f36a869/LICENSE) | MIT，Copyright 2014 Rob McGuire-Dale | 行/列/宫单位与候选数约束、先处理候选数再求解，以及题目唯一性的必要性。其按给定数数量命名难度没有直接沿用：上游44个给定数被称为hard，而本项目通过求解技巧验证简单度。 |
| [Lucky Fox Design / sudoku-generator](https://github.com/luckyfoxdesign/sudoku-generator/tree/e4e43f9024fe8212d6407f177587054a876484ce) | [README](https://github.com/luckyfoxdesign/sudoku-generator/blob/e4e43f9024fe8212d6407f177587054a876484ce/README.md)、[LICENSE](https://github.com/luckyfoxdesign/sudoku-generator/blob/e4e43f9024fe8212d6407f177587054a876484ce/LICENSE) | MIT，Copyright 2026 Lucky Fox Design | 用实际求解技巧定义难度；简单题应可只靠裸单数（某格仅剩一个候选数）解完。只查阅说明与许可证，未声称审计其生成器代码。 |

上述SHA通过GitHub公开API核对，是本次查阅时对应分支最新提交。上游依赖、媒体、CSS、文案与题库均未下载并集成到运行包；运行时不请求这些网站。

## 实际实现与来源边界

- **2048**：独立TypeScript实现，使用按方向排列的四条索引线和一次消费相邻输入对。没有移植上游`GameManager`、`Grid`、`Tile`类。输出每个旧块的from/to/value/merged供界面动画使用。总分、最高分、移动次数、胜利后继续状态与盘面可序列化。
- **贪吃蛇**：独立不可变状态函数，16×16、初始4格、180ms固定节奏（计时由UI负责）。每次step只接纳一个方向，UI须限定每tick最多一个有效排队转向。吃到立即增长，尾格仅在不增长时释放；死亡保留最后合法盘面。采纳上游的空格枚举策略，使用整数格索引Set进行本地实现，无上游源码段落复制。
- **数独**：没有使用第三方题目数据。先用`(row * 3 + floor(row / 3) + column) % 9 + 1`构造合法完成盘；使用种子260619的本地LCG打乱移除顺序，只保留可裸单数解完的移除。最终六个掩码各有44、45、46、47、48、49个给定数。新题随机置换数字、宫带/宫栈、带内行/栈内列，并可转置；这些变换保留规则与解的个数。题目模板和全部逻辑是本项目新增代码。
- **数独交互**：固定题目数字不可改；笔记只适用于空格；正式填数清除同行列宫的相同笔记，撤销同时恢复盘面与笔记。提示先排除错误输入，再选择实际候选数唯一的格子；有隐藏单数分支可返回对应行/列/宫。完成只增加一次本局完成计数，撤销重填不重复计数。提示次数不能被撤销抹去。
- **存档**：聚合初始状态固定，便于普通开局与回归检查；玩家明确重开时各小游戏使用新随机数。所有状态仅包含JSON数据。解码对非法子盘局部恢复，保留正常兄弟小游戏与有效最高分；蛇恢复为等待开始。数独模板解答使用最多32项缓存，读取存档不跑回溯求解器。

这里的“独立实现”仅表示没有复制/改写上游源码文本或随包分发上游资产，不表示游戏规则由本项目首创。上游作者与MIT许可证链接保留在本研究记录中；将来若实际复制其源码，必须同时随分发内容保留对应完整版权与许可声明。

## 已完成验证

执行：`node node_modules/tsx/dist/cli.mjs --test tests/v26-minigames.test.ts`，15项通过。

- 蛇：显式开始、禁止反向、合法尾格移动、撞墙与撞身、立即增长、仅自由格出食物、满盘终止、终局不再推进。
- 2048：四方向、同轮不连锁合并、动画来源、90/10临界值、两块初始、无效移动零随机消耗、得分与最高分、2048后显式继续、无合法移动结束。
- 数独：全部6个模板及48个随机变换，通过独立位掩码回溯计数器证实恰有1解；另证实完整裸单数路径。验证固定格、笔记清理、冲突、擦除、撤销、错误输入修复、候选解释和只计一次完成。
- 存档：确定性初始化、JSON往返、恢复不自动开蛇、无共享数组引用、损坏数据局部恢复。

纯逻辑测试不代替界面、键鼠、暂停、实际动画、集成存读档与发布验证；这些由本轮根代理及界面代理统一执行。
