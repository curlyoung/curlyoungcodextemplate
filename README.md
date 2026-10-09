这是一个理工学科通用项目组织模板，用于构建可发表、可复现、可迭代、可审查的人工智能赋能理工学科基础设施级工程规范。它摒弃了计算机行业项目架构的过多功能，将文档、数据、程序、结果、日志，用简单科学的方式组织在一起，对AI辅助编程极其友好。计算机赋能的理工学科从业者使用它，能使项目组织方式简单且高效。

> 作者：科利杨curlyoung
> 
> 邮箱：curlyoung@outlook.com
> 
> 涉及领域：数学、通信、计算机、人工智能
> 
> 教育背景：北京邮电大学-电子科学与技术-博士，加泰罗尼亚理工大学-网络与电信系统-访博
> 
> 工作履历：实习(一流科技人工智能 南湖研究院光纤通信 诺基亚无线通信) 入职卫星通信单位至今
> 
> 资格证书：系统架构设计师、网络规划设计师、嵌入式系统工程师；专利代理师资格证、法律职业资格证

# 使用方法

1. 下载并解压本项目，将项目顶层目录修改为你希望命名的项目名，推荐使用 lower_snake_case 小蛇形命名法。

2. 使用 Conda 包管理工具创建一个供该项目使用的同名的环境，将 `AGENTS.md` 中唯一的 `template` 字样修改为你所使用的项目名。

3. 阅读并理解本文件对项目结构的讲解后，将本文件中的内容删除，`README.md` 将被用于你未来项目的描述。

4. 如果你使用 Codex 等 AI 工具辅助工作，请将你本地的 `%USERPROFILE%\.codex\config.toml` 文件与此模板所提供的`config.toml`发给 AI 做对比，它能帮助你查找自己的 Codex 是否设置有不合理的地方，比如未合理安装工作空间等问题。尤其是将其中 Git 自动管理的部分加入到你的配置文件中，这能使得你的版本管理清晰且省心。

   ```tom
   git-pull-request-merge-method = "squash"
   git-commit-instructions = """
   Use Conventional Commits: <type>(<scope>): <summary>
   Allowed types: feat, fix, docs, refactor, perf, test, chore, ci, build.
   Use concise English summaries in imperative mood.
   Keep the summary under 72 characters.
   Use a scope when the affected module is clear.
   Suggested scopes: python, matlab, tests, docs, experiments, results, git.
   Use chore(git) for .gitignore or repository-maintenance changes.
   Do not use vague messages such as "update files", "fix code", or "changes"."""
   ```

5. 如果你所要做的项目需要 MATLAB 或 Python 之外的编程语言，请在 `\code\` 路径下新建相应的目录存放源码。

# 项目结构

```
<repository root>/
│
├── AGENTS.md
├── README.md
├── .gitignore
├── environment.yml
│
├── code/		# 源码区
│   ├── task<id>_<entry_name>.m
│   ├── task<id>_<entry_name>.py
│   ├── task<id>_<entry_name>.yaml
│   ├── python/
│   │   ├── pyproject.toml
│   │   ├── <entry_name>.py
│   │   └── <entry_name>/
│   │   │   ├── __init__.py
│   │   │   └── <entry_name>.py
│   │   ├── configs/
│   │   │   └── <entry_name>.yaml
│   │   └── tests/
│   │       ├── test_<entry_name>.py
│   │       └── outputs/
│   └── matlab/
│       ├── mproject.prj
│       ├── <entry_name>.m
│       ├── +<entry_name>/
│       │   └── <entry_name>.m
│       ├── configs/
│       │   └── <entry_name>.yaml
│       └── tests/
│           ├── test_<entry_name>.m
│           └── outputs/
│
├── data/		# 数据区
│   ├── external/
│   ├── experiment/
│   ├── simulation/
│   └── processed/
│
├── docs/		# 文档区
│   ├── <entry_name>.md
│   ├── tasks/
│   │   └── task<id>_<entry_name>.md
│   └── references/
│       ├── <entry_name>.pdf
│       └── <entry_name>.docx
│
└── results/	# 结果区
    └── task<id>_<entry_name>/
        ├── logs/
        ├── metadata.json
        ├── resolved_config.yaml
        ├── metrics/
        │   ├── <entry_name>.csv
        │   └── <entry_name>.json
        └── figures/
            ├── <entry_name>.png
            └── <entry_name>.svg
```

`environment.yml` 用于描述 conda + pip 环境依赖。

`README.md` 用于描述项目说明、参考链接、复现步骤等项目的概述。

`.gitignore` 是 Git 的忽略规则文件，用于告诉 Git 哪些文件或目录纳入版本控制。

`.git/` 是 Git 元数据目录，用于保存项目版本历史、分支、提交记录、暂存区状态、远程仓库配置等信息。

`AGENTS.md` 为 Codex 提供随仓库生效的项目指导，这是本项目的关键设计，具体内容如下：

## `data/` 数据区

```
data/
├── external/
├── experiment/
├── simulation/
└── processed/
```

**此区域设计目标：让项目数据与程序严格隔离。**`data/` 不纳入版本控制。

`data/external/` 放置由外部获取的源数据；

`data/experiment/` 放置由实验获取的源数据；

`data/simulation/` 放置由仿真获取的源数据；

`data/processed/` 放置由源数据处理后得到的派生数据，供项目直接读取和使用。

## `docs/` 文档区

```
docs/
├── <entry_name>.md
├── tasks/
│   └── task<id>_<entry_name>.md
└── references/
    ├── <entry_name>.pdf
    └── <entry_name>.docx
