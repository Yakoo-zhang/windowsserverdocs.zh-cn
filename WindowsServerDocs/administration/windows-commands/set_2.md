---
title: set_2
description: 适用于 set_2 的 Windows 命令主题，用于设置用于创建卷影副本的上下文、选项、详细模式和元数据文件。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fa467625997824a11b2303572a063d591f59bdd6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834380"
---
# <a name="set_2"></a>set_2

设置用于创建卷影副本的上下文、选项、详细模式和元数据文件。 如果不使用参数，则**set**会列出所有当前设置。

## <a name="syntax"></a>语法

```
set
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
set verbose {on|off}
set metadata <MetaData.cab>
```

## <a name="set-sub-commands"></a>设置子命令

|子命令|说明|
|-----------|-----------|
|上下文|设置用于创建卷影副本的上下文。 请参阅设置语法和参数的[上下文](set-context.md)。|
|选项|设置创建卷影副本的选项。 有关语法和参数，请参阅[Set 选项](set-option.md)。|
|详细|打开或关闭详细输出模式。 请参阅[设置详细](set-verbose.md)的语法和参数。|
|metadata|设置阴影创建元数据文件的名称和位置。 请参阅设置语法和参数的[元数据](set-metadata.md)。|
|/?|在命令提示符下显示帮助。|

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)