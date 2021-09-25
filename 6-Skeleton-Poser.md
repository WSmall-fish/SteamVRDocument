# 6 Skeleton Poser（骨骼姿态）
&emsp;&emsp;Skeleton Poser 系统有一个简单的目的：当拿起物理对象时，你在游戏中的手应该变形为拿着对象的姿势。 这些稳固的姿势可以直接在 Unity 编辑器中创作和调整，以便随着游戏的进行快速迭代。 您可以在姿势之上应用奇特的效果，例如附加的每指动画和动态抓握，以及多姿势混合。

&emsp;&emsp;该系统的价值来自于简化的工作流程。 姿势不是处理导入的动画和噩梦般的动画图，而是存储为紧凑的资源，动画会根据与您所持物体相关联的姿势自动应用。 这允许在较小的时间预算内进行更复杂的手部行为。

![在这里插入图片描述](https://img-blog.csdnimg.cn/8db6b5131d7c4f1e8d14073c98d3f9ee.png#pic_center)

&emsp;&emsp;这些是这些工具的基本功能。它们优于 Unity 动画的地方在于，姿势是在场景视图中创建的，复杂的行为可以通过轻按几个开关堆叠起来。

&emsp;&emsp;要将手部姿势添加到游戏中的任何对象，只需向其中添加`SteamVR_Skeleton_Poser`脚本即可。 Poser 脚本有两个部分，我们将在下面的内容中介绍这两部分。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0eaef01a9a7341a292153db0c3236757.png#pic_center)

## 6.1 The Basics（基本需求）
&emsp;&emsp;<kbd>SteamVR_Skeleton_Poser</kbd>脚本旨在独立于<kbd>SteamVR</kbd>交互系统运行，并可添加到您自己的系统中，但 SteamVR 交互系统开箱即用，是快速试用的好方法。

&emsp;&emsp;<kbd>SteamVR_Skeleton_Poses</kbd>是包含特定手部姿势和一些每指动画信息的<kbd>ScriptableObject</kbd>。

&emsp;&emsp;可以通过<kbd>SteamVR_Skeleton_Poser</kbd>脚本及其方便的用户界面添加和修改多个姿势。 您可以为一个 Poser 添加任意数量的姿势，但您可能最多只需要几个。 使用姿势编辑器中的按钮，可以创建新姿势，可以在姿势之间复制姿势数据，可以镜像姿势数据，可以将姿势重置为各种基础，并且可以将场景视图中的骨架更改保存为 改变姿势。 您还可以通过手指移动下拉菜单添加每个手指的附加动画。 这让手指可以根据骨架输入移动，同时保持姿势的约束。 有几种类型的手指运动：
- <kbd>Static</kbd>：没有手指移动。 只使用姿势。
- <kbd>Free</kbd>：手指自由移动。 忽略姿势。
- <kbd>Extend</kbd>：手指可以抬起到完全伸展的位置，但不能比姿势的位置弯曲得更远
- <kbd>Contract</kbd>：手指可以卷曲到完全收缩的位置，但不能张开超过姿势所在的位置。

&emsp;&emsp;使用 Poser 的混合编辑器选项卡，您可以设置混合行为，以复杂的方式混合和堆叠多个姿势。 将混合编辑器视为动画控制器，将姿势视为动画。 您可以添加三种类型的混合行为：手动、模拟操作或布尔操作。 手动行为必须由代码驱动，只需简单调用：

```csharp
Poser.SetBlendingBehaviourValue(string behaviourName, float value)
```

&emsp;&emsp;另一方面，模拟和布尔动作行为由选定的动作自动驱动。 平滑值将是应用于它们的平滑速度，0 表示无。 模拟动作不需要平滑，但推荐用于布尔驱动的行为，因为它们看起来会更平滑。

![在这里插入图片描述](https://img-blog.csdnimg.cn/25495dad8fee465fbc1b78d59fe1102e.png#pic_center)

## 6.2 Using the Skeleton Poser with the SteamVR Interaction system（将 Skeleton Poser 与 SteamVR 交互系统结合使用）
&emsp;&emsp;Poser 组件将自动与 SteamVR 交互系统一起工作。 您需要做的就是将 SteamVR_Skeleton_Poser 脚本添加到可交互的游戏对象中。 交互上有几个设置，您应该确保更改：
- 禁用 `Interactable.HideHandOnAttach`。 如果你留下它，这会隐藏你美丽的姿势！
- 启用 `Interactable.HideControllerOnAttach`。 这将确保您的控制器不会妨碍您的手部姿势。
- 如果您正在创建一个希望能够拿起的可交互对象，请向其中添加 `Throwable` 脚本。
- 如果您希望投掷物不穿过环境，只需设置以下附件标志：`SnapOnAttach、DetachFromOtherHand、VelocityMovement、TurnOffGravity`。
这就是得到一个简单的可交互的 poser 支持所需要的全部。

&emsp;&emsp;如前所述，SteamVR_Skeleton_Poser 脚本旨在独立于 SteamVR 交互系统运行。 如果您使用 `SteamVR_Behaviour_Skeleton` 脚本来为您的手设置动画，您可以通过调用 `BlendToPoser()` 告诉它混合到特定姿势器的输出。

&emsp;&emsp;如果您使用不同的解决方案来为您的骨骼设置动画，Poser 可以按照 `SteamVR_Skeleton_PoseSnapshot` 数据类的格式根据命令生成姿势，该数据类保存所有骨​​骼的对象偏移和位置/旋转。 调用 `poser.GetBlendedPose`，传递 `SteamVR_Behaviour_Skeleton` 或`SteamVR_Action_Skeleton` 和 `SteamVR_Input_Sources` 手部标识符。 这将根据该特定姿势的各种行为和选项为您提供完全合成的姿势，您可以自由地将其应用于您的骨骼。

## 6.3 Pose Editor（姿态编辑器）
&emsp;&emsp;姿势编辑器用于创建和编辑姿势（`Steamvr_Skeleton_Pose`），可以将其作为脚本对象保存到您的项目中，并用于该对象或游戏中的任何其他对象。

![在这里插入图片描述](https://img-blog.csdnimg.cn/ef41087f382443dfbc4ce627c1600288.png#pic_center)

&emsp;&emsp;当您第一次将脚本添加到游戏对象上时，在 Inspector 面板会看到一个选项，可以从项目中选择一个姿势，或者创建一个新姿势。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f122fc0bf8864d68be5da3fb4a756388.png#pic_center)

&emsp;&emsp;点击创建（Create）后，Unity 会在 Cube 下生成相应的手部模型的克隆体（Clone）：

![在这里插入图片描述](https://img-blog.csdnimg.cn/e36fe36cc7cb4bd2add924b979d993eb.png#pic_center)

&emsp;&emsp;要预览您正在创作的姿势，请单击 “左手” 和 “右手” 部分中的手形图标以在场景中打开和关闭预览。 这些预览骨骼在它们的变换中保存了您的所有修改，因此请记住不要禁用已经进行修改的 Hand，除非它们已使用 “`Save Pose`” 按钮保存。

![在这里插入图片描述](https://img-blog.csdnimg.cn/38017dc53c624738aa50ff9e5399600d.png#pic_center)

&emsp;&emsp;执行此操作时在场景中实例化的手是临时的，只要脚本正确跟踪它们，就会在游戏运行时销毁它们。 在应用于预制件之前禁用双手预览是一种很好的做法，因为预制件中的骨架是凌乱、大且不必要的。

&emsp;&emsp;当只启用一个姿势时，最容易编辑姿势，但要使此选项卡中的某些按钮起作用，您需要启用两只预览手。 如果按钮变灰，您可能需要启用一个或两个骨架来激活它。

&emsp;&emsp;如果您想修改骨骼的姿势，只需打开可交互对象下方的层次结构。 你可以看到已经添加了一个 vr 手套骨架，你可以进去编辑这些骨骼的变换来形成你的姿势。

![在这里插入图片描述](https://img-blog.csdnimg.cn/bccbc525d28849f087a4271bcf683520.png#pic_center)

&emsp;&emsp;点击选择手部骨骼的各个节点，旋转节点可以调整手部姿态。

![在这里插入图片描述](https://img-blog.csdnimg.cn/a97024f492b341d3bca4fe466221a858.png#pic_center)


&emsp;&emsp;如果你想做出不对称的姿势，比如说一个不对称的物体——你可以为右手和左手创作一个不同的姿势。 但是，对于简单或对称的对象，您可能希望双手具有相同的姿势，因此您可以使用 Copy x Pose to y hand 按钮将您所做的任何单手修改复制到另一只手上。 当姿势被复制时，手会自动镜像到你的对象上，并且通常会给出完美的结果。 小心此操作，因为它会永久覆盖另一只手的姿势。

![在这里插入图片描述](https://img-blog.csdnimg.cn/c9e1f8658f2c40018c0d02f68da1ae17.png#pic_center)

&emsp;&emsp;修改完成后，点选 Show Left Preview，查看左右手的预览。

![在这里插入图片描述](https://img-blog.csdnimg.cn/8f5871d402074c1a9be293bd43ee1416.png#pic_center)

&emsp;&emsp;预览完成后，点击 Copy Right Pose To Left Hand，使得双手姿态一致。点击 Save Pose 保存修改。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b2e91ea80d6a431fb30ab8cca07c3c8b.png#pic_center)

&emsp;&emsp;记得将 Interactable 脚本下的 HIde Hand On Attach 取消勾选，勾选了则代表手抓握物体时隐藏手，如果不取消勾选，运行时看不到手部模型。我们可以根据不同物体定制其握持动作。

![在这里插入图片描述](https://img-blog.csdnimg.cn/bfdd2ca8fc3641c79b9c9fa12ab7edfa.png#pic_center)


&emsp;&emsp;要向对象添加更多可用姿势，或创建新姿势，请点击顶部姿势列表旁边的小加号按钮。 您将看到创建了一个新选项卡，默认情况下未选择任何姿势，您可以再次从项目中选择一个姿势或创建一个新姿势。 添加 SteamVR_Skeleton_Poser 的姿势将成为稍后可用于混合的姿势。 除了标记为 (MAIN) 的第一个姿势之外，这些顺序无关紧要，被标记为（MAIN）的姿势将是基本姿势。

![在这里插入图片描述](https://img-blog.csdnimg.cn/13b9b91571494df58b62c39787efce33.png#pic_center)

&emsp;&emsp;在每个手形图标下方，您可能已经注意到手指移动的所有选项。 这是用于附加动画，您希望骨骼系统的单个手指动画应用到您创建的姿势之上。 默认情况下，这将设置为静态，但还有其他三个选项。

- <kbd>Static 静态</kbd>：无附加动画 。
- <kbd>Free 自由</kbd>：如果你不希望你的姿势适用于手指，在这种情况下，它只会听从骨骼系统。
- <kbd>Extend 伸展</kbd>：如果手中的姿势是手指的最紧握姿势，则在玩家抬起手指时，手指就会抬起。 这可能是最常见的，因为姿势主要是围绕物体。
- <kbd>Contract 收缩</kbd>：与伸展相反，手指处于任何姿势都是手指的最大伸展值，并且只允许进一步向拳头姿势收缩。 

![在这里插入图片描述](https://img-blog.csdnimg.cn/aa57d98a048d4bbeb868263914a32d27.png#pic_center)



## 6.4 Blending Editor（混合编辑器）
&emsp;&emsp;混合编辑器用于创建更加复杂的行为，即在多个姿势之间混合。

![在这里插入图片描述](https://img-blog.csdnimg.cn/3ad25bd186e84d2abc049f4a65f492ca.png#pic_center)

&emsp;&emsp;点击底部的加号按钮来添加一个新的混合行为，默认情况下称为 new Behaviour。 您可以启用和禁用行为，它们有一个 Influence 滑块，如果您不想在运行时严格启用和禁用它们，您可以在其中关闭和打开它们并使用更多渐变（中间值）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/002afce0352c40ed8c50a6630c2fa98d.png#pic_center)


&emsp;&emsp;他们有一个目标姿势，默认情况下，他们将混合到主要姿势。 因为主要姿势是基础，所以这不会做任何事情。 相反，您需要将其设置为已添加到姿势编辑器列表中的次要姿势之一。

&emsp;&emsp;共有三种不同类型的混合行为：

|![在这里插入图片描述](https://img-blog.csdnimg.cn/8d5776907a154cebb1314aa1793e953c.png#pic_center)| ![在这里插入图片描述](https://img-blog.csdnimg.cn/c6db1cbabb6f476e88f963ad669ff1a2.png#pic_center) | ![在这里插入图片描述](https://img-blog.csdnimg.cn/2e03ce75d5e14a4ea25e446d98d189ea.png#pic_center)|
|:--:|:--:|:--:|
| **Manual**：如果您希望此混合由脚本控制或仅在此处使用此值滑块在 Inspector 中设置，您将使用什么。 | **Analog**：允许您将此混合行为权重映射到项目中的模拟操作之一。 平滑速度可让您对此进行一些平滑处理。 0 意味着没有平滑，任何高于零的都将是缓慢的，随着值的增加，平滑变得越来越快。 一个合适的值应该在 10 到 30 之间，尽管您可能根本不想要任何平滑，因为这是一个模拟动作。 |**Boolean**：这与模拟动作非常相似，不同之处在于它可以映射到项目中的布尔动作，例如按下按钮。 在这种行为类型中，平滑可能更重要一点，因为如果您没有任何平滑，它将立即跳转。 同样，建议使用 10 到 30 之间的值。 |

![在这里插入图片描述](https://img-blog.csdnimg.cn/ec49e76b71c94601b9962e249bf4b698.png#pic_center)

&emsp;&emsp;如果将混合行为的类型选择为后两种，我们可以为混合行为设置 Action。Analog Action类型对应 Action_single，Boolean Action类型对应 Action_bool。

![在这里插入图片描述](https://img-blog.csdnimg.cn/97aacab0e7134ef7b41b1a8a94d9d2d6.png#pic_center)

&emsp;&emsp;我们可以添加多个行为，从而在 Blending Behaviour 设置实现不同 Action 绑定不同的手势。但需要注意的是，混合行为需要我们为物体设置多个 Pose。这里我们以示例场景中的 Squishy 物体为例，演示如何设置并绑定。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7762f701de1c48f3924450d11feb542b.png#pic_center)

&emsp;&emsp;如上图所示，Squishy 有两个 Pose，如下所示：

|![在这里插入图片描述](https://img-blog.csdnimg.cn/84a58a27ec014782a70a005e29ce1d15.png#pic_center)| ![在这里插入图片描述](https://img-blog.csdnimg.cn/4f05d3da70f2485d9ff230e8cb381c5d.png#pic_center)|
|--|--|

&emsp;&emsp;其中示例场景中的 Blending Editor 中已经为副姿势设置了 Action 对应于我们手柄的扳机键，这里我们对另一个 Pose 添加 Pose。我们指定动作（Action）为 Grip，在手柄中我们设置了 Grip 动作对应于手柄的侧边键。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5c92abd0b31a48f0a5bd597559b257ea.png#pic_center)

&emsp;&emsp;平滑速度对应于 Pose 切换的平滑程度，0 意味着没有平滑，瞬间切换。

|![在这里插入图片描述](https://img-blog.csdnimg.cn/5d5d7e981ad649be83a2533056c26738.png#pic_center)|![在这里插入图片描述](https://img-blog.csdnimg.cn/a72e2c40d9314fa1802525685f004cb3.png#pic_center)|
|--|--|

（写完这部分才发现好像不这样设置也能实现这个效果，直接在示例场景中直接扳机键或者侧边键就行 o_0，不过操作没问题）

&emsp;&emsp;每个混合行为的最后一个选项是 Mask。 任何使用过 Unity 的人形动画系统的人都会发现这个 UI 非常熟悉，而那些没有使用过的人会发现它是不言自明的。 如果您不使用 Mask，则混合行为将应用于整只手。 如果您选择使用 Mask，那么您可以选择手的不同部分来应用混合。 绿色部分将应用混合行为，而灰色部分则不会。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7818c44b26944d9ca8b3c9290937c2e1.png#pic_center)

&emsp;&emsp;通过 Mask 我们可以混合多个姿态，从而实现同一动作的部分混合使用，也可以实现不同动作的部分组合使用。我们使用正方体（Cube）为例，首先创建一个手部姿势（PoseA），之后我们复制 PoseA，对 PoseA 的食指进行编辑，得到 PoseB，两个动作仅仅食指姿势不一致。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b14565980b724bf9b6c4aa24b3c77f9e.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/0554453644754811bd9e91e4070447dd.png#pic_center)

&emsp;&emsp;我们为两个姿势设置相对应的 Behaviour，同时针对 PoseB 姿势的 Mask 进行设置，勾选 Use Mask 并只保留食指部分的 Pose：


![在这里插入图片描述](https://img-blog.csdnimg.cn/6dff26ea96ac4226b1d8bb235d2adfef.png#pic_center)

&emsp;&emsp;其中 PoseA 对应扳机键，PoseB 对应侧边键，在扣动扳机拿起物体时，可以在按下侧边键可以看到食指动作的变化。


## 6.5 Manual Behaviours（手动行为）
&emsp;&emsp;模拟和布尔行为会自动生成动画，但您必须通过代码手动修改。这是一个示例脚本，它将使用正弦波调制名为 “Example Behaviour” 的行为：

```csharp
using UnityEngine;
using System.Collections;
using Valve.VR;

public class PoseModulator : MonoBehaviour 
{
    SteamVR_Skeleton_Poser poser;

    private void Start()
    {
        poser = GetComponent<SteamVR_Skeleton_Poser>();
    }

    private void Update()
    {
    	// 设置 blendingBehaviour 的混合值，在 Manual type 的行为中效果最好。
        poser.SetBlendingBehaviourValue("Example Behaviour", Mathf.Sin(Time.time * 10) / 2 + 0.5f);
    }
}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/8e5faa9d4f6c455b8c3c9b964fde6c2c.png#pic_center)

&emsp;&emsp;结果：

![在这里插入图片描述](https://img-blog.csdnimg.cn/1f08a272b34541f1949b076e4f212bfe.gif#pic_center)

## 6.6 Scaling（缩放）
&emsp;&emsp;出于各种原因，许多游戏都以不同的规模制作。 重要的是您的播放器可能会被放大或缩小。 姿势在运行时以任何 Player 比例应用，这很好，但姿势创作工具默认以正常比例完成。 如果您制作的对象应该在更大的比例下可交互，这将是一个问题，因为您在处理姿势时获得的预览与您在游戏中看到的姿势不匹配。 为了解决这个问题，我们添加了一个属性 Preview Pose Scale，它允许您更改姿势编辑器的工作比例。

![在这里插入图片描述](https://img-blog.csdnimg.cn/d55fee42a51c4ce58915e5c8d5804957.png#pic_center)

&emsp;&emsp;此值应设置为您的 Player 的任何比例。

&emsp;&emsp;从不同的预览比例保存的姿势将无法区分，它只是编辑器的助手，可以显示您的姿势从不同比例的手应用的样子。
