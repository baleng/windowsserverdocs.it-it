---
title: ren
description: Informazioni su come rinominare un file o una directory con il comando ren.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2ba3f6a13dc03c0b6a5561be9f0f692546a25149
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384584"
---
# <a name="ren"></a>ren

Rinomina file o directory. Questo comando è analogo a come il **rinominare** comando.

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|[\<Drive >:] [\<Path >] \<FileName1 >|Specifica il percorso e nome del file o set di file che si desidera rinominare. *Filename1* può includere caratteri jolly ( **&#42;** e **?** ).|
|\<FileName2 >|Specifica il nuovo nome per il file. È possibile utilizzare caratteri jolly per specificare un nuovo nome per più file.|
|/?|Visualizza la guida al prompt dei comandi.|

## <a name="remarks"></a>Note

- È possibile specificare una nuova unità o percorso quando la ridenominazione dei file.
- Non è possibile utilizzare il **ren** comando per rinominare i file su unità disco o spostare file in una directory diversa.
- È possibile utilizzare caratteri jolly ( **&#42;** e **?** ) in entrambi i parametri *filename* . I caratteri sono rappresentati da caratteri jolly in *FileName2* siano identici ai caratteri corrispondenti in *FileName1*.
- *FileName2* deve essere un nome file univoco. Se *FileName2* corrisponde a un nome di file esistente, **ren** Visualizza il messaggio seguente:  
  ```
  Duplicate file name or file not found
  ```

## <a name="BKMK_examples"></a>Esempi

Per modificare tutte le estensioni di file con estensione txt nella directory corrente alle estensioni di file con estensione doc, digitare:
```
ren *.txt *.doc 
```
Per modificare il nome di una directory da Chap10 in Paragr10, digitare:
```
ren chap10 part10 
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)