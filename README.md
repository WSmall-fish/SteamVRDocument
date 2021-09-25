# SteamVRDocument

This article is based on the translation of SteamVR plug-in development document and summarizes the basic usage of SteamVR development process.

本文档基于 SteamVR 插件的开发文档翻译并总结 SteamVR 开发过程中的基本用法。本文总结汇总了 SteamVR 插件文档的内容，对文档部分内容进行了删减。目前仅仅只是翻译汇总，部分内容可能存在纰漏，后续会结合开发过程逐步更新修改此文章的内容。本文的 SteamVR 版本为 2.7.3，配套头戴式设备为 HTC VIVE 2.0Pro。

**插件官方文档地址：**[https://valvesoftware.github.io/steamvr_unity_plugin/articles/intro.html](https://valvesoftware.github.io/steamvr_unity_plugin/articles/intro.html)

---
### 文档目录

#### 1. Quickstart（快速开始）

    1.1 Download（下载插件）
    1.2 SteamVR Input Window（输入窗口）
    1.3 Copy JSONs（复制 JSON）
    1.4 Save and Generate（保存并生成）
    1.5 Interaction System（交互系统）

#### 2. Render Models（渲染模式）

    2.1 The Component（组件）
    2.2 Attaching Objects（附着对象）
    2.3 Notes（注意）

#### 3. SteamVR Input（输入系统）

    3.1 Boolean 类型
    3.2 Single 类型
    3.3 Vector2 类型
    3.4 Vector3 类型
    3.5 Pose 类型
    3.6 Skeleton 类型
    3.7 Vibration 类型
    3.8 Using actions（动作使用）
    3.9 New action sets（新建动作集）

#### 4. Skeleton Input（骨骼输入）

    4.1 Range Of Motion（运动范围）
    4.2 Skeletal Transform Space（骨骼变换空间）
    4.3 Finger Curls（手指弯曲）
    4.3 Finger Splays（手指伸展）
    4.4 Skeletal Tracking Level（骨骼跟踪级别）
    4.5 SteamVR_Behaviour_Skeleton
    4.6 SteamVR_Behaviour_Skeleton Events

#### 5. Interaction System（交互系统）

    5.1 Getting started（入门指南）
    5.2 Sample scene（示例场景）
    5.3 Documentation（文件）
        5.3.1 Core
        5.3.2 Player
        5.3.3 Hand
        5.3.4 Interactable
        5.3.5 Throwable
        5.3.6 LinearDrive
        5.3.7 CircularDrive
        5.3.8 LinearMapping
        5.3.9 VelocityEstimator
        5.3.10 IgnoreHovering
        5.3.11 UIElement
        5.3.12 ItemPackage
        5.3.13 ItemPackageSpawner
        5.3.14 ItemPackageReference
        5.3.15 PlaySound
        5.3.16 SoundPlayOneShot
        5.3.17 Util
        5.3.18 InteractableHoverEvents
        5.3.19 InteractableButtonEvents
        5.3.20 ComplexThrowable
        5.3.21 DistanceHaptics
        5.3.22 Player (Prefab)
        5.3.23 BlankController (Prefab)
    5.4 Teleport（传送）
        5.4.1 Teleport
        5.4.2 TeleportMarkerBase
        5.4.3 TeleportArea
        5.4.4 TeleportPoint
        5.4.5 TeleportArc
        5.4.6 AllowTeleportWhileAttachedToHand
        5.4.7 IgnoreTeleportTrace
        5.4.8 Teleporting (Prefab)
        5.4.9 TeleportPoint (Prefab)
    5.5 Render Model（渲染模型）
        5.5.1 Hints
        5.5.2 ControllerButtonHints
        5.5.3 Longbow
            5.5.3.1 Longbow.cs
            5.5.3.2 ArrowHand.cs
            5.5.3.3 Arrow.cs
            5.5.3.4 ArrowheadRotation.cs
            5.5.3.5 SoundBowClick
            5.5.3.6 ArcheryTarget.cs
            5.5.3.7 FireSource.cs
            5.5.3.8 ExplosionWobble.cs
            5.5.3.9 Balloon.cs
            5.5.3.10 BalloonColliders.cs
            5.5.3.11 BalloonHapticBump.cs
            5.5.3.12 BalloonSpawner.cs
    5.6 Samples（示例）
        5.6.1 ControllerHintsExample
        5.6.2 InteractableExample

####  6. Skeleton Poser（骨骼姿态）

    6.1 The Basics（基本需求）
    6.2 Using the Skeleton Poser with the SteamVR Interaction system（将 Skeleton Poser 与 SteamVR 交互系统结合使用）
    6.3 Pose Editor（姿态编辑器）
    6.4 Blending Editor（混合编辑器）
    6.5 Manual Behaviours（手动行为）
    6.6 Scaling（缩放）
