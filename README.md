# Dapp开发指南
本文档为协会内部的Dapp开发指南，遵循本文档开发的Dapp可**完美接入协会钱包ZJUBCA.WALLET**，同时也兼容主流钱包(如Scatter,MEET.ONE等)。

在开发协会内部Dapp或内外通用的Dapp时，**请务必遵循本开发指南**。

## 基础设施
由于协会钱包主要基于[EOS麒麟测试网(kylin testnet)](https://github.com/cryptokylin/CryptoKylin-Testnet/blob/master/README_CN.md)。Dapp应优先适配kylin测试网。

## 前端
### 设计
#### 原则
1. 所有Dapp均以H5的形态接入协会钱包，因此Dapp**应优先适配移动端**。为了使Dapp更通用，我们推荐使用**响应式页面**。
2. 所有操作应是简洁、明确的，特别是**需要签名授权**的操作，在设计和流程上须简洁明了。

#### UI库
为了统一UI风格与减轻技术选型的成本，我们推荐以下UI框架：
- material-ui - 谷歌出品的设计语言
  - [vue-material](https://vuematerial.io)
  - [react-material](https://material-ui.com)
- ant-design - 蚂蚁金服著名前端框架，适合企业级中后台应用
  - [vue-ant-design](https://vue.ant.design/docs/vue/introduce-cn/)
  - [react-ant-design](https://ant.design/index-cn) 
- [element-ui](https://element.eleme.io/) - 饿了么出品，适合企业级中后台应用

### 技术
#### SDK
目前所有的Dapp均采用Scatter提供的SDK与区块链交互[官方文档](https://get-scatter.com/docs/getting-started)。协会钱包实现了Scatter几乎所有的[API接口](https://github.com/Blockchain-zju/zjubca.wallet#scatter-api-%E5%85%BC%E5%AE%B9scatterjs)。不同于Scatter的socket通信方案，协会钱包与Dapp的交互采用iframe间消息通信的方案实现（受限于ionic技术本身），但对应用层来说开发体验一致。

为了减轻Dapp开发者的负担，做到**code once, run everywhere**，我们专门对主流桌面钱包Scatter的SDK进行了二次开发。

**IMPORTANT!!!! 请Dapp开发者务必使用[zjubca-scatter-js](https://github.com/Blockchain-zju/zjubca-scatter-js)作为Dapp与区块链交互的SDK。** 如此可实现兼容协会钱包与市面上所有实现了Scatter接口的主流钱包。

对于eos.js的版本选择，我们**建议使用稳定的[v16.0.9](https://github.com/EOSIO/eosjs/tree/v16.0.9)**。

#### 框架
考虑到Dapp的复杂度及开发周期，为了统一协会内技术栈，降低协会开发者开发成本，我们优先推荐[vue.js](https://cn.vuejs.org/)。

您也可选用下列技术框架：

- [React](https://reactjs.org/)
- [Angular](https://angular.io/)

#### 注意事项
1. Dapp内涉及**发送交易**的操作，均会拉起钱包原生组件对交易进行签名，再交由Dapp端发送至区块链节点，因此**Dapp端须自行处理response**。
2. Dapp所用的网络节点与钱包**互相隔离，互不影响**。
3. 切忌用自己的公网私钥作为测试用私钥！！！（也不要用别人的）

## 合约
请忘了solidity,C/C++ 值得你拥有。

### 开发
[官方入门教程](https://developers.eos.io/eosio-home/docs)

为了更好的开发体验，我们推荐使用[js4eos](https://github.com/itleaks/js4eos/blob/master/README_zh.md)进行合约项目初始化与自动化测试。你也可以自行定义项目结构与开发范式。**非常欢迎在开发体验上贡献实践经验**。

### 资源开销
1. 由于测试网token可免费获得，出于对用户体验的考虑，我们**建议合约中涉及的所有RAM开销均由合约开发者自行承担**。
2. 开发者应合理设计合约代码以防止额外的资源开销。

### 合约安全
常见的合约攻击手段须避开。参考[智能合约攻击方式汇总](https://mp.weixin.qq.com/s?__biz=MzU1NDc3NDI5MQ==&mid=2247484619&idx=1&sn=1b3c2817487b52e5c68c06fbade72bb8&chksm=fbdf3eb7cca8b7a17daefa6ca01700a2df9afc0c0b697693f93d8194d4c6077b0ba0ab1b0a45&mpshare=1&scene=1&srcid=1110ESYf047WrCIqSVs1hRk7#rd)

## 案例
- [zjubca.vote](https://github.com/Blockchain-zju/zjubca.vote)

