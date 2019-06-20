---
title: ftp ls_1
description: 'Argomento i comandi di Windows per * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6abf8466f90ac29846f2e1ee7d305e7e4280231e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438629"
---
# <a name="ftp-ls1"></a>ftp: ls_1

> Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> 
> Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Visualizza un elenco abbreviato di file e le sottodirectory del computer remoto.   
## <a name="syntax"></a>Sintassi  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Parametri  

|      Parametro      |                                                                       Descrizione                                                                        |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<remotedirectory>] | Specifica la directory per il quale si desidera visualizzare un elenco. Se non viene specificata alcuna directory, viene utilizzata la directory di lavoro corrente nel computer remoto. |
|    [<LocalFile>]    |               Specifica un file locale in cui archiviare l'elenco. Se non viene specificato un file locale, i risultati vengono visualizzati sullo schermo.               |

## <a name="BKMK_Examples"></a>Esempi  
Visualizzare un breve elenco dei file e le sottodirectory del computer remoto.  
```  
ls  
```  
Ottenere un elenco delle directory abbreviato **dir1** nel computer remoto e salvarlo in un file locale denominato **Elendir. txt.**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Riferimenti aggiuntivi  
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)  