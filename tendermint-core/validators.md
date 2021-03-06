# 验证者

验证者负责在区块链中提交新块。这些验证者通过广播 _votes_ 参与共识协议，其中包含由每个验证者的私钥签名的加密签名。

一些权益证明共识算法旨在创建一个“完全”分布式系统，让所有利益相关者（甚至那些不总是在线的）都参与提交块。
Tendermint 有一个不同的方法来创建块。验证者应该是在线的，并且验证者集由一些外部流程许可/管理。不需要权益证明，但可以在 Tendermint 协商一致的基础上执行。也就是说，验证者可能需要在链上、链外发布抵押品，或者根本不需要发布任何抵押品。

验证者有一个加密密钥对和相应数量的“投票权”。投票权不必相同。

## 成为一个验证者

有两种方法可以成为验证者。

1.  它们可以预先建立在[创世纪状态](./using-tendermint.md#genesis)
2.  ABCI 应用程序通过更改现有验证者集来响应 EndBlock 消息。

## 提交一个块

_+2/3 是 “大于2/3”的缩写_

在该块同一 `round` 上 +2/3 的验证者s设置签名[预提交投票](../spec/blockchain/blockchain.md#vote)时，将提交一个块。
+2/3 预提交投票组称为[_提交_](../spec/blockchain/blockchain.md#commit)。虽然在相同的高度和轮上为相同的块使用任意 +2/3 组预提交可以作为验证，但是在下一个块中包含公认的提交（请参见 [LastCommit](../spec/blockchain/blockchain.md#lastcommit)）。
