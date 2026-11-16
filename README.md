# 2027 高考志愿填报指北

[《2027高考志愿填报指南》](https://jackiezheng.github.io/gaokao-2027-guide/)的姊妹篇。**指南讲方法，指北给资料**：把「高报笔记」全库按原目录完整汇编成一本可检索、可打印的书。

## 交付物

| 文件 | 说明 |
|---|---|
| `index.html` | 网页版，单页内嵌全部样式与封面图，无外部依赖；左侧导航支持逐层级折叠 / 展开，可整体收起 |
| `single.html` | 单页自包含版（`file://` 双击可用、无 fetch 依赖）；**仅本地交付，不发布到 GitHub**（2026-11-08 用户定） |
| `2027高考志愿填报指北_v{版本号}.pdf` | A4 打印版，页眉 / 页脚连续页码，多级书签（专业篇四级）直达篇名所在页与页内位置；文件名带构建版本号（2026-11-15 用户定）；同样仅本地交付 |
| `data/build_manifest.json` | 本次构建清单（篇目顺序、逐篇指纹、目录结构、页数与书签数） |
| `assets/style.css` | 版式：提取自指南 `build_html.py` 的 CSS，替换主色系与页眉文字；封面改全 cqw 等比缩放、正文改两端对齐，末尾追加篇数括注与导航折叠样式 |
| `assets/cover_watercolor.png` | 封面底图：指南水彩封面做「绿 → 靛蓝」色调映射，构图与留白不变 |
| `assets/sponsor.jpg` | 文末赞赏码：网页版 / PDF 以 base64 内联，线上仓库 README 以相对路径引用 |
| `notes_render.py` / `build_notes.py` / `verify.py` | 内容层 / 构建层 / 校验层，对应指南的 `body.py` / `build_html.py` / `verify.py` |
| `publish_pages.py` | 网页版发布脚本：把 `index.html` + `.nojekyll` + 整本书介绍 `README.md` + `assets/sponsor.jpg` 推到独立公开仓库并启用 Pages；PAT 只从环境变量读，不落盘、不进仓库 |
| 在线站点 | <https://jackiezheng.github.io/gaokao-2027-notes/>（仓库 `JackieZheng/gaokao-2027-notes`，public，Pages 源为 main 根目录） |
| `data/smoke.*`、`data/diag*.py`、`data/check_nav.py`、`data/check_align.py`、`data/check_cover.py`、`data/preview_p*.png`、`data/nav_*.png`、`data/cover_*.png` | 小样冒烟、指纹排查、导航交互 / 对齐实测、封面多视口溢出实测与视觉质检的临时产物，可删除 |

## 与《指南》的异同

| 项目 | 指南 | 指北 |
|---|---|---|
| 主体色调 | 墨绿 `#2E7D6B` | **靛蓝藏青 `#1F4E79`**（含浅底 `#EAF1F8`、卡片底 `#F1F5FA`、浅边 `#C6D6E8`、深主色 `#12304A`） |
| 辅助色 | 警示红 `#C0563B`、提示金 `#C98A2B`、信息蓝 `#1F6FB2`、正文墨 `#33414A` | **全部沿用** |
| 版式 | A4、`@page` 页眉页脚、h1/h2/h3、表格、callout、荧光关键词、目录、封面、浮动书签、文末致谢 | **全部沿用** |
| 流程 | 内容层 → 单页 HTML（base64 内嵌） → Chrome/Edge headless 打印 PDF → pymupdf 注入书签 → 校验 | **全部沿用** |
| 内容 | 自撰方法论手册（46 章） | 高报笔记原文汇编（四大篇章 666 篇 + 词条附录） |

> 《指南》文末原有的下载二维码与小程序码属于其自身分发资源，本册不复制，避免指向错误资源；本册文末另放笔者自己的微信赞赏码（`assets/sponsor.jpg`），与《指南》无关。

## 收录与编排口径

- **四大篇章顺序**：专业 → 院校 → 城市 → 攻略；各篇章篇数由构建时扫描得出，不写死。
- **目录按原来的级别编排**：以 `笔记目录索引.md` 的分组和磁盘路径为准，**学科门类与专业大类不合并**：
  - 专业篇：篇章(1) → 学科门类(2) → 专业类(3) → 篇名(4)；
  - 院校篇：篇章(1) → 省级行政区(2) → 篇名(3)；
  - 城市篇 / 攻略篇：篇章(1) → 篇名(2)，按原顺序平铺。
- **原文一字不改**：不做删减、摘要、润色、数据更新；只把标题、段落、表格、列表、加粗、脚注等 Markdown 标记排成书页版式。脚注释义在原文位置原样列出。**每篇笔记的篇名居中**；段落、列表项、表格单元格与提示框一律**两端对齐**（末行仍左对齐，避免短行被拉出稀疏字距），标题、封面、目录、导航、致谢保持各自原有对齐。
- **重点关键词荧光标注**：源笔记里没有荧光标记（《指南》的 504 处是人工挑的），故按篇自动提取**本篇重点 / 关键词**——篇名、原文加粗、小节要点、术语词条、关键数据（分数段 / 比例），泛词、年份与破碎片段由停用词 / 首尾虚字规则剔除。在正文出现处套 `mark.kw`（**亮青蓝荧光笔 + 2px 亮蓝实线下划线**，亮度与《指南》的暖黄荧光相当、冷色系一眼可分，色系跟随本书主色且改回实线），每篇 3–8 个词、最多 11 处（**仅指重点词主规则**），第一轮保证每个词各标一次、第二轮才补标，避免挤在开头。**只给可见文字套标签，一个字不改**，逐篇指纹仍一致；规则写在 `notes_render.py`，笔记增删后重跑构建自动重算，不写死词表。`print-color-adjust: exact` 让 Chrome 打印 PDF 时也保留荧光背景。
- **脚注标注词全部补高亮**（2026-11-07 用户「加标注的词同时要高亮 / 全部补」）：每个词条角标 `<sup class="fn-ref">` 前面的被标注词都要有同款荧光。重点词主规则（每篇 ≤11 处）会漏掉大量脚注词，故在 `notes_render.py` 追加 `highlight_fn_anchors_html()`：前置原文 = 词条名时精确补标；前置为别名 / 近义写法 / 数字（如「碳中和[^双碳]」「人工智能[^AI]」「985高校[^985]」）时按「末尾词组 + 虚词剥离」定位；已高亮、各级标题、上标、行内代码、脚注定义与已有荧光内部一律跳过。补标用 `<mark class="kw fn">` 归入同一荧光类名、可见文字零改写，逐篇 `fn_anchor_marks` 写进清单，全书 6084 个角标前置有荧光率 100%。
- **多义词脚注按语境消歧**（2026-11-08 用户「要结合前后文来判断」）：源笔记里按词条名机械匹配加的脚注，遇到一词多义会挂错释义——例如「轨道交通+冶金+矿业+材料」**三位一体**是组合结构，不是浙江省综合评价招生。`notes_render.py` 的 `drop_misapplied_fn_refs()` 在渲染前按前后文判定：只有上下文命中该词条的专属语义线索（综合评价 / 学业水平 / 学考 / 高考成绩 / 综合素质评价 / 三位一体招生 / 浙江紧邻词组）才保留角标，否则连引用带本篇脚注定义一并移除；被误标的词本身仍是普通正文文字，附录《高报词条》里的词条释义不受影响。判定表 `AMBIGUOUS_FN_CONTEXT` 可扩展，未列入的词条行为完全不变；渲染、关键词提取、字数统计与零改写指纹四处共用同一份清理结果。全书 6 处组合义误标已同时从源 .md 清理干净。
- **右下角「问题反馈」浮动按钮**（2026-11-08）：网页版 `single.html` 与 C 版 `index.html` 共用 `build_notes.py` 的 `FEEDBACK_FAB_HTML`，固定在视口右下角。默认只显示青蓝圆底的白色对话气泡 + 问号（**内联 SVG**，无外部图片、无版权风险、零新增资源、任意尺寸清晰）；悬停或键盘聚焦时按钮向右滑出「问题反馈」四字，并在按钮上方弹出**自定义气泡**（不用浏览器原生 `title`，避免长文案被截断），文案逐字为「如果您发现书中有错误，或者有好的意见/建议，欢迎联系我们。如果链接无法打开，也可以加微信：JackieZhengChina 联系我们反馈。」。`aria-label` + `aria-describedby` 兜底，`prefers-reduced-motion` 下关闭过渡。点击在新标签打开本仓库 issue `https://github.com/JackieZheng/gaokao-2027-notes/issues/1`。样式写在 `assets/style.css`：默认隐藏 + `@media screen` 显示 + `@media print` 强制隐藏，**PDF 完全不受影响**。★ 发布脚本 `publish_pages.py` 的 `PUBLIC_ALLOW` 只精确放行 issue 链接与微信号中的公开 GitHub 用户名，其它脱敏模式照常生效。
- **右上角「全文搜索」**（2026-11-08）：C 版正文分块懒加载，浏览器 `Ctrl+F` 只能搜到已加载片段，故构建时由 `build_c_edition()` 在写 691 个片段的**同一循环**里同源产出 `assets/search-index.js`（每篇锚点 / 篇名 / 可见正文段落，约 9.4MB、Pages gzip 约 2.8MB）；点图标才用 `<script src>` 按需加载，单页版 `file://` 双击打开也不受 `fetch` CORS 限制，两版共用一份索引。图标固定右上角、默认半透明、悬停 / 聚焦完全显示；点击动画展开并居中，**面板展开时图标隐藏、面板收回时图标恢复**（两者不同时存在），点击页面空白 / `Esc` / 关闭按钮 / 点结果均可收回。多个关键词用空格分隔、按 **OR 或关系**（任一词命中即出结果，命中段落多的排前），结果在输入框下方列出，面板 `max-height:80vh` 且滚动条**只加在结果容器**；结果条目 `<a href="#sec-N" data-kw="完整查询串">` 复用 C 版 `go()` 只加载目标片段，等 `data-ready` 后由 `__searchLocate()` 滚到命中段落，并把**每个搜索词都标出来**（长词优先，避免短词先把长词切断；单页版直接定位）。命中词本身就是书里的重点词 / 院校专业名、落在 `mark.kw` / `mark.kw fn` / `mark.ent` 内部时，仍会叠加一层暖黄搜索底色（`mark .search-hit-kw`），原有青蓝荧光与亮蓝实线下划线保留、双色可辨；`clearHits()` 还原后调用 `normalize()` 合并文本节点，反复搜索不会让 DOM 碎片化。上次搜索词存 `localStorage`，再次打开自动回填并重跑，避免书更新后展示过期结果。`@media print` 隐藏面板并还原临时高亮，PDF 不受影响；`publish_pages.py` 已把索引登记进发布清单，漏登记会让线上 404。
- **篇尾结束符（网页 / PDF 统一）**：每篇末尾一枚「———— ☃️ ————」，左右实线由 `flex: 1 1 auto` 自动吃掉剩余宽度、横向铺满，网页连续长页与 A4 打印页共用同一套 CSS；雪人数量由 `build_notes.py` 的 `SNOWMAN_COUNT` 控制（第一版 1 个，以后每版只改这一个数字，全书逐篇自动重算）。结束符放在 `<article>` 内部，打印时随本篇最后一页、不会单独成页；网页版另留约一行半篇间空白，原来单调的 `border-bottom` 已移除。装饰符为 `aria-hidden` 且不计入正文文字，逐篇零改写指纹不受影响。
- **封面与前言**：封面「本书收录什么」卡片、装帧信息与前言总述两段按约定保留；前言署「笔者（雪人老师）日常的文章及笔记，按分类完整汇编」。书中不再出现「原文照排，不作删改」式的编写声明、编排口径说明、免责说明与使用说明。
- **封面文字自动缩放**：沿用《指南》的 `container-type: inline-size`，封面全部字号用 `clamp(2px, X cqw, 原 px 上限)`、padding / margin / 边框 / 阴影同步改 cqw，随容器宽度**等比缩放**；不再用 `clamp(7px, …)` 这类会把字钳住不再缩小的 px 下限。A4 打印（21cm）时数值仍命中原上限、版面不变；手机窄屏不会溢出。九档视口（320–1600px）实测见 `data/check_cover.py`。
- **姊妹篇链接**：网页版封面卡片第 4 条、**前言首段**的《2027高考志愿填报指南》都是真正的 `target="_blank"` 链接，指向 <https://jackiezheng.github.io/gaokao-2027-guide/>（PDF 中也可点击），全书正文里不再出现裸书名。线上仓库 README 的两处书名同样链向该地址；但 **GitHub 会剥离 README 里的 `target="_blank"`**（GFM 与仓库实际页面均已实测），README 内只能同标签跳转，按住 Ctrl/⌘ 点击可自行新开窗口。
- **统计数字全部动态**：封面总篇数、前言总篇数与各分支篇数、篇章 / 门类 / 专业类 / 省份标题后的括注，以及封面第一条「四大篇章共 N 篇高报笔记全文，全书共计约 X 万字，约 N 页；」，均由运行时扫描 / 实测结果生成；笔记增删后重跑构建自动更新，源码里不写死任何统计数字。
- **万字数口径**：统计所有收录笔记原文（含词条附录，附录按剔除开头元说明后的正文）中的**汉字数** `[\u3400-\u9fff]`，不含标点、空白、数字、字母与 Markdown 标记；除以 10000 后保留一位小数。当前值见 `data/build_manifest.json` 的 `total_hanzi` / `wan_text`，产物与清单之外不写固定数字。
- **页数口径**：封面「约 N 页」取**最终 PDF 的实测页数**，不是估算也不写死。构建时先以上次实测页数作初值，打印完成后按本次 PDF 页数回填 HTML 并重打，直到网页版与 PDF 封面写的是同一个实测值（最多 3 次收敛）；结果同时写入清单 `cover_pages` / `pdf_pages`。回填只替换封面页数占位里的数字，不触碰任何正文，逐篇零改写指纹不受影响。
- **附录例外**：根目录《高报词条.md》开头的 3 行凡例式元说明按约定剔除（含「共收录 N 个词条」按模式匹配，词条数变化也能自动剔除），词条正文一字不动；`verify.py` 对附录用同一剔除规则比对指纹（如不需要附录，构建时加 `--no-glossary`）。

## 网页版导航

左侧「指北导航」按目录层级组织（专业篇为 **篇章 → 门类 → 专业类 → 篇名** 四级）：

- 默认只显示一级条目（条数随目录结构变化），点击条目前的 `▸` 逐层展开，再点收起；箭头与同一行标题上下居中对齐（`data/check_align.py` 用浏览器实测中心偏差）；
- 顶部「全部展开 / 全部折叠」一键切换；展开状态记在浏览器本地，刷新后保持；
- 点击条目跳转并自动收起面板；点击面板之外的正文 / 页面空白同样收起面板；`Ctrl/Cmd + B` 或 `Esc` 开关面板；
- 面板导航树最末（「致谢」之后）有「☕ 赞赏作者」固定入口，直达文末赞赏码。本书是 14 MB 单页长文档、末尾区块需约 10 秒才解析进 DOM，若在加载完成前点击（或直接带 `#sponsor` 打开），脚本会在 `DOMContentLoaded` 后自动补滚，避免「点了没反应 / 滚到底却看不到赞赏码」；
- 打印 / 导出 PDF 时面板与按钮整体隐藏，不进入书页；网页版的篇间留白与分隔线同样只在屏幕显示，打印时由 `article.note { page-break-before: always; }` 逐篇另起页。

## 增补笔记后怎么重建

1. 把新 `.md` 放进对应分支目录，沿用原有层级（例：`专业/工学/计算机类/新专业.md`、`院校/江苏/某某大学.md`）。
2. **可选**：同步更新 `笔记目录索引.md`，可指定它出现在目录里的位置；不更新也会被自动收录，只是排在该分组末尾。
3. 重新构建：`python build_notes.py`（默认全量重建 HTML + PDF + 书签 + 清单）。
4. 校验：`python verify.py`。
5. 只想看版式：`python build_notes.py --limit 8`（小样产物写到 `data/`）；改了 HTML 但不想重算内容：`--print-only` 只重打 PDF；打印被超时中断：`--finalize-only` 只补书签与清单。
6. **同步线上站点**：设置环境变量 `GAOKAO_PAGES_PAT`（PowerShell 用 `$env:GAOKAO_PAGES_PAT="..."`，PAT 只进内存、不写文件）→ 执行 `python publish_pages.py`。站点 README 的篇数与万字从新清单自动更新，两处《指南》书名链向指南 Pages；Pages 步骤幂等（已启用时只 GET 确认，重复 POST 创建会返回 404 并把「文件已推送」误判为失败）；`--dry-run` 不联网只核对文件与脱敏，`--fix-history` 用于清理历史里的个人邮箱。★ 发布清单由 `collect()` 动态收集，`LOCAL_ONLY_FILES` 明确排除 `single.html` 与 PDF（仅本地交付）；`verify.py` 第 44 项会实测清单确认 `single.html` 未被列入。

> 全量打印约需 2–3 分钟。若终端命令被会话超时中断，HTML 与 PDF 通常已经生成完毕，此时**不要重跑打印**，直接执行 `--finalize-only` 补做书签与清单即可。

## 环境约定

- 解释器：本机 **Python 3.12**（含 pymupdf 1.24.10、Pillow、playwright 1.63.0）。不要用 WorkBuddy 自带的 3.13 —— `import pymupdf` 在该环境会段错误（指南项目的修改记录里有同样结论）。
- PDF 打印：Chrome / Edge headless `--print-to-pdf`；打印参数 `--print-to-pdf-no-header`，页眉页脚由 CSS `@page` 生成。**输入 HTML 与输出 PDF 都用带时间戳的唯一文件名**（`data/_print_*.html` / `data/_out_*.pdf`），避免 Chrome 复用 `file://` 缓存、或在目标 PDF 已存在时静默不覆盖而输出旧版正文；打印后还会硬校验「命名目标数 ≥ 当前目录结构条数」。
- 书签：不靠字体颜色猜标题，而是用指南同款 **「目录锚点 → PDF 命名目标」** 机制，`resolve_names()` 拿到每个标题的页码与页内 y 坐标，再 `set_toc()` 注入多级大纲（专业篇四级）。
- 笔记库根目录：`notes_render.py` 的 `NOTES_ROOT`，或环境变量 `GAOKAO_NOTES_ROOT`。资料库搬家时只需改这一处。
- 浏览器与依赖均复用本机已有环境（chromium-1243），不需要额外安装。

## 校验口径

`verify.py` 逐项输出 ✅ / ⚠️：

1. **全量收录** —— 笔记库每个 `.md` 都在构建清单里；
2. **目录编排顺序** —— 逐篇与《笔记目录索引》比对；
3. **原文零改写** —— 逐篇比对「源文件文字指纹」与「HTML 可见文字指纹」（附录按元说明行剔除规则）；
4. **HTML 容器 / 锚点闭合 / 主色与页眉**；
5. **编写声明已清除** —— 禁用短语命中检查；
6. **篇数括注挂标题** —— 篇章与分组均为标题内小字，无独立说明段；
7. **导航逐层折叠** —— 可折叠父节点数 = 折叠按钮数，展开 / 折叠工具与默认隐藏规则齐全；
8. **专业目录层级不合并** —— 出现四级篇名，且不存在「门类/专业类」合并式分组标题；
9. **统计数字与清单一致 / 无硬编码** —— 篇章括注、封面与前言篇数与本次扫描清单一致，源码里不写死统计数字；
10. **笔记篇名居中**、**PDF 页数与多级书签页内定位**、**命名目标缺失**；
11. **封面统计动态一致** —— 万字从源文件独立重算汉字数，与封面「全书共计约 X 万字」及构建清单三方比对；「约 N 页」与 PDF 实测页数、清单 `cover_pages` / `pdf_pages` 四方一致，并核对封面句式；源码里不含写死的万字或页数数字；
12. **正文两端对齐** —— `p / li / td / .callout` 为 `justify` 且末行左对齐，篇名居中与目录 / 导航左对齐同时保留；
13. **封面文字等比缩放** —— 封面字号 clamp 下限不钳死、padding / margin 均为 cqw、A4 上限保持不变；
14. **全书指南新窗口链接** —— 封面卡片与前言首段的书名均为 `target="_blank"` / `rel="noopener noreferrer"` 链接且指向指南 Pages，链接外不得再出现裸书名；
15. **文末赞赏码** —— 正文末尾内联的 base64 与 `assets/sponsor.jpg` 逐字节一致，项目 README 与线上仓库 README 末尾均引用该图；区块带 `id="sponsor"`，图片带 `width/height="1152"` 与 `aspect-ratio: 1 / 1`，解码失败也按 1:1 占位、不会塌成零高度；
16. **重点荧光标注** —— 全书 `mark.kw`（含脚注补标 `mark.kw fn`）数与构建清单逐篇 `marks` 一致，691 篇每篇至少 1 处；重点词主规则每篇 ≤11 处，脚注标注词补齐后每篇 ≤120 处（密度另由第 21 项覆盖率把关）；样式为亮青蓝渐变 + `2px solid #1F6FB2` 实线（不得为虚线），且与《指南》的暖黄 / 金色不同（防止被覆盖回同款）（原文零改写由第 3 项指纹校验兜底）；
17. **篇尾雪人结束符** —— 667 篇各 1 枚、每枚雪人数 = `SNOWMAN_COUNT`，实线 `flex: 1 1 auto` 自动铺满，屏幕与打印同源，旧 `border-bottom` 已移除，逐篇分页规则不变；
18. **PDF 篇尾结束符** —— PDF 全文文本检出雪人数 ≥ 篇数 × `SNOWMAN_COUNT`（每篇各 1 枚），页底冗余不超过 3 枚；Chrome 在正文正好占满整页时会把页底结束符重复画到下一页，已用 `page-break-after: avoid` 把正文末块与结束符绑定，装饰留白页从 20 页压到 4 页，冗余数与留白页数写入校验明细。
19. **赞赏快捷入口** —— 浮动导航中的 `bmSponsor` 链接指向 `#sponsor`、必须落在「致谢」条目之后（导航树最末）且文件前 30 万字符内（整棵导航随文档开头即解析完），`DOMContentLoaded` 补滚脚本与入口样式齐备；解决 14 MB 长文档增量解析导致的「文末赞赏码有时看不到」。
20. **面板点击外收起** —— 点击面板之外的正文 / 空白自动收起浮动导航（面板内部、折叠箭头与开关按钮不受影响），脚本片段 `t.closest('#bmPanel') / t.closest('#bmToggle')` 必须齐备。
21. **脚注标注词全高亮** —— 每个 `sup.fn-ref` 前 8 字内必须能找到荧光结束标签（覆盖率 ≥98%，实测 100%）；补标处数与清单 `fn_anchor_marks` 汇总一致，补标不进各级标题、不嵌进已有 mark，可见文字零改写由第 3 项指纹校验兜底。
22. **多义词脚注按语境消歧** —— 「三位一体」在全书 6 处均为 A+B+C 组合义：产物中不得存在该词的 `sup.fn-ref` 角标、`mark.kw` / `mark.kw fn` 荧光；附录《高报词条》里的「三位一体招生」词条释义必须保留；`notes_render.py` 的 `AMBIGUOUS_FN_CONTEXT` 与 `drop_misapplied_fn_refs()` 不得被删；逐篇清单登记 `fn_dropped`（渲染层实际补删处数）。
23. **问题反馈浮动按钮** —— 单页版与 C 版各恰好 1 个 `.feedback-fab-wrap` + 1 个 `a.feedback-fab`，`href` 指向本仓库 issue `.../issues/1`、`target="_blank"` 与 `rel="noopener noreferrer"` 齐备、**不得残留原生 `title`**、`aria-label` / `aria-describedby` 指向 `role="tooltip"` 气泡、气泡文案逐字一致（含微信号 `JackieZhengChina`）、图标为内联 `<svg>`（不含 `<img>` 等外部图片）、悬停文字由 `.feedback-fab-label` 承载；`assets/style.css` 须同时具备默认隐藏、`@media screen` 显示、悬停展开气泡与 `@media print` 强制隐藏，保证 PDF 不出现；`publish_pages.py` 的 `PUBLIC_ALLOW` 白名单齐备，避免公开反馈渠道被脱敏误拦。

24. **全文搜索** —— 单页版与 C 版各恰好 1 个 `button.search-fab` + 1 个 `div.search-panel`（输入框 / 统计行 / 结果容器三段齐备）；`assets/search-index.js` 以 `window.SEARCH_INDEX=` 开头、条目数与构建清单篇数一致，每篇 `a` / `t` / `p` 齐备，附录用 `note-glossary` 锚点；`SEARCH_JS` 须含空格分词、OR 命中判定（任一词命中即出结果）、`localStorage` 上次词回填、`__searchLocate` 篇内定位与结果链接 `data-kw`；`lazy_js` 的 `go(h,kw)` 扩展齐备；`assets/style.css` 须有半透明 / hover 全显、`max-height:80vh`、`.search-results` 独立 `overflow-y:auto`、收起态缩回图标的 transform，以及 `@media print` 隐藏面板与还原 `.search-hit` / `.search-hit-kw` 临时高亮；`publish_pages.py` 的 `collect()` 必须登记 `assets/search-index.js`；另须断言 `wrapKw` 不再跳过 `mark`（命中词可叠加 `mark .search-hit-kw`）、`data-kw` 带完整查询串并逐词标示、`clearHits` 归一化，以及 `open()` / `close()` 用 `.is-hidden` 让面板与图标互斥。

`data/check_nav.py` 用本机 playwright 复验交互（默认只显示一级、逐级展开、全部展开 / 折叠），条数随内容自动变化，不写固定值；`data/check_align.py` 逐条实测折叠箭头与标题文字的垂直中心偏差（阈值 1.5px）；`data/check_cover.py` 在 320 / 360 / 375 / 414 / 600 / 768 / 1024 / 1280 / 1600px 九档视口下量测封面内容是否溢出（要求纵向、横向、末块越界均为 0），并导出窄屏截图。

---

时间仓促，才疏学浅，如有遗误，万望指正，不胜感谢。

                                    雪人
                          二〇二六年十一月  于天津

## 关联项目

本书的姊妹篇是 [《2027高考志愿填报指南》](https://jackiezheng.github.io/gaokao-2027-guide/)（仓库 [JackieZheng/gaokao-2027-guide](https://github.com/JackieZheng/gaokao-2027-guide)）。

**指南讲方法，指北给资料**：《指南》是方法论手册，教你"怎么填"；本书把「高报笔记」全库按原目录完整汇编成一本可检索、可打印的资料书，供你查阅数据与事实。

## 许可协议

本项目采用 [知识共享 署名-非商业性使用 4.0 国际（CC BY-NC 4.0）](https://creativecommons.org/licenses/by-nc/4.0/) 许可。

- ✅ **可分发**：允许转载、分享、公开传播
- ✅ **可修改**：允许改编、整理、再创作
- ❌ **不可商用**：不得用于商业出版及其它商业用途
- 📌 **须署名**：使用时须注明原作者（雪人老师）及来源，并保留本许可说明

完整法律文本见仓库根目录 [LICENSE](./LICENSE)。

## 赞赏

若这本小书对您有帮助，欢迎扫码赞助一杯咖啡。

<p align="center"><img src="assets/sponsor.jpg" alt="雪人 的赞赏码" width="300"></p>

<!-- ============================================================ -->
<!-- JackieZheng/gaokao-2027-notes 完整徽标组                      -->
<!-- 统一风格：flat-square 扁平化，适配高考笔记类项目                -->
<!-- 三行分组：① 仓库动态状态 ② 项目定位 ③ 可选扩展                -->
<!-- ============================================================ -->

<!-- 🔹 第一行：仓库核心动态状态（自动同步实时数据） -->
<p align="center">
[![License](https://img.shields.io/github/license/JackieZheng/gaokao-2027-notes?style=flat-square&color=blue)](https://github.com/JackieZheng/gaokao-2027-notes/blob/main/LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/JackieZheng/gaokao-2027-notes?style=flat-square&logo=github&logoColor=white&color=yellow)](https://github.com/JackieZheng/gaokao-2027-notes/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/JackieZheng/gaokao-2027-notes?style=flat-square&logo=github&logoColor=white&color=orange)](https://github.com/JackieZheng/gaokao-2027-notes/network/members)
[![Last Commit](https://img.shields.io/github/last-commit/JackieZheng/gaokao-2027-notes?style=flat-square&color=green)](https://github.com/JackieZheng/gaokao-2027-notes/commits/main)
[![Open Issues](https://img.shields.io/github/issues-raw/JackieZheng/gaokao-2027-notes?style=flat-square&color=critical)](https://github.com/JackieZheng/gaokao-2027-notes/issues)
[![Contributors](https://img.shields.io/github/contributors/JackieZheng/gaokao-2027-notes?style=flat-square&color=lightgrey)](https://github.com/JackieZheng/gaokao-2027-notes/graphs/contributors)
</p>

<!-- 🔹 第二行：高考笔记专属定制标识（贴合项目定位） -->
<p align="center">
[![Project Topic](https://img.shields.io/badge/Topic-Gaokao_2027-red?style=flat-square&logo=bookstack&logoColor=white)](https://github.com/topics/gaokao)
[![Content Type](https://img.shields.io/badge/Type-%E9%AB%98%E8%80%83%E5%BF%97%E6%84%BF%E5%A1%AB%E6%8A%A5%E7%AC%94%E8%AE%B0-purple?style=flat-square&logo=notion&logoColor=white)](https://github.com/JackieZheng/gaokao-2027-notes)
[![Main Format](https://img.shields.io/badge/Format-Markdown-black?style=flat-square&logo=markdown&logoColor=white)](https://www.markdownguide.org/)
[![Update Frequency](https://img.shields.io/badge/%E6%9B%B4%E6%96%B0%E9%A2%91%E7%8E%87-%E6%8C%81%E7%BB%AD%E7%BB%B4%E6%8A%A4-brightgreen?style=flat-square)](https://github.com/JackieZheng/gaokao-2027-notes/commits)
[![Suitable For](https://img.shields.io/badge/%E9%80%82%E7%94%A8%E4%BA%BA%E7%BE%A4-2027%E5%B1%8A%E9%AB%98%E8%80%83%E7%94%9F-blueviolet?style=flat-square)](https://github.com/JackieZheng/gaokao-2027-notes)
</p>

<!-- 🔹 第三行：可选扩展（配置 CI 或在线站点后再启用，未配置会显示 error） -->
<p align="center">
[![Build Status](https://img.shields.io/github/actions/workflow/status/JackieZheng/gaokao-2027-notes/deploy.yml?label=%E6%96%87%E6%A1%A3%E9%83%A8%E7%BD%B2&style=flat-square)](https://github.com/JackieZheng/gaokao-2027-notes/actions)
[![Docs Preview](https://img.shields.io/badge/%E5%9C%A8%E7%BA%BF%E9%A2%84%E8%A7%88-Vercel-000000?style=flat-square&logo=vercel)](https://gaokao-2027-notes.vercel.app/)
</p>
