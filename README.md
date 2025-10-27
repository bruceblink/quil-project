# quil-project

简洁的 Quil + Clojure 示例/启动项目（sketch），用于快速创建交互式可视化与实验。


## 目录

- [简介](#简介)
- [要求](#要求)
- [安装](#安装)
- [运行](#运行)
- [示例代码](#示例代码)
- [项目结构](#项目结构)
- [依赖建议](#依赖建议)
- [贡献](#贡献)
- [许可证](#许可证)


## 简介

此仓库包含基于 Quil（Clojure 封装的 Processing）的小型示例与启动代码，方便快速搭建交互式图形草图（sketch）。适用于学习 Quil、快速原型或教学演示。

## 要求

- Java 8+
- Clojure（建议 1.10+）
- Leiningen 或 Clojure CLI（clj）

## 安装

克隆仓库：

```bash
git clone https://github.com/bruceblink/quil-project.git
cd quil-project
```

使用 Leiningen：

```bash
lein deps
```

或使用 Clojure CLI（若使用 deps.edn）：

```bash
clj -Sdeps '{:deps {}}
```

（视项目实际配置选择一种构建工具）

## 运行

使用 Leiningen（若 project.clj 配置了 main）：

```bash
lein run
```

使用 Clojure CLI（替换为实际的 main 命名空间）：

```bash
clj -M -m quil-project.core
```

如果不了解 main 命名空间，请在 `src/` 下查找包含 -main 或 quil/start 调用的命名空间并替换上面的 `quil-project.core`。

在 REPL 中启动（便于交互开发）：

```bash
# Leiningen
lein repl
# 或 Clojure CLI
clj
```

在 REPL 中加载并运行示例命名空间，例如：

```clojure
(require '[quil.core :as q])
(require '[quil-project.core :as core])
(core/start)
```

## 示例代码

下面是一个最小的 Quil sketch 示例，供参考：

```clojure
(ns quil-project.core
  (:require [quil.core :as q]))

defn setup []
  (q/frame-rate 30)
  {:x 0})

(defn update-state [state]
  (update state :x inc))

(defn draw-state [state]
  (q/background 255)
  (q/fill 0)
  (q/ellipse (:x state) 100 50 50))

(defn -main [& _]
  (q/defsketch example
    :title "quil-project: example"
    :size [600 400]
    :setup setup
    :update update-state
    :draw draw-state))
```

将上述代码保存为 `src/quil_project/core.clj` 或相应命名空间，然后运行。

## 项目结构（示例）

- src/ - 源代码
- resources/ - 资源文件（图片、配置等）
- deps.edn / project.clj - 构建与依赖
- README.md - 项目说明

## 依赖建议

在 deps.edn 或 project.clj 中添加 Quil：

- [quil "3.1.0"]

根据需要调整 Clojure 与 Quil 的版本。

## 贡献

欢迎通过 issues 或 pull requests 贡献。请在 PR 中说明变更目的、复现步骤以及如何测试。

建议在提交前运行 linter/格式化工具并确保示例可以在本地启动。

## 许可证

本仓库默认使用 MIT 许可证（如需更改，请添加或替换 LICENSE 文件）。
