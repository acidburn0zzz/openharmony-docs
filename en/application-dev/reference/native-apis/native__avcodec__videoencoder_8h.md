# native_avcodec_videoencoder.h


## Overview

Declares the native APIs used for video encoding.

**Since:**
9

**Related Modules:**

[VideoEncoder](_video_encoder.md)


## Summary


### Types

| Name | Description | 
| -------- | -------- |
| [OH_VideoEncodeBitrateMode](_video_encoder.md#oh_videoencodebitratemode) | Enumerates the bit rate modes of video encoding.  | 


### Enums

| Name | Description | 
| -------- | -------- |
| [OH_VideoEncodeBitrateMode](_video_encoder.md#oh_videoencodebitratemode) { CBR = 0, VBR = 1, CQ = 2 } | Enumerates the bit rate modes of video encoding.  | 


### Functions

| Name | Description | 
| -------- | -------- |
| [OH_VideoEncoder_CreateByMime](_video_encoder.md#oh_videoencoder_createbymime) (const char \*mime) | Creates a video encoder instance based on a Multipurpose Internet Mail Extension (MIME) type. This API is recommended in most cases.  | 
| [OH_VideoEncoder_CreateByName](_video_encoder.md#oh_videoencoder_createbyname) (const char \*name) | Creates a video encoder instance based on a video encoder name. To use this API, you must know the exact name of the video encoder.  | 
| [OH_VideoEncoder_Destroy](_video_encoder.md#oh_videoencoder_destroy) (OH_AVCodec \*codec) | Clears the internal resources of a video encoder and destroys the video encoder instance.  | 
| [OH_VideoEncoder_SetCallback](_video_encoder.md#oh_videoencoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | Sets an asynchronous callback so that your application can respond to events generated by a video encoder. This API must be called prior to **Prepare**.  | 
| [OH_VideoEncoder_Configure](_video_encoder.md#oh_videoencoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | Configures a video encoder. Typically, you need to configure the attributes of the video track that can be encoded. This API must be called prior to **Prepare**.  | 
| [OH_VideoEncoder_Prepare](_video_encoder.md#oh_videoencoder_prepare) (OH_AVCodec \*codec) | Prepares internal resources for a video encoder. This API must be called after **Configure**.  | 
| [OH_VideoEncoder_Start](_video_encoder.md#oh_videoencoder_start) (OH_AVCodec \*codec) | Starts a video encoder. This API can be called only after the encoder is prepared successfully. After being started, the encoder starts to report the [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) event.  | 
| [OH_VideoEncoder_Stop](_video_encoder.md#oh_videoencoder_stop) (OH_AVCodec \*codec) | Stops a video encoder. After the encoder is stopped, you can call **Start** to start it again.  | 
| [OH_VideoEncoder_Flush](_video_encoder.md#oh_videoencoder_flush) (OH_AVCodec \*codec) | Clears the input and output data in the internal buffer of a video encoder. This API invalidates the indexes of all buffers previously reported through the asynchronous callback. Therefore, before calling this API, ensure that the buffers corresponding to the indexes are no longer required.  | 
| [OH_VideoEncoder_Reset](_video_encoder.md#oh_videoencoder_reset) (OH_AVCodec \*codec) | Resets a video encoder. To continue encoding, you must call **Configure** and **Start** to configure and start the encoder again.  | 
| [OH_VideoEncoder_GetOutputDescription](_video_encoder.md#oh_videoencoder_getoutputdescription) (OH_AVCodec \*codec) | Obtains the attributes of the output data of a video encoder. The **OH_AVFormat** instance in the return value will become invalid when this API is called again or when the **OH_AVCodec** instance is destroyed.  | 
| [OH_VideoEncoder_SetParameter](_video_encoder.md#oh_videoencoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | Sets dynamic parameters for a video encoder. This API can be called only after the encoder is started. Incorrect parameter settings may cause encoding failure.  | 
| [OH_VideoEncoder_GetSurface](_video_encoder.md#oh_videoencoder_getsurface) (OH_AVCodec \*codec, [OHNativeWindow](_native_window.md) \*\*window) | Obtains an input surface from a video encoder. This API must be called prior to **Prepare**.  | 
| [OH_VideoEncoder_FreeOutputData](_video_encoder.md#oh_videoencoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | Frees an output buffer of a video encoder.  | 
| [OH_VideoEncoder_NotifyEndOfStream](_video_encoder.md#oh_videoencoder_notifyendofstream) (OH_AVCodec \*codec) | Notifies a video encoder that input streams end. This API is recommended in surface mode.  | 