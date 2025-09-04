# 白平衡 (White Balance)

白平衡是 ISP 中的关键步骤，用于校正图像色温，使白色物体在不同光照下仍呈现白色。

## 常见方法

- **手动白平衡**：指定参考白色区域
- **自动白平衡 (AWB)**：基于统计或算法（如灰度世界假设）
- **色温校正**：调整 RGB 增益

## Python 示例

```python
def white_balance(image):
    # 简单的灰度世界假设
    avg_r = image[:,:,0].mean()
    avg_g = image[:,:,1].mean()
    avg_b = image[:,:,2].mean()
    avg_gray = (avg_r + avg_g + avg_b) / 3
    image[:,:,0] = image[:,:,0] * (avg_gray / avg_r)
    image[:,:,1] = image[:,:,1] * (avg_gray / avg_g)
    image[:,:,2] = image[:,:,2] * (avg_gray / avg_b)
    return np.clip(image, 0, 255).astype(np.uint8)