我会先做一次“只读调研”，快速定位官网、编辑器页面和云端配置相关代码与构建入口，然后给你一份可执行的分支/改造规划草案。接下来先并行扫目录与关键关键词，避免遗漏。

Searched for regex `官网|home|landing|index|site|门户` (`**/apps/web/src/**`), 200 results

Searched for regex `editor|codemirror|markdown|preview|render|useEditorStore` (`**/apps/web/src/**`), 200 results

Searched for regex `cloud|remote|api|worker|upload|config|private|env|token|endpoint|wrangler|netlify` (`**/apps/web/**`), 200 results

我已经定位到核心入口：当前 Web 端基本是“编辑器即首页”，并且云端相关主要集中在 Vite 环境变量、Cloudflare Worker 代理和上传/导入接口。下一步我会读取关键文件确认三块的边界、可拆分点和私有化改造风险。

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/App.vue)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/main.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/worker/index.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/vite.config.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/ImportMarkdownDialog.vue#1-1), lines 1 to 220

我将按你的三大块并行做“深一点的发现”：分别用 Explore 子代理扫描官网入口、编辑器域模型、云端配置与外部依赖，输出可落地的改造建议和风险清单。

官网入口与页面结构

编辑器架构与可定制点

云端配置私有化扫描

Searched for files matching `**/apps/web/src/views/**/*[Ee]ditor*`, 1 match

Searched for files matching `**/apps/web/src/components/**/*[Pp]anel*`, 6 matches

Searched for regex `useEditorStore|useThemeStore|useUiStore|useTemplateStore` (`**/apps/web/src/stores/**`), 11 results

Searched for files matching `**/apps/web/src/stores/**`, 15 matches

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/main.ts)

Searched for files matching `**/apps/web/src/views/**`, 1 match

Searched for files matching `**/apps/web/src/*router*`, no matches

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/index.html#1-1), lines 1 to 30

Searched for regex `https?://|http://|\.doocs\.org|\.netlify|api\.github`, 100 results

Searched for regex `import\.meta\.env|process\.env\.VITE|process\.env\.WRANGLER`, 3 results

Searched for regex `upload|analytics|proxy|wechat|api.key|secret|token`, 100 results

Searched for files matching `**/vite.config.ts`, 1 match

Searched for files matching `**/wrangler.jsonc`, 1 match

Searched for files matching `**/wxt.config.ts`, 1 match

Searched for files matching `**/netlify.toml`, 1 match

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/views/CodemirrorEditor.vue#1-1), lines 1 to 100

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/EditorPanel.vue#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/PreviewPanel.vue#1-1), lines 1 to 60

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/App.vue#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/modules)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/vite.config.ts#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/wxt.config.ts#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/vite.config.ts#1-1), lines 1 to 100

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/wxt.config.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/netlify.toml)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/wrangler.jsonc)

Searched for text `landing|home|docs|website|官网|商业|about` (`**/apps/web/src/**`), 20 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/public)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/md-cli/server.js#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/md-cli/package.json)

Searched for text `wechat proxy appid appsecret domain`, no results

Searched for text `anything-md plantuml mermaid render api`, no results

Searched for text `VITE_API VITE_PROXY VITE_HOST baseURL`, no results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/UploadImgDialog.vue#1-1), lines 1 to 250

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/entrypoints)

Searched for text `createRouter|useRouter|router` (`**/apps/web/**`), no results

Searched for text `SEO|analytics|GoogleAnalytics|meta` (`**/packages/shared/src/**`), 3 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/README.md#1-1), lines 1 to 100

Searched for regex `plantuml|mermaid|anything|api\.github`, 50 results

Searched for regex `request\.js|http|fetch|axios` (`**/apps/web/src/**`), 50 results

Searched for regex `store\.js|config\.ts` (`**/packages/shared/src/**`), no results

Searched for files matching `**/http.ts`, no matches

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/editor.ts#1-1), lines 1 to 60

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/render.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/theme.ts#1-1), lines 1 to 120

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/template.ts#1-1), lines 1 to 80

Searched for text `AboutDialog` (`**/apps/web/src/components/**`), 8 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/netlify.toml)

Searched for text `build` (`**/apps/web/package.json`), 17 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/package.json#1-1), lines 1 to 50

Searched for regex `plantuml|svg|render` (`**/packages/core/src/**`), 50 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/ImportMarkdownDialog.vue#80-80), lines 80 to 150

Searched for regex `fetch|request|http` (`**/packages/shared/src/**`), 22 results

Searched for files matching `**/packages/shared/src/utils/fetch.ts`, 1 match

Searched for regex `RightSlider|AccountPanel|SettingPanel|ExportDialog|UploadDialog` (`**/apps/web/src/components/**/*.vue`), 15 results

Searched for files matching `**/apps/web/src/components/**/*[Ss]lider*`, 1 match

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/export.ts#1-1), lines 1 to 100

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/ui.ts#1-1), lines 1 to 80

