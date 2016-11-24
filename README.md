# Annca
Android solution to simplify work with different camera apis. Include video and photo capturing features with possibility to select quality for appropriate media action etc. In current solution were used some approaches from <a href="https://github.com/google/grafika">Grafika project</a> and <a href="https://github.com/googlesamples/android-Camera2Video">Google camera samples</a>.

<img src="https://github.com/memfis19/Annca/blob/master/art/default_camera.png" width="200px" /> <img src="https://github.com/memfis19/Annca/blob/master/art/settings_for_video_limitation.png" width="200px" /><img src="https://github.com/memfis19/Annca/blob/master/art/video_camera.png" width="200" /><img src="https://github.com/memfis19/Annca/blob/master/art/video_low_quality.png" width="200" />

## Example of using
Add Annca activities to the your app manifest file:
```
<activity
        android:name="io.github.memfis19.annca.internal.ui.camera.Camera1Activity"
        android:screenOrientation="portrait"
        android:theme="@style/ThemeFullscreen" />
<activity
        android:name="io.github.memfis19.annca.internal.ui.camera2.Camera2Activity"
        android:screenOrientation="portrait"
        android:theme="@style/ThemeFullscreen" />
<activity
        android:name="io.github.memfis19.annca.internal.ui.preview.PreviewActivity"
        android:screenOrientation="portrait"
        android:theme="@style/ThemeFullscreen" />
```
#### Please note that `android:screenOrientation="portrait"` is mandatory. In current implementation device rotation is detecting via sensor.

Don't forget to put permissions or request them:
```
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
A code example of the most simple using:
```
 AnncaConfiguration.Builder builder = new AnncaConfiguration.Builder(activity, CAPTURE_MEDIA);
 new Annca(builder.build()).launchCamera();
```
and thats it. You can use more extended settings i.e.:
```
 AnncaConfiguration.Builder videoLimited = new AnncaConfiguration.Builder(activity, CAPTURE_MEDIA);
 videoLimited.setMediaAction(AnncaConfiguration.MEDIA_ACTION_VIDEO);
 videoLimited.setMediaQuality(AnncaConfiguration.MEDIA_QUALITY_AUTO);
 videoLimited.setVideoFileSize(5 * 1024 * 1024);
 videoLimited.setMinimumVideoDuration(5 * 60 * 1000);
 new Annca(videoLimited.build()).launchCamera();
```
in this example you request video capturing which is limited by file size for 5Mb and predefined minimum video duration for 5 min. To achieve this result Annca will decrease video bit rate, so use it carefully to avoid unexpected result (i.e. low quality).

##### How to get result?
```
 @Override
  protected void onActivityResult(int requestCode, int resultCode, Intent data) {
      super.onActivityResult(requestCode, resultCode, data);
      if (requestCode == CAPTURE_MEDIA && resultCode == RESULT_OK) {
          String filePath = data.getStringExtra(AnncaConfiguration.Arguments.FILE_PATH);
      }
   }
```

## How to add to your project?
```
compile 'io.github.memfis19:annca:0.2.1'
```
## Know issue
Library has not release yet, so it contains some issues.

## Roadmap
-Improve determinig camera quality settings;</br>
-Improve Camera customizing possibilities;</br>
-Extend annca configuration settings.

# [LICENSE](/LICENSE.md)

###### MIT License

###### Copyright (c) 2016 Rodion Surzhenko

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
