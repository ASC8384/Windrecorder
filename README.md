![Windrecorder](https://github.com/yuka-friends/Windrecorder/blob/main/__assets__/product-header-cn.jpg)
<h1 align="center"> 🦝 Windrecorder | 捕风记录仪</h1>
<p align="center"> An Open Source <a href="https://www.rewind.ai/">Rewind</a>’s alternative tool on Windows to help you retrieve memory cues.</p>
<p align="center">一款运行在 Windows 平台上的 <a href="https://www.rewind.ai/">Rewind</a> 替代工具，帮助你找回记忆线索</p>

<p align="center"> <a href="https://github.com/yuka-friends/Windrecorder/blob/main/__assets__/README-en.md">English</a>  | <a href="https://github.com/yuka-friends/Windrecorder/blob/main/README.md">简体中文</a> | <a href="https://github.com/yuka-friends/Windrecorder/blob/main/__assets__/README-ja.md">日本語</a> </p>

---

这是一款可以持续记录屏幕画面、通过关键词搜索等方式随时找回相关记忆的工具。

**它的所有能力（录制、识别处理、存储回溯等）完全运行在本地，无需联网，不上传任何数据，只做应该做的事。**

![Windrecorder](https://github.com/yuka-friends/Windrecorder/blob/main/__assets__/product-preview-cn.jpg)

> [!WARNING]
> 🤯 该项目仍在较早期开发阶段，体验与使用上可能会遇上些小问题。如果遇到，欢迎提出 issue 反馈、关注更新。

> [!IMPORTANT]  
> 该项目正在添加功能与进行架构改动，可能导致早期版本用户无法正常升级更新等问题。
> 别担心！带上属于你的 `videos`、 `db`、 `config\config_user.json`目录与文件，随时可以迁移到最新的版本上。

# 🦝 安装

## 自动安装（未就绪）

从 [Releases](https://github.com/yuka-friends/Windrecorder/releases) 下载整合包，将其解压到希望存储数据的目录下即可使用。


## 手动安装

- 下载 [ffmpeg](https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-essentials.zip) ，将其中bin目录下的ffmpeg.exe解压至 `C:\Windows\System32` 下（或其他位于 PATH 的目录下）

- 安装 [Git](https://git-scm.com/downloads)、[Python](https://www.python.org/ftp/python/3.10.11/python-3.10.11-amd64.exe)（安装时勾选 Add python.exe to PATH）、[Pip](https://pip.pypa.io/en/stable/installation/)；
    - **注意！目前暂未支持 python 3.12**，推荐使用 python 3.10，即上面链接指向的版本

- 导航到想要安装此工具的目录下（推荐放在空间富足的分区中），通过终端命令 `git clone https://github.com/yuka-friends/Windrecorder` 下载该工具；

    - 可以打开想要安装的文件夹，在路径栏输入`cmd`并回车，进入当前目录终端，将以上命令贴入、回车执行；

- 打开目录下的`install_update_setting.bat`进行工具安装与配置，顺利的话就可以开始使用了！

    - 如因网络原因报错，可在脚本安装依赖前添加代理`set https_proxy=http://127.0.0.1:xxxx`、或添加大陆[镜像源](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)；


# 🦝 如何使用

目前暂时需要通过打开目录下的批处理脚本来使用工具：

- 通过打开目录下的`start_record.bat`开始记录屏幕；

> 注意：需要一直将终端窗口最小化放在后台运行来记录。同样地，当需要暂停录制时只需关闭终端窗口即可。

- 通过打开目录下的`start_webui.bat`来回溯、查询记忆、进行设置；

> 最佳实践：在webui中设置开机自启动`start_record.bat`，即可无感记录下一切。当电脑空闲无人使用时，`start_record.bat`会自动暂停录制并压缩、清理过期视频；Just set it and forget it！

---
### Roadmap:
- [x] 以较小的文件体积稳定持续地录制屏幕
- [x] 只识别发生变化的画面，在数据库中存储索引
- [x] 完善的图形界面（webui）
- [x] 词云、时间轴、光箱、散点图的数据总结
- [x] 录制完片段后自动识别，闲时自动维护、清理与压缩视频
- [x] 多语言支持：已完成界面与 OCR 识别的 i18n 支持
- [ ] 重构代码，使其更规范与易于开发、具有更好性能
- [ ] 打包工具、提供更便利的使用模式，使之用户友好
- [ ] 添加画面模态的识别，以实现对画面内容描述的搜索
- [ ] 添加数据库加密功能
- [ ] 记录前台进程名与记录OCR词语对应位置，以在搜索时作为线索呈现
- [ ] 添加词嵌入索引、本地/API LLM 查询
- [ ] 添加多屏幕的记录支持（取决于 pyautogui 未来特性加入）
- [ ] 🤔


# 🦝 Q&A | 常见问题
Q: 打开 webui 时没有近期一段时间的数据。

- A: 当 start_record.bat 正在索引数据时，webui 将不会创建最新的临时数据库文件。
解决方法：在 start_record.bat 索引完毕后，刷新 webui 界面，或删除 db 目录下后缀为 _TEMP_READ.db 的数据库文件后刷新即可。此项策略未来将会修复重构。 [#26](https://github.com/yuka-friends/Windrecorder/issues/26)

Q: 在打开webui时提示：`FileNotFoundError: [WinError 2] The system cannot find the file specified: './db\\user_2023-10_wind.db-journal'`

- A: 通常在初次访问 webui 时、start_record.bat 仍正在索引数据时出现。
解决方法：在 start_record.bat 后台索引完毕后，删除 db 文件夹下对应后缀为 _TEMP_READ.db 的数据库文件后刷新即可。

Q: 录制过程中鼠标闪烁

- A：Windows历史遗留问题，可尝试[该帖](https://stackoverflow.com/questions/34023630/how-to-avoid-mouse-pointer-flicker-when-capture-a-window-by-ffmpeg)方法解决🤔。（其实习惯了不去在意也还好（逃

Q: Windows.Media.Ocr.Cli OCR 不可用/识别率过低

- A1: 检查系统中是否添加了目标语言的语言包/输入法：https://learn.microsoft.com/en-us/uwp/api/windows.media.ocr

- A2: 早期版本的默认策略会将高度大于 1500 的屏幕分辨率视为「高 DPI /高分辨率屏幕」，其录制视频分辨率将缩小至原来的四分之一。比如在 3840x2160 的 4k 显示器上，录制视频的分辨率将为 1920x1080，而这可能导致 OCR 识别准确率的下降。如果你在高分辨率屏幕上使用较小的字体或缩放，可以前往`录制与视频存储`中关闭此选项，且可以将`原视频保留几天后进行压缩`的天数设定为较小的值，从而在视频 OCR 索引后一段时间压缩视频体积。

- A3: Windows.Media.Ocr.Cli 对较小的文本识别率可能不良，通过在设置中打开「相近字形搜索」选项可以提高搜索时的召回命中率。

# 🧡
引入了这些项目的帮助：

- https://github.com/DayBreak-u/chineseocr_lite

- https://github.com/zh-h/Windows.Media.Ocr.Cli


---

🧡 喜欢这个工具？欢迎到 Youtube 与流媒体音乐平台上听听 [長瀬有花 / YUKA NAGASE](https://www.youtube.com/channel/UCf-PcSHzYAtfcoiBr5C9DZA) 温柔的音乐，谢谢！

> "Your tools suck, check out my girl Yuka Nagase, she's amazing, I code 10 times faster when listening to her." -- @jpswing