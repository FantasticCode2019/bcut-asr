<h1 align="center">Bcut-ASR</h1>

使用必剪 API 进行云端语音字幕识别和声音合成，支持 CLI 和 module 调用

## ✨Feature

- 可直接上传`flac`, `aac`, `m4a`, `mp3`, `wav`音频格式
- 自动调用 ffmpeg, 实现视频伴音和其他音频格式转码
- 支持`srt`, `json`, `lrc`, `txt`格式字幕输出
- 字幕支持断句和首位时间标记
- 可使用 stdout 输出字幕文本
- 可根据可用声音列表，合成各种声音
- 可微调合成参数

## 🚀Install

首先确保 ffmpeg 已安装，且 PATH 中可以访问，若未安装可以使用如下命令（已安装请无视）：

Linux：

```bash
sudo apt install ffmpeg
```

Windows：

```powershell
winget install ffmpeg
```

本项目暂时未发布 pypi，应使用本地安装，Python 版本应 >= 3.10，需要安装 poetry 

```bash
git clone https://github.com/SocialSisterYi/bcut-asr
cd bcut-asr
poetry lock
poetry build -f wheel
pip install dist/bcut_tools-0.0.3-py3-none-any.whl # Example
```

## 📃Usage

### CLI Interface

```bash
bcut_tools asr video.mp4
```

或

```bash
bcut_tools asr video.mp4 subtitle.srt
```

或

```bash
bcut_tools asr video.mp4 -f srt - > subtitle.srt
```

长音频指定任务状态轮询间隔(秒)，避免接口频繁调用

```bash
bcut_tools asr video.mp4 -f srt -i 30 - > subtitle.srt
```

```bash
bcut_tools tts -l
                                     必剪可用语音列表                                     
 Category             Name                 Voice                          Voice Engine    
 特色                 梦想家               xianyumengxiangjia-guichu      bili-fewshot    
                      大将锐评             fanzhiyi-guichu                bili-fewshot    
                      激昂张飞             zhangfei-guichu                bili-fewshot    
                      麦克阿瑟             maikease                       bili-fewshot    
                      理塘小子             dingzhen                       bili-fewshot    
                      说唱小哥             heyboy                         bili-fewshot    
                      机甲战警             jixiezhanjing                  bili-fewshot    
                      锤大力               wangdachui                     bili-fewshot    
                      体虚生               tixunan                        bili-fewshot    
                      游戏解说             sunxiaochuan                   bili-fewshot    
                      北京小伙             hutong_daye                    minimax
                      土味老爹             audiobook_male_2               minimax
                      电子奸臣             dianzijianchen                 bili-fewshot    
                      曼波                 shigeju                        bili-fewshot    
 角色                 猴哥                 houge                          bili-fewshot    
                      树人                 luxun                          bili-fewshot    
                      萌奇                 xiaomeng                       bili-fewshot    
                      愤怒阿瞒             caocaogaifan-guichu            bili-fewshot    
                      智谋丞相             zhugeliang-guichu              bili-fewshot    
                      熊熊                 xionger                        bili-fewshot    
                      魔法老爹             laodie                         bili-fewshot    
                      海宝                 haibao                         bili-fewshot    
                      豪迈二爷             guanyu-guichu                  bili-fewshot    
                      春日部               chunribu                       bili-fewshot    
                      紫薇                 ziwei                          bili-fewshot    
                      海星                 haixing                        bili-fewshot    
                      名侦探               kenanvc                        bili-fewshot    
 解说                 青年主播             zhubo                          bili-fewshot    
                      舌尖美食             meishi                         bili-fewshot    
                      译制腔               yizhi                          bili-fewshot    
                      娱乐扒妹             bamei                          bili-fewshot
                      解说男声             jieshuonannew                  bili-fewshot
                      亲切播报             Sentimental_Lady               minimax
                      沉稳叙事             Tough_Boss                     minimax
                      新闻主播             audiobook_female_2             minimax
                      生动解说             male-qn-jingying               minimax
                      稳重熟男             Romantic_Husband               minimax
                      财经主播             presenter_male                 minimax
                      电台主播             Stressed_Lady                  minimax
                      说书老爷             badao_shaoye                   minimax
                      知识讲解             Confident_Woman                minimax
                      解说女声             jieshuonv                      bili-fewshot
                      治愈男声             huayuanbaobao                  bili-fewshot
                      娱乐扒哥             bage                           bili-fewshot
                      低音炮               diyinpao                       bili-fewshot
 童声                 萌小孩               xiaoxin                        bili-fewshot
                      小鬼头               daimeng                        bili-fewshot
                      超萌奶娃             nvhai                          bili-fewshot
                      元气正太             zhengtai                       bili-fewshot
 女声                 爽快学姐             vc_mock_clone_bumianjie_vocals minimax
                                           _01_1213_1527
                      玉玲                 liyuling                       bili-fewshot
                      清仓促销员           xiaoxiao                       bili-fewshot
                      TVB女声              tvbfemale                      bili-fewshot
                      知性女生             db6                            bili-fewshot
                      温柔女孩             wenrounvsheng                  bili-fewshot
                      知性姐姐             vc_mock_clone_xiaoa_vocals_01_ minimax
                                           1213_1530
                      舒缓解说             Spanish_SophisticatedLady      minimax
                      元气少女             xindong                        bili-fewshot
                      休闲学姐             Podcast_girl_platform          minimax
                      糖系女声             tianmei                        bili-fewshot
 男声                 鸡血广告             jixueguanggao                  bili-fewshot
                      热血男孩             xiaoyao                        bili-fewshot
                      轻松少年             qingsong                       bili-fewshot
                      森系少年             db8                            bili-fewshot
                      磁性男声             audiobook_male_1               minimax
                      理科男声             Male_botong_platform           minimax
                      幽默小哥             wenrou_tongzhuo                minimax
                      清亮男声             dj_m_chat_0306_05              minimax
                      亲切男声             Xiaoyi_mix_platform            minimax
                      知性小哥             Boyan_new_platform             minimax
                      憨厚男声             Humorous_Elder                 minimax
                      深情男主             wenrou_yisheng                 minimax
 语言                 四川话               zh-CN-sichuan-YunxiNeural      microsoft
                      山东话               zh-CN-shandong-YunxiangNeural  microsoft
                      粤语男声             zh-HK-WanLungNeural            microsoft
                      台湾话               zh-TW-HsiaoChenNeural          microsoft
                      粤语女声             zh-HK-HiuMaanNeural            microsoft
                      说书先生             xiaopo                         bili-fewshot
                      上海话               wuu-CN-XiaotongNeural          microsoft
                      东北话               zh-CN-liaoning-XiaobeiNeural   microsoft
                      英文男声             v50                            bili-fewshot
                      天津话               tianjinhua                     bili-fewshot
                      陕西话               zh-CN-shaanxi-XiaoniNeural     microsoft
                      河南话               zh-CN-henan-YundengNeural      microsoft
                      中英双语             xindong                        bili-fewshot
```

