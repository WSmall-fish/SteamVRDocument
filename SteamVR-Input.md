# 3 SteamVR Input（输入系统）

SteamVR Unity 插件的核心是 action(动作)。 虚拟现实正在快速发展，我们需要我们的软件能够与硬件一起发展。 SteamVR 输入将代码的设备特定部分抽象化，因此您可以专注于用户的意图 - 他们的 action(动作)。 而不是编写代码来识别 “将 Trigger 按钮下拉 75% 的方式来抓取块”，您现在可以只关注最后一点， “抓住块”。 您仍然可以为 “抓取” 的含义配置默认值，但用户可以在标准界面中将其重新绑定到他们设定的偏好（首选项）。 当新的输入设备出现时，您的用户可以发布绑定以共享该设备，而无需更改代码。

Input System 与之前处理用户输入有显著的不同，使用 SteamVR Input System，开发人员可以在应用程序之外定义默认的动作并与按键进行绑定，而不需要将输入视为某一特定设备的特定按键。这样新的设备可以快速适配应用程序，无需更改代码。比如，当开发者检测玩家是否抓取某个物体的时候，不是检测 Vive 控制器的 Trigger 键或 Oculus Touch 控制器的 Grip 键是否被按下，而是检测预定义的 "Grab" 动作是否为 True 即可。作为开发者，可以在 SteamVR 中为 Grab 动作设置默认按键和阈值，当程序运行时，也可修改这些数值以满足玩家的个人偏好。基于这种机制，不光能够解决控制器碎片化的问题，也可以快速适配未来发布的设备。

>**action**（动作）：程序中定义的用户行为，例如：传送、左右转动等。我们可以将这些动作与不同设备手柄的按键进行绑定。
>开发过程中，我们只需要定义好用户可执行的动作，使用不同设备的用户只需要在手柄设置面板中自定义动作与按键的绑定就可以使用我们开发的程序了。
>也即不需要重新编写代码，只需在设置面板更改动作的绑定。

**[核心]：关注动作而不是按键本身！因为不同设备按键不同，但对于应用只需知道动作而不用在意按键。这样就能使得开发者在编程中专注于用户的动作，而不是具体的控制器按键。**

这种抽象输入的风格与许多其他公司正在考虑的类似。 大多数主要虚拟现实硬件公司的成员都加入了 Khronos，创建了仍在开发中的 OpenXR 标准。（OpenXR 是一套标准接口，它介于设备生产商与内容制作之间。）

SteamVR 将动作分为 6 种不同类型的输入和一种输出类型：

- <kbd>Boolean</kbd> - true or false
- <kbd>Single</kbd> - an analog value
- <kbd>Vector2</kbd> - two analog values
- <kbd>Vector3</kbd> - three analog values
- <kbd>Pose</kbd>- position, rotation, velocity, and angular velocity（位置、旋转、速度和角速度）
- <kbd>Skeleton</kbd> - Orientations for each bone in a hand（手中每根骨头的方向）
- <kbd>Vibration</kbd> - Actuating haptic motors（驱动触觉电机——震动输出）

## 3.1 Boolean 类型

Boolean 类型的动作是 True 或 False 的值。 例如，Grab 是一个常见的动作，要么为真，要么为假。 要么打算抓取某物，要么不抓取，不存在中间状态。 对于 Vive Wand，这可能意味着将扳机扣动 75%，对于 Oculus Touch，这可能意味着将手柄扳机扣动 25%，对于 Knuckles，这可能是电容感应和力感应的某种组合。 但最终它分解为真值或假值。在 Unity 中对应类为<kbd>SteamVR_Action_Boolean</kbd>，通常用于按钮动作。

## 3.2 Single 类型

