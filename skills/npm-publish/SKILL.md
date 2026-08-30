---
name: npm-publish
description: Publish this project to the official npm registry when the user explicitly requests an npm release. Covers repository gates, validation, authentication, publication, and verification.
---

# npm 发布

仅在用户明确要求发布时执行外部发布操作。不要把发布授权扩展为 Git push、tag 或其他未请求操作。

## 流程

1. 阅读仓库指令并检查分支、工作区、版本元数据和发布文档。确认要求的能力/架构文档已同步、能正常渲染且已被 Git 跟踪。保留用户未提交的修改；若 `main` 落后于开发分支且用户尚未授权合并，先停止并询问。
2. 始终显式使用官方 registry `https://registry.npmjs.org/`，不要依赖本机默认 registry；默认值可能是 `registry.npmmirror.com`。
3. 用官方 registry 查询目标版本，已存在则停止：
   `npm view <package>@<version> version --registry=https://registry.npmjs.org/`
4. 依次运行 `npm run typecheck`、`npm test`、`npm run build` 和 `npm pack --dry-run`。确认包名、版本、内容和 Git 状态符合预期，且没有生成 `.tgz` 文件。若 Windows 上测试后某文件显示修改但 `git diff` 为空，先比较工作区与 index hash，再只刷新该文件，不要重置用户修改。
5. 检查官方 npm 身份：
   `npm whoami --registry=https://registry.npmjs.org/`
   若未登录或 token 失效，运行 `npm login --auth-type=web --registry=https://registry.npmjs.org/`，打开浏览器并等待用户完成授权。不得输出或索取 token、密码或 OTP。
6. 发布 scoped public 包：
   `npm publish --access public --registry=https://registry.npmjs.org/`
   npm 可能再次要求浏览器确认；打开官方确认页并等待结果。结果不明确时先查询 registry，不要盲目重试。
7. 从官方 registry 验证版本和 dist-tag，再报告结果：
   `npm view <package>@<version> name version dist.tarball --json --registry=https://registry.npmjs.org/`
   `npm view <package> dist-tags --json --registry=https://registry.npmjs.org/`

只暂存本次产生的文件或 hunk。若未提交修改阻止分支切换，不要 stash、reset 或覆盖用户文件；只有在已获合并授权且确认是严格快进时，才采用不触碰工作区的快进方式，否则询问用户。