```

**此区域设计目标：作为 Codex 和开发者理解项目与实施开发的依据。** `docs/references/` 不纳入版本控制。

`docs/` 放置供 Codex 理解项目的 Markdown 文档。

`docs/tasks/` 放置项目的各项任务文档 `task<id>_<entry_name>.md`，描述任务的设计方案，源码区同名任务脚本执行后，将结果、分析结论及相关记录追加至相应文档。

`docs/references/` 放置未经加工的原始参考文档，用于开发者制定项目规划、编写任务文档。

## `results/` 结果区

```
results/
└── task<id>_<entry_name>/
    ├── logs/
    ├── metadata.json
    ├── resolved_config.yaml
    ├── metrics/
    │   ├── <entry_name>.csv
    │   └── <entry_name>.json
    └── figures/
        ├── <entry_name>.png
        └── <entry_name>.svg
```

**此区域设计目标：存放各项任务的执行产物与诊断日志。**`results/` 不纳入版本控制。

`results/task<id>_<entry_name>/` 放置源码区同名任务脚本的执行产物。

`results/task<id>_<entry_name>/logs/` 放置任务运行日志。

`results/task<id>_<entry_name>/metadata.json` 记录任务运行环境信息。

`results/task<id>_<entry_name>/resolved_config.yaml` 记录任务生效的完整配置信息。

`results/task<id>_<entry_name>/metrics/` 放置数值产出，结构信息保存为 `<entry_name>.json` 文件，表格信息保存为 `<entry_name>.csv` 文件。

`results/task<id>_<entry_name>/figures/` 放置图片产出，每张图片保存 PNG 和 SVG 两种格式。

## `code/` 源码区

```
code/
├── task<id>_<entry_name>.m
├── task<id>_<entry_name>.py
├── task<id>_<entry_name>.yaml
├── python/
│   ├── pyproject.toml
│   ├── <entry_name>.py
│   └── <entry_name>/
│   │   ├── __init__.py
│   │   └── <entry_name>.py
│   ├── configs/
│   │   └── <entry_name>.yaml
│   └── tests/
│       ├── test_<entry_name>.py
│       └── outputs/
└── matlab/
    ├── mproject.prj
    ├── <entry_name>.m
    ├── +<entry_name>/
    │   └── <entry_name>.m
    ├── configs/
    │   └── <entry_name>.yaml
    └── tests/
        ├── test_<entry_name>.m
        └── outputs/
```

**此区域设计目标：作为项目的统一任务入口，让模型、算法、逻辑实现为可组合、复用、测试的模块化系统。**`code/python/tests/` 和 `code/matlab/tests/` 不纳入版本控制。

`code/` 根目录下放置任务运行脚本与任务配置文件。`code/task<id>_<entry_name>.py` 与 `code/task<id>_<entry_name>.m` 调用功能源码，`code/task<id>_<entry_name>.yaml` 声明任务需求参数。

`code/python/pyproject.toml` 用于管理 Python 项目的构建配置、项目元信息、依赖环境以及开发工具配置。

`code/python/<entry_name>/` 为 Python package 源码目录，通过 editable 模式安装。

`code/matlab/mproject.prj` 用于定义 MATLAB 工程结构、路径配置、启动环境和工程任务管理。

`code/matlab/+<entry_name>/` 为 MATLAB package 源码目录，通过 package 命名空间组织可复用算法模块和函数接口。

`code/python/configs/` 与 `code/matlab/configs/` 放置默认配置文件，`code/python/configs/<entry_name>.yaml` 与 `code/matlab/configs/<entry_name>.yaml` 声明模块默认参数。

任务运行完毕将任务需求参数、模块默认参数以及运行过程中的覆盖参数一同记录为任务生效的完整配置信息，置于 `results/task<id>_<entry_name>/` 目录下。 

`code/python/tests/` 与 `code/matlab/tests/` 放置测试程序，子目录 `code/python/tests/outputs/` 与 `code/matlab/tests/outputs/` 放置测试输出内容。

所有任务脚本和测试命令均从 `<repository root>/` 执行，执行命令样例如下：

```
conda run -n <env_name> python code/task<id>_<entry_name>.py
matlab -batch "run('code/task<id>_<entry_name>.m')"
conda run -n <env_name> python -m pytest code/python/tests/test_<entry_name>.py
matlab -batch "run('code/matlab/tests/test_<entry_name>.m')"
```

Codex 执行代码修改或验证任务时，优先使用项目已有测试和开发工具链。根据任务需求选择单元测试、冒烟测试、回归测试等验证方式；对于复杂模块，可增加静态检查、覆盖率分析或性能测试。
