# Master Blockchain
## Solidity 面试题集

### 一、语言特性和设计模式

1. view 和 pure 的区别
2. payable 关键字的用途及注意事项
3. receive 和 fallback 函数的用法详解
4. call() 与 transfer() 的区别对比
5. 如何通过结构化存储解决代理合约的存储冲突？（需说明 slot 分配原理与 EIP-1967 实现）
6. 对比 CREATE 与 CREATE2 的地址生成算法，说明后者在确定性部署中的应用场景
7. 解释 Solidity 0.8.0 算术运算的溢出检查机制，何时应使用 unchecked 块优化 Gas？
8. 设计可升级合约时，如何避免函数选择器冲突？（需分析 4 字节哈希碰撞概率）
9. 为什么 abi.encodePacked 可能引发哈希碰撞？给出安全替代方案
10. 如何实现一个 Gas 高效的动态数组迭代器？（需对比 storage/memory 访问成本）
11. 解释 external 与 public 函数在 EVM 调用层面的区别，为何外部调用优先用 external？
12. 设计一个支持批量转账的 ERC20 扩展合约，需解决 Gas 消耗线性增长问题
13. 为什么 Solidity 废弃 years 时间单位？给出精确计算时间间隔的最佳实践
14. 如何通过 assembly 内联汇编优化 Keccak256 计算？（需对比 Solidity 原生实现）
15. 解释 pragma solidity ^0.8.0 中 ^ 符号的含义（版本兼容性规则）
16. 对比 memory 与 storage 变量的生命周期与 Gas 成本差异
17. 列出 Solidity 支持的 5 种值类型（value types）及其默认值
18. 为什么 string 类型不能直接比较？安全比较的方法是什么？
19. 说明 view 和 pure 函数的区别，各举一个应用场景
20. 如何声明一个可接收 ETH 的函数？需使用哪个关键字？
21. 描述 mapping 的底层存储机制，为何查询效率是 O(1)？
22. 说明 enum 类型的用途，并给出一个状态机实现的例子
23. 解释 fallback 和 receive 函数的触发条件与区别
24. 为什么 bytes1 比 string 存储短文本更省 Gas？
25. 说明 delete 操作符对 mapping 和 array 的不同作用
26. 解释 immutable 与 constant 变量的异同
27. 合约构造函数 constructor 与普通函数的执行差异
28. 如何通过 modifier 实现权限检查？写出一个 onlyOwner 修饰器
29. 如何在合约中实现链式调用（如 obj.setA(1).setB(2)）？


### 二、安全漏洞与防御

1. 什么是重入攻击，如何避免重入攻击
2. 分析重入攻击在 ERC777 中的特殊风险，给出基于检查-效果-交互模式的防御代码
3. 为什么 selfdestruct 可能破坏代理合约逻辑？如何设计防自杀机制？
4. 解释闪电贷攻击的三步利用链条，列举 3 种 DeFi 协议中的防御策略
5. 如何通过 commit-reveal 方案防止抢跑（frontrunning）？计算其时间成本
6. 设计一个防篡改的随机数生成器，需解决区块时间戳操纵问题
7. 为什么 delegatecall 会导致 msg.sender 链式传递异常？画图说明调用栈变化
8. 列举 EIP-712 签名验证中可能出现的 5 种中间人攻击方式
9. 如何检测并修复 ERC20 的 approve 竞态条件漏洞？
10. 解释 gas griefing 攻击原理，给出合约间调用的 Gas 限制策略
11. 分析 tx.origin 与 msg.sender 的滥用风险，给出身份验证最佳实践
12. 解释 msg.sender 与 tx.origin 的区别及安全风险
13. 分析 transfer、send 和 call 转账方式的 Gas 与安全性差异
14. 设计防重入锁的三种实现方式（布尔锁、检查-效果-交互、OpenZeppelin 库）
15. 为什么 selfdestruct 可能破坏合约逻辑？如何防范？
16. 分析 ERC20 的 approve 竞态条件漏洞及解决方案
17. 为什么链上随机数生成依赖 blockhash 不安全？改进方案
18. 分析闪电贷的三步攻击模式及 DeFi 协议防御策略
19. 设计一个基于 commit-reveal 的防抢跑（frontrunning）方案
20. 为什么 extcodesize 检查无法防止构造函数中的攻击？
21. 解释代理合约的存储冲突问题及 EIP-1967 解决方案


### 三、EVM 底层与 Gas 优化

