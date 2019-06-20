---
title: agente di scrittura
description: 'Argomento i comandi di Windows per * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cf98295-411d-4705-8573-f898ff45c140
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8aee4ecca85c7d5f46ee79f3ad928b746c02e7bb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439982"
---
# <a name="writer"></a>agente di scrittura



verifica che un writer o un componente è incluso o esclude un writer o un componente della procedura di backup o ripristino. Se utilizzata senza parametri, **writer** Visualizza la Guida al prompt dei comandi.

## <a name="syntax"></a>Sintassi

```
writer verify [<Writer> | <Component>]
writer exclude [<Writer> | <Component>]
```

## <a name="parameters"></a>Parametri

| Parametro  |                                                                                      Descrizione                                                                                      |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   verify   | Verifica che il writer specificato o il componente è incluso nella procedura di backup o ripristino. La procedura di backup o ripristino avrà esito negativo se il writer o il componente non è incluso. |
|  exclude   |                                                   Esclude il writer specificato o il componente della procedura di backup o ripristino.                                                    |
| [\<Writer> |                                                                                     <Component>]                                                                                      |

## <a name="BKMK_examples"></a>Esempi

Per verificare un writer, specificando il relativo GUID (ad esempio, 4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f), digitare:
```
writer verify {4dc3bdd4-ab48-4d07-adb0-3bee2926fd7f}
```
Per escludere un writer con il nome "Del Writer del sistema", digitare:
```
writer exclude "System Writer"
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)