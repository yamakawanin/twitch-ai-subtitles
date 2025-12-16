License
本项目采用 Non-Commercial License。
仅允许学习、研究与课程演示用途，禁止任何形式的商业使用。
如需商用，请联系作者获得书面许可
Twitch 实时字幕系统（ASR + EN→ZH）
基于 Twitch 直播音频流的实时字幕系统。
流程：HLS → VAD 语音分段 → Whisper 语音识别 → MarianMT 英中翻译 → Gradio Web UI
功能
支持 Twitch Cookie 模式（通过 yt-dlp 自动解析 HLS）
支持 手动输入 .m3u8 HLS 链接
WebRTC VAD 分段，降低实时延迟
Faster-Whisper 语音识别
MarianMT 英→中翻译
Gradio 前端（实时字幕 / 历史字幕 / 日志）
环境要求
系统
Python 3.10+(版本不能太高，确保有对应的torch)
ffmpeg（需加入 PATH）
yt-dlp（仅 Cookie 模式需要）
Python 依赖
pip install -U pip
pip install gradio faster-whisper webrtcvad transformers torch numpy
如仓库中提供 requirements.txt，可直接：
pip install -r requirements.txt
启动方式
python main.py
浏览器访问：
http://127.0.0.1:7860
若入口文件名不是 main.py，请替换为实际文件名。
使用说明
模式一：Twitch Cookie 模式
选择 Cookie Mode
填写：
Twitch Username(主播名字）
auth-token
persistent
点击 Initialize / Start
模式二：手动 HLS
选择 Manual HLS
粘贴 .m3u8 链接
点击 Initialize / Start
参数建议
Whisper 模型：base / small 延迟低，medium / large 更准但更慢
Beam Search：值越小速度越快
VAD aggressiveness：过大可能漏语音，过小容易误触发
Max segment seconds：减小可降低整体延迟
常见问题
一直显示 “Listening…”
直播未开启或 HLS 不可访问
ffmpeg 未正确安装
VAD 阈值过高，可适当降低
首次启动较慢
Whisper 与翻译模型首次加载属正常现象
字幕延迟较大
使用更小的 Whisper 模型
降低 beam
调小最大分段时长
使用 GPU（如可用）
