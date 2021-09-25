# 2 Render Models（渲染模式）

由于沉浸在虚拟现实中时您的整个视野都会被覆盖，因此拥有您所握持的控制器的虚拟表示会很有帮助。SteamVR 提供了一种简单的方法，不仅可以获取通用控制器模型，还可以获取具有单独驱动组件的模型。 因此，当您在现实生活中扣动控制器上的扳机时，您也可以在虚拟世界中看到它也在拉动。 这有助于提高可用性并有力地促进存在感。

## 2.1 The Component（组件）

交互系统和简单示例场景都有使用渲染模型的装备。 在 <kbd>[Camera Rig]</kbd> 预制件的 Simple Sample 场景中，您将找到<kbd>Controller (left)</kbd>和<kbd>Controller (right)</kbd>。 这些游戏对象上有一个<kbd>SteamVR_Behaviour_Pose</kbd>组件，用于设置变换的位置和旋转。

![在这里插入图片描述](https://img-blog.csdnimg.cn/19198925a5cc4508be3a32a4221cf169.png#pic_center)

在这些对象下，您将看到名为<kbd>Model</kbd>的 GameObjects，其中包含我们的<kbd>SteamVR_RenderModel</kbd>组件。 它有几个成员：
 
![在这里插入图片描述](https://img-blog.csdnimg.cn/c434dde0b980402dacdbd7c57e3afd82.png#pic_center)

- <kbd>Index 索引</kbd>：这是控制器的 “跟踪设备索引”。 它是渲染模型系统用来向底层系统标识控制器的整数 id。 在之前的 SteamVR 迭代中，这也用于访问该控制器上的输入，但现在这是通过 “输入系统” 完成的。
- <kbd>Model Override 模型覆盖</kbd>：通常出于测试目的，您可以指定要显示的模型，而不是动态评估连接的设备类型。
- <kbd>Shader 着色器</kbd>：如果您更喜欢使用不同的着色器来渲染模型，您可以在此处指定它。 默认情况下，使用 Unity 的标准着色器。
- <kbd>Verbose 详细</kbd>：将输出调试日志以告诉您脚本发生了什么。
- <kbd>Create Components 创建组件</kbd>：在勾选的情况下为每个组件创建单独的游戏对象。
- <kbd>Update Dynamically 动态更新</kbd>：将移动单个组件与其物理对应物内联。

## 2.2 Attaching Objects（附着对象）

开发人员通常希望将游戏对象附加到控制器上的特定点。 为此，我们在控制器的每个部分下放置了一个名为 “attach” 的游戏对象，该部分以相关部分为中心。 为便于访问，您可以访问<kbd>SteamVR_RenderModel</kbd>脚本并调用<kbd>GetComponentTransform(string componentName)</kbd>，它将返回 \a Transform（不进行任何 GC 分配）。 此处的 componentName 参数区分大小写，因此请确保传入的组件名称与运行时在 Hierarchy 视图中显示的完全相同。

![在这里插入图片描述](https://img-blog.csdnimg.cn/35703c9d9d4644419575bcdd7dee92da.png#pic_center)


## 2.3 Notes（注意）
<kbd>SteamVR_RenderModel</kbd>组件需要与设置其索引的对象位于同一游戏对象上。 在<kbd>[CameraRig]</kbd>预制件中，这是由<kbd>SteamVR_Behaviour_Pose</kbd>脚本完成的。