```bash
bcut_tools tts "使用必剪 API 进行云端语音字幕识别和声音合成，支持 CLI 和 module 调用" --voice "dingzhen" --voice-engine "bili-fewshot"
```

```bash
bcut_tools -h    
usage: bcut-tools [-h] {asr,tts} ...

必剪命令行工具

positional arguments:
  {asr,tts}
    asr       语音识别
    tts       语音合成

options:
  -h, --help  show this help message and exit


bcut_tools tts -h
usage: bcut-tools tts [-h] [-l] [-o [OUTPUT]] [--meta-output [META_OUTPUT]] [--sep-output [SEP_OUTPUT]] [-i [1.0]]
                      [--pitch-rate [0]] [--speech-rate [SPEECH_RATE]] [--sample-rate [SAMPLE_RATE]] [--volume [VOLUME]]
                      [--voice [VOICE]] [--voice-engine [VOICE_ENGINE]]
                      [text]

必剪语音合成

positional arguments:
  text                  合成文本内容

options:
  -h, --help            show this help message and exit
  -l, --list, --available-voices
                        显示可用的声音列表
  -o [OUTPUT], --output [OUTPUT]
                        输出音频文件
  --meta-output [META_OUTPUT]
                        输出元数据文件
  --sep-output [SEP_OUTPUT]
                        输出分割数据文件
  -i [1.0], --interval [1.0]
                        任务状态轮询间隔(秒)
  --pitch-rate [0]      音调
  --speech-rate [SPEECH_RATE]
                        语速
  --sample-rate [SAMPLE_RATE]
                        采样率
  --volume [VOLUME]     音量
  --voice [VOICE]       使用 bcut-tools tts avail
  --voice-engine [VOICE_ENGINE]
                        引擎类型

支持输出音频格式: wav

bcut_tools asr -h
usage: bcut-tools asr [-h] [-f [{srt,json,lrc,txt}]] [-i [1.0]] input [output]

必剪语音识别

positional arguments:
  input                 输入媒体文件
  output                输出字幕文件, 可stdout

options:
  -h, --help            show this help message and exit
  -f [{srt,json,lrc,txt}], --format [{srt,json,lrc,txt}]
                        输出字幕格式
  -i [1.0], --interval [1.0]
                        任务状态轮询间隔(秒)

支持输入音频格式: flac, aac, m4a, mp3, wav 支持自动调用ffmpeg提取视频伴音
```

### Module

```python
from bcut_tools import BcutASR
from bcut_tools.orm import ResultStateEnum

asr = BcutASR('voice.mp3')
asr.upload() # 上传文件
asr.create_task() # 创建任务

# 轮询检查结果
while True:
    result = asr.result()
    # 判断识别成功
    if result.state == ResultStateEnum.COMPLETE:
        break

# 解析字幕内容
subtitle = result.parse()
# 判断是否存在字幕
if subtitle.has_data():
    # 输出srt格式
    print(subtitle.to_srt())
```

输入视频

```python
from bcut_tools import run_everywhere
from argparse import Namespace


f = open("file.mp4", "rb")
argg = Namespace(format="srt", interval=30.0, input=f, output=None)
run_everywhere(argg)

```