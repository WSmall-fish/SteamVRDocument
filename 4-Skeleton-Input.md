# 4 Skeleton Input（骨骼输入）

在 VR 中看到你的物理控制器很好，但人们真正想要的是能够看到他们的手。 随着 VR 控制器的进步，我们看到了截然不同的功能。 一些控制器只能按下按钮（无触摸），有些控制器甚至在半空中也能给出良好的手指估计，我们开始看到手套和相机具有完整的每个关节位置/旋转跟踪。 SteamVR Skeleton Input 为您提供了一个 API 来获取所有这些不同类型设备的每个关节数据。 对于数据较少的设备，我们根据按下的按钮估计手指位置，而对于更高级的控制器，数据只是通过。

## 4.1 Range Of Motion（运动范围）

我们有两个运动范围可供您获取骨骼数据。 如果您正在寻找精确到真实世界的数据，您可以使用<kbd>WithController</kbd>运动范围。 这意味着我们会在控制器允许的范围内尽可能地估计您的手指在现实世界中的位置。<kbd>WithoutController</kbd>为您提供从手指张开的扁平手到握成拳头的全方位范围。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5f74b01af306417e9b4757ac35a17208.png#pic_center)

| With Controller | Without Controller |
|--|--|
|![在这里插入图片描述](https://img-blog.csdnimg.cn/b4ab6dbf36b344c9b877b5e063ddd508.gif#pic_center)|![在这里插入图片描述](https://img-blog.csdnimg.cn/a461e135710a4c0b89d9c8db80f9c4eb.gif#pic_center) |

## 4.2 Skeletal Transform Space（骨骼变换空间）

根据您使用此数据的用例，您可能希望获得相对于不同事物的位置和旋转。 默认情况下，我们获得相对于它们的父级的位置和旋转。 但是您也可以相对于模型获取它们。

## 4.3 Finger Curls（手指弯曲）

对于某些事情，访问手指卷曲程度的概要可能更有用，而不是每个手指上 4 个关节的位置和旋转。 这些值的范围从 0 到 1，其中 1 表示完全卷曲。 您可以在<kbd>skeletonAction.fingerCurls[]</kbd>以数组的形式访问<kbd>curl</kbd>信息，或者在<kbd>skeletonAction.indexCurl</kbd>、<kbd>skeletonAction.middleCurl</kbd>、<kbd>skeletonAction.RingCurl</kbd>、<kbd>skeletonAction.pinkyCurl</kbd>和<kbd>skeletonAction.thumbCurl</kbd>中单独命名。

## 4.3 Finger Splays（手指伸展）

了解手指之间的间隙也是一个常用的信息。 为此，我们以与 Curls（弯曲）类似的方式提供数据。 从 0 到 1 的范围表示手指之间的间隙大小。<kbd>skeletonAction.fingerSplays[]</kbd>作为数组，或单独命名为<kbd>skeletonAction.thumbIndexSplay</kbd>、<kbd>indexMiddleSplay</kbd>、<kbd>middleRingSplay</kbd>和<kbd>ringPinkySplay</kbd>。

## 4.4 Skeletal Tracking Level（骨骼跟踪级别）

不同的控制器具有不同的能力来跟踪手指的各个关节。 在这里，我们提供了一个概览值，可以让您大致了解当前控制器的保真度级别。

- <kbd>Estimated 预估</kbd>：设备无法直接确定身体部位的位置。 设备提供的任何骨骼姿势都是根据活动按钮、触发器、操纵杆或其他输入传感器估计的。 示例包括 Vive 控制器和游戏手柄。
- <kbd>Partial 局部</kbd>：可以直接测量身体部位的位置，但自由度比实际身体部位少。设备可能无法测量某些身体部位的位置，而是根据其他输入数据进行估计。示例包括仅测量手指卷曲度的指关节或手套。
- <kbd>Full 完整</kbd>：可以在身体部位的整个运动范围内直接测量身体部位的位置。示例包括高端动作捕捉系统或测量每个手指节段旋转的手套。

## 4.5 SteamVR_Behaviour_Skeleton

骨骼行为（skeleton behaviour）是一个组件，它使 unity 中常见的<kbd>Skeleton Input</kbd>任务变得更容易。 通过设置<kbd>skeletonAction</kbd>和<kbd>inputSource</kbd>你可以让行为为你做很多工作。

- <kbd>updatePose</kbd>：将此设置为 true 将在每次更新骨骼时在您的游戏空间中定位游戏对象。
- <kbd>mirroring</kbd>：如果此骨骼数据应跨 x 轴镜像。
- <kbd>SetRangeOfMotion(EVRSkeletalMotionRange newRangeOfMotion, float blendOverSeconds = 0.1f)</kbd>：为您提供一种简单的方法来混合一个新的运动范围。
- <kbd>BlendToSkeleton(float overTime = 0.1f)</kbd>：完全混合以使用骨骼数据为骨骼设置动画。
- <kbd>BlendToPoser(SteamVR_Skeleton_Poser poser, float overTime = 0.1f)</kbd>：完全混合以使用 Poser 为骨骼设置动画。
- <kbd>BlendToAnimation(float overTime = 0.1f)</kbd>：完全混合到预定义的 Unity 动画。
- <kbd>BlendTo(float blendToAmount, float overTime)</kbd>：允许您指定 poser/animation（姿势器/动画）数据和 skeleton input（骨骼输入）数据之间的混合程度。
- <kbd>Transform GetBone(int joint)</kbd>：通过关节索引 (SteamVR_Skeleton_JointIndexes) 返回特定骨骼的变换（Transform）。
- <kbd>ForceToReferencePose(EVRSkeletalReferencePose referencePose)</kbd>：强制骨骼进入 SteamVR 定义的特定参考姿势。 一般用于调试目的。
- <kbd>Vector3[] GetBonePositions()</kbd>：提供一个数组，其中包含请求的空间中的所有骨骼位置。
- <kbd>Quaternion[] GetBoneRotations()</kbd>：提供一个数组，其中包含请求的空间中所有骨骼旋转。

![在这里插入图片描述](https://img-blog.csdnimg.cn/b973fe3869d74363a6307eba0db1a912.png#pic_center)

## 4.6 SteamVR_Behaviour_Skeleton Events

有两种形式的骨骼行为（skeleton behaviour）有五个有用的事件。 您可以订阅 unity 事件或更传统的 C# 事件。 C# 事件的好处是大多数 IDE 会根据事件类型自动为您创建一个带有命名参数的函数。

- <kbd>onBoneTransformsUpdated</kbd>：在更新了骨转换之后，将会触发。
- <kbd>onTransformUpdated</kbd>：在更新了根转换之后，将触发。
- <kbd>onTransformChanged</kbd>：根变换更改后，将触发(移动/旋转)。
- <kbd>onConnectedChanged</kbd>：当设备连接或断开时，执行此动作。
- <kbd>onTrackingChanged</kbd>：每当此设备的跟踪状态发生更改时执行。

![在这里插入图片描述](https://img-blog.csdnimg.cn/71df42aefd754dbcab78e0f82ea3a161.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/77b60095f7cf469186ea1295c3a7b944.png#pic_center)
