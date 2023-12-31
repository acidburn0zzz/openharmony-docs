# 音视频封装

开发者可以调用本模块的Native API接口，完成音视频封装，即将音频、视频等编码后的媒体数据，按一定的格式存储到文件里。

当前支持的封装能力如下：

| 封装格式 | 视频编解码类型        | 音频编解码类型   | 封面类型       |
| -------- | --------------------- | ---------------- | -------------- |
| mp4      | MPEG-4、 AVC（H.264） | AAC、MPEG（MP3） | jpeg、png、bmp |
| m4a      | MPEG-4、 AVC（H.264） | AAC              | jpeg、png、bmp |

**适用场景**

- 录像、录音
  
  保存录像、录音文件时，需要先对音视频流进行编码，再封装为文件。

- 音视频编辑
  
  完成编辑后的音视频，需要封装为文件。

- 音视频转码

  转码后，保存文件时需要封装。

## 开发步骤

详细的API说明请参考[API文档](../reference/native-apis/_a_v_muxer.md)。

> **说明：**
> 
> 如果调用封装能力写本地文件，需要[申请相关权限](../security/accesstoken-guidelines.md)：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

参考以下示例代码，完成音视频封装的全流程。以封装mp4格式的音视频文件为例。

1. 调用OH_AVMuxer_Create()创建封装器实例对象。

   ``` c++
   // 设置封装格式为mp4
   OH_AVOutputFormat format = AV_OUTPUT_FORMAT_MPEG_4;
   // 以读写方式创建fd
   int32_t fd = open("test.mp4", O_CREAT | O_RDWR | O_TRUNC, S_IRUSR | S_IWUSR);
   OH_AVMuxer *muxer = OH_AVMuxer_Create(fd, format);
   ```

2. （可选）调用OH_AVMuxer_SetRotation()设置旋转角度。
   
   ``` c++
   // 旋转角度，视频画面需要旋转的时候设置
   OH_AVMuxer_SetRotation(muxer, 0);
   ```

3. 添加音频轨。
   
   **方法一：用OH_AVFormat_Create创建format**

   ``` c++
   int audioTrackId = -1;
   OH_AVFormat *formatAudio = OH_AVFormat_Create();
   OH_AVFormat_SetStringValue(formatAudio, OH_MD_KEY_CODEC_MIME, OH_AVCODEC_MIMETYPE_AUDIO_AAC); // 必填
   OH_AVFormat_SetIntValue(formatAudio, OH_MD_KEY_AUD_SAMPLE_RATE, 44100); // 必填
   OH_AVFormat_SetIntValue(formatAudio, OH_MD_KEY_AUD_CHANNEL_COUNT, 2); // 必填
   
   int ret = OH_AVMuxer_AddTrack(muxer, &audioTrackId, formatAudio);
   if (ret != AV_ERR_OK || audioTrackId < 0) {
       // 音频轨添加失败
   }
   OH_AVFormat_Destroy(formatAudio); // 销毁
   ```
   
   **方法二：用OH_AVFormat_CreateAudioFormat创建format**
   
   ``` c++
   int audioTrackId = -1;
   OH_AVFormat *formatAudio = OH_AVFormat_CreateAudioFormat(OH_AVCODEC_MIMETYPE_AUDIO_AAC, 44100, 2);
   
   int ret = OH_AVMuxer_AddTrack(muxer, &audioTrackId, formatAudio);
   if (ret != AV_ERR_OK || audioTrackId < 0) {
       // 音频轨添加失败
   }
   OH_AVFormat_Destroy(formatAudio); // 销毁
   ```

