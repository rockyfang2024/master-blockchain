# master-blockchain
区块链面试题


## solidity

### 语言特性和设计模式

- view和pure的区别
- payable关键字的用途以及注意事项
- 讲讲receive和fallback函数的用法
- 讲讲call()和transfer()的区别
- ‌如何通过结构化存储解决代理合约的存储冲突？‌（需说明slot分配原理与EIP-1967实现）
- 对比CREATE与CREATE2的地址生成算法，说明后者在确定性部署中的应用场景
- 解释Solidity 0.8.0算术运算的溢出检查机制，何时应使用unchecked块优化Gas？
- 设计可升级合约时，如何避免函数选择器冲突？‌（需分析4字节哈希碰撞概率）
- 为什么abi.encodePacked可能引发哈希碰撞？给出安全替代方案‌‌13
- ‌如何实现一个Gas高效的动态数组迭代器？‌（需对比storage/memory访问成本）
- 解释external与public函数在EVM调用层面的区别，为何外部调用优先用external？
- ‌设计一个支持批量转账的ERC20扩展合约，需解决Gas消耗线性增长问题
- 为什么Solidity废弃years时间单位？给出精确计算时间间隔的最佳实践
- 如何通过assembly内联汇编优化Keccak256计算？‌（需对比Solidity原生实现）
- 解释pragma solidity .8.0中^符号的含义（版本兼容性规则）
- 对比memory与storage变量的生命周期与Gas成本差异
- 列出Solidity支持的5种值类型(value types)及其默认值
- 为什么string类型不能直接比较？安全比较的方法是什么？
- 说明view和pure函数的区别，各举一个应用场景
- 如何声明一个可接收ETH的函数？需使用哪个关键字？
- 描述mapping的底层存储机制，为何查询效率是O(1)？
- 说明enum类型的用途，并给出一个状态机实现的例子
- 解释fallback和receive函数的触发条件与区别
- 为什么bytes1比string存储短文本更省Gas？
- 说明delete操作符对mapping和array的不同作用
- 解释immutable与constant变量的异同
- 合约构造函数constructor与普通函数的执行差异
- 如何通过modifier实现权限检查？写出一个onlyOwner修饰器
- 如何在合约中实现链式调用（如obj.setA(1).setB(2)）？


### 安全漏洞与防御

- 什么是重入攻击，如何避免重入攻击
‌- 分析重入攻击在ERC777中的特殊风险，给出基于检查-效果-交互模式的防御代码
- 为什么selfdestruct可能破坏代理合约逻辑？如何设计防自杀机制？
- 解释闪电贷攻击的三步利用链条，列举3种DeFi协议中的防御策略
‌- 如何通过commit-reveal方案防止抢跑(frontrunning)？计算其时间成本‌‌
‌- 设计一个防篡改的随机数生成器，需解决区块时间戳操纵问题
‌- 为什么delegatecall会导致msg.sender链式传递异常？画图说明调用栈变化‌‌
‌- 列举EIP-712签名验证中可能出现的5种中间人攻击方式‌
- ‌如何检测并修复ERC20的approve竞态条件漏洞？
‌- 解释gas griefing攻击原理，给出合约间调用的Gas限制策略‌
‌- 分析tx.origin与msg.sender的滥用风险，给出身份验证最佳实践
- 解释msg.sender与tx.origin的区别及安全风险
- 分析transfer、send和call转账方式的Gas与安全性差异
- 设计防重入锁的三种实现方式（布尔锁、检查-效果-交互、OpenZeppelin库）
- 为什么selfdestruct可能破坏合约逻辑？如何防范？
- 分析ERC20的approve竞态条件漏洞及解决方案
- 为什么链上随机数生成依赖blockhash不安全？改进方案
- 分析闪电贷的三步攻击模式及DeFi协议防御策略
- 设计一个基于commit-reveal的防抢跑(frontrunning)方案
- 为什么extcodesize检查无法防止构造函数中的攻击？
- 解释代理合约的存储冲突问题及EIP-1967解决方案


### EVM底层与Gas优化