1. 计算 SSTORE 从零值到非零值的 Gas 消耗公式，解释 EIP-3529 的影响
2. 为什么 extcodesize 检查无法阻止合约创建期间的攻击？
3. 分析 JUMP 与 JUMPI 指令在 EVM 执行中的 Gas 差异，如何优化控制流？
4. 设计一个 Gas 成本恒定的动态数组扩容算法（需考虑 Slot 打包）
5. 解释 warm/cold 存储访问的 2100 Gas 差异，如何预热关键地址？
6. 如何通过 bitmask 压缩多个布尔状态变量以减少 SLOAD 次数？
7. 对比 memory 与 calldata 的 ABI 编码差异，说明何时应强制使用 calldata
8. 计算 EIP-1559 的 BASEFEE 动态调整公式，分析其对 Gas 竞价的影响
9. 为什么 log 事件比 storage 更省 Gas？给出事件数据分片存储方案
10. 设计一个支持批量验证的 Merkle Proof 处理器，优化链上计算成本
11. 计算 1 ether 等于多少 wei 和 gwei？
12. 为什么 Solidity 不支持浮点数运算？替代方案是什么？
13. 如何安全生成 0 到 100 的随机数？分析其局限性
14. 为什么 now 关键字被废弃？替代方案是什么？
15. 设计一个 Gas 优化的动态数组扩容算法（考虑 Slot 打包）
16. 对比 assert 与 require 的异常处理机制及 Gas 消耗差异
17. 如何通过 assembly 内联汇编优化 keccak256 计算？
18. 解释 EIP-1559 的 BASEFEE 动态调整机制及其对 Gas 的影响
19. 如何实现跨合约调用时的 Gas 预留？分析 gasleft() 的使用
20. 解释 unchecked 块的使用场景及算术溢出风险
21. 如何通过位运算压缩多个布尔状态变量以减少存储开销？
22. 解释 warm/cold 存储访问的 Gas 差异及预热技巧
23. 计算一笔普通 ETH 转账交易的最低 Gas 消耗（含基础成本与计算成本）


### 四、协议标准与扩展

1. 实现 ERC721 的 _beforeTokenTransfer 钩子，防止非预期代币转移
2. 解释 ERC20 的 permit 功能如何通过离线签名节省 Gas？
3. 设计一个支持租赁功能的 ERC4907 扩展合约
4. 如何通过 ERC2771 实现元交易？分析转发合约的信任假设
5. 对比 ERC721A 与传统 ERC721 的批量铸造 Gas 效率差异
6. 实现一个符合 EIP-2612 的 Token，支持 nonce 防重放
7. 解释 ERC1155 的 _doSafeBatchTransferAcceptanceCheck 安全逻辑
8. 设计跨链 ERC20 桥接合约，解决双花问题
9. 如何通过 EIP-712 结构化哈希实现链下订单签名？
10. 分析 ERC4626 金库合约的滑点保护机制
11. 如何通过 event 记录合约日志？与直接存储相比的优势
12. 列出 3 个全局变量（如 block.timestamp）及其用途
13. 为什么 CREATE2 能实现确定性地址部署？给出应用场景
14. 如何实现合约的可升级性？分析透明代理与 UUPS 模式的优劣
15. 解释 delegatecall 的上下文保持特性及典型应用场景
16. 如何通过 struct 和 mapping 实现高效查询的用户管理系统？
17. 解释 EIP-712 结构化签名的工作原理及防重放机制
18. 设计一个支持批量转账的 ERC20 扩展合约，优化 Gas 消耗
19. 对比 ERC721 与 ERC1155 在批量交易中的 Gas 效率差异
20. 设计一个支持元交易的 ERC2771 合约，分析转发者信任问题
21. 分析 ERC4626 金库合约的滑点保护机制
22. 设计一个支持租赁功能的 ERC4907 扩展合约


### 五、高级架构与数学

1. 实现一个基于 ZK-SNARK 的匿名投票合约，需设计 Nullifier 机制
2. 解释椭圆曲线配对在预编译合约 ecadd 中的实现原理
3. 设计一个状态通道结算合约，支持多签名争议超时
4. 如何通过环签名实现混币器？计算其匿名集大小与 Gas 关系
5. 实现一个基于 VRF 的链上彩票合约，解决区块哈希预测问题
6. 解释 Plonk 验证合约的 Gas 成本主要来自哪些椭圆曲线操作？
7. 设计一个支持隐私存款的 Tornado Cash 改进版，解决监管合规问题
8. 如何通过多项式承诺优化 Merkle Tree 的链上验证？
9. 实现一个基于 EIP-4337 的账户抽象钱包合约
10. 分析 Optimistic Rollup 欺诈证明合约的 7 天挑战期安全假设