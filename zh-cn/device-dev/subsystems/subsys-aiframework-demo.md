# 开发示例<a name="ZH-CN_TOPIC_0000001077767514"></a>

以开发唤醒词识别为例，开发者可在Hi3516DV300开发板上，基于AI引擎框架开发唤醒词识别的sdk以及唤醒词识别的plugin，通过编译命令编出新的版本镜像并将其烧入版本。同时，开发者开发唤醒词识别的应用，该应用能够接收外部音频，将listen到的音频传入SDK中的接口，若音频中带有关键词，唤醒词识别的应用会识别出相应的词语，并打印在命令行中。

本示例中唤醒词识别的场景中唤醒词是固定的，当开发者传入的音频包含”Hi，小问“，启动的应用就会打印"\[Hi, xiaowen\]"，当不包含时，会打印'\[UNKNOWN\]"。

-   **[唤醒词识别SDK的开发示例](subsys-aiframework-demo-sdk.md)**  

-   **[唤醒词识别插件的开发示例](subsys-aiframework-demo-plugin.md)**  

-   **[唤醒词识别配置文件的开发示例](subsys-aiframework-demo-conf.md)**  

