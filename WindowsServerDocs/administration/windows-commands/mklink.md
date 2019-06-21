---
title: mklink
description: 'Argomento i comandi di Windows per * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ce4df22-2dbc-48fc-9c16-b721ae85f857
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ea80b81b268b31f637c72a828fee8b6f0229a47
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280021"
---
# <a name="mklink"></a>mklink
Crea un collegamento simbolico.

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
mklink [[/d] | [/h] | [/j]] <Link> <Target>
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|/d|Crea un collegamento simbolico di directory. Per impostazione predefinita **mklink** crea un collegamento simbolico del file.|
|/h|Crea un collegamento fisso anziché un collegamento simbolico.|
|/j|Crea una giunzione Directory.|
|\<Collegamento >|Specifica il nome del collegamento simbolico che viene creato.|
|\<Target>|Specifica il percorso (relativo o assoluto) che si intende il nuovo collegamento simbolico.|
|/?|Visualizza la guida al prompt dei comandi.|

## <a name="BKMK_examples"></a>Esempi

L'esempio seguente illustra la creazione e la rimozione di un collegamento simbolico denominato MyFolder e MyFile.file dalla directory radice della directory \Users\User1\Documents e un example.file che si trova all'interno della directory:
```
mklink /d \MyFolder \Users\User1\Documents
mklink /h \MyFile.file \User1\Documents\example.file
rd \MyFolder
del \MyFile.file
```
## <a name="additional-references"></a>Altri riferimenti
-   [New-Item](https://docs.microsoft.com/powershell/module/microsoft.powershell.management/new-item?view=powershell-6)
-   [del](https://docs.microsoft.com/windows-server/administration/windows-commands/del)
-   [rmdir](https://docs.microsoft.com/windows-server/administration/windows-commands/rd)
