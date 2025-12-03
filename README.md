# Hybrid Physics-Informed Vehicle Dynamics Prediction
# 混合物理感知车辆动力学预测系统

本项目实现了一个先进的**混合驱动（Hybrid Data-driven & Physics-based）**车辆动力学预测模型。它结合了传统的车辆二自由度动力学方程与现代深度学习架构（CNN-LSTM），旨在利用驾驶员输入和车辆状态精确预测车辆的动力学响应（纵向、横向及横摆加速度）。

## 🌟 项目核心亮点

1.  **混合建模架构 (Hybrid Architecture)**:
    *   **CNN-LSTM 主干**: 利用一维卷积提取局部特征，LSTM 处理时序依赖。
    *   **物理嵌入**: 在神经网络的前向传播中内置了基于 `physics.py` 的动力学方程。
2.  **两种融合模式**:
    *   **残差网络模式 (Residual Mode)**: 物理模型作为基准，神经网络学习物理模型的误差（Residual），极大提高了模型的泛化能力和收敛速度。
    *   **特征增强模式 (Feature Mode)**: 物理计算结果作为高阶特征输入全连接层。
3.  **完整的工程链路**:
    *   包含从数据加载、滑动窗口序列化、标准化、训练、验证到测试评估的全流程。

## 📂 文件结构说明

```text
.
├── config.py           # [配置] 路径设置、物理参数(质量/摩擦系数等)、训练超参数
├── physics.py          # [物理] 纯物理模型实现(VehicleDynamicsModel)及基准绘图
├── main.py             # [核心] 混合模型定义(HybridVehicleDynamicsModel)与训练主程序
├── test.py             # [测试] 加载训练好的模型并在测试集上评估性能
├── data/               # [数据] 存放输入输出的 .txt 原始数据
├── model/              # [产出] 存放训练好的 .pth 模型权重
├── scalers/            # [产出] 存放 sklearn 的 StandardScaler 文件
└── results/            # [产出] 存放训练过程 Loss 曲线及预测对比图表
