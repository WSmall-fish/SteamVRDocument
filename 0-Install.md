# SteamVR 插件安装
## 一、版本说明

|软件| 版本 |
|--|--|
| Unity | 2019.1.2.f1 |
|SteamVR Plugin |V2.7.3 |
| HMD| HTC VIVE Pro 2.0|

## 二、安装步骤
### 1.下载插件

在 Unity 的菜单栏找到 Asset Store，点击进入 Unity 官方的资源商店

![在这里插入图片描述](https://img-blog.csdnimg.cn/1e882d3916cd45dcad45a782fb015614.png#pic_center)

搜索 SteamVR 导入Unity 即可

![image](https://user-images.githubusercontent.com/91367865/134771075-3ca14ea4-7abc-49ef-9c27-2f4663d731ac.png)


### 2.相关配置

将插件导入完成后，Unity 控制台提示错误：

![在这里插入图片描述](https://img-blog.csdnimg.cn/649f55706cdc482a907b19e2adaa735e.png#pic_center)

报错原因是导入的命名空间（包）不存在，这里我们双击错误提示，在跳转的 VS 中注释导包代码，保存后回到 Unity

![在这里插入图片描述](https://img-blog.csdnimg.cn/8bb56778401f4767a643e35c8794f7d8.png#pic_center)

---

**配置 SteamVR Input：**
在 Unity 中导入 Steam VR 插件，导入完成后可以在 Window 菜单栏中打开 Steam VR 的输入窗口

![在这里插入图片描述](https://img-blog.csdnimg.cn/9d73bd108b4c47efacf9ba104f55dab7.png#pic_center)

在打开SteamVR Input 窗口的过程中，插件会检测项目中是否存在 actions.json 文件，该文件存储了项目中动作（Action）与动作集（Action Sets）的信息，在打开SteamVR Input窗口时会读取该文件。如果没有 actions.json，插件会建议使用默认提供的示例文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/49a23037066c40f591fce7e77df844b8.png#pic_center)

点击 Yes 后，会生成默认的与输入有关的 json 配置文件：

![在这里插入图片描述](https://img-blog.csdnimg.cn/e125a2a9a2e44b758a9bb952f6c7b47b.png#pic_center)


拷贝上述 Json 文件步骤完成后并，点击窗口底部的 “Save and Generate（保存并生成）” 按钮。

![在这里插入图片描述](https://img-blog.csdnimg.cn/9c2592ceaff242daba9f0899bbca8801.png#pic_center)

---

之后会跳出弹窗，提示我们需要选择安装 API，这里我们选择 Unity XR，点击 Unity XR：

![在这里插入图片描述](https://img-blog.csdnimg.cn/173eb3f8224e40389592fda29677bc52.png#pic_center)

**注：** 如果它不弹出这个窗口，也可以在 SteamVR 文件夹中任意选择一个场景点击运行尝试让它弹出窗口

![在这里插入图片描述](https://img-blog.csdnimg.cn/b22aa5ff5e734527a0ac03eebb1f8d41.png#pic_center)

点击 Unity XR 后，Unity 接着弹出如下窗口：

![在这里插入图片描述](https://img-blog.csdnimg.cn/25cc32e91963424393e4a5976bc87e0b.png#pic_center)

提示添加失败，而且此时控制台也会报错，我们需要去包管理工具（package manager）内自行添加：

![在这里插入图片描述](https://img-blog.csdnimg.cn/584b23a99f3a43ab8429da6b83cd012b.png#pic_center#pic_center)

我们进入包管理页面，找到 openVR 点击 Install 安装即可。

---

**导包显示一直在加载：**
如果打开包管理出现下面情况，可以等它加载包：

![在这里插入图片描述](https://img-blog.csdnimg.cn/8122194f56714860afb430ddaec05246.png#pic_center)

如果一直加载不出来，直接断开网络，打开包管理页面找到 OpenVR 点击安装：

![在这里插入图片描述](https://img-blog.csdnimg.cn/a549e59466cc4c9195a79d322338e338.png#pic_center)

安装完成后如下图所示，再连接上网络：

![在这里插入图片描述](https://img-blog.csdnimg.cn/905ad8b7416e484e8feb46b39552cf69.png#pic_center)

---

点击运行 SteamVR 文件夹中的场景，控制台提示如下错误：

![在这里插入图片描述](https://img-blog.csdnimg.cn/cc0e1595026741cbb6819cea84196e45.png#pic_center)

报错原因是因为我们没有连接 VR 设备，只需连接好 VR 设备即可。这里我们连接好 VR 设备再点击运行：

![在这里插入图片描述](https://img-blog.csdnimg.cn/56bb45094c604528a291e83bd744c95b.png#pic_center)

此时提示警告需要我们检查 VR 支持，这里我们只需要打开项目设置页面，找到 Player，勾选其中的 VR 支持

![在这里插入图片描述](https://img-blog.csdnimg.cn/a29d0a3edb0e4dd0bd0a6a59adcb43b6.png#pic_center)

完成上述步骤后再点击运行：

![在这里插入图片描述](https://img-blog.csdnimg.cn/4d9803e5ccdb45f18d9e8dff2042c4a5.png#pic_center)

这里提示警告，我们的 VR SDK Oculus 初始化失败，原因是我们点选 VR 支持时，连带 Oculus 一起选了，我们只需要回到刚才的页面删掉即可。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0f969ce6efc6419e8e456f4fc01a5e5f.png#pic_center)

点击运行，无任何报错情况，安装完成。

![在这里插入图片描述](https://img-blog.csdnimg.cn/3e2f256ada6b4099a79b89f6820d61be.png#pic_center)

#
# 总结

导包过程较为简单，主要是将插件导入 Unity 后的错误，根据控制台的提示解决错误就好。
