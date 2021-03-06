---
title: verify
description: 用于验证的 Windows 命令主题，它会告知**cmd**是否验证文件已正确写入磁盘。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a0777999a604a23e2de83eda6b89c926cb241c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830050"
---
# <a name="verify"></a>verify



告诉**cmd**是否验证文件是否已正确写入磁盘。 如果不使用参数，则**验证**将显示当前设置。

有关如何使用此命令的示例，请参阅[示例](#BKMK_examples)。

## <a name="syntax"></a>语法

```
verify [on | off]
```

### <a name="parameters"></a>参数

|参数|说明|
|---------|-----------|
|[打开 \|]|打开或关闭**验证**设置。|
|/?|在命令提示符下显示帮助。|

## <a name="examples"></a><a name=BKMK_examples></a>示例

若要显示当前**验证**设置，请键入：
```
verify
```
若要启用**验证**设置，请键入：
```
Verify on
```

## <a name="additional-references"></a>其他参考

- [命令行语法项](command-line-syntax-key.md)