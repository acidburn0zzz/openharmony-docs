# AudioEncoder


## Overview

Provides the functions for audio encoding.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

**Since:**
9


## Summary


### Files

| Name | Description | 
| -------- | -------- |
| [native_avcodec_audioencoder.h](native__avcodec__audioencoder_8h.md) | Declares the native APIs used for audio encoding. <br>File to Include: <multimedia/player_framework/native_avcodec_audioencoder.h> | 


### Functions

| Name | Description | 
| -------- | -------- |
| [OH_AudioEncoder_CreateByMime](#oh_audioencoder_createbymime) (const char \*mime) | Creates an audio encoder instance based on a Multipurpose Internet Mail Extension (MIME) type. This API is recommended in most cases.  | 
| [OH_AudioEncoder_CreateByName](#oh_audioencoder_createbyname) (const char \*name) | Creates an audio encoder instance based on an audio encoder name. To use this API, you must know the exact name of the audio encoder.  | 
| [OH_AudioEncoder_Destroy](#oh_audioencoder_destroy) (OH_AVCodec \*codec) | Clears the internal resources of an audio encoder and destroys the audio encoder instance.  | 
| [OH_AudioEncoder_SetCallback](#oh_audioencoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | Sets an asynchronous callback so that your application can respond to events generated by an audio encoder. This API must be called prior to **Prepare**.  | 
| [OH_AudioEncoder_Configure](#oh_audioencoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | Configures an audio encoder. Typically, you need to configure the attributes of the audio track that can be encoded. This API must be called prior to **Prepare**.  | 
| [OH_AudioEncoder_Prepare](#oh_audioencoder_prepare) (OH_AVCodec \*codec) | Prepares internal resources for an audio encoder. This API must be called after **Configure**.  | 
| [OH_AudioEncoder_Start](#oh_audioencoder_start) (OH_AVCodec \*codec) | Starts an audio encoder. This API can be called only after the encoder is prepared successfully. After being started, the encoder starts to report the [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) event.  | 
| [OH_AudioEncoder_Stop](#oh_audioencoder_stop) (OH_AVCodec \*codec) | Stops an audio encoder. After the encoder is stopped, you can call **Start** to start it again.  | 
| [OH_AudioEncoder_Flush](#oh_audioencoder_flush) (OH_AVCodec \*codec) | Clears the input and output data in the internal buffer of an audio encoder. This API invalidates the indexes of all buffers previously reported through the asynchronous callback. Therefore, before calling this API, ensure that the buffers corresponding to the indexes are no longer required.  | 
| [OH_AudioEncoder_Reset](#oh_audioencoder_reset) (OH_AVCodec \*codec) | Resets an audio encoder. To continue encoding, you must call **Configure** and **Start** to configure and start the encoder again.  | 
| [OH_AudioEncoder_GetOutputDescription](#oh_audioencoder_getoutputdescription) (OH_AVCodec \*codec) | Obtains the attributes of the output data of an audio encoder. The caller must manually release the **OH_AVFormat** instance in the return value.  | 
| [OH_AudioEncoder_SetParameter](#oh_audioencoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | Sets dynamic parameters for an audio encoder. This API can be called only after the encoder is started. Incorrect parameter settings may cause encoding failure.  | 
| [OH_AudioEncoder_PushInputData](#oh_audioencoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) attr) | Pushes the input buffer filled with data to an audio encoder. The [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) callback reports available input buffers and their indexes. After being pushed to the decoder, a buffer is not accessible until the buffer with the same index is reported again through the [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) callback.  | 
| [OH_AudioEncoder_FreeOutputData](#oh_audioencoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | Frees an output buffer of an audio encoder.  | 


## Function Description


### OH_AudioEncoder_Configure()

  
```
OH_AVErrCode OH_AudioEncoder_Configure (OH_AVCodec * codec, OH_AVFormat * format )
```
**Description**<br>
Configures an audio encoder. Typically, you need to configure the attributes of the audio track that can be encoded. This API must be called prior to **Prepare**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 
| format | Indicates the handle to an **OH_AVFormat** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_CreateByMime()

  
```
OH_AVCodec* OH_AudioEncoder_CreateByMime (const char * mime)
```
**Description**<br>
Creates an audio encoder instance based on a Multipurpose Internet Mail Extension (MIME) type. This API is recommended in most cases.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| mime | Indicates the pointer to a MIME type. For details, see [OH_AVCODEC_MIMETYPE_AUDIO_AAC](_codec_base.md#oh_avcodec_mimetype_audio_aac).  | 

**Returns**

Returns the pointer to an **OH_AVCodec** instance.


### OH_AudioEncoder_CreateByName()

  
```
OH_AVCodec* OH_AudioEncoder_CreateByName (const char * name)
```
**Description**<br>
Creates an audio encoder instance based on an audio encoder name. To use this API, you must know the exact name of the audio encoder.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| name | Indicates the pointer to an audio encoder name.  | 

**Returns**

Returns the pointer to an **OH_AVCodec** instance.


### OH_AudioEncoder_Destroy()

  
```
OH_AVErrCode OH_AudioEncoder_Destroy (OH_AVCodec * codec)
```
**Description**<br>
Clears the internal resources of an audio encoder and destroys the audio encoder instance.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_Flush()

  
```
OH_AVErrCode OH_AudioEncoder_Flush (OH_AVCodec * codec)
```
**Description**<br>
Clears the input and output data in the internal buffer of an audio encoder. This API invalidates the indexes of all buffers previously reported through the asynchronous callback. Therefore, before calling this API, ensure that the buffers corresponding to the indexes are no longer required.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_FreeOutputData()

  
```
OH_AVErrCode OH_AudioEncoder_FreeOutputData (OH_AVCodec * codec, uint32_t index )
```
**Description**<br>
Frees an output buffer of an audio encoder.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 
| index | Indicates the index of an output buffer.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_GetOutputDescription()

  
```
OH_AVFormat* OH_AudioEncoder_GetOutputDescription (OH_AVCodec * codec)
```
**Description**<br>
Obtains the attributes of the output data of an audio encoder. The caller must manually release the **OH_AVFormat** instance in the return value.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns the handle to an **OH_AVFormat** instance, which must be manually released.


### OH_AudioEncoder_Prepare()

  
```
OH_AVErrCode OH_AudioEncoder_Prepare (OH_AVCodec * codec)
```
**Description**<br>
Prepares internal resources for an audio encoder. This API must be called after **Configure**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_PushInputData()

  
```
OH_AVErrCode OH_AudioEncoder_PushInputData (OH_AVCodec * codec, uint32_t index, OH_AVCodecBufferAttr attr )
```
**Description**<br>
Pushes the input buffer filled with data to an audio encoder. The [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) callback reports available input buffers and their indexes. After being pushed to the decoder, a buffer is not accessible until the buffer with the same index is reported again through the [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) callback.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 
| index | Indicates the index of an input buffer.  | 
| attr | Indicates the attributes of the data contained in the buffer.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_Reset()

  
```
OH_AVErrCode OH_AudioEncoder_Reset (OH_AVCodec * codec)
```
**Description**<br>
Resets an audio encoder. To continue encoding, you must call **Configure** and **Start** to configure and start the encoder again.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_SetCallback()

  
```
OH_AVErrCode OH_AudioEncoder_SetCallback (OH_AVCodec * codec, OH_AVCodecAsyncCallback callback, void * userData )
```
**Description**<br>
Sets an asynchronous callback so that your application can respond to events generated by an audio encoder. This API must be called prior to **Prepare**.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 
| callback | Indicates a collection of all callback functions. For details, see [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md).  | 
| userData | Indicates the pointer to user-specific data.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_SetParameter()

  
```
OH_AVErrCode OH_AudioEncoder_SetParameter (OH_AVCodec * codec, OH_AVFormat * format )
```
**Description**<br>
Sets dynamic parameters for an audio encoder. This API can be called only after the encoder is started. Incorrect parameter settings may cause encoding failure.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 
| format | Indicates the handle to an **OH_AVFormat** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_Start()

  
```
OH_AVErrCode OH_AudioEncoder_Start (OH_AVCodec * codec)
```
**Description**<br>
Starts an audio encoder. This API can be called only after the encoder is prepared successfully. After being started, the encoder starts to report the [OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) event.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.


### OH_AudioEncoder_Stop()

  
```
OH_AVErrCode OH_AudioEncoder_Stop (OH_AVCodec * codec)
```
**Description**<br>
Stops an audio encoder. After the encoder is stopped, you can call **Start** to start it again.

\@syscap SystemCapability.Multimedia.Media.AudioEncoder

 **Parameters**

| Name | Description | 
| -------- | -------- |
| codec | Indicates the pointer to an **OH_AVCodec** instance.  | 

**Returns**

Returns **AV_ERR_OK** if the operation is successful.

Returns an error code defined in [OH_AVErrCode](_core.md#oh_averrcode) if the operation fails.