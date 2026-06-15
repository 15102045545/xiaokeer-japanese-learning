# 当前实现事实溯源

本文件允许记录技术细节，仅用于审计 PRD 事实来源。PRD 正文不应依赖这些技术路径作为产品形态限制。

## 前端入口与页面行为

| 证据 | 文件与行号 | 事实 |
| --- | --- | --- |
| 日语资源页支持编辑模式/文档模式切换 | `xiaokeer-a-vue/src/views/japanese/japanese/index.vue:1-27` | 页面通过开关在资源维护和文档/卡片视图之间切换。 |
| 资源维护视图绑定日语资源主题，并注入批量课程音频事件和单条播放事件 | `xiaokeer-a-vue/src/views/japanese/japanese/index.vue:9-16` | 编辑模式使用通用页面容器承载资源维护；支持选中资源事件和单条资源事件。 |
| 单条播放使用资源的第一个日语朗读音频地址 | `xiaokeer-a-vue/src/views/japanese/japanese/index.vue:47-54` | 资源行可触发日语音频播放。 |
| 文档模式加载基础卡片数据 | `xiaokeer-a-vue/src/views/japanese/japanese/index.vue:56-60` | 切换文档模式时请求卡片数据。 |
| 批量课程音频生成从选中资源标识触发 | `xiaokeer-a-vue/src/views/japanese/japanese/index.vue:62-64` | 选中资源后调用课程音频生成能力，并展示返回结果。 |
| 学习游戏调用翻译、统计、提交、刷新和输入模式切换能力 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:13-29` | 游戏页有日语转中文翻译、统计读取、学习结果提交、今日统计刷新、输入法切换。 |
| 游戏回车处理流程 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:58-116` | 回车后翻译、展示弹窗、播放原文音频一次、计算耗时、提交结果、刷新统计、提示学习成功。 |
| 游戏提交保存来源 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:87-95` | 游戏提交的来源写死为“蓝宝书N1-文法”。 |
| 游戏进入时刷新统计 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:120-129` | 页面加载后先刷新今日统计，再读取统计。 |
| 游戏统计展示内容 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:169-177` | 展示今日学习数量、今日学习时间、统计起点、累计小时和累计句子数。 |
| 游戏输入区输入模式辅助 | `xiaokeer-a-vue/src/views/japanese/japanese/japanese_put_game.vue:147-155` | 鼠标进入输入区切换日文，离开切换中文，回车触发攻略。 |
| 卡片组件播放音频 | `xiaokeer-a-vue/src/views/resource/components/JapaneseWordItemView.vue:11-20` | 卡片点击听音时使用日语音频 URL 播放。 |
| 卡片展示日语文本与音频文本 | `xiaokeer-a-vue/src/views/resource/components/JapaneseWordItemView.vue:26-47` | 有资源标识时展示卡片内容和听音入口；无资源时展示空卡片。 |

## 通用资源维护行为

| 证据 | 文件与行号 | 事实 |
| --- | --- | --- |
| 资源维护容器包含关联资源、新增、事件、查询和数据区域 | `xiaokeer-a-vue/src/components/XiaokeerElPageContainer.vue:1-90` | 维护页提供链接、新增、批量事件、查询、分页、导出等通用能力。 |
| 查询区域支持分页、导出、查询、清空 | `xiaokeer-a-vue/src/components/XiaokeerElPageContainer.vue:72-90` | 列表查询具备分页和导出按钮。 |
| 数据表格支持行选择和行级事件 | `xiaokeer-a-vue/src/components/XiaokeerElPageContainer.vue:99-220` | 用户可以选中资源并执行行级操作。 |
| 新增和编辑流程 | `xiaokeer-a-vue/src/components/XiaokeerElPageContainer.vue:780-846` | 新增打开空表单，编辑先取详情，确认后保存并刷新列表。 |
| 批量事件确认与全量确认机制 | `xiaokeer-a-vue/src/components/XiaokeerElPageContainer.vue:900-969` | 未选择资源时会提示是否对全表执行，并要求输入确认文本；确认不匹配会提示错误。 |

## 后端资源、游戏和音频行为

| 证据 | 文件与行号 | 事实 |
| --- | --- | --- |
| 日语资源字段定义 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinPo.java:28-49` | 资源包含标识、创建时间、日语文本、日语音频、中文含义、中文音频和来源。 |
| 音频列表读写 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinPo.java:56-76` | 日语和中文音频以列表语义读写，空时返回空列表。 |
| 游戏统计字段 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinGamePo.java:20-31` | 统计包含标识、创建时间、累计时长、累计数量、今日时长、今日数量和今日日期。 |
| 学习提交字段 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/SubmitGameResultForm.java:15-23` | 单次提交包含日语文本、日语音频、中文含义、中文音频、来源和耗时。 |
| 获取游戏统计 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:49-58` | 读取固定统计记录，记录不存在时抛出“未找到游戏统计信息”。 |
| 刷新今日统计 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:61-75` | 如果统计日期不是今天，今日数量和今日时长置 0，并更新今日日期。 |
| 提交游戏结果并更新统计 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:77-105` | 每次提交累计数量加 1，累计时长加本次耗时；跨日先重置今日统计，再累加今日数量和时长；同时创建一条日语资源。 |
| 生成课程音频入口 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:108-115` | 根据资源标识生成合成音频并返回音频资源。 |
| 批量 TTS 与批量翻译入口 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:117-129` | 选中资源可执行朗读音频生成和中文释义翻译。 |
| 基础卡片数据入口 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinController.java:131-138` | 返回二维卡片数据，注释说明用于清音、浊音、半浊音、拨音文档。 |
| 关联学习资料 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:98-107` | 提供日语工具、五十音练习、在线读音、速记、网课视频等链接。 |
| 基础卡片数据筛选 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:109-135` | 卡片数据使用来源“日语基础”筛选，并填充空卡片。 |
| 批量朗读音频生成 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:137-178` | 对选中资源生成日语和中文朗读音频，并追加到对应音频列表；单条失败被捕获后继续处理。 |
| 来源分组 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:180-184` | 资源可按来源分组。 |
| 课程音频合成顺序 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:186-215` | 只纳入同时具备日语和中文音频的资源；拼接顺序为中文、短暂停顿、日语三次，并重复两轮。 |
| 批量中文翻译 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:220-230` | 对选中资源使用日语文本翻译中文含义，并批量更新。 |
| 返回视图时音频列表结构化 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/resource_japanese/JapaneseWuShiYinServiceImpl.java:233-238` | 资源返回时将日语和中文音频转换为列表。 |

