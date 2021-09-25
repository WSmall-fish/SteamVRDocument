# 5 Interaction System（交互系统）
&emsp;&emsp;Valve 发布 The Lab 后，我们从该项目中汲取了经验，并创建了一个交互系统，其他人可以在他们自己的项目中使用。 此系统已更新为使用 SteamVR 输入和新的 SteamVR 骨骼输入系统。 该系统可以作为如何使用这些新系统的示例。 它包括以下示例：

- <kbd>Interaction with Unity UI elements</kbd>：与 Unity UI 元素的交互
- <kbd>Pickup, Drop, and Throw</kbd>：拾起，放下，扔出去
- <kbd>Multiple variations on throwing velocities</kbd>：投掷速度的多种变化
- <kbd>Bow and Arrow</kbd>：弓和箭
- <kbd>Wheel interactions</kbd>：轮交互
- <kbd>Proximity button</kbd>：邻近按钮
- <kbd>Variety of Skeleton Input examples</kbd>：各种骨骼输入示例
- <kbd>Teleporting</kbd>：传送
- <kbd>Using held objects</kbd>：使用抓握对象
- <kbd>Using Skeleton Input to form a hand around a held object</kbd>：使用骨骼输入在手持物体周围形成一只手

![在这里插入图片描述](https://img-blog.csdnimg.cn/7d168a1db6dd48fa95260966ca8e7f08.png#pic_center)

## 5.1 Getting started（入门指南）
- 创建新场景
- 删除 “Main Camera” 对象（不删除主相机的话。看到的是主相机的画面，而不能看到 VR 相机的画面。）
- 将 “Player” 预制件从 Assets/SteamVR/InteractionSystem/Core/Prefabs 拖入场景中。 这个预制件设置了主要的 Player 组件和手。 它还与所需的所有相关 SteamVR 输入操作挂钩。
- 拖入后就能够在头显中看到场景以及在场景中跟踪的控制器。
- 如果控制器有支持骨骼输入，就可以看到触摸和按下控制器上按钮的手。
- 将 Interactable 组件添加到场景中的任何对象。 然后，此对象上的所有其他组件将开始从玩家手中接收相关消息。（查看 Samples/Scripts/InteractableExample.cs 示例用法）
- 我们已经包含了一些常用的可交互类，例如 Throwable。 将此组件添加到您的对象将允许它被玩家捡起并抛出。
- 然后，可以将 Skeleton Poser 组件添加到具有 Interactable 的 GameObject，并在与它交互时摆出您想要的手的外观。
- 要将传送添加到场景中，将传送预制件从传送/预制件拖到场景中。 这将设置所有传送逻辑。
- 从 Teleport/Prefabs 中拖入一些 TeleportPoint 预制件以添加玩家可以传送到的位置。
- 您还可以将 TeleportArea 组件添加到场景中的任何对象。 这将允许玩家沿着该对象的碰撞器传送到任何地方。



&emsp;&emsp;有了这些基本的构建块，就可以继续创建一些相当复杂的对象。 至于示例，可以查看 SteamVR/InteractionSystem/Samples/Scenes 中的 Interactions_Example 场景。

## 5.2 Sample scene（示例场景）
&emsp;&emsp;Samples/Scenes 文件夹中的示例场景 Interactions_Example 包括所有主要组件，是您熟悉系统的好地方。 该场景包含以下元素：

- <kbd>Player 玩家</kbd>：玩家预制体是整个系统的核心。其他大部分组件都取决于玩家是否出现在场景中。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f198ebe2c13c4e46af05ea0ccebdcc11.png#pic_center)

- <kbd>Teleporting 传送</kbd>：传送预制体处理系统的所有传送逻辑。

![在这里插入图片描述](https://img-blog.csdnimg.cn/1d6d850ba2bb4a97a2757306604b2515.png#pic_center)

- <kbd>InteractableExample 交互示例</kbd>：这显示了一个非常简单的交互，展示了从手接收消息并对其做出反应的基本方面。

![在这里插入图片描述](https://img-blog.csdnimg.cn/bc4ab8b8610e4ebda8614a1cf93da10e.png#pic_center)

- <kbd>Throwables 投掷物</kbd>：这些展示了如何使用交互系统来创建各种不同类型的可抛出对象。 阅读每个表格旁边的说明以获取更多信息。

![在这里插入图片描述](https://img-blog.csdnimg.cn/01cd225e05184118be5bab25318cb8ec.png#pic_center)

- <kbd>Skeleton 骨骼</kbd>：有几个不同的手部模型示例，以及关于骨骼的程度的选项。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0db09fc73f8342a28766f3dd9fb2dcb8.png#pic_center)

- <kbd>Proximity Button 接近按钮</kbd>：一个常见的任务是需要按下按钮。物理按钮比平面界面更令人满意，但物理交互系统可能很快变得复杂起来。我们没有深入探讨这个问题，而是包含了一个只要靠近控制器就可以按下的按钮。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e065255f22684198928bb1c02ed1f51e.png#pic_center)

- <kbd>Interesting Interactables 有趣的交互</kbd>：这些是使用 Skeleton Poser 系统和 Throwables 的稍微复杂的例子。 使用手榴弹，您将获得两种不同的姿势，具体取决于您如何拿起它们。 Happy Ball 在您的手中移动并挤压。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b44c2f0b46e241829a55060973d723d7.png#pic_center)

- <kbd>UI & Hints UI和提示</kbd>：这显示了如何在交互系统中处理提示，以及如何使用它与按钮等 Unity UI 小部件进行交互。

![在这里插入图片描述](https://img-blog.csdnimg.cn/35a54e9c41c440ba971ac2b6f7e7727f.png#pic_center)

- <kbd>LinearDrive 直线驱动</kbd>：这是一个稍微复杂一些的交互，它结合了一些不同的部分来创建一个可以由简单交互控制的动画对象。

![在这里插入图片描述](https://img-blog.csdnimg.cn/8b81e244a31d4ee28e0906c8f34a9e2a.png#pic_center)

- <kbd>CircularDrive 环形驱动</kbd>：这展示了如何对交互进行约束并以不同的方式映射，从而导致更复杂的运动。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7ab3cfe18fa84ca59b842e4b7e62a59c.png#pic_center)

- <kbd>Longbow 长弓</kbd>：这是实验室中实际使用的长弓。 它现在已更新为输入系统和骨骼姿态。这是我们使用这一系统创造的较为复杂的对象之一，并展示了如何将简单的部件组合成一个完整的游戏机制。在这个示例场景中查看不同的对象可以让你更好地了解交互系统的广度，以及如何将其不同部分结合起来创造复杂的游戏对象。

![在这里插入图片描述](https://img-blog.csdnimg.cn/fa2c8ad77f25473fbe004f4b46bcbcdc.png#pic_center)

## 5.3 Documentation（文件）
&emsp;&emsp;现在我们将更深入地了解交互系统中包含的一些基本组件。 该系统分为几个不同的部分：

### 5.3.1 Core
&emsp;&emsp;交互系统的核心是 Player、Hand 和 Interactable 类。 提供的 Player 预制件为场景设置了 Player 对象和 SteamVR 相机。

- 交互系统通过向手交互的任何对象发送消息来工作。 然后，这些对象会对消息做出反应，并且可以根据需要将自己附着在手上。
- 要使任何对象从手接收消息，只需将 Interactable 组件添加到该对象即可。 当手进行悬停检查时，将考虑该对象。
- 我们还包含了一些常用的交互工具，例如 Throwable 或 LinearDrive。
- Player 预制件还创建了一个 InputModule，它允许手模仿鼠标事件以轻松使用 Unity UI 小部件。
- 交互系统还包括后退模式，允许使用键盘和鼠标进行典型的第一人称摄像机控制。 这也允许鼠标可以像玩家的一只手一样操作。 当并非团队中的每个人都可以使用 VR 头盔时，此模式特别有用。（2D Debug：点击后可以通过鼠标和键盘操作 Player 移动）

![在这里插入图片描述](https://img-blog.csdnimg.cn/670c6c82b5cf4c24b10894f5de7b0a0f.png#pic_center)

### 5.3.2 Player
&emsp;&emsp;Player 类就像一个单例对象，这意味着场景中应该只有一个 Player 对象。

- 除了跟踪手和 hmd（Head mounted display，头戴式显示器） 之外，Player 本身不会做太多事情。
- 它可以在整个项目中进行全局访问，交互系统的许多方面都假设 Player 对象始终存在于场景中。
- 它还可以跟踪您是处于 VR 模式还是 2D 后退模式。
- 通过 Player 类使用访问器允许其他组件在不知道是否使用 VR 头盔或鼠标/键盘的情况下同样运行。
- 2D 回退模式很有用，但也有其局限性。 我们主要使用这种模式来测试只需要一只手和触发按钮的非常简单的交互。 它主要在开发过程中很有用，因为并不是团队中的每个人都始终随身携带控制器上的 VR 头盔。
- Player 还包括一些有用的属性：
	
	- <kbd>hmdTransform</kbd>：这将始终返回当前相机的 Transform。 这可能是 VR 头盔或 2D 后置相机。
	- <kbd>feetPositionGuess</kbd>：这会根据 hmd 的位置猜测玩家脚的位置。 由于我们实际上并不知道他们脚的位置，因此取决于玩家的站立方式，这可能非常不准确。
	- <kbd>bodyDirectionGuess</kbd>：这与 feetPositionGuess 相似，因为它可能不准确

![在这里插入图片描述](https://img-blog.csdnimg.cn/5bc6e113870e431eaef1200b613222e3.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/6ed55a4589c64dd29bb00629fbdc4e9a.png#pic_center)


- 注意：Player 类设置为使用图标在编辑器场景视图中显示脚和手，但由于 Unity 的工作方式，这些图标必须位于特定文件夹中才能工作。 这些图标在核心/图标下提供。 将它们移动到项目资源树根目录中名为 “Gizmos” 的文件夹中，它们应该可以工作了。
- 2D 回退模式在测试过程中很有用，但您可能不想在完成的游戏中提供这种模式。 有两种方法可以禁用它：
	- 在进行构建之前，取消选中场景中玩家对象上的 “Allow Toggle To 2D” 布尔值。
	- 将 “HIDE_DEBUG_UI” 添加到项目 PlayerSettings 中的脚本定义符号列表中。 这只会禁用游戏构建中的 2D 调试视图，同时允许您在编辑器中继续使用它。

![在这里插入图片描述](https://img-blog.csdnimg.cn/ee64894ee1c6492e9452b50a893b9755.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/a55d825668f94f3989a8ccddb30d35f3.png#pic_center)

### 5.3.3 Hand
- Hand 类为交互系统承担了大部分繁重的工作。
- Hand 检查其悬停的对象（可交互对象）并根据当前悬停状态向它们发送消息。
- 手一次只能在一个物体上悬停，同时只能有一只手在一个物体上悬停。
- 对象可以附着在手上，也可以从手上分离出来。 手的焦点只能是一个物体，但可以同时有多个物体附着在手上。
- 一旦一个物体与手分离，那么之前附着在手上的物体（如果它仍然附着）成为手上聚焦的物体
- 当手上没有任何东西时，它将始终显示控制器。
- 附着的对象可以设置 AttachmentFlags 来确定手和被附着的对象（被抓取的物体）的行为。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7e3f421b6c94460a9bd00d3c053a650a.png#pic_center)


- 可以根据情况锁定手，以免悬停在其他物体或任何物体上。
- 这些是手发送给正在与之交互的对象的消息（messages）：
	- <kbd>OnHandHoverBegin</kbd>：当手刚开始悬停在对象上时发送
	- <kbd>HandHoverUpdate</kbd>：发送手悬停在对象上的每一帧
	- <kbd>OnHandHoverEnd</kbd>：当手停止悬停在对象上时发送
	- <kbd>OnAttachedToHand</kbd>：当对象附着到手时发送
	- <kbd>HandAttachedUpdate</kbd>：当对象附着在手上时每帧发送一次
	- <kbd>OnDetachedFromHand</kbd>：当对象从手上分离时发送
	- <kbd>OnHandFocusLost</kbd>：当附着对象失去焦点时发送，因为其他东西已附加到手上
	- <kbd>OnHandFocusAcquired</kbd>：当附着对象获得焦点时发送，因为前一个焦点对象已与手分离

![在这里插入图片描述](https://img-blog.csdnimg.cn/bf44a5eaa9c34421a572b769f81d1937.png#pic_center)

&emsp;&emsp;在添加 Interactable 脚本的对象上添加下面的脚本，通过手柄的交互获取手柄与物体交互时的 SendMessage。这里仅对部分进行演示：

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Valve.VR.InteractionSystem;

public class HandEvent : MonoBehaviour
{
    private void OnHandHoverBegin(Hand hand)
    {
        Debug.Log("当手刚开始悬停在对象上时发送-->" + hand.name);
    }

    private void HandHoverUpdate(Hand hand)
    {
        Debug.Log("发送手悬停在对象上的每一帧-->" + hand.name);
    }

    private void OnHandHoverEnd(Hand hand)
    {
        Debug.Log("当手停止悬停在对象上时发送-->" + hand.name);
    }
}
```



![在这里插入图片描述](https://img-blog.csdnimg.cn/0a26f0e151ec408da10ad6b3e3dab741.png#pic_center)



- 这些是手发送给其子对象的消息：
	- <kbd>OnHandInitialized</kbd>：当手第一次通过将自身与 SteamVR 跟踪控制器的设备 ID 相关联进行初始化时发送
	- <kbd>OnParentHandHoverBegin</kbd>：当手开始悬停在某物上时发送
	- <kbd>OnParentHandHoverEnd</kbd>：当手停止悬停在某物上时发送
	- <kbd>OnParentHandInputFocusAcquired</kbd>：当游戏窗口获得输入焦点时发送
	- <kbd>OnParentHandInputFocusLost</kbd>：当游戏窗口失去输入焦点时发送
- 这些成员处理附加和分离：
	- <kbd>AttachObject</kbd>：使用传入的 AttachmentFlags 从手上附加对象
	- <kbd>DetachObject</kbd>：从手上分离对象并可选择将其恢复到其原始父对象
	- <kbd>currentAttachedObject</kbd>：返回手上的焦点附加对象，如果有的话
- Hand 还具有一些有用的属性和功能，可用于自定义其行为：
	- <kbd>OtherHand</kbd>：这是玩家的另一只手。 这对于需要与双手交互的物体（例如长弓）很有用。
	- <kbd>HoverSphereTransform 和 Radius</kbd>：这可用于自定义手的悬停范围。
	- <kbd>HoverLayerMask</kbd>：可以更改此设置，以便手仅悬停在某些图层中的对象上。
	- <kbd>HoverUpdateInterval</kbd>：根据您的游戏要求，可以或多或少地进行悬停检查。
	- <kbd>HoverLock/Unlock</kbd>：这用于使手仅悬停在某个对象上。 传入 null 将使手在悬停锁定时不会悬停在任何东西上。 此技术用于在传送弧处于活动状态时使手不会悬停在物体上。
	- <kbd>GetGrabStarting/GetGrabEnding</kbd>：这些用于确定当时是否正在触发布尔抓取操作。 有两种类型的抓斗 - 抓握和捏抓抓。 这些通常与手柄按钮和触发按钮相关联，但在 Knuckles 控制器上具有特殊功能。
	- <kbd>GetAttachmentTransform</kbd>：对象可以使用手上的“附件变换”来确定如何捕捉到手。 这些只是 Hand 对象的命名子对象。 Player 预制件包含 “Attach_ControllerTip” 作为示例。

![在这里插入图片描述](https://img-blog.csdnimg.cn/56e7e0e71ae942ebb2a3cfb7f9ea1f82.png#pic_center)

### 5.3.4 Interactable
- Interactable 类更像是一个标识符。 它向手标识此对象是可交互的。
- 任何带有此组件的对象都会收到来自 Hand 的相关消息。

**总结：**<kbd>可以给场景中的物体添加 Interactable 脚本标明物体是可以交互的。添加脚本后，当手接近物体时，物体边缘黄色高亮，提示物体能够进行交互。</kbd>

![在这里插入图片描述](https://img-blog.csdnimg.cn/cb22536544574260bc61d0edfa7ef3b2.png#pic_center)

### 5.3.5 Throwable
- 这是最基本的交互对象之一。
- 当一只手悬停在该物体上并按下其中一个抓取按钮（通常是扳机或抓握）时，玩家可以捡起该物体。
- 物体附着在手上并在按下按钮时保持在那里。
- 当按钮被释放时，手中的任何速度都会被赋予抛出的物体。
- 这使您可以创建可以拾取和投掷的基本对象。

**注意：**<kbd>Throwable 脚本需要配合刚体组件一起使用。当物体身上没有挂载刚体组件时，添加 Throwable 脚本时会自动帮物体挂载刚体组件</kbd>

**补充：**<kbd>Throwable 脚本一般与 Interactable 脚本一起使用，用来创建可交互的游戏物体</kbd>

&emsp;&emsp;在示例场景中，我们可以通过 Throwing 处的示例了解 Throwable 脚本的使用：

![在这里插入图片描述](https://img-blog.csdnimg.cn/3c807c1d7e2243fb91db1bd31ff98f71.png#pic_center)

&emsp;&emsp;其中，物体投掷时的速度估算模式可以在 Inspector 面板进行设置：

![在这里插入图片描述](https://img-blog.csdnimg.cn/5a7820739750424a9ece0044e878a2c0.png#pic_center)
|释放速度类型|详细|
|--|--|
|Get From Hand|从手部获取速度|
|Short Estimation|在释放时，将基于前三帧估计速度|
|Advanced Estimation|在释放时，将找到你投掷的峰值速度，并根据周围的三个帧估计速度|

&emsp;&emsp;在 Throwable 脚本中，我们还可以设置物体抓取时是否穿过物体。通过设置我们可以在抓取物体时使得手以及物体无法穿透场景中的其他物体。

|可以穿透|无法穿透|
|--|--|
|  ![在这里插入图片描述](https://img-blog.csdnimg.cn/50ab10e734a141d4af6eb5ec1b994413.png)| ![在这里插入图片描述](https://img-blog.csdnimg.cn/5e8230a3db324952bbb5c13264f50641.png)|

&emsp;&emsp;我们可以在 Inspector 面板利用 AttachmentFlags 参数进行设置，相关参数对应左右如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/8ca53e72e20e42f89fa406cb8ac9a8bf.png#pic_center)

&emsp;&emsp;在开发过程中，我们根据需要对 AttachmentFlags 进行部分选择来达到我们要的交互效果。例如，实现按动一下扳机键拾取，再按动一下扳机键放下。

### 5.3.6 LinearDrive
- 这允许用手在开始位置和结束位置之间移动对象。
- 对象的当前位置用于设置一个 LinearMapping。

![在这里插入图片描述](https://img-blog.csdnimg.cn/63628039e8ea459fa69bee22f3e224b4.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/4381a222249b4ee68f565564da0b3ce0.png#pic_center)
### 5.3.7 CircularDrive
- 这允许手以圆周运动的方式移动物体。
- 对象的当前位置用于设置一个 LinearMapping。

![在这里插入图片描述](https://img-blog.csdnimg.cn/050038990f824fdabfb6c12dbf9e385f.png#pic_center)
### 5.3.8 LinearMapping
- 这是一个由 LinearDrive 或 CircularDrive 设置的数字。
- 该映射可用于将简单的手部交互映射为更复杂的行为。
- Longbow 中的弦就是一个例子，它使用 LinearMapping 将弓弦的拉动映射到长弓回拉动画。
- 其他几个类使用映射来插入它们的属性
	- LinearAnimation
	- LinearAnimator
	- LinearBlendShape
	- LinearDisplacement
	- HapticRack
### 5.3.9 VelocityEstimator
- 此类可用于根据对象位置的变化来估计对象的速度和加速度。
- 在大多数情况下，如果您从实际控制器获得速度和加速度，您将获得更准确的结果，但有时这是不可能的，例如在使用 2D 回退模式下的 “手（鼠标）” 时。

![在这里插入图片描述](https://img-blog.csdnimg.cn/526fc7b700544d4a93cd0521d1508d63.png#pic_center)
### 5.3.10 IgnoreHovering
- 如果您希望在执行悬停检查时手将其忽略，则可以将其添加到对象或特定碰撞器。

### 5.3.11 UIElement
- 将这个组件添加到现有的UI小部件中，手就可以与它进行交互了。
- 这将根据手部交互生成鼠标悬停和单击事件，并通过 Unity 事件系统将它们发送到现有 UI 小部件。
- 此外，它还将生成一个 OnHandClick 事件，该事件也将传递给单击元素的手。

### 5.3.12 ItemPackage
- ItemPackage 是旨在暂时覆盖手部功能的对象的集合。
- 长弓就是一个例子。 当长弓附在手上时，它接管了手的基本功能。
- ItemPackages 的概念是能够被捡起并放回它们被捡起的地方。
- 一旦被捡起，它们就会一直附着在手上，直到放回原处。 无需按住按钮即可将它们固定在手上。 手仍然像正常一样传递消息，但这些对象通常会禁用手的一些基本功能，例如在它们附着时悬停。
- The Lab 的 ItemPackage 的其他示例是气球工具或 Xortex 无人机控制器。 这两个对象在连接时都会接管手的基本功能。
- ItemPackage 可以是 1 个手或 2 个手。
### 5.3.13 ItemPackageSpawner
- 这将处理何时生成和收起 ItemPackage 以及如何在生成后将项目附加到手的逻辑。
- 它还处理在拾取时显示项目的预览或项目的轮廓。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7d5b8ab987a64c3790c10de028dbbacc.png#pic_center)
### 5.3.14 ItemPackageReference
- 可以将此组件添加到项目中，以表明它是项目包的一部分。

### 5.3.15 PlaySound
- 此类允许使用更多参数播放 AudioClips。
- 可以接收多个AudioClips，每次随机播放1个。
- 它还可以随机播放剪辑。

### 5.3.16 SoundPlayOneShot
- 该类专门针对只播放一次且不循环播放或播放时需要暂停的声音。

![在这里插入图片描述](https://img-blog.csdnimg.cn/27cf647104e54a48b994e695a6d3660a.png#pic_center)

### 5.3.17 Util
- 这是一个充满整个交互系统使用的小型实用函数的类。

### 5.3.18 InteractableHoverEvents
- 此类在接收到来自手的消息时生成 UnityEvents。
### 5.3.19 InteractableButtonEvents
- 此类将控制器按钮输入转换为 UnityEvents。
### 5.3.20 ComplexThrowable
- 本类使用物理关节而不是简单的父方法将物体附着在手上。
- 这允许在附加对象后与对象进行更多基于物理的交互。
- 注意：这个类有点实验性质。 由于我们并没有在 The Lab 中真正使用它，因此它可能功能不完整并且可能有问题。
### 5.3.21 DistanceHaptics
- 根据 2 个变换之间的距离触发触觉脉冲。
### 5.3.22 Player (Prefab)
- 这是交互系统的单一部分，结合了其所有基本部分。
- 这个预制件以某种方式安排了玩家和手，使它们都可以轻松访问。
- 它还包含 SteamVR 和 2D 回退系统的所有设置
- 交互系统的大多数其他组件取决于玩家。
- 一个场景中应该只有其中 1 个。
### 5.3.23 BlankController (Prefab)
- 当手没有其他任何东西时，它会被使用。
- 控制器的渲染模型是通过 SteamVR 加载的，所有部件都是连接在一起的。
## 5.4 Teleport（传送）
- The Lab 的传送系统支持传送到特定传送点或更一般的传送区域。
- 重要的类是 Teleport、TeleportPoint 和 TeleportArea。
- 所有功能都包含在 Teleport/Prefabs 中的 Teleporting 预制件中。 该预制件包括传送系统运行的所有逻辑。
- 将 TeleportPoints 或 TeleportAreas 添加到场景中以添加玩家可以传送到的地点。


### 5.4.1 Teleport
- 这个类处理传送的大部分逻辑。
- 按下触摸板时，会显示传送指针。 如果释放触摸板时指针指向有效位置，则玩家会传送。
	- 可以在 2D 回退模式下按键盘上的 “T” 来调出传送指针。
- 当玩家传送时，游戏会淡入淡出状态。
- 此类跟踪场景中的所有传送标记，并根据传送指针的状态通知它们淡入/淡出。
- 在某些情况下，对于地面场景使用一个不同于传送网格的单独网格是很有用的。 在这些情况下，传送系统将从它击中传送网格的位置开始追踪，并尝试将玩家放置在地板网格上。 这样做的目的是尝试将场景中的视觉地板与玩家游戏区域中的物理地板匹配起来。
- 有一些属性可能需要调整：
	- <kbd>tracerLayerMask</kbd>：这是传送指针将尝试击中的所有层
	- <kbd>floorFixupMask</kbd>：地板所在的层。
	- <kbd>floorFixupMaximumTraceDistance</kbd>：查找地板的最大跟踪距离。
	- <kbd>ShowPlayAreaMarker</kbd>：切换是否在传送时显示玩家游戏区域的矩形。 这可以帮助在他们的物理空间中定位玩家。
	- <kbd>arcDistance</kbd>：传送弧应该走多远。 增加这个数字将允许玩家在场景中传送得更远。 这个值可能需要针对每个场景进行调整。

![在这里插入图片描述](https://img-blog.csdnimg.cn/561406a15ea2473180a8bd4989a96830.png#pic_center)

### 5.4.2 TeleportMarkerBase
- 这是所有传送标记的基类。
- 它包含 Teleport 类希望出现在所有传送标记中的方法。
- 你可以使用它作为你的基类来创建一种新型的传送标记。
- 传送标记可以被锁定或解锁。 玩家无法传送到锁定的标记。

### 5.4.3 TeleportArea
- 这是一个由网格组成的传送区域。
- 当传送到这些时，玩家将准确传送到他们指向的位置（加上地板固定）
- 将此组件添加到具有碰撞器和网格渲染器的任何对象，以允许玩家在其上传送。

![在这里插入图片描述](https://img-blog.csdnimg.cn/1161952ce69943dabd378572d74ee132.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5bCP5LqM5LiK6YWSIFR-VA==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
&emsp;&emsp;**[注]：需要事先将 Teleporting 预制体拖拽至场景中！否则即使添加脚本也无法实现传送功能。针对 TeleportPoint 也是类似的，也需要事先将该预制体拖拽至场景中。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/4c2d7c93f9224a158e51fe386237ed8d.png#pic_center)


### 5.4.4 TeleportPoint
- 这是玩家可以传送到的传送点。
- 当传送到这些上时，玩家将传送到该点的原点，而不管他们指向的点。
- 这些点可以命名。
- 这些点还具有将玩家传送到新场景的能力。 （这不是功能齐全的，因为您必须将其连接到场景加载系统。）

![在这里插入图片描述](https://img-blog.csdnimg.cn/115d2bd8f3114c9fac38fafd23c5f65e.png#pic_center)

### 5.4.5 TeleportArc
- 这会为传送指针绘制弧线并为传送系统进行物理跟踪。
### 5.4.6 AllowTeleportWhileAttachedToHand
- 默认情况下，您无法使用附有物品的手进行传送。 将此组件添加到附加对象会绕过该规则。
- 这由 BlankController 和 longbow Arrow 对象使用，以便玩家即使在它们附着在手上时也可以传送。
### 5.4.7 IgnoreTeleportTrace
- 将此添加到具有碰撞器的对象将允许传送轨迹穿过它。
- 处理此问题的另一种方法是将该对象放在 TeleportArc 不检查的不同层上。
- 这用于长弓箭以允许传送轨迹穿过箭尖。
### 5.4.8 Teleporting (Prefab)
- 这个预制件设置了整个传送系统。
- 将它拖到您的场景中将使您能够在游戏中调出传送指针。
- 传送系统的所有视觉和声音都可以通过修改这个预制件的属性来改变。
### 5.4.9 TeleportPoint (Prefab)
- 将这些添加到您的场景中以添加玩家可以传送到的位置。
- 注意：此场景中的某些对象的名称是硬编码的，如果要更改模型，则需要修改某些代码。
## 5.5 Render Model（渲染模型）
与<kbd>SteamVR_Render_Model</kbd>组件不同，交互系统中的这个<kbd>Render_Model</kbd>组件处理控制器模型和手部模型，并单独启用/禁用它们。
### 5.5.1 Hints
- 提示系统在控制器上显示提示。
- 提示的设置方式可以单独调用控制器上的每个按钮。
- 还可以显示与每个按钮相关的文本提示。
### 5.5.2 ControllerButtonHints
- 提示是根据控制器的渲染模型设置的。
- SteamVR 提供了从渲染模型组件到按钮 ID 的映射。 此映射用于确定控制器的哪个部分对应于哪个按钮。
- 激活按钮提示后，该按钮将在控制器模型上持续闪烁，直到提示关闭。
- 提示可以仅用于按钮，也可以带有与按钮关联的可选文本提示。
- 有一些静态方法用于与提示系统交互：
	- <kbd>ShowButtonHint</kbd>：使指定手上的指定按钮闪烁。
	- <kbd>HideButtonHint</kbd>：停止闪烁指定手上的指定按钮。
	- <kbd>HideAllButtonHints</kbd>：停止闪烁指定手上的所有按钮。
	- <kbd>IsButtonHintActive</kbd>：检查指定的按钮是否在指定的手上闪烁。
	- <kbd>ShowTextHint</kbd>：显示带有与指定手上的指定按钮相关联的传入字符串的文本提示。
	- <kbd>HideTextHint</kbd>：隐藏指定按钮上指定手的文本提示。
	- <kbd>HideAllTextHints</kbd>：隐藏指定手牌上当前活动的所有文本提示。
	- <kbd>GetActiveHintText</kbd>：获取指定按钮的活动提示文本。
### 5.5.3 Longbow
- Longbow 是使用交互系统创建的复杂游戏机制的一个例子。
- 此处包含的版本与我们在 The Lab 中提供的版本完全相同，包括所有模型、材料和声音。
- Longbow 是使用 ItemPackage 系统构建的。 它由 LongbowItemPackage 预制件组成，该预制件在主手生成 Longbow 预制件，在另一手生成 ArrowHand 预制件。
- 每次发射箭头时，ArrowHand 预制件都会在手中生成一个新的箭头。
- 所有弓箭逻辑都存在于以下脚本中：
#### 5.5.3.1 Longbow.cs
- 它处理弓在无锁定和无锁定模式下如何控制的逻辑
- 它还跟踪拉弓弦的距离
#### 5.5.3.2 ArrowHand.cs
- 根据箭头的位置和控制器按钮处理箭矢和发射箭矢
- 处理在需要时在手中产生箭头
#### 5.5.3.3 Arrow.cs
- 被发射的实际箭头
- 该脚本处理箭头的所有飞行逻辑，包括碰撞检测和决定何时坚持目标
#### 5.5.3.4 ArrowheadRotation.cs
- 每次产生新箭头时随机旋转箭头
#### 5.5.3.5 SoundBowClick
- 播放拉弓弦的声音。
- Longbow 文件夹中的其他脚本处理长弓目标的逻辑
#### 5.5.3.6 ArcheryTarget.cs
- 这是通用射箭目标的脚本。
- 它在被箭头击中时调用 UnityEvent。
#### 5.5.3.7 FireSource.cs
- 表示可以点燃的对象。 一旦着火，这个物体就会在与另一个 FireSource 接触时传播火势。
#### 5.5.3.8 ExplosionWobble.cs
- 用于使射箭目标（箭靶）摆动。
#### 5.5.3.9 Balloon.cs
#### 5.5.3.10 BalloonColliders.cs
#### 5.5.3.11 BalloonHapticBump.cs
#### 5.5.3.12 BalloonSpawner.cs
- 这些脚本处理当 weeble 被箭头击中时产生的气球的逻辑。

## 5.6 Samples（示例）
- 有一些类是专门为在示例场景中显示一些示例而创建的。
### 5.6.1 ControllerHintsExample
- 这个类展示了如何使用提示系统。
### 5.6.2 InteractableExample
- 这个类展示了一个非常简单的接收和响应来自手的消息的例子。
