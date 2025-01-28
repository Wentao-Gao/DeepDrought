
# 🌏 **DeepDrought: AI-Driven Extreme Drought Prediction**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Research](https://img.shields.io/badge/Research-Climate%20AI-brightgreen.svg)](#)

---

## 📖 **项目简介**

**DeepDrought** 是一个专注于利用深度学习技术预测南澳大利亚极端干旱（黑天鹅事件）的研究项目。本项目旨在通过引入**物理约束的深度学习模型**与**不确定性量化技术**，解决传统方法在低概率高冲击事件预测中的不足。

---

## 🎯 **研究目标**

1. **探索气候因子与南澳降水的高维非线性关系**  
   研究 ENSO（厄尔尼诺南方涛动）、IOD（印度洋偶极子）、SAM（南方环状模）等气候因子的时滞和叠加效应对区域干旱的触发机制。

2. **构建物理约束的深度学习模型**  
   利用图神经网络（GNN）和时空 Transformer，结合物理方程（如水量平衡），提升模型对极端事件的预测能力。

3. **开发不确定性量化框架**  
   输出未来降水的概率分布而非单值预测，帮助量化极端干旱风险，支持更稳健的决策。

---

## 💡 **技术亮点**

### 1. **物理嵌入的图神经网络**
- 构建基于 ENSO/IOD/SAM 遥相关的图结构，将气候因子作为节点，将它们的因果关系（通过 PCMCI 等算法识别）作为边权重。
- 嵌入物理约束（如降水-蒸散发-径流的守恒关系）以增强模型解释力。

### 2. **数据增强与样本扩充**
- 使用条件生成对抗网络（GAN）和扩散模型（Diffusion Models）合成极端尾部干旱样本，解决稀缺数据问题。

### 3. **不确定性量化**
- 通过贝叶斯深度学习（Bayesian Transformers）或蒙特卡洛 Dropout，生成概率分布以量化预测的不确定性。
- 特别关注极端干旱事件的风险区间。

### 4. **可解释性**
- 基于注意力权重的可视化，分析关键气候因子的触发路径。
- 使用反事实分析探索不同气候场景对预测结果的影响。

---

## 🗂️ **研究方法与架构**

### 1. **数据来源**
- **气候因子数据**:
  - ENSO（Niño3.4 指数）、IOD 和 SAM（AAO 指数）。
  - 数据来源：NOAA 气候数据中心。
- **观测降水与温度数据**:
  - 来源：澳大利亚气象局（BoM）。
  - 分辨率：0.05° 网格化数据。
- **模式输出数据**:
  - CMIP6 模式历史模拟与情景预测数据。

### 2. **技术路线**

#### **(1) 数据预处理与增强**
- 多源数据融合：将气候因子与区域降水数据对齐，并通过插值处理缺失值。
- 数据增强：基于 GAN 和扩散模型合成稀缺的极端干旱情景。

#### **(2) 模型架构设计**
- **Graph Transformer**:
  - 编码器：基于图注意力机制（GAT）提取气候因子间的高维非线性关系。
  - 解码器：生成多步降水概率分布。
  - 物理约束：通过嵌入水量平衡方程，确保模型输出物理一致性。

#### **(3) 训练与验证**
- **预训练阶段**:
  - 在 CMIP6 模式数据上预训练，学习广泛的气候动力学先验。
- **微调阶段**:
  - 在 BoM 观测数据上微调，提升区域适用性。
- **极端事件聚焦**:
  - 对历史极端干旱数据增加权重，优化模型对尾部分布的预测能力。

#### **(4) 不确定性分析**
- 深度概率建模：通过扩散模型输出未来降水概率密度分布（PDF）。
- 风险评估：量化极端尾部事件（如干旱）的发生概率。

---

## 🌟 **项目优势**

- **跨领域结合**: 深度学习、气候科学与物理约束的结合，提供更具解释力的预测。  
- **技术创新**: 图 Transformer 与生成模型的结合，增强稀缺数据的建模能力。  
- **决策支持**: 不确定性量化输出直接服务于干旱管理与风险评估。  

---

## 🗓️ **项目计划**

| 阶段         | 时间段          | 任务                                                                 | 输出成果                                   |
|--------------|-----------------|----------------------------------------------------------------------|-------------------------------------------|
| **阶段 1**   | 0~6 个月        | 数据收集与预处理，搭建基本框架                                        | 数据管道代码 + 数据清洗文档                |
| **阶段 2**   | 6~12 个月       | 模型初步开发（Graph Transformer + 物理约束）                          | 模型训练代码 + 初步实验结果                |
| **阶段 3**   | 12~18 个月      | 数据增强（GAN/扩散模型），提升极端尾部事件建模能力                     | 增强后的训练数据集 + 模型对比实验          |
| **阶段 4**   | 18~24 个月      | 不确定性分析与可解释性工具开发                                       | 风险评估报告 + 注意力权重可视化            |
| **阶段 5**   | 24~36 个月      | 综合验证与论文撰写                                                  | 博士论文 + 学术论文（目标：ICLR/NeurIPS） |

---

## 📘 **参考文献**

1. **Runge, J., et al.** (2019). Detecting causal associations in large nonlinear time series datasets. *Science Advances*, 5(11), eaau4996.  
2. **Van Dijk, A. I., et al.** (2013). The Millennium Drought in southeast Australia (2001–2009): Natural and human causes and implications for water resources, ecosystems, economy, and society. *Water Resources Research*, 49(2), 1040–1057.  
3. **Cai, W., et al.** (2011). Teleconnection pathways of ENSO and the IOD and the mechanisms for impacts on Australian rainfall. *Journal of Climate*, 24(15), 3910–3923.  

---

