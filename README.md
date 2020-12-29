# 简介/Brief Introduction

LWS 是 light wallet service 的缩写，是架设在 BigBang Core 公有区块链主干网络和终端数据采集传感器设备之间的一座桥梁。通过它，BigBang Core 核心钱包的区块和交易数据及时地更新和缓存在 LWS 自有的高速内存数据库及本地数据库中。
根据这些数据，它会计算出不同终端设备持有密钥所对应的公钥地址的最新 UTXO 集合，并通过与 AWS 的 IoT Core 的 mqtt 连接，将这些信息发布（publish）到亚马逊云端设施上，由其 message broker 向对应的订阅（subscribe）了这些信息的终端设备转发。相应地，终端设备会根据这些与自己相关的 UTXO 列表，在获取了监控监测采集的数据后打包这些数据到交易中，通过 mqtt 发布到亚马逊 IoT Core。经由后者的 message broker 向订阅了这些设备的发送交易主题的 LWS推送，LWS 会校验这些交易，如果验证成功，则会通过 Socket API 向BigBang Core 核心钱包转发这部分交易，后者收到之后通过 P2P 网络接口向 BigBang Core 全网广播这些交易，出块节点收集这些交易，最终完成其打包区块上链的操作。

Light wallet service （a.k.a. LWS） is a bridge set up between the mainnet of the BigBang Core public blockchain and the data acquisition sensor. The BigBang Core‘s core wallet block and transaction data are instantly updated and cached in LWS’s built-in high-speed-memory database and local database. Based on those data, it will calculate the latest UTXO set of public key addresses corresponding to keys held by different end devices and will publish this information to Amazon cloud through the mqtt connection with AWS IoT Core. the message broker forwards it to the device that has subscribed to the information. Correspondingly, according to these UTXO lists related to themselves, the end devices will package that information into transactions after acquiring monitored and collected data and publish it on Amazon’s IoT Core through mqtt. The latter’s message broker makes transaction-themed LWS pushes to devices that have subscribed. The LWS will verify these transactions, Once verified successfully, it will pass on these transactions to BigBang Core’s core wallet through Socket API. The receiver will broadcast these transactions to BigBang Core through the P2P network after receiving it. The producer collects these transactions and finally completes the operation of its packaging block on the chain.

白皮书/White Paper：  

中文：https://www.bigbangcore.com/whitepaper/BigBang_Technical_WhitePaper.pdf  
English：https://www.bigbangcore.com/whitepaper/BigBang_Technical_WhitePaper_EN.pdf

操作文档（Wiki）地址：
https://github.com/bigbangcore/LWS/wiki
