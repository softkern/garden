---
title: Zed加Ollama：AI代码编辑器本地版
description: 使用 Zed+Ollama 搭建一个完全免费，自带大模型助手的AI编辑器
date: 2024-12-29
tags:
    - zed
    - ollama
    - ai
---

近几年AI大模型发展迅速，应用到了各行各业，编程领域更是如此，AI编程工具层出不穷，[v0.dev](https://v0.dev/)、 [bolt.new](https://bolt.new/)、[Cursor](https://www.cursor.com/)、[Windsurf](https://codeium.com/windsurf)等等AI代码编辑器也深受程序员喜爱，我也经常使用，体验也确实很好，能够输出直接可用的项目代码，但是想要尽情使用就必须付费了，本篇文章将用 Zed+Ollama 搭建一个完全免费，自带大模型助手的AI编辑器，使用体验虽然不及上述工具，但可以处理以下简单问题。

## Ollama

Ollama 是一个支持在本地管理、部署和运行大模型的工具。可以在自己的电脑上搭建并允许类似 GPT 这样的大模型。

特点：

1. 代码开源，完全免费，离线使用
2. 使用简单，命令行操作方便快捷
3. 支持[多种模型](https://ollama.com/library "多种模型")，例如：[Llama 3](https://ollama.com/library/llama3 "Llama 3"), [Phi 3](https://ollama.com/library/phi3 "Phi 3"), [Mistral](https://ollama.com/library/mistral "Mistral"), [Gemma](https://ollama.com/library/gemma "Gemma")等等

支持的各种开源模型，详细信息可以到[Ollama 官网](https://ollama.com/ "Ollama 官网")查看

|                    |       |       |                                |
| ------------------ | ----- | ----- | ------------------------------ |
| Llama 3            | 8B    | 4.7GB | `ollama run llama3`            |
| Llama 3            | 70B   | 40GB  | `ollama run llama3:70b`        |
| Phi 3 Mini         | 3.8B  | 2.3GB | `ollama run phi3`              |
| Phi 3 Medium       | 14B   | 7.9GB | `ollama run phi3:medium`       |
| Gemma              | 2B    | 1.4GB | `ollama run gemma:2b`          |
| Gemma              | 7B    | 4.8GB | `ollama run gemma:7b`          |
| Mistral            | 7B    | 4.1GB | `ollama run mistral`           |
| Moondream 2        | 1.4B  | 829MB | `ollama run moondream`         |
| Neural Chat        | 7B    | 4.1GB | `ollama run neural-chat`       |
| Starling           | 7B    | 4.1GB | `ollama run starling-lm`       |
| Code Llama         | 7B    | 3.8GB | `ollama run codellama`         |
| Llama 2 Uncensored | 7B    | 3.8GB | `ollama run llama2-uncensored` |
| LLaVA              | 7B    | 4.5GB | `ollama run llava`             |
| Solar              | 10.7B | 6.1GB | `ollama run solar`             |

## 安装 Ollama

Ollama 在官网提供了 MacOS 和 Windows 的图形安装程序，可以直接从 [下载页面](https://ollama.com/download "下载页面")获得对应系统的安装程序，另外为 Linux 系统提供了命令直接进行安装：

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

## 基本使用方法

查看安装情况：

```bash
ollama -v
```

如果输出了版本号，代表安装成功。

运行指定模型:

```bash
ollama run mistral
```

上文的表格中包含了各个模型的运行方式，在初次运行指定模型时会先进行下载，需要一点时间，完成下载后就会直接进入到交互界面：
![](https://img.softkern.com/2024/06/f463285a82e0d9f077eaf6e0f3e1c751.png)

接下来就可以与大模型进行交流了：
![](https://img.softkern.com/2024/06/d267189ddffb007151b1d5371018ffcb.png)

也可以使用中文进行交流：
![](https://img.softkern.com/2024/06/4128bcc7b681f17568d646cfe7aed66a.png)

也可以直接使用阿里的 qwen 和 qwen2 模型：
![](https://img.softkern.com/2024/06/4ca6f64cb2ec2b607c0688796e3f4b2e.png)

## 在 Zed 中使用本地大模型

Zed 是 Atom 和 Tree-sitter 的创建者提供的一个高性能多人代码编辑器。它也是开源的。运行速度飞快，目前插件生态也在逐步完善，感兴趣的可以去[Zed 官网](https://zed.dev/ "官网")查看，这里就不细说了。

Zed 原生便具有助手面板，可以直接输入 openai 的 API 密钥进行使用，而本文要做的就是使用 Ollama 运行的本地大模型来替代 API KEY 。

首先要做的就是下载并运行 `mistral` 模型：

```bash
ollama run mistral
```

然后将其拷贝为 `gpt-4-turbo-preview`:

```bash
ollama cp mistral gpt-4-turbo-preview

```

对 Zed 助手进行配置, 将下面的内容添加到 Zed 的配置文件中：

```bash
{
  "assistant": {
    "version": "1",
    "provider": {
      "name": "openai",
      "type": "openai",
      "default_model": "gpt-4-turbo-preview",
      "api_url": "http://localhost:11434/v1"
    }
  }
}
```

然后在助手面板(assistant panel) 输入密钥后回车，密钥是：

```bash
ollama
```

然后重启 Zed, 就可以体验了:
![](https://img.softkern.com/2024/06/d75ceda202b0568033160a82e9922a4d.png)

## 其他

Ollama 还有很多其他玩法，比如: 搭配 lobechat, 部署一个属于自己的 ChatGPT，如果大家感兴趣，可以到 Ollama 的 Github 仓库查看更多玩法。