Searched for files matching `**/apps/web/src/components/**/AboutDialog.vue`, 1 match

Searched for text `IndexHtml|html|SEO|meta title description` (`**/apps/web/src/**`), 20 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components)

Searched for text `md.doocs.org` (`**/apps/web/src/**/*.vue`), 1 result

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/lib)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/utils)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/editor-header/AboutDialog.vue)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor)

Searched for files matching `**/apps/web/src/modules/**`, 1 match

Searched for regex `mpAccounts|Account|userProfile|settings` (`**/apps/web/src`), no results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/RightSlider.vue#1-1), lines 1 to 100

Searched for text `md.doocs.org`, 11 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/md-cli/index.js#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/pnpm-workspace.yaml)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/mpAccounts.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/post.ts#1-1), lines 1 to 60

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/aiConfig.ts#1-1), lines 1 to 100

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/shared/src/constants/ai-config.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/shared/src/utils/fetch.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/shared/src/configs/ai-service-options.ts#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/core/src/renderer/renderer-impl.ts#250-250), lines 250 to 450

Searched for text `router|route` (`**/apps/web/src/stores/**`), no results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/.github/workflows/deploy.yml)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/ai)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/post-slider)

Searched for regex `cssEditor|customComponent|aiImage` (`**/apps/web/src/stores`), no results

Searched for files matching `**/apps/web/src/**/*[Cc]omposable*`, no matches

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/core/src/renderer/renderer-impl.ts#455-455), lines 455 to 477

Searched for regex `www\.plantuml\.com` (`**/packages/core/src/**`), 2 results

Searched for regex `md\.doocs\.org|md-pages\.doocs\.org|proxy-ai` (`**/apps/web/src/**`), 5 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/views/CodemirrorEditor.vue#1-1), lines 1 to 100

Searched for text `window.location|hash|pathname` (`**/apps/web/src/**`), 20 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/wrangler.jsonc#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/composables)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores)

Searched for regex `export const` (`**/apps/web/src/stores`), no results

Searched for regex `WeChat|wechat|proxyOrigin|getWechat` (`**/apps/web/src/utils/**`), 13 results

Searched for regex `wechat\.proxy|WeChat\.proxy|proxyOrigin` (`**/apps/web/src/**`), 16 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/core/src/extensions/plantuml.ts#1-1), lines 1 to 150

Searched for text `route|router|redirect` (`**/apps/web/src/composables/**`), no results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/assets)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/cssEditor.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/customComponent.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/aiImageConfig.ts#1-1), lines 1 to 80

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/folderSource.ts#1-1), lines 1 to 100

Searched for regex `storage|localStorage|store|config` (`**/apps/web/src/utils/**`), 30 results

Searched for regex `fetch|request|api|endpoint` (`**/apps/web/src/stores/**`), 30 results

Searched for files matching `**/apps/web/src/utils/storage.ts`, 1 match

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/utils/file.ts#150-150), lines 150 to 450

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/index.html#1-1), lines 1 to 60

Read memory

Searched for regex `infographic|katext|mermaid|marked` (`**/packages/core/src/extensions/**`), 30 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/utils/storage.ts#1-1), lines 1 to 160

Searched for regex `api|fetch|render` (`**/packages/core/src/extensions/infographic.ts`), 9 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/core/src/extensions/infographic.ts#1-1), lines 1 to 50

Read memory

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/components/editor/RightSlider.vue#40-40), lines 40 to 220

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/views/CodemirrorEditor.vue#100-100), lines 100 to 120

Searched for regex `import.*Store|useStore` (`**/apps/web/src/components/editor`), no results

Created memory file [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/memory-tool/memories/OThhYjk0NTktNDhjZS00MTBmLWExMTAtMzAzZjZmMjRkZTll/wechat-editor-official-website-analysis.md)

Created memory file [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/memory-tool/memories/OThhYjk0NTktNDhjZS00MTBmLWExMTAtMzAzZjZmMjRkZTll/cloud-privatization-audit.md)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/App.vue#1-1), lines 1 to 50

Searched for regex `defineStore` (`**/apps/web/src/stores`), no results

Searched for text `export const use` (`**/apps/web/src/stores/*.ts`), 15 results

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/quickCommands.ts#1-1), lines 1 to 50

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/stores/confirm.ts#1-1), lines 1 to 50

Read memory

Created memory file [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/memory-tool/memories/repo/editor-architecture-analysis.md)

我拿到了两个子代理的详细报告文件，接下来会读出核心结论并和本地代码交叉验证，避免只基于推断给你建议。

Read [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/chat-session-resources/98ab9459-48ce-410f-a110-303f6f24de9e/call_GrhDdfI4JrTqBYrCqwSy6jXc__vscode-1780097048662/content.txt)

Read [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/chat-session-resources/98ab9459-48ce-410f-a110-303f6f24de9e/call_wAYJZxi7FoOxomkDzWP8QRlC__vscode-1780097048663/content.txt)

