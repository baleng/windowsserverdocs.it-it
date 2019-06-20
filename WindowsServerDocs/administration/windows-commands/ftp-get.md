---
title: ftp get
description: Ottenere argomento i comandi di Windows per il servizio ftp
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d70355c4-58ef-43e0-916b-c7ecf77e6ee4 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28961ccf0ae04b52586728f9c68a9b2ca3e69b1d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438772"
---
# <a name="ftp-get"></a>ftp: get

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Copia un file remoto nel computer locale usando il tipo di trasferimento di file corrente.   
## <a name="syntax"></a>Sintassi  
```  
get <remoteFile> [<LocalFile>]  
```  
### <a name="parameters"></a>Parametri  

|   Parametro   |                                                              Descrizione                                                               |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------|
| <remoteFile>  |                                                   Specifica il file remoto da copiare.                                                   |
| [<LocalFile>] | Specifica il nome del file da utilizzare nel computer locale. Se *LocalFile* non viene specificato, il file viene assegnato il *FileRemoto* nome. |

## <a name="remarks"></a>Note  
Il **ottenere** è identico al comando il **recv** comando.  
## <a name="BKMK_Examples"></a>Esempi  
Copia **txt** nel computer locale usando il tipo di trasferimento di file corrente.  
```  
get test.txt  
```  
Copia **test. txt** nel computer locale come **test1.txt** utilizzando il file corrente tipo di trasferimento.  
```  
Get test.txt test1.txt  
```  
## <a name="additional-references"></a>Riferimenti aggiuntivi  
-   [ftp: ascii](ftp-ascii.md)  
-   [ftp: binary](ftp-binary.md)  
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)  