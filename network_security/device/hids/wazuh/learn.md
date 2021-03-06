# Wazuh 学习

Wazuh开源安全平台是一种多功能软件，可通过一组丰富的组件和集成来提供对环境安全性的了解。 鉴于Wazuh的高度适应性，它提供的可能性很多。在我们文档的这一部分，您将找到一系列渐进的动手经验，以加快您对Wazuh的掌握。 一些实验室将需要在以前的实验室中可以获得的技能，因此我们建议您按顺序进行。

## 准备您的Wazuh实验室环境

![1](_resources/vpc-diagram1.png)



## 检测SSH暴力攻击

在这里，您将对Linux Agent实例进行小的SSH蛮力攻击。 您将看到Wazuh如何检测和记录每个登录失败，以及在同一时间窗口中检测到来自同一源IP的足够登录失败时，如何生成更高严重性的警报。 您还将检查实际触发的规则以及随后可以在Kibana中看到的丰富警报记录。
