# yamdc-plugins

`yamdc` 的外部插件 bundle 仓库，主要包含：

- plugin bundle manifest
- 插件 YAML 文件
- 插件测试用例
- 相关测试脚本与 GitHub Actions

当前仓库内置了插件回归测试：

- PR 合入 `master` 时会自动执行 `.github/workflows/plugin-test.yml`
- 也支持手动触发 `workflow_dispatch`
- 手动触发时可指定 `yamdc_ref`，例如：`latest`、`master`、`v1.0.0`

本地可以直接运行：

```bash
bash ./scripts/run_plugin_test.sh
```

等价的底层命令是：

```bash
yamdc plugin-test --plugin=./ --casefile=./cases --output=json
```

其中：

- `plugin` 指向 bundle 根目录，根目录下的 `manifest.yaml` 用于指定插件入口
- `casefile` 可以是单个 JSON 文件，也可以是一个目录
- 当 `casefile` 是目录时，会扫描目录下全部 `*.json` 文件并合并执行
- 推荐将可稳定运行的插件用例统一收拢到 `cases/default.json`；当单个 case 需要覆盖插件名时，可在 case 项中显式写 `plugin` 字段

如需指定 yamdc 二进制路径：

```bash
YAMDC_BIN=/path/to/yamdc bash ./scripts/run_plugin_test.sh
```