现在我在做最后一轮证据校验：把子代理提到的外部域名、构建开关和上传链路逐条核对到实际代码，确保后续建议可直接执行。

Searched for regex `anything-md.doocs.org|proxy-ai.doocs.org|plantuml.com|G-7NZL3PZ0NK|api.weixin.qq.com` (`**/*.{ts,vue,js,mjs,html,jsonc}`), 17 results

Searched for regex `CF_WORKERS|CF_PAGES|SERVER_ENV|envPrefix|VITE_` (`**/apps/web/**`), 14 results

Searched for regex `githubUpload|aliOSS|txCOS|getMpToken|proxyOrigin|upload` (`**/apps/web/src/utils/**`), 90 results

Searched for regex `DEFAULT_SERVICE_ENDPOINT|ai-service-options|service endpoint|apiKey` (`**/packages/shared/src/**`), 5 results

我已完成关键字符串核验，结论基本可靠。现在补读几个入口文件（HTML/部署/存储引擎）后，我会给你一版“三大块定制”的战略分析和执行顺序。

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/index.html)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/netlify.toml)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/wxt.config.ts)

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/apps/web/src/utils/storage.ts#1-1), lines 1 to 260

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/shared/src/configs/ai-service-options.ts#1-1), lines 1 to 180

Read [](file:///Users/geekmister/Desktop/Workspace/Repositories/Geekmister/wechat-editor/packages/shared/src/constants/ai-config.ts)

我已经有足够上下文了，接下来先和你对齐几个关键决策（部署形态、官网形态、私有化深度）；确认后我会产出一份可执行的分阶段计划并写入会话计划文件。

Read memory

正在分析你的回答...

你的选择已明确：先做云端私有化，官网走独立子应用，目标是企业版私有化并落地国内自建云。下面我会基于这个方向生成一版可执行计划并同步到会话计划文件。

Read memory

Created memory file [](file:///Users/geekmister/Library/Application%20Support/Code/User/workspaceStorage/a8343aec0f56aac523805ed69882e5ee/GitHub.copilot-chat/memory-tool/memories/OThhYjk0NTktNDhjZS00MTBmLWExMTAtMzAzZjZmMjRkZTll/plan.md)

结论先说：你的三块定制方向是合理的，但从工程风险和商业落地速度看，必须先把“云端配置私有化”做成平台能力，再推进 editor 深改和官网独立，不然后面会反复返工。

我已基于代码现状完成分析，并按你确认的目标（云端优先、官网独立子应用、企业版私有化、国内自建云）整理了可执行路线图，已同步到会话计划文件。

**现状分析**
1. 官网现状
1. 当前前端是“编辑器即首页”，没有独立官网路由层，入口直接挂编辑器：App.vue、CodemirrorEditor.vue。
2. SEO/品牌信息主要在静态 HTML，商业化承载能力弱：index.html。
3. 你的“独立官网子应用”决策是正确的，可明显降低后续营销页面改版对编辑器稳定性的影响。

2. Editor 页面现状
1. 编辑器主链路成熟但耦合度高，核心在编辑器状态、渲染状态、UI 状态三角：editor.ts、render.ts、ui.ts。
2. 低风险可快速商业化的点很多（模板、导出、账户、AI 配置），高风险点是渲染内核和 CodeMirror 主链。
3. 结论：先做低耦合增值，再碰高耦合内核。

3. 云端配置私有化现状
1. 存在多个硬编码公网依赖，含 AI、Markdown 转换、PlantUML、微信 API、埋点等：ai-config.ts、ImportMarkdownDialog.vue、plantuml.ts、file.ts、vite.config.ts。
2. 多数敏感配置仍以前端存储/直连方式使用，企业版私有化需要网关化与密钥托管。
3. 现有存储抽象已经给了很好切入点：storage.ts。

**推荐执行顺序（已固化到计划）**
1. Phase 0：先固化分支协作规则（main 同步 upstream，develop 日常开发，main-custom 商业化发布）。
2. Phase 1：做配置中心化与环境策略统一（去硬编码、可切换私有域名）。
3. Phase 2：做企业版核心（统一网关、密钥托管、审计权限、CSP/脱敏/限流）。
4. Phase 3：推进 editor 商业化功能（先低耦合模块）。
5. Phase 4：落地独立官网子应用（marketing 与 editor 解耦部署）。
6. Phase 5：建立长期 upstream 同步与回归机制。

**关键风险提醒**
1. 如果不先完成 Phase 1/2，后续 editor 和官网会重复改 API 与配置层，成本会翻倍。
2. 上传链路分散在单文件多 provider，改造时需要“契约优先”，否则回归面很大：file.ts。
3. 扩展端权限白名单要同步私有化域名，不然浏览器扩展会失效：wxt.config.ts。

下一步如果你同意，我可以继续给你一版“可直接开工的里程碑拆分”（按 2 周迭代，细到每期交付物与验收标准）。
