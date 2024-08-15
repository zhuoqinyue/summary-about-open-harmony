# 总结

经过为期三个月的鸿蒙教学, 对鸿蒙 OS 也有一些新的理解, 下面围绕鸿蒙特性, 文档等做一些简要的总结

## 鸿蒙文档

截止目前该文档的撰写时间, `HarmonyOS NEXT` [文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases-V5/next-dev-beta-rn-V5) 可在官网看到 `Beta3` 版本的配套文档. 需要 `API 12 Beta3` 才可使用.

在 2024 开发者大会之前, 所有的文档以及编辑器, 模拟器, `sdk` 等都只能通过比赛以及内部渠道获取, 才可尝鲜. 所以 2024 开发者大会也是鸿蒙面向全世界开发者的一次里程碑节点.
[![开发者大会](/imgs/2024dev.png '2024 开发者大会')](https://developer.huawei.com/home/hdc/hdc2024.html?promotion_cid=1002)

现在想尝鲜鸿蒙的开发者已经可以再官网下载对应的套件资源, 一键安装.

### 方舟

开发鸿蒙 App, 你需要对一些术语有一个清晰的认知, 方舟大致包含三个部分, 也是构建一个鸿蒙 App 的基础

#### ArkTS（方舟编程语言）

ArkTS 是 HarmonyOS 优选的应用高级开发语言。ArkTS 提供了声明式 UI 范式、状态管理支持等相应的能力，让开发者可以以更简洁、更自然的方式开发应用。

它在保持 TypeScript 基本语法风格的基础上，进一步通过规范强化静态检查和分析，使得在程序运行之前的开发期能检测更多错误，提升代码健壮性，并实现更好的运行性能。

#### ArkUI（方舟 UI 框架）

ArkUI（方舟 UI 框架）为应用的 UI 开发提供了完整的基础设施，包括简洁的 UI 语法、丰富的 UI 功能（组件、布局、动画以及交互事件），以及实时界面预览工具等，可以支持开发者进行可视化界面开发。

针对不同的应用场景及技术背景，方舟UI框架提供了两种开发范式，分别是基于ArkTS的声明式开发范式（简称“声明式开发范式”）和兼容JS的类Web开发范式（简称“类Web开发范式”）。

- **声明式开发范式**：采用基于TypeScript声明式UI语法扩展而来的ArkTS语言，从组件、动画和状态管理三个维度提供UI绘制能力。

- **类Web开发范式**：采用经典的HML、CSS、JavaScript三段式开发方式，即使用HML标签文件搭建布局、使用CSS文件描述样式、使用JavaScript文件处理逻辑。该范式更符合于Web前端开发者的使用习惯，便于快速将已有的Web应用改造成方舟UI框架应


#### ArkWeb（方舟Web）
ArkWeb（方舟Web）提供了Web组件，用于在应用程序中显示Web页面内容，为开发者提供页面加载、页面交互、页面调试等能力。

- **页面加载**：Web组件提供基础的前端页面加载的能力，包括加载网络页面、本地页面、html格式文本数据。

- **页面交互**：Web组件提供丰富的页面交互的方式，包括：设置前端页面深色模式，新窗口中加载页面，位置权限管理，Cookie管理，应用侧使用前端页面JavaScript等能力。

- **页面调试**：Web组件支持使用Devtools工具调试前端页面。

### HELLO WORLD

现在来到老生常谈的 `hello world` 环节, 我们就根据文档的指引新建空白项目.

```ts
// index.ets
@Entry
@Component
struct Index {
    @State message: string = 'Hello World'
    build() {
        Row() {
            Column() {
                Text(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
            }
      .width('100%')
        }
    .height('100%')
    }
}
```

> 在查看文档的时候, 以及尝鲜时, 请把焦点放在 **`Stage` 模型**

### 页面跳转

页面间的导航可以通过页面路由 `router` 来实现。页面路由 `router` 根据页面 `url` 找到目标页面，从而实现跳转。使用页面路由请导入 `router` 模块。

```ts
import { router } from '@kit.ArkUI'
```

如果需要实现更好的转场动效，推荐使用 `Navigation`。

<br />

## 鸿蒙特性

这期间, 对鸿蒙特性也有所了解, 以下特性是鸿蒙开发者以及鸿蒙赛道上的参与者都可以去了解甚至深入挖掘的特性, 基于这些特性能够开发出更加符合现代化的鸿蒙 app.

- 分布式设备管理
- 意图框架(Intents Kit)
- 集成 AI

### 分布式设备管理简介

随着用户不同种类的终端设备数量不断增多，将不同设备作为本端设备能力的扩展，使设备之间协同合作完成各种复杂场景即为设备的分布式业务。

分布式设备管理提供如下四大功能：

1. **发现**
   发现周围终端设备并上报。周围设备需要连接同局域网或者同时打开蓝牙，可以根据设备类型、距离、设备是否可信等进行筛选。

2. **绑定**
   不同设备协同合作完成分布式业务的前提是设备间可信，对于周边发现的不可信设备，可通过绑定使彼此建立可信关系，提供 pin 码、碰、扫、靠等设备认证框架，支持对接各种认证交互接口。

3. **查询**
   查询功能包含：查询本机设备信息、查询周围的在线的可信设备、查询可信设备信息。

4. **监听**
   监听设备上、下线。设备上线表示设备间已经可信，业务可以发起分布式操作；设备下线表示分布业务不可用。

#### 约束与限制

使用设备管理能力，需要用户确认不同设备已连接同一局域网或者蓝牙开关已开启，否则该能力不可用。

设备信息属于用户敏感数据，所以即使用户已连接同一局域网或者蓝牙开关已开启，应用在获取设备位置前仍需向用户申请数据同步权限。在用户确认允许后，系统才会向应用提供设备管理能力。

#### 申请分布式权限

应用在使用分布式设备管理系统能力前，需要检查是否已经获取用户授权访问分布式数据同步信息。如未获得授权，可以向用户申请需要的分布式数据同步权限。

`ohos.permission.DISTRIBUTED_DATASYNC`：分布式数据同步权限

#### 开发指导

[设备发现开发指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/devicemanager-guidelines-V5#%E8%AE%BE%E5%A4%87%E5%8F%91%E7%8E%B0%E5%BC%80%E5%8F%91%E6%8C%87%E5%AF%BC)

<br/>

### 意图框架(Intents Kit)简介

Intents Kit（意图框架服务）是 HarmonyOS 级的意图标准体系 ，意图连接了应用/元服务内的业务功能。

你可以浅显的理解与 **douyin**, **bilibili** 的推荐方案类似, 但是实际上意图框架是在系统内做对应分发, 但是体验并不亚于上面所提及的平台.

意图框架能帮开发者将应用/元服务内的业务功能，智能分发到各系统入口，这个过程即智慧分发。其中系统入口包括：小艺对话、小艺搜索、小艺建议等。
![系统入口、意图框架、鸿蒙生态的关系](/imgs/yitu.png '对应关系')

#### 优势

利用 HarmonyOS 的大模型、多维设备感知等 AI 能力，准确且及时地获取到用户显性、潜在意图，从而实现个性化、多模态、精准的智慧分发。

#### 开发指导

以下有几种常用场景, 可参照以下对应方案:

- [习惯推荐方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/intents-habit-rec-V5)
- [事件推荐方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/intents-event-rec-V5)
- [本地搜索方案](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/intents-search-rec-V5)

<br/>

### AI 能力简介

鸿蒙 OS 的 AI 能力有多种场景, 也包括了意图框架, 这些 AI 能力不一一赘述, 可参考以下文档:

- [Core Speech Kit（基础语音服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/core-speech-kit-guide-V5)
- [Core Vision Kit（基础视觉服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/core-vision-kit-guide-V5)
- [HiAI Foundation Kit（HiAI Foundation 服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/hiai-foundation-kit-guide-V5)
- [Intents Kit（意图框架服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/intents-kit-guide-V5)
- [MindSpore Lite Kit（昇思推理框架服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/mindspore-lite-kit-V5)
- [Natural Language Kit（自然语言理解服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/natural-language-kit-guide-V5)
- [Neural Network Runtime Kit（Neural Network 运行时服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/neural-network-runtime-kit-V5)
- [Speech Kit（场景化语音服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/speech-kit-guide-V5)
- [Vision Kit（场景化视觉服务）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/vision-kit-guide-V5)

AI 抠图, AI 识物等更多现代化场景都均可在鸿蒙系统内部找到成熟的方案实现, 无需在赘加第三方库或者训练模型等.

<br />

## 鸿蒙上架

鸿蒙 App 上架是一件较为麻烦且繁琐的事情, 你需要**提前一个月**准备如下资料:

- 隐私条款
- App 备案
- 软件著作权

### 注意点

- 不是很建议个人开发者上架
- App 最好完善对应的鉴权以及登陆
- 能有接入广告的能力(但是接入广告的审核会更加严格)