- 计算SSTORE从零值到非零值的Gas消耗公式，解释EIP-3529的影响
‌- 为什么extcodesize检查无法阻止合约创建期间的攻击？
‌- 分析JUMP与JUMPI指令在EVM执行中的Gas差异，如何优化控制流？
‌- 设计一个Gas成本恒定的动态数组扩容算法‌（需考虑Slot打包）
‌- 解释warm/cold存储访问的2100 Gas差异，如何预热关键地址？
‌- 如何通过bitmask压缩多个布尔状态变量以减少SLOAD次数？
‌- 对比memory与calldata的ABI编码差异，说明何时应强制使用calldata‌
‌- 计算EIP-1559的BASEFEE动态调整公式，分析其对Gas竞价的影响
‌- 为什么log事件比storage更省Gas？给出事件数据分片存储方案
‌- 设计一个支持批量验证的Merkle Proof处理器，优化链上计算成本
- 计算1 ether等于多少wei和gwei？
- 为什么Solidity不支持浮点数运算？替代方案是什么？
- 如何安全生成0到100的随机数？分析其局限性
- 为什么now关键字被废弃？替代方案是什么？
- 设计一个Gas优化的动态数组扩容算法（考虑Slot打包）
- 对比assert与require的异常处理机制及Gas消耗差异
- 如何通过assembly内联汇编优化keccak256计算？
- 解释EIP-1559的BASEFEE动态调整机制及其对Gas的影响
- 如何实现跨合约调用时的Gas预留？分析gasleft()的使用
- 解释unchecked块的使用场景及算术溢出风险
- 如何通过位运算压缩多个布尔状态变量以减少存储开销？
- 解释warm/cold存储访问的Gas差异及预热技巧
- 计算一笔普通ETH转账交易的最低Gas消耗（含基础成本与计算成本）


### 协议标准与扩展

- ‌实现ERC721的_beforeTokenTransfer钩子，防止非预期代币转移
‌- 解释ERC20的permit功能如何通过离线签名节省Gas？
‌- 设计一个支持租赁功能的ERC4907扩展合约
‌- 如何通过ERC2771实现元交易？分析转发合约的信任假设‌
‌- 对比ERC721A与传统ERC721的批量铸造Gas效率差异‌
‌- 实现一个符合EIP-2612的Token，支持nonce防重放‌
‌- 解释ERC1155的_doSafeBatchTransferAcceptanceCheck安全逻辑
‌- 设计跨链ERC20桥接合约，解决双花问题‌‌
‌- 如何通过EIP-712结构化哈希实现链下订单签名？
‌- 分析ERC4626金库合约的滑点保护机制
- 如何通过event记录合约日志？与直接存储相比的优势
- 列出3个全局变量（如block.timestamp）及其用途
- 为什么CREATE2能实现确定性地址部署？给出应用场景
- 如何实现合约的可升级性？分析透明代理与UUPS模式的优劣
- 解释delegatecall的上下文保持特性及典型应用场景
- 如何通过struct和mapping实现高效查询的用户管理系统？
- 解释EIP-712结构化签名的工作原理及防重放机制
- 设计一个支持批量转账的ERC20扩展合约，优化Gas消耗
- 对比ERC721与ERC1155在批量交易中的Gas效率差异
- 设计一个支持元交易的ERC2771合约，分析转发者信任问题
- 分析ERC4626金库合约的滑点保护机制
- 设计一个支持租赁功能的ERC4907扩展合约

### 高级架构与数学

- 实现一个基于ZK-SNARK的匿名投票合约，需设计Nullifier机制‌
- ‌解释椭圆曲线配对在预编译合约ecadd中的实现原理‌
‌- 设计一个状态通道结算合约，支持多签名争议超时‌
‌- 如何通过环签名实现混币器？计算其匿名集大小与Gas关系‌
‌- 实现一个基于VRF的链上彩票合约，解决区块哈希预测问题
‌- 解释Plonk验证合约的Gas成本主要来自哪些椭圆曲线操作？
‌- 设计一个支持隐私存款的Tornado Cash改进版，解决监管合规问题
‌- 如何通过多项式承诺优化Merkle Tree的链上验证？‌‌
‌- 实现一个基于EIP-4337的账户抽象钱包合约
‌- 分析Optimistic Rollup欺诈证明合约的7天挑战期安全假设‌‌