## 数据结构证据

| 证据 | 文件与行号 | 事实 |
| --- | --- | --- |
| 日语资源表结构 | `xiaokeer-a-server/xiaokeer-server-app/src/main/resources/db/xiaokeer2_schema.sql:80-96` | 资源持久字段包含标识、创建时间、日语文本、日语音频、中文含义、中文音频、来源、类型和表格位置字段。 |
| 游戏统计表结构 | `xiaokeer-a-server/xiaokeer-server-app/src/main/resources/db/xiaokeer2_schema.sql:98-107` | 统计持久字段包含标识、创建时间、累计时长、累计数量、今日时长、今日数量和今日日期。 |
| 游戏统计初始化 | `xiaokeer-a-server/xiaokeer-server-app/src/main/resources/db/xiaokeer2_schema.sql:109-114` | 初始化固定标识为 `1` 的统计记录，所有计数和时长为 `0`。 |
| 音频资源基础字段 | `xiaokeer-a-server/xiaokeer-common/src/main/java/core/xiaokeer/core_file/StorageFilePo.java:16-24` | 音频/文件资源有标识、创建时间戳、访问地址、存储路径和文件类型。 |
| 音频资源扩展字段 | `xiaokeer-a-server/xiaokeer-common/src/main/java/core/xiaokeer/core_file/StorageAudioFilePo.java:8-12` | 音频资源有对应文本、发音类型和时长。 |

## 外部能力证据

| 证据 | 文件与行号 | 事实 |
| --- | --- | --- |
| 日语到中文翻译入口 | `xiaokeer-a-server/xiaokeer-common/src/main/java/core/xiaokeer/support/helper/translate/TranslateController.java:22-25` | 存在日语到中文翻译能力，返回翻译结果对象。 |
| 翻译结果含原文、译文、原文音频、译文音频 | `xiaokeer-a-server/xiaokeer-common/src/main/java/core/xiaokeer/support/helper/translate/TranslateResult.java:8-23` | 游戏流程使用该结构沉淀双语文本和音频。 |
| 翻译后下载并转换音频 | `xiaokeer-a-server/xiaokeer-common/src/main/java/core/xiaokeer/support/helper/translate/TranslateHelper.java:37-66` | 翻译能力返回原文与译文音频，并保存为可复用音频资源。 |
| 输入模式切换 | `xiaokeer-a-server/xiaokeer-server-app/src/main/java/core/xiaokeer/common_toolkit/ToolkitController.java:20-35` | 存在切换中文和日文输入模式的辅助能力。 |

## 发现的不确定点

- 数据结构中存在类型和表格位置字段，但当前资源对象未稳定暴露为业务字段，卡片视图还存在运行时随机排布行为，因此 PRD 正文未把它们写成已确认核心模型。
- 游戏页代码注释提到“原文三遍、译文一遍、原文三遍”的播放序列，但当前生效代码只播放原文一次，因此 PRD 正文按当前生效行为记录。
- 未选择资源时的全量批量确认机制存在于通用页面容器，但日语特定批量能力是否能正确、安全地全量执行未确认。
- 卡片播放组件中音频字段处理方式存在结构化列表和字符串解析混用迹象，PRD 正文只抽象为“音频资源列表”。