Single 类型的动作是从 0 到 1 的模拟值，类似于浮点型（float）。在这些场景中，您需要更多数据而不仅仅是真或假。 这些比您预期的要少。 如果之前您正在读取 0 到 1 的值，然后等待它达到某个点，即阈值，那么您可以使用布尔操作完成相同的操作，从而使您的最终用户更容易进行自定义。 单个动作的一个很好的例子是 SteamVR 交互系统中遥控车的油门。 您作为用户所采取的动作可能因您希望汽车行驶的速度而异。在 Unity 中对应类为<kbd>SteamVR_Action_Single</kbd>，常用于获取 Trigger 键的键程值。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e5fe4336e0d741c99b5f35fa58c972b6.png#pic_center)

## 3.3 Vector2 类型

Vector2 类型的动作是两个模拟值的组合，是二维数据。 一般在 VR 中，这类动作最好通过径向菜单或 2D 定位来表示。 在 SteamVR 交互系统中，我们有一个驾驶遥控车和游戏平台（platformer）类型角色的示例。 在 Vive Wand 上，它映射到触摸板，但在 Oculus Touch 和 Knuckles 上，它映射到操纵杆。 对于遥控车，我们使用 y 轴来确定向前或向后的方向，使用 x 轴来确定转弯。 使用游戏平台（platformer），我们将 x/y 输入映射到角色移动的方向和幅度。在 Unity 中对应类为<kbd>SteamVR_Action_Vector2</kbd>，与 Unity 或 C# 中的 Vector2 类型相似，常用于获取 Trackpad 上手指接触点坐标。

## 3.4 Vector3 类型

Vector3 类型的动作不常用，是三维数据，有 3 个数据成员。 在 SteamVR Home 中，这用于滚动，x、y 和 z 是要滚动的页面数量。在 Unity 中对应类为<kbd>SteamVR_Action_Vector3</kbd>。

## 3.5 Pose 类型

Pose 类型的动作表示三维空间中位置和旋转，一般用于跟踪 VR 控制器。 用户可以通过在控制器上设置姿势代表的点来自定义这些绑定。 一些用户可能会发现稍微不同的跟踪位置或旋转对他们来说感觉更好。在 Unity 中对应类为<kbd>SteamVR_Action_Pose</kbd>，用于获取手柄控制器的运动数据。

## 3.6 Skeleton 类型

Skeleton 类型的动作使用 SteamVR 骨骼输入来获得我们对握住 VR 控制器时手指方向的最佳估计。这种类型的动作能够获取用户在持握手柄控制器时的手指关节数据，通过返回数据，结合手部渲染模型，能够更加真实的呈现手部在虚拟世界的姿态，虽然不及像 LeapMotion 等设备获取手指输入那样精确，但是足以获得良好的沉浸感。在 Unity 中对应类为<kbd>SteamVR_Action_Skeleton</kbd>（提供用于呈现手部模型的骨骼数据，每个关节点的位置和旋转）。

## 3.7 Vibration 类型

Vibration 类型的动作用于触发 VR 设备上的触觉反馈。 这可以是控制器、背心，甚至是椅子。

## 3.8 Using actions（动作使用）

创建动作后，您可以在自己的脚本中使用它们，也可以使用我们创建的用于处理一些常见任务的统一组件。 它们被命名为 <kbd>SteamVR_Action_Boolean</kbd>、<kbd>SteamVR_Action_Single</kbd>、<kbd>SteamVR_Action_Vector2</kbd>、<kbd>SteamVR_Action_Vector3</kbd>、<kbd>SteamVR_Action_Pose</kbd>和<kbd>SteamVR_Action_Skeleton</kbd>。 将它们拖到 GameObject 上以查看它们可以做什么。

我们可以在 C# 脚本中定义对应类型的动作（具体代码参照后面文件所示）：