4. 添加视频轨。

   **方法一：用OH_AVFormat_Create创建format**

   ``` c++
   int videoTrackId = -1;
   char *buffer = ...; // 编码config data，如果没有可以不传
   size_t size = ...;  // 编码config data的长度，根据实际情况配置
   OH_AVFormat *formatVideo = OH_AVFormat_Create();
   OH_AVFormat_SetStringValue(formatVideo, OH_MD_KEY_CODEC_MIME, OH_AVCODEC_MIMETYPE_VIDEO_MPEG4); // 必填
   OH_AVFormat_SetIntValue(formatVideo, OH_MD_KEY_WIDTH, 1280); // 必填
   OH_AVFormat_SetIntValue(formatVideo, OH_MD_KEY_HEIGHT, 720); // 必填
   OH_AVFormat_SetBuffer(formatVideo, OH_MD_KEY_CODEC_CONFIG, buffer, size); // 非必须
   
   int ret = OH_AVMuxer_AddTrack(muxer, &videoTrackId, formatVideo);
   if (ret != AV_ERR_OK || videoTrackId < 0) {
       // 视频轨添加失败
   }
   OH_AVFormat_Destroy(formatVideo); // 销毁
   ```
   
   **方法二：用OH_AVFormat_CreateVideoFormat创建format**
   
   ``` c++
   int videoTrackId = -1;
   char *buffer = ...; // 编码config data，如果没有可以不传
   size_t size = ...;  // 编码config data的长度，根据实际情况配置
   OH_AVFormat *formatVideo = OH_AVFormat_CreateVideoFormat(OH_AVCODEC_MIMETYPE_VIDEO_MPEG4, 1280, 720);
   OH_AVFormat_SetBuffer(formatVideo, OH_MD_KEY_CODEC_CONFIG, buffer, size); // 非必须
   
   int ret = OH_AVMuxer_AddTrack(muxer, &videoTrackId, formatVideo);
   if (ret != AV_ERR_OK || videoTrackId < 0) {
       // 视频轨添加失败
   }
   OH_AVFormat_Destroy(formatVideo); // 销毁
   ```

5. 添加封面轨。

   **方法一：用OH_AVFormat_Create创建format**

   ``` c++
   int coverTrackId = -1;
   OH_AVFormat *formatCover = OH_AVFormat_Create();
   OH_AVFormat_SetStringValue(formatCover, OH_MD_KEY_CODEC_MIME, OH_AVCODEC_MIMETYPE_IMAGE_JPG);
   OH_AVFormat_SetIntValue(formatCover, OH_MD_KEY_WIDTH, 1280);
   OH_AVFormat_SetIntValue(formatCover, OH_MD_KEY_HEIGHT, 720);
   
   int ret = OH_AVMuxer_AddTrack(muxer, &coverTrackId, formatCover);
   if (ret != AV_ERR_OK || coverTrackId < 0) {
       // 添加封面失败
   }
   OH_AVFormat_Destroy(formatCover); // 销毁
   ```
   
   **方法二：用OH_AVFormat_CreateVideoFormat创建format**

   ``` c++
   int coverTrackId = -1;
   OH_AVFormat *formatCover = OH_AVFormat_CreateVideoFormat(OH_AVCODEC_MIMETYPE_IMAGE_JPG, 1280, 720);
   
   int ret = OH_AVMuxer_AddTrack(muxer, &coverTrackId, formatCover);
   if (ret != AV_ERR_OK || coverTrackId < 0) {
       // 添加封面失败
   }
   OH_AVFormat_Destroy(formatCover); // 销毁
   ```

6. 调用OH_AVMuxer_Start()开始封装。
   
   ``` c++
   // 调用start，写封装文件头。start后，不能设置媒体参数、不能添加媒体轨
   if (OH_AVMuxer_Start(muxer) != AV_ERR_OK) {
       // 异常处理
   }
   ```

7. 调用OH_AVMuxer_WriteSample()，写入封装数据。
   
   包括视频、音频、封面数据。

   ``` c++
   // start后，才能开始写入数据
   int size = ...;
   OH_AVMemory *sample = OH_AVMemory_Create(size); // 创建AVMemory
   // 往sampleBuffer里写入数据参考OH_AVMemory的使用方法
   // 封装封面，必须一次写完一张图片
   
   // 创建buffer info
   OH_AVCodecBufferAttr info;
   info.pts = ...; // 当前数据的开始播放的时间，单位微秒
   info.size = size; // 当前数据的长度
   info.offset = 0; // 偏移，一般为0
   info.flags |= AVCODEC_BUFFER_FLAGS_SYNC_FRAME; // 当前数据的标志。具体参考OH_AVCodecBufferFlags
   int trackId = audioTrackId; // 选择写的媒体轨
   
   int ret = OH_AVMuxer_WriteSample(muxer, trackId, sample, info);
   if (ret != AV_ERR_OK) {
       // 异常处理
   }
   ```

8. 调用OH_AVMuxer_Stop()，停止封装。

   ``` c++
   // 调用stop，写封装文件尾。stop后不能写入媒体数据
   if (OH_AVMuxer_Stop(muxer) != AV_ERR_OK) {
       // 异常处理
   }
   ```

9. 调用OH_AVMuxer_Destroy()销毁实例，释放资源。

   ``` c++
   if (OH_AVMuxer_Destroy(muxer) != AV_ERR_OK) {
       // 异常处理
   }
   muxer = NULL;
   close(fd); // 关闭文件描述符
   ```