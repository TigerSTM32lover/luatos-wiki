# multimedia - 多媒体

> 本页文档由[这个文件](https://gitee.com/openLuat/LuatOS/tree/master/luat/../components/multimedia/luat_lib_multimedia.c)自动生成。如有错误，请提交issue或帮忙修改后pr，谢谢！

> 本库有专属demo，[点此链接查看multimedia的demo例子](https://gitee.com/openLuat/LuatOS/tree/master/demo/multimedia)

## audio.start(id, audio_format, num_channels, sample_rate, bits_per_sample, is_signed)

启动一个多媒体通道准备播放音频

**参数**

|传入值类型|解释|
|-|-|
|int|多媒体播放通道号，0或者1|
|int|音频格式|
|int|声音通道数|
|int|采样频率|
|int|采样位数|
|boolean|是否有符号，默认true|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功true, 失败false|

**例子**

```lua
audio.start(0, audio.PCM, 1, 16000, 16)

```

---

## audio.write(id, data)

往一个多媒体通道写入音频数据

**参数**

|传入值类型|解释|
|-|-|
|string|or zbuff 音频数据|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true,否则返回false|

**例子**

```lua
audio.write(0, "xxxxxx")

```

---

## audio.stop(id)

停止指定的多媒体通道

**参数**

|传入值类型|解释|
|-|-|
|int|audio id,例如0|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true,否则返回false|

**例子**

```lua
audio.stop(0)

```

---

## audio.pause(id, pause)

暂停/恢复指定的多媒体通道

**参数**

|传入值类型|解释|
|-|-|
|int|audio id,例如0|
|boolean|onoff true 暂停，false 恢复|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true,否则返回false|

**例子**

```lua
audio.pause(0, true) --暂停通道0
audio.pause(0, false) --恢复通道0

```

---

## audio.on(id, event, func)

注册audio播放事件回调

**参数**

|传入值类型|解释|
|-|-|
|int|audio id, audio 0写0, audio 1写1|
|function|回调方法|

**返回值**

|返回值类型|解释|
|-|-|
|nil|无返回值|

**例子**

```lua
audio.on(0, function(id, str)
    print(id, str)
end)

```

---

## audio.play(id, path)

播放或者停止播放一个文件，播放完成后，会回调一个audio.DONE消息，可以用pause来暂停或者恢复，其他API不可用。考虑到读SD卡速度比较慢而拖累luavm进程的速度，所以尽量使用本API

**参数**

|传入值类型|解释|
|-|-|
|int|音频通道|
|string|文件名，如果为空，则表示停止播放|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true,否则返回false|

**例子**

```lua
audio.play(0, "xxxxxx")		--开始播放某个文件
audio.play(0)				--停止播放某个文件

```

---

## audio.isEnd(id, path)

检查当前文件是否已经播放结束

**参数**

|传入值类型|解释|
|-|-|
|int|音频通道|

**返回值**

|返回值类型|解释|
|-|-|
|boolean|成功返回true,否则返回false|

**例子**

```lua
audio.isEnd(0)


```

---

## audio.config(id, paPin, onLevel)

配置一个音频通道的特性，比如实现自动控制PA开关。注意这个不是必须的，一般在调用play的时候才需要自动控制，其他情况比如你手动控制播放时，就可以自己控制PA开关

**参数**

|传入值类型|解释|
|-|-|
|int|音频通道|
|int|PA控制IO|
|int|PA打开时的电平|
|return|无|

**返回值**

无

**例子**

```lua
audio.config(0, pin.PC0, 1)	--PA控制脚是PC0，高电平打开

```

---

## codec.create(codec.MP3)

创建编解码用的codec

**参数**

|传入值类型|解释|
|-|-|
|int|多媒体类型，目前支持decode.MP3|
|boolean|是否是编码器，默认true，是解码器|

**返回值**

|返回值类型|解释|
|-|-|
|userdata|成功返回一个数据结构,否则返回nil|

**例子**

```lua
-- 创建decoder
local decoder = codec.create(codec.MP3)--创建一个mp3的decoder

```

---

## codec.info(decoder, file_path)

decoder从文件中解析出音频信息

**参数**

|传入值类型|解释|
|-|-|
|coder|解码用的decoder|
|string|文件路径|

**返回值**

无

**例子**

无

---

## codec.data(decoder, out_buff)

decoder从文件数据中解析出音频数据

**参数**

|传入值类型|解释|
|-|-|
|coder|解码用的decoder|
|zbuff|存放输出数据的zbuff，空间必须不少于16KB|

**返回值**

无

**例子**

无

---

## codec.release(coder)

释放编解码用的coder

**参数**

无

**返回值**

无

**例子**

无

---

