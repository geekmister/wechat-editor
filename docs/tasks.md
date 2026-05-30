**执行基线（先定规矩）**

1. 分支策略：main 只跟上游；develop 做集成；main-custom 仅承载商业化。
2. 发布策略：每个 Phase 完成后在 main-custom 打标签；develop 保留可回放合并记录。
3. 完成定义（DoD）：代码合并 + 文档更新 + 三端验证 + 回归通过。
4. 阻塞规则：Phase 1 未完成，不得进入 Phase 2 的后端契约联调。

**任务清单（可执行）**

### Phase 0：分支与发布基线（阻塞后续）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P0-01 | 固化分支保护与合并策略 | README.md | 无 | 分支策略文档 | 团队确认 main/develop/main-custom 流程且可执行 | TL |
| P0-02 | 建立里程碑标签规范 | CHANGELOG.md | P0-01 | Tag 命名规则 | 每个阶段有统一标签格式 | TL |
| P0-03 | 生成冲突高风险目录清单 | CodemirrorEditor.vue, stores, src | P0-01 | 冲突地图文档 | 清单覆盖高耦合区域并标注负责人 | FE TL |
| P0-04 | 建立回滚预案模板 | docs | P0-02 | 回滚 Runbook | 关键改造均有回滚步骤 | DevOps |
| P0-05 | 建立基线 CI 检查项 | package.json | P0-01 | 基线校验项清单 | type-check、lint、web build、ext zip 全可运行 | FE |

### Phase 1：云端私有化 P1（配置中心与环境策略）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P1-01 | 盘点硬编码外部域名与 API | ai-config.ts, ai-service-options.ts, plantuml.ts, file.ts | P0-03 | 依赖清单 | 列出 AI/上传/PlantUML/代理全入口 | FE |
| P1-02 | 设计运行时配置模型（cloud/public/private） | types, lib | P1-01 | 配置 Schema | 模式与字段完整、可序列化 | FE |
| P1-03 | 实现前端配置读取层（替代硬编码） | main.ts, App.vue, vite.config.ts | P1-02 | 配置加载模块 | 不改业务代码即可切换域名 | FE |
| P1-04 | 接入域名映射矩阵（AI/上传/PlantUML/微信代理） | file.ts, plantuml.ts, ai-service-options.ts | P1-03 | 可替换端点层 | 配置切换后链路全通 | FE |
| P1-05 | Web 与扩展侧环境对齐 | wxt.config.ts, entrypoints | P1-04 | 双端环境策略 | Web/WXT 配置行为一致 | FE |
| P1-06 | 增加配置健康检查页面或诊断日志 | views, utils | P1-03 | 诊断能力 | 可看见当前模式与端点来源 | FE |
| P1-07 | 编写配置接入文档 | docs | P1-04 | 配置文档 | 新人按文档可完成环境切换 | FE |
| P1-08 | Phase 1 集成验收 | package.json | P1-01~P1-07 | 验收记录 | 配置替换验证全部通过 | QA |

### Phase 2：云端私有化 P2（网关契约、密钥托管、审计安全）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P2-01 | 输出统一网关 API 契约草案 | docs | P1-08 | 网关契约 v1 | 上传/AI/代理响应结构统一 | BE |
| P2-02 | 前端网关客户端适配层 | file.ts, storage.ts | P2-01 | 网关调用 SDK | 前端仅调用企业网关域名 | FE |
| P2-03 | 密钥迁移设计（localStorage 到后端托管） | storage.ts, stores | P2-01 | 迁移方案文档 | 浏览器不再保存高敏密钥 | FE+BE |
| P2-04 | 实施令牌化会话机制 | stores, utils | P2-03 | 会话令牌流程 | 调用链仅使用短期令牌 | FE+BE |
| P2-05 | 增加审计字段（租户/用户/请求） | file.ts, index.ts | P2-02 | 审计日志规范 | 请求链路可追踪 | BE |
| P2-06 | 安全基线（CSP、脱敏、限流/熔断） | index.html, index.ts | P2-05 | 安全加固清单 | 漏洞扫描与抽检通过 | BE+DevOps |
| P2-07 | 三端联调（Web/Workers/WXT） | src, index.ts, wxt.config.ts | P2-02~P2-06 | 联调报告 | 上传/导入/AI 三端一致通过 | QA |
| P2-08 | Phase 2 里程碑发布 | CHANGELOG.md | P2-07 | 发布记录 | main-custom 打里程碑标签 | TL |

