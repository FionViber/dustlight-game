# 第三方内容与来源 · V2

## 程序依赖

- **React / React DOM**：Copyright Meta Platforms, Inc. and affiliates，MIT License。完整声明见 `licenses/React-LICENSE.txt`、`licenses/React-DOM-LICENSE.txt`。
- **Lucide**：ISC License，含适用的上游Feather图标声明，见 `licenses/Lucide-LICENSE.txt`。旧版实现和锁定依赖仍保留该库；当前V2的主要游戏图标使用新生成素材。
- TypeScript、Vite等开发工具的具体版本和许可证随 `package-lock.json` 及各依赖包保存。运行预构建游戏不需要安装开发依赖。

## 字体、鼠标与生成美术

`public/fonts/western.ttf`及游戏鼠标来源于用户明确允许使用的字体、`CUR.png`。它们是项目随包资源，并非调用操作系统字体。其他参考图仅用于选择少量风格参考，未直接作为成品素材使用；原始参考目录保持只读。

场景、立绘、物品、按钮及界面装饰通过本次获准的内置图像工具生成。未指定或验证底层模型版本，不能将其标为已锁定“GPT Image 2”。原始PNG及修订归档在 `public/art/v2/`、`art-sources/v2/`，WebP衍生文件在 `public/art/optimized/`；转换来源、哈希和尺寸见 `art-sources/optimization-report.json`。提示词和生成过程另见项目美术记录。

用户提供资产的商业发行许可仍需随正式发行资料确认；当前文档不替字体或鼠标补写未提供的授权条款。

## 图书原文

三部英文电子书来自Project Gutenberg，正文之外的来源、制作人员和许可证也完整保存在本地TXT中，阅读器有原始文件入口：

| 作品 | 电子版 |
| --- | --- |
| Mark Twain — Adventures of Huckleberry Finn | [Project Gutenberg #76](https://www.gutenberg.org/ebooks/76) |
| Henry David Thoreau — Walden，附Civil Disobedience | [Project Gutenberg #205](https://www.gutenberg.org/ebooks/205) |
| Frederick Douglass — Narrative of the Life of Frederick Douglass | [Project Gutenberg #23](https://www.gutenberg.org/ebooks/23) |

来源页标注这些版本为美国公版。该标注不等于对所有地区、所有后制版本或整个游戏的统一授权。详细版次、制作人员、下载链接与本地哈希见 [BOOK_SOURCES.md](BOOK_SOURCES.md)。当前没有引用中文译本。

## 报道与声音

远方新闻依据美国国会图书馆数字化报刊核实，采用简短转述；地方告示和虚构报纸名称为本项目创作。出处、刊期和价格样本见 [报刊与公告板设计.md](报刊与公告板设计.md)。没有将真实报纸扫描图作为游戏美术。

交互音效与风声由Web Audio本地合成。三首BGM由用户提供；独立影音馆的两部历史影片及三首录音来源、年份和对应版本权利核查见 `art-sources/v21/media/README.md` 与运行包 `media/CREDITS.txt`。影片和音乐从本游戏静态资源加载，不向资料来源站请求播放文件。

## 小游戏规则参考

贪吃蛇、2048与初级数独采用本项目独立实现及新生成美术。规则与交互参考 [Gabriele Cirulli / 2048](https://github.com/gabrielecirulli/2048)、[Emrys Muhammad / snake-game](https://github.com/Emrysmuhammad/snake-game)、[Rob McGuire-Dale / sudoku.js](https://github.com/robatron/sudoku.js) 与 [Lucky Fox Design / sudoku-generator](https://github.com/luckyfoxdesign/sudoku-generator)。这些上游项目均为MIT许可；本发行包没有移植其源码、网页样式或题库。固定版本、许可链接及实际实现边界见 `art-sources/v26/MINIGAME_RESEARCH.md`。

## 连续人物动作参考

Amos 的双骨骼逆运动学与接地处理参考并改编了 [sprite-maker](https://github.com/JohnKinyanjui/sprite-maker)（commit `9de73a6136a1a045af2e8769349fbadc17dbef69`）的相关思路。MIT 完整声明见 `licenses/sprite-maker-MIT.txt`。人物部件图为本项目生成；未运行其完整 Rust/MCP 制作流程。
