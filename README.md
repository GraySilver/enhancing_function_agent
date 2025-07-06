## Enhancing FunctionCalling Agent

- **Author:** allenyzx
- **Version:** 0.0.1
- **Type:** agent-strategy

### Description
一个有用的Agent策略，参考了一部分关于[EASYTOOL: Enhancing LLM-based Agents with Concise Tool Instruction](https://arxiv.org/pdf/2401.06201)逻辑，代码实现基于微软提供的[EASYTOOL](https://github.com/microsoft/JARVIS/tree/main/easytool)。
![The four-stage framework of LLM-based agents in tool-usage applications.](https://github.com/GraySilver/enhancing_function_agent/blob/main/_assets/1.jpg)


使用前：
![](https://github.com/GraySilver/enhancing_function_agent/blob/main/_assets/use_before.jpg)


使用后：
![](https://github.com/GraySilver/enhancing_function_agent/blob/main/_assets/use_after1.jpg)


### Features:
#### Task Planning
将复杂用户问题分解为可独立执行的原子子任务。通过LLM生成结构化任务列表（{"Tasks": [...]}格式），每个任务包含： 
1. 自然语言描述的原子任务;
2. 唯一任务ID标识;
3. 确保任务完整性和自洽性

#### Task Topology
建立任务间的逻辑依赖关系图：
1. 分析任务执行顺序和依赖关系
2. 输出[{"task":..., "id":..., "dep":[...]}]格式的拓扑结构
3. 支持多级依赖处理（列表/字符串/整数格式转换）
4. 内置错误重试机制（最多5次)

#### Choose Tool:
为每个子任务匹配最佳工具：
1. 基于工具描述（tool_dic）和任务需求动态选择
2. 输出[{"ID": XX}]格式的选择结果
3. 过滤已使用工具避免重复
错误重试机制保障稳定性

#### Tool Check:
智能判断是否需要工具调用：
1. 实时性检测（需要实时信息时强制调用）
2. 数据获取检测（ID/位置/排名等结构化数据需求）
3. 外部资源检测（数据库/网络搜索需求）
输出{"Reason":..., "Choice":"Yes/No"}决策依据

### Changelog
#### v0.0.1
- Initial release.

