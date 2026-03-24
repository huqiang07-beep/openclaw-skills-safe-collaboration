# openclaw-skills-safe-collaboration

OpenClaw 修改安全护栏技能。

该仓库提供一个面向生产环境的 OpenClaw 系统变更安全技能。

## 技能包

- `openclaw-safe-collaboration/SKILL.md`

## 技能作用

该技能要求在高风险 OpenClaw 操作中采用双角色协作：

- **Supervisor（监管员）**：风险分析、安全约束、回滚优先
- **Developer（开发员）**：在监管约束下实施变更

目标是降低服务中断、配置损坏、插件和服务操作失误的风险。

## 适用场景

- 修改 `~/.openclaw/openclaw.json`
- 安装/卸载 OpenClaw 插件
- 重启/重载 OpenClaw Gateway 服务
- 调整频道配置（飞书、钉钉等）
- 修改 Agent 路由与系统级设置

## 安装方式

将技能目录复制到 Cursor/OpenClaw 的技能目录：

```bash
mkdir -p ~/.cursor/skills
cp -R ./openclaw-safe-collaboration ~/.cursor/skills/
```

复制完成后，重启会话（或刷新技能加载）使其生效。

## 触发条件

当用户请求 OpenClaw 系统级操作时，应自动触发该技能，尤其是：

- 配置文件修改
- 插件生命周期操作
- 服务生命周期操作
- Gateway/频道路由变更

## 强制执行流程

1. 监管员风险评估
2. 开发员实施变更
3. 监管员校验结果
4. 受控执行与健康验证

必须校验：

- 配置合法性（JSON/Schema）
- 依赖与路径兼容性
- 服务变更后健康状态
- 回滚可行性

## 强制输出结构

回答需要包含以下四段：

1. `Supervisor Analysis`
2. `Developer Implementation`
3. `Supervisor Verification`
4. `Execution Result`

## 示例请求

- “升级 OpenClaw，并确保 gateway 正常运行。”
- “修复飞书多 Agent 路由，不能影响现有可用链路。”
- “安装插件 X，并验证不引入配置回归。”

## 验收标准

满足以下条件才算完成：

- `openclaw doctor` 无阻断错误
- 配置无 invalid 警告
- 必需插件/频道状态健康
- Gateway/服务运行正常

## 说明

- 该技能优先保证系统稳定，再追求执行速度。
- 适用于对 OpenClaw 可用性要求较高的生产/准生产环境。
