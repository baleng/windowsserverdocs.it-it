---
title: informazioni e cache Bitsadmin
description: Argomento comandi di Windows per la **cache Bitsadmin e info** -dump di una voce specifica della cache.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11963ff5640ef30e597e5e802778aff121c0efb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381975"
---
# <a name="bitsadmin-cache-and-info"></a>informazioni e cache Bitsadmin



Dump di una voce della cache specifica.

## <a name="syntax"></a>Sintassi

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|RecordID|GUID associato alla voce della cache.|

## <a name="BKMK_examples"></a>Esempi

Nell'esempio seguente viene eseguito il dump della voce della cache con RecordID di {6511FB02-E195-40A2-B595-E8E2F8F47702}.
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)