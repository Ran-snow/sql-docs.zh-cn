---
title: azdata notebook 参考
titleSuffix: SQL Server big data clusters
description: azdata notebook 命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f147e2b4ec785c3723d09cac6eb3548511946780
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158232"
---
# <a name="azdata-notebook"></a>azdata notebook

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的参考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata notebook view](#azdata-notebook-view) | 查看笔记本。  用于在首次出现单元执行错误时停止的选项。
[azdata notebook run](#azdata-notebook-run) | 运行笔记本。  首次出现错误时停止执行。
## <a name="azdata-notebook-view"></a>azdata notebook view
此命令可生成笔记本文件，并可将 markdown、代码和输出转换为彩色终端格式。
```bash
azdata notebook view --path -p 
                     [--continue-on-error -c]
```
### <a name="examples"></a>示例
查看笔记本。  这会显示所有单元。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb'
```
查看笔记本。  这会显示所有单元，除非遇到输出中含有错误的单元。  在这种情况下，输出随即停止。
```bash
azdata notebook view --path '/home/me/notebooks/demo_notebook.ipynb' --stop-on-error
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要查看的笔记本的路径。
### <a name="optional-parameters"></a>可选参数
#### `--continue-on-error -c`
继续显示其他单元，并忽略笔记本输出中找到的任何单元错误。  默认行为是出错时停止。  停止使得了解出错的第一个单元更加容易。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。
## <a name="azdata-notebook-run"></a>azdata notebook run
此命令会创建一个临时目录，并将该目录中的指定笔记本中作为工作目录执行。
```bash
azdata notebook run --path -p 
                    [--output-path]  
                    [--output-html]  
                    [--arguments -a]  
                    [--interactive -i]  
                    [--clear -c]
```
### <a name="examples"></a>示例
运行笔记本。
```bash
azdata notebook run --path '/home/me/notebooks/demo_notebook.ipynb'
```
### <a name="required-parameters"></a>必需的参数
#### `--path -p`
要运行的笔记本的文件路径。
### <a name="optional-parameters"></a>可选参数
#### `--output-path`
用于笔记本输出的目录路径。  含有输出数据的笔记本和任何笔记本生成的文件都是相对于此目录而生成的。
#### `--output-html`
可选标志指示是否另外将输出笔记本转换为 HTML 格式。  创建第二个输出文件。
#### `--arguments -a`
要注入到笔记本执行的笔记本参数的可选列表。  编码为 JSON 字典。  示例: "{" name ":" value "," name2 ":" value2 "}"
#### `--interactive -i`
在交互模式下运行笔记本。
#### `--clear -c`
在交互模式下, 在呈现单元格之前清除控制台。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

- 有关其他“azdata”命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 

- 有关如何安装 **azdata** 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。