![在这里插入图片描述](https://img-blog.csdnimg.cn/9b2bbaee2f7c4c61bfeabd3b4588257b.png#pic_center)

将脚本挂载到物体身上，在 Inspector 面板中可以给定义的动作进行赋值：

![在这里插入图片描述](https://img-blog.csdnimg.cn/e14ea3a9a0b54d74a64db489686f8b47.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/025485a833e241f3b7610b837f61dba2.png#pic_center)

动作的完整路径参照 action.json 文件中所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/4f89ef54c23e4eedae53c026904718ae.png#pic_center)

也可以通过代码直接获取动作，获取动作的方法有很多种（可以参照 SteamVR 插件的 API 文档），如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/382d0de0f2964b34a40d4d6a138760ae.png#pic_center)

```csharp
//通过该动作的完整路径获取动作--/actions/[actionSet]/[direction]/[actionName]
//动作的路径参照上图--/actions/default/in/InteractUI

//T--期望返回的动作类型，actionName--动作的名字，caseSensitive--检索时是否区分大小写
public static T GetAction<T>(string actionName, bool caseSensitive = false)
public static SteamVR_Action_Single GetSingleAction(string actionName, bool caseSensitive = false)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/0058389344114dee87b6f9158bfb5b72.png#pic_center)

代码如下图所示，可以通过这两种方式指定动作：

![在这里插入图片描述](https://img-blog.csdnimg.cn/519f3ffc93854340a40a41afde900b41.png#pic_center)

赋值后运行程序，在 Inspector 面板中可以看到已经赋好的值：

![在这里插入图片描述](https://img-blog.csdnimg.cn/abe8538f9c184e6e81cdab7586232f19.png#pic_center)

创建动作之后，可以进行动作测试。打开 SteamVR Input Live View 窗口，可以看到动作的触发情况：

![在这里插入图片描述](https://img-blog.csdnimg.cn/762e3b96f512499b9f2133f09c719ed6.png#pic_center)

红色代表动作未绑定按键，绿色代表就是触发了的 action（动作）：

![在这里插入图片描述](https://img-blog.csdnimg.cn/8262fd80b72b459da33995f57a7cf805.png#pic_center)

获取手柄输入，利用代码获取手柄的输入：

```csharp
//如果 action（state）当前值为 true，则返回 true--返回当前动作的状态，检测按键是否一直被按住
//传入 SteamVR_Input_Sources
public bool GetState(SteamVR_Input_Sources inputSource)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/1b40ff2fc2ae418899c519a862e702c8.png#pic_center)

```csharp
//如果 action 的值在最近的更新中已更改为 true（从 false），则返回 true--按下按键
//传入 SteamVR_Input_Sources
public bool GetStateDown(SteamVR_Input_Sources inputSource)
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b5fb875691c04252a0b40dc7cc363e32.png#pic_center)

```csharp
//如果 action 的值在最近的更新中已更改为 false（从 true），则返回 true--松开按键
//传入 SteamVR_Input_Sources
public bool GetStateUp(SteamVR_Input_Sources inputSource)
```

<kbd>SteamVR_Input_Sources 输入源</kbd>：方法传入参数类型：

![在这里插入图片描述](https://img-blog.csdnimg.cn/38d27332dc1f4f88b59897da3711897a.png#pic_center)

代码示例：

```csharp
private void Update()
{
    if (Boolean_Action.GetState(SteamVR_Input_Sources.Any))
    {
        Debug.Log("正在按扳机键！");
    }
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/33116f2ed2234fbc9662ce5ff690a119.png#pic_center)

```csharp
private void Update()
{
	if (Boolean_Action.GetStateDown(SteamVR_Input_Sources.RightHand))
	{
		Debug.Log("右手扳机键被按下！");
	}
	if (Boolean_Action.GetStateUp(SteamVR_Input_Sources.RightHand))
	{
		Debug.Log("右手扳机键被松开");
	}
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/513bb3e262824a3983727954edd4e4d3.png#pic_center)

完整代码如下所示：
```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Valve.VR;

public class ActionDemo : MonoBehaviour
{
    public SteamVR_Action_Boolean Boolean_Action;
    public SteamVR_Action_Single Single_Action;
    public SteamVR_Action_Vector2 Vector2_Action;
    public SteamVR_Action_Vector3 Vector3_Action;
    public SteamVR_Action_Pose Pose_Action;
    public SteamVR_Action_Skeleton Skeleton_Action;

    private void Start()
    {
        Boolean_Action = SteamVR_Input.GetAction<SteamVR_Action_Boolean>("InteractUI");
        Single_Action = SteamVR_Input.GetSingleAction("Squeeze");
    }

    private void Update()
    {
        //if (Boolean_Action.GetState(SteamVR_Input_Sources.Any))
        //{
        //    Debug.Log("正在按扳机键！");
        //}
        if (Boolean_Action.GetStateDown(SteamVR_Input_Sources.RightHand))
        {
            Debug.Log("右手扳机键被按下！");
        }
        if (Boolean_Action.GetStateUp(SteamVR_Input_Sources.RightHand))
        {
            Debug.Log("右手扳机键被松开");
        }
    }
}
```

## 3.9 New action sets（新建动作集）

在开发过程中，我们经常需要根据项目需求定制化相应的动作集。新建动作集可以通过 SteamVR Input 面板进行设置：

![在这里插入图片描述](https://img-blog.csdnimg.cn/85263d3362b148cc9995c2b5d6c675be.png#pic_center)

通过点击 SteamVR Input 面板中 Action Sets 的 “+” 号我们可以新建一个动作集：

![在这里插入图片描述](https://img-blog.csdnimg.cn/91282ee2f44b474aaa6418787cd9112e.png#pic_center)


在新建的动作集下方的下拉菜单中，我们可以设置该动作集在动作绑定界面的形式：
- <kbd>per hand</kbd>：单个设置，用户需每个控制器单独设置绑定
- <kbd>mirrored</kbd>：在动作绑定界面提供镜像模式的复选框，勾选后，仅需对一个控制器进行绑定，该控制器的绑定会映射到另一个
- <kbd>hidden</kbd>：该动作集不会在动作绑定界面显示

通过 Actions 下的 “+” 号我们可以为新建的动作集添加动作：

![在这里插入图片描述](https://img-blog.csdnimg.cn/f6cc1eb67fdd4bcfa985fec770001526.png#pic_center)

其中，Type 也即我们上文提到的动作类型。面板中的 Required 用于设置该动作在动作绑定界面中的提示方式：
- <kbd>optional</kbd>：可选，指该动作用户可以选择绑定或者不绑定，这种动作在界面中不会进行提示
- <kbd>suggested</kbd>：建议，建议对该动作进行绑定，对部分特定程序可能会有影响
- <kbd>mandatory</kbd>：强制的，强制要求用户绑定该动作，不绑定该动作影响程序的使用

这几种提示方式在我们开发过程中，可以针对项目各个动作进行要求，以便用户更好地进行动作的绑定。面板中的 Localized String（本地化的字符串），用以设置该动作在绑定界面的显示文本。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e8ef3a3933e04bdc80cb8128aace1d5f.png#pic_center)

动作集中的动作添加完毕后，点击 Save and generate，保存并生成。之后，我们就可以通过点击 Open binding UI 进入动作绑定界面：

![在这里插入图片描述](https://img-blog.csdnimg.cn/761df345f49b4effbb83251a6c6dd2a8.png#pic_center)

在动作绑定界面，我们新建的动作集提示存在动作未绑定，我们需要对动作集中的动作进行绑定。提示文本即我们在前面设置的 Localized String。镜像模式即我们在创建动作集时下拉菜单里的 mirrored。

![在这里插入图片描述](https://img-blog.csdnimg.cn/6538a9396246433ea9c7fd4e965ba28d.png#pic_center)

之后我们便可以根据我们动作的类型进行按键的绑定，选择不同的按键进行设置。绑定完成后需要点击设置位置下的 “√” 进行保存更改。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e92587515f3244f5ae2928d0fa6f8fff.png#pic_center)