### Phase 3：Editor 商业化定制（先低耦合后中耦合）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P3-01 | 模板体系增强（企业模板包） | stores, components | P2-01 | 模板管理能力 | 模板导入导出与权限策略可用 | FE |
| P3-02 | 导出能力增强（批量/格式策略） | stores, components | P3-01 | 导出策略配置 | 导出成功率与性能达标 | FE |
| P3-03 | 账户管理扩展（企业账号域） | stores, components | P2-04 | 账户模块增强 | 多账号策略可配置 | FE |
| P3-04 | AI 供应商策略层（按租户切换） | ai-service-options.ts, stores | P2-02 | AI 策略配置 | 按租户动态选择服务商 | FE+BE |
| P3-05 | 主题与样式编辑器增强 | components, CodemirrorEditor.vue | P3-01 | 企业主题能力 | 主题切换与样式覆盖稳定 | FE |
| P3-06 | 上传策略可视化配置 | components, file.ts | P2-02 | 上传策略面板 | 配置生效且可审计 | FE |

### Phase 4：官网独立子应用（与 Phase 3 并行，发布依赖 Phase 1）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P4-01 | 创建 marketing 子应用骨架 | web, package.json | P1-08 | 新子应用目录与构建脚本 | 可独立本地开发与构建 | FE |
| P4-02 | 官网信息架构（品牌/定价/文档/案例） | docs | P4-01 | IA 与页面清单 | 信息架构评审通过 | PM+FE |
| P4-03 | 编辑器入口跳转与域名策略 | App.vue, index.html | P4-01 | 跳转与入口规范 | 官网与编辑器职责清晰 | FE |
| P4-04 | 品牌资产与埋点统一 | index.html, vite.config.ts | P4-02 | 埋点规范 v1 | 无重复埋点，口径一致 | FE+数据 |
| P4-05 | 官网发布与回归 | CHANGELOG.md | P4-03,P4-04 | 官网发布记录 | PC/移动端通过验收 | QA |

### Phase 5：长期与 upstream 同步（持续机制）

| ID | 任务 | 关键文件 | 依赖 | 交付物 | 验收标准 | 责任 |
|---|---|---|---|---|---|---|
| P5-01 | 建立固定同步窗口（双周或月度） | README.md | P0-01 | 同步日历 | 周期执行可落地 | TL |
| P5-02 | 三层补丁策略落文档 | patches, pnpm-workspace.yaml | P5-01 | 补丁策略文档 | 通用/商业化/高冲突分层明确 | FE TL |
| P5-03 | 同步回归矩阵自动化清单 | package.json, package.json | P5-01 | 回归矩阵 | 上传/渲染/扩展端优先回归 | QA |
| P5-04 | 冲突热点重构（插件化/配置化） | src, src | P5-02 | 低冲突改造 | 同步冲突集中且可快速解 | FE |
| P5-05 | 每次同步后发布审计报告 | CHANGELOG.md | P5-03 | 同步报告模板 | 每次同步均可追溯 | TL |

---

**统一验收清单（每个里程碑都执行）**
1. 配置可替换：AI、Anything-MD、PlantUML、微信代理可仅通过配置切换到私有域名。
2. 安全抽检：浏览器 localStorage 与请求头中无高敏密钥。
3. 三端兼容：Web、Cloudflare Workers、WXT 扩展上传/导入/AI 全通过。
4. 代码质量：执行以下命令全部通过。  
pnpm run type-check  
pnpm run lint  
pnpm web build  
pnpm web ext:zip
5. 同步演练：main 合入 develop，再择优进 main-custom，冲突在预期目录内。

**建议排期（10 周版）**
1. 第 1 周：Phase 0 全量完成。
2. 第 2-3 周：Phase 1 完成并发布里程碑。
3. 第 4-6 周：Phase 2 完成（含安全与审计）。
4. 第 5-8 周：Phase 3 并行推进低耦合与中耦合项。
5. 第 6-9 周：Phase 4 并行完成并上线。
6. 第 10 周起：Phase 5 持续执行。

**关键风险与预案**
1. 风险：网关契约反复变更。预案：P2-01 先冻结 v1 字段，采用向后兼容扩展。
2. 风险：高耦合区改动引发回归。预案：先做低耦合功能，核心渲染链延后。
3. 风险：扩展端权限与域名白名单不一致。预案：P1-05 提前统一 WXT 环境策略。
4. 风险：与 upstream 冲突扩散。预案：P5-04 将商业化逻辑插件化和配置化隔离。

如果你要，我下一步可以直接给你同结构的 Jira 导入版（CSV 字段：Epic、Story、Task、Depends On、DoD、Owner、Sprint）。
