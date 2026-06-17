# 代码重构示例：拆解耦合的支付模块

## 场景

你有一个 2000 行的 `payment.py`，里面混杂了微信支付、支付宝、银联三种支付方式的逻辑。
改一个支付方式要改 5 个地方，测试要跑 30 分钟。

## 应用解耦力框架

### Step 1: 找裂缝

| 判据 | 分析 | 结论 |
|:-----|:-----|:------|
| 维度差异 | 三种支付方式属于"接入层"，共享逻辑属于"业务层" | ✅ 这是天然裂缝 |
| 职责差异 | "怎么接入支付" vs "支付成功后的业务流程" 是不同的职责 | ✅ 应当分开 |
| 变化原因差异 | 微信接口变化 vs 业务规则变化 vs 对账需求变化 | ✅ 变化原因不同 |

**裂缝位置**：沿着"支付方式接入"和"支付核心业务"之间的边界。

### Step 2: 切割

```
payment.py (2000行)
  ├── 微信支付逻辑    (600行)  →  WechatGateway
  ├── 支付宝逻辑      (600行)  →  AlipayGateway
  ├── 银联逻辑        (500行)  →  UnionpayGateway
  └── 支付核心业务    (300行)  →  PaymentService (下单/退款/对账)
```

### Step 3: 桥接

```python
# 接口契约
class PaymentGateway(ABC):
    def create_order(self, amount: int) -> Order
    def refund(self, order_id: str) -> bool
    def query(self, order_id: str) -> OrderStatus

# 每个接入层实现此接口
class WechatGateway(PaymentGateway): ...
class AlipayGateway(PaymentGateway): ...
class UnionpayGateway(PaymentGateway): ...

# 业务层只依赖接口，不依赖具体实现
class PaymentService:
    def __init__(self, gateway: PaymentGateway):
        self.gateway = gateway
```

## 结果

- 新增支付方式 = 新增一个 Gateway 文件 + 一行注册代码
- 修改某个支付接口 = 只改一个文件
- 测试 = 每个 Gateway 独立测试，30 分钟 → 5 分钟
