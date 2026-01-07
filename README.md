# Kissing Number Optimizer (PyTorch)

本项目利用 PyTorch 框架，通过梯度下降优化算法（Adam）寻找 $n$ 维空间中 $m$ 个单位球体相互接触的可行配置。

## 核心功能
* **多启动搜索**：支持随机初始化多次重启，以跳出局部最优解。
* **GPU 加速**：自动检测 CUDA 环境，加速大规模矩阵运算。
* **动态归一化**：在优化过程中强制点集投影在单位球面上，确保几何约束的严谨性。

---

## 运行实验 (run.py)

使用 `run.py` 作为主入口。它内置了 `argparse` 参数解析器，允许灵活配置实验。

### 命令行参数说明

| 参数 | 缩写 | 类型 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| `--n` | `-n` | `int` | `3` | 空间的维度 (Dimension) |
| `--m` | `-m` | `int` | `12` | 尝试放置的点集数量 (Number of points) |
| `--restarts` | 无 | `int` | `5` | 随机初始化的重启次数，增加此值可提高成功率 |
| `--steps` | 无 | `int` | `5000` | 每次训练的最大迭代步数 |
| `--lr` | 无 | `float` | `0.01` | 优化器的学习率 |
| `--output` | 无 | `str` | `result.pt` | 结果保存的文件名 |

### 示例用法
```bash
# 基础运行 (3D, 12个点)
python run.py -n 3 -m 12

# 高阶搜索 (4D, 24个点，增加重启次数)
python run.py -n 4 -m 24 --restarts 20 --steps 10000 --lr 0.005
```
### 可视化结果 (view_result.py)
目前只支持3维的可视化，通过matplotlib库实现。
```bash
python view_result.py
