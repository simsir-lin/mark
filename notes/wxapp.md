### 注意事项
* setData 最大1m

### 音频
* 权限判断
* 录音和播放音频的情况下 切换后台+锁屏都会触发暂停事件（onPause）
* 录音时超过限制的时长是不会触发Error事件只会触发Stop事件