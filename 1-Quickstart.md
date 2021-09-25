# 1 Quickstart（快速开始）

## 1.1 Download（下载插件）

插件下载有很多方式，可以前往 Steam 平台下载，也可以在 Unity Asset Store 搜索 Steam VR 进行下载。

安装部分内容参考 Install.md 文件操作。

**Steam：**[https://store.steampowered.com/app/250820/SteamVR/](https://store.steampowered.com/app/250820/SteamVR/)

**Unity Asset Store：**[https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647](https://assetstore.unity.com/packages/tools/integration/steamvr-plugin-32647)

## 1.2 SteamVR Input Window（输入窗口）

在 Unity 中导入 Steam VR 插件，导入完成后可以在 Window 菜单栏中打开 Steam VR 的输入窗口。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9d73bd108b4c47efacf9ba104f55dab7.png#pic_center)

## 1.3 Copy JSONs（复制 JSON）

单击确定复制默认的 "SteamVR Input JSON" 文件。 这些 actions（动作）和 binding（绑定）将帮助交互系统工作，并为您提供如何开始的示例。


在打开SteamVR Input 窗口的过程中，插件会检测项目中是否存在 actions.json 文件，该文件存储了项目中动作（Action）与动作集（Action Sets）的信息，在打开SteamVR Input窗口时会读取该文件。如果没有 actions.json，插件会建议使用默认提供的示例文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/49a23037066c40f591fce7e77df844b8.png#pic_center)

点击 Yes 后，会生成默认的与输入有关的 json 配置文件：

![在这里插入图片描述](https://img-blog.csdnimg.cn/e125a2a9a2e44b758a9bb952f6c7b47b.png#pic_center)

插件会将示例文件 actions.json 以及一些当前主流控制器的按键绑定配置文件拷贝到项目中的 StreamingAssets/SteamVR 下，在之后程序运行时，也将从此文件夹中读取用户关于动作（action）的配置信息。

## 1.4 Save and Generate（保存并生成）

拷贝上述 Json 文件并打开窗口后，点击底部的 “保存并生成” 按钮。 这将保存您的操作并生成一些类来初始化它们，并使您可以在编辑器中和通过代码轻松访问它们。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9c2592ceaff242daba9f0899bbca8801.png#pic_center)

在窗口中有四个 Action Sets（动作集）以及动作集包含的 Actions（动作），我们可以在面板中根据需求自定义动作集（添加自己的动作集或者删除原有动作集的内容）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5b0b4c17f710431c82a4e655912daba9.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/b7323445228248339ccbc993c081d400.png#pic_center)

我们自定义完成动作的设置后，可以点击 Open binding UI 就可以对动作进行绑定。

![在这里插入图片描述](https://img-blog.csdnimg.cn/c9bb9e1e24974265ab33a4bc0b7fc199.png#pic_center)

当点击 Save and Generate 按钮后，插件将为动作以及动作集生成可编程访问的对象类，将它们放置在项目的 SteamVR_Input 目录下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/a779c96bd9e94154a87c414dab0673d5.png#pic_center)

## 1.5 Interaction System（交互系统）

完成上述操作后，打开 “交互系统” 示例场景，我们可以在 **Assets/SteamVR/InteractionSystem/Samples/Interaction_Example** 找到示例场景。

![在这里插入图片描述](https://img-blog.csdnimg.cn/ac72edd23fc44bea87071ff4a8c0aea3.png#pic_center)

然后连接头盔，控制器等设备，点击 Unity 的播放，开始探索 “交互系统” 的示例场景。

**注**：示例场景中包含很多常用的功能，在日后的开发过程中，可能需要实现类似示例场景中的功能。例如，利用射线实现 UI 交互、利用手柄抓握物体、传送等。可以多体验一下示例场景，学习相关功能的实现。

