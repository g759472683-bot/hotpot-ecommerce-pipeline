# 视频生成方案

> 更新日期：2026-03-31
> 负责人：废物

---

## 1. MiniMax API 测试报告

### 密钥验证
- **API Key**: `sk-api-Mlxw...`（已验证有效）
- **Endpoint**: `https://api.minimaxi.com/v1/video_generation`
- **查询Endpoint**: `https://api.minimaxi.com/v1/query/video_generation`
- **文件下载**: `https://api.minimaxi.com/v1/files/retrieve`

### 测试结果
| 项目 | 结果 |
|---|---|
| 密钥有效性 | ✅ 通过 |
| 1080P+6秒 | ✅ 成功 |
| 768P+10秒 | ✅ 成功 |
| 生成耗时 | 约60-90秒 |
| 文件格式 | MP4 |

---

## 2. 视频样片

### 样片1：电影感风格
- **标签**: cinematic
- **Prompt**: 傍晚的城市天际线，镜头缓缓推进，暖黄色灯光渐次亮起，画面色调偏冷后期调色，氛围孤独而浪漫。
- **Model**: MiniMax-Hailuo-2.3
- **时长/分辨率**: 6秒 / 1080P
- **Task ID**: 382448713187412
- **File ID**: 382405224820989
- **下载链接**: https://public-cdn-video-data-algeng.oss-cn-wulanchabu.aliyuncs.com/inference_output%2Fvideo%2F2026-03-31%2F82af8e9e-6d41-4a52-a577-1622a9dbe59f%2Foutput_aigc.mp4?Expires=1774957417&OSSAccessKeyId=LTAI5tAmwsjSaaZVA6cEFAUu&Signature=i9qVrRC0XvqQ5oiV0k%2FMDi1LzYc%3D

### 样片2：时尚清新风格
- **标签**: fresh
- **Prompt**: 咖啡馆内，一杯拿铁放在木质桌面上，镜头从俯拍慢慢拉远，阳光从窗户洒入，色调明亮清新。
- **Model**: MiniMax-Hailuo-2.3
- **时长/分辨率**: 6秒 / 1080P
- **Task ID**: 382447252083088
- **File ID**: 382430145818865
- **下载链接**: https://public-cdn-video-data-algeng.oss-cn-wulanchabu.aliyuncs.com/inference_output%2Fvideo%2F2026-03-31%2F6ddf22e8-37b2-4923-b04d-1f5e4b106ddf%2Foutput_aigc.mp4?Expires=1774957417&OSSAccessKeyId=LTAI5tAmwsjSaaZVA6cEFAUu&Signature=ELTlwdBQ0oTcBCV8Rj3DyT7SpIY%3D

### 样片3：快节奏活力风格
- **标签**: dynamic
- **Prompt**: 街头滑板少年跳起动作，镜头快速切换跟随，背景是城市霓虹色彩，节奏感强，色调鲜艳。
- **Model**: MiniMax-Hailuo-2.3
- **时长/分辨率**: 6秒 / 1080P
- **Task ID**: 382450499768710
- **File ID**: 382451104379202
- **下载链接**: https://public-cdn-video-data-algeng.oss-cn-wulanchabu.aliyuncs.com/inference_output%2Fvideo%2F2026-03-31%2Fa8889fa9-67cf-4686-b0ab-ec78b8c27626%2Foutput_aigc.mp4?Expires=1774957418&OSSAccessKeyId=LTAI5tAmwsjSaaZVA6cEFAUu&Signature=F5CvyvT3CycdS03C0PKmkxn6%2Fbo%3D

---

## 3. 视频模板库规范

### 三套风格模板

| 模板 | 适用场景 | 色调 | 镜头运动 | 时长 |
|---|---|---|---|---|
| **电影感** | 情感类/品牌故事 | 偏冷/低饱和 | 缓慢推进/环绕 | 10秒最佳 |
| **时尚清新** | 产品展示/种草 | 明亮/暖色 | 缓慢拉远/平移 | 6-10秒 |
| **快节奏活力** | 潮流/促销/开场 | 鲜艳/高饱和 | 快切/跟拍 | 6秒 |

### Prompt构造公式

**电影感模板**：
```
镜头[推进/环绕]，[主体]在[场景]中[动作]，
[氛围：孤独/浪漫/悬疑]，
画面色调偏冷/暖，[景别描述]。
```

**时尚清新模板**：
```
[特写/俯拍/平移]，[主体/产品]在[场景]中，
[阳光/自然光]，[色调明亮清新/暖色调]，
氛围[轻松/惬意/温馨]。
```

**快节奏活力模板**：
```
镜头快速切换跟随[主体]，
背景是[城市/运动场景]，
节奏感强，色调[鲜艳/霓虹]，
[动作描述]，[镜头运动方式]。
```

### AI合规标识嵌入位置

所有视频必须在以下位置之一嵌入水印：
- **首选**：右下角，白色半透明文字"内容由AI生成"
- **备选**：左下角，同上规格

FFmpeg命令示例：
```bash
ffmpeg -i input.mp4 -vf "drawtext=text='内容由AI生成':fontsize=36:fontcolor=white@0.7:x=(w-text_w)-20:y=h-50" -c:a copy output_marked.mp4
```

---

## 4. 已知限制

| 项目 | 限制 |
|---|---|
| 1080P最长时长 | 6秒 |
| 768P最长时长 | 10秒 |
| 单次最大并发 | 建议3个任务 |
| 每日建议上限 | 50条（成本控制） |
