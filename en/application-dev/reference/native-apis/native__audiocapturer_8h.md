# native_audiocapturer.h


## Overview

The **native_audiocapturer.h** file declares the functions related to an audio capturer.

\@syscap SystemCapability.Multimedia.Audio.Core

**Since**

10

**Related Modules**

[OHAudio](_o_h_audio.md)


## Summary


### Functions

| Name| Description| 
| -------- | -------- |
| [OH_AudioCapturer_Release](_o_h_audio.md#oh_audiocapturer_release) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer) | Releases an audio capturer.| 
| [OH_AudioCapturer_Start](_o_h_audio.md#oh_audiocapturer_start) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer) | Starts an audio capturer.| 
| [OH_AudioCapturer_Pause](_o_h_audio.md#oh_audiocapturer_pause) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer) | Pauses an audio capturer.| 
| [OH_AudioCapturer_Stop](_o_h_audio.md#oh_audiocapturer_stop) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer) | Stops an audio capturer.| 
| [OH_AudioCapturer_Flush](_o_h_audio.md#oh_audiocapturer_flush) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer) | Flushes obtained audio data.| 
| [OH_AudioCapturer_GetCurrentState](_o_h_audio.md#oh_audiocapturer_getcurrentstate) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, [OH_AudioStream_State](_o_h_audio.md#oh_audiostream_state) \*state) | Obtains the state of an audio stream.| 
| [OH_AudioCapturer_GetLatencyMode](_o_h_audio.md#oh_audiocapturer_getlatencymode) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, [OH_AudioStream_LatencyMode](_o_h_audio.md#oh_audiostream_latencymode) \*latencyMode) | Obtains the latency mode of an audio stream.| 
| [OH_AudioCapturer_GetStreamId](_o_h_audio.md#oh_audiocapturer_getstreamid) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, uint32_t \*streamId) | Obtains the stream ID of an audio stream.| 
| [OH_AudioCapturer_GetSamplingRate](_o_h_audio.md#oh_audiocapturer_getsamplingrate) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, int32_t \*rate) | Obtains the sampling rate of an audio stream.| 
| [OH_AudioCapturer_GetChannelCount](_o_h_audio.md#oh_audiocapturer_getchannelcount) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, int32_t \*channelCount) | Obtains the number of channels for an audio stream.| 
| [OH_AudioCapturer_GetSampleFormat](_o_h_audio.md#oh_audiocapturer_getsampleformat) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, [OH_AudioStream_SampleFormat](_o_h_audio.md#oh_audiostream_sampleformat) \*sampleFormat) | Obtains the sampling format of an audio stream.| 
| [OH_AudioCapturer_GetEncodingType](_o_h_audio.md#oh_audiocapturer_getencodingtype) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, [OH_AudioStream_EncodingType](_o_h_audio.md#oh_audiostream_encodingtype) \*encodingType) | Obtains the encoding type of an audio stream.| 
| [OH_AudioCapturer_GetCapturerInfo](_o_h_audio.md#oh_audiocapturer_getcapturerinfo) ([OH_AudioCapturer](_o_h_audio.md#oh_audiocapturer) \*capturer, [OH_AudioStream_SourceType](_o_h_audio.md#oh_audiostream_sourcetype) \*sourceType) | Obtains the usage scenario of an audio capturer.| 
