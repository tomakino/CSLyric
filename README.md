![HEAD](https://socialify.git.ci/tomakino/CSLyric/image?description=1&descriptionEditable=%E4%B8%80%E4%B8%AA%E5%9C%A8%E7%8A%B6%E6%80%81%E6%A0%8F%E6%98%BE%E7%A4%BA%E6%AD%8C%E8%AF%8D%E7%9A%84Xposed%E6%A8%A1%E5%9D%97&font=Jost&language=1&name=1&owner=1&stargazers=1&theme=Auto)

![图片](demo.gif)

## 软件介绍
本软件为适用于`LSPosed`的`Xposed模块`，提供系统级歌词显示扩展功能。

***

## 首次使用
1. 点击`↻` 选择 `重启系统界面`
1. 点击`设置` - `设置锚点`（推荐`Clock`）
1. 点击`↻` 选择 `重启作用域`
1. 尝试播放一首音乐。

***

## 更新模块后
点击`↻` 选择 `一键重启`

***

## 已支持软件
| 名称          |     基于版本 | 歌词提供方式  |
|-------------|---------:|---------|
| QQ音乐        | 13.6.5.8 | Hook    |
| 网易云音乐       |   9.1.05 | 魅族状态栏歌词 |
| 酷狗音乐        |   12.3.6 | Hook    |
| Salt Player |   10.4.3 | 魅族状态栏歌词 |
| Apple Music |    4.8.0 | Hook    |
| 酷我音乐        | 10.9.1.1 | 车载蓝牙歌词  |
| 酷狗音乐概念版     |    3.5.2 | 车载蓝牙歌词  |
***
## 常见问题

### 歌词不显示？
#### 参考方案
1. 歌词提供方式为`魅族状态栏歌词模式`需要在音乐软件设置里打开`魅族状态栏歌词开关`。<br/>
1. 歌词提供方式为`车载蓝牙歌词模式`需要在音乐软件设置里打开`车载蓝牙歌词开关`。

### 歌词不滚动或者遮挡？
请适当调整歌词宽度。

### 如何隐藏时间和通知图标？
打开视图控制器找到有`notification`相关内容的条目设置为`在播放时隐藏`。
