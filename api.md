通过系统广播控制歌词显示

### 更新歌词
```java
CSLyricHelper.PlayInfo playInfo = new CSLyricHelper.PlayInfo("base64 format icon", "com.example.musicplayer");
playInfo.isPlaying = true;
CSLyricHelper.updateLyric(context, playInfo, new CSLyricHelper.LyricData("这是一段歌词"));
```

### 设置暂停状态
```java
 CSLyricHelper.PlayInfo playInfo = new CSLyricHelper.PlayInfo(null, "com.example.musicplayer");
 playInfo.isPlaying = false;
 CSLyricHelper.pause(this, playInfo);
```

### 设置播放状态
```java
CSLyricHelper.PlayInfo playInfo = new CSLyricHelper.PlayInfo(null, "com.example.musicplayer");
playInfo.isPlaying = true;
CSLyricHelper.playing(context, playInfo);
```

### 接收歌词
```java
IntentFilter filter = new IntentFilter("com.makino.cslyric.getter.action.LYRIC");
BroadcastReceiver broadcastReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        Bundle extra = intent.getExtras();
        if (extra == null) return;
        String type = intent.getStringExtra("type");
        String playInfoSource = extra.getString("playInfo");
        String lyricDataSource = extra.getString("lyricData");
        //...
    }
};
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
    context.registerReceiver(broadcastReceiver, filter, Context.RECEIVER_EXPORTED);
} else {
    context.registerReceiver(broadcastReceiver, filter);
}
```

### 封装库
```java

import android.content.Context;
import android.content.Intent;
import android.util.JsonWriter;
import java.io.IOException;
import java.io.StringWriter;

/**
 * CSLyricHelper 提供了一些静态方法来更新和控制歌词显示。
 */
public class CSLyricHelper {
    
    /**
     * 发送更新歌词信息的广播。
     *
     * @param context 上下文，用于发送广播。
     * @param playInfo 歌曲播放信息。
     * @param lyricData 歌词数据。
     */
    public static void updateLyric(Context context, PlayInfo playInfo, LyricData lyricData) {
        Intent intent = new Intent("com.makino.cslyric.getter.action.LYRIC");
        intent.putExtra("type", "update");
        intent.putExtra("lyricData", lyricData.toString());
        intent.putExtra("playInfo", playInfo.toString());
        context.sendBroadcast(intent);
    }

    /**
     * 发送暂停控制信息的广播。
     *
     * @param context 上下文，用于发送广播。
     * @param playInfo 歌曲播放信息。
     */
    public static void pause(Context context, PlayInfo playInfo) {
        Intent intent = new Intent("com.makino.cslyric.getter.action.LYRIC");
        intent.putExtra("type", "pause");
        intent.putExtra("playInfo", playInfo.toString());
        context.sendBroadcast(intent);
    }

    /**
     * 发送正在播放信息的广播。
     *
     * @param context 上下文，用于发送广播。
     * @param playInfo 歌曲播放信息。
     */
    public static void playing(Context context, PlayInfo playInfo) {
        Intent intent = new Intent("com.makino.cslyric.getter.action.LYRIC");
        intent.putExtra("type", "playing");
        intent.putExtra("playInfo", playInfo.toString());
        context.sendBroadcast(intent);
    }

    /**
     * LyricData 类用于封装歌词信息，并实现其字符串表示形式的生成。
     */
    public static class LyricData {

        public String lyric;

        public LyricData(String lyric) {
            this.lyric = lyric;
        }

        @Override
        public String toString() {
            StringWriter sw = new StringWriter();
            try (JsonWriter jw = new JsonWriter(sw)) {
                jw.beginObject();
                jw.name("lyric").value(lyric);
                jw.endObject();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return sw.toString();
        }
    }

    /**
     * PlayInfo 类用于封装播放信息，并实现其字符串表示形式的生成。
     */
    public static class PlayInfo {

        public String icon;

        public String packageName;

        public boolean isPlaying;

        public PlayInfo(String icon, String packageName) {
            this.icon = icon;
            this.packageName = packageName;
        }

        @Override
        public String toString() {
            StringWriter sw = new StringWriter();
            try (JsonWriter jw = new JsonWriter(sw)) {
                jw.beginObject();
                jw.name("icon").value(icon);
                jw.name("packageName").value(packageName);
                jw.name("isPlaying").value(isPlaying);
                jw.endObject();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return sw.toString();
        }
    }
}


```
