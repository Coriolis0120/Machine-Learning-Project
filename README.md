# Kissing Number（PyTorch）

一个用 PyTorch 做“kissing number”构型搜索的小项目。目标是在 n 维空间里，找到 m 个单位向量，使得任意两两内积不超过 0.5。

## 快速开始
- 建环境并安装依赖：
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirement.txt
```

## 运行实验 (run.py)

使用 `run.py` 作为主入口。它内置了 `argparse` 参数解析器，允许灵活配置实验。

### 运行示例
```bash
# 3D / 12 点（经典案例）
python run.py -n 3 -m 12

# 4D / 24 点（更难，建议加大重启与步数）
python run.py -n 4 -m 24 --restarts 300 --steps 30000 --lr 0.02
```

## 参数速览（run.py）
| 参数 | 默认值 | 作用 |
| --- | --- | --- |
| `-n` / `--n` | 3 | 空间维度 |
| `-m` / `--m` | 12 | 点的数量 |
| `--restarts` | 5 | 随机重启次数，越大越稳 |
| `--steps` | 5000 | 单次训练的步数上限 |
| `--lr` | 0.01 | 学习率 |
| `--threshold` | 0.5 | 内积阈值（越低越严格） |
| `--check-every` | 50 | 每隔多少步评测一次可行性 |
| `--no-scheduler` | 关闭 | 关闭余弦学习率调度（默认开启） |
| `--no-smooth-max` | 关闭 | 关闭“平滑最大违规”项（默认开启，聚焦最坏点对） |
| `--smooth-max-alpha` | 50.0 | 平滑最大项的温度系数 |
| `--smooth-max-weight` | 1.0 | 平滑最大项的权重 |
| `--use-repulsion` | 关闭 | 启用分散项，拉开点间距离 |
| `--repulsion-alpha` | 10.0 | 分散项的 alpha |
| `--repulsion-lambda` | 1e-3 | 分散项的权重 |
| `--no-post-refine` | 关闭 | 关闭失败后的后续精炼（默认开启） |
| `--post-refine-steps` | 4000 | 精炼阶段的步数 |
| `--post-refine-lr` | -1.0 | 精炼学习率（-1 表示自动用 0.5*lr） |
| `--refine-top-k` | 5 | 失败后挑选前 K 个最接近阈值的候选再微调 |
| `--refine-steps` | 4000 | 精炼阶段步数（独立于 post-refine-steps） |
| `--refine-lr` | -1.0 | 精炼学习率（-1 表示自动用 0.5*lr） |
## 可视化（3D）
使用 [view_results.py](view_results.py) 在无显示环境保存图片到 `outputs/`。
```bash
python view_result.py
