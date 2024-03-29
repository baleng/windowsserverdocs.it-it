---
title: Wbadmin get versions
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b986acc4-d083-4d32-9434-862314ed5e97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b7ba0749c8ef347e27590bde4eed7bbcf25af7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362363"
---
# <a name="wbadmin-get-versions"></a>Wbadmin get versions



Elenca i dettagli di backup archiviati nel computer locale o in un altro computer. Quando questo sottocomando viene utilizzato senza parametri, vengono elencati tutti i backup del computer locale, anche se tali backup non sono disponibili. I dettagli forniti per una copia di backup includono l'ora di backup, il percorso di archiviazione di backup, l'identificatore di versione (necessario per il **wbadmin ottenere elementi** sottocomando e per eseguire ripristini) e il tipo di ripristino è possibile eseguire.

Per ottenere dettagli sui backup disponibili tramite questo sottocomando, è necessario essere un membro del **Backup Operators** gruppo o **amministratori** gruppo, oppure è necessario che siano state delegate le autorizzazioni appropriate. Inoltre, è necessario eseguire **wbadmin** da un prompt dei comandi con privilegi elevati. (Per aprire un prompt dei comandi con privilegi elevati **Command prompt** e quindi fare clic su **Esegui come amministratore**.)

Per esempi di come utilizzare questo sottocomando, vedere [esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
wbadmin get versions
[-backupTarget:{<BackupTargetLocation> | <NetworkSharePath>}]
[-machine:BackupMachineName]
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|-backupTarget|Specifica il percorso di archiviazione che contiene i backup che si desidera visualizzare i dettagli per. Utilizzare per l'elenco dei backup archiviati in tale percorso di destinazione. I percorsi di destinazione di backup possono essere collegate localmente le unità disco, volumi, cartelle condivise remote, supporti rimovibili come unità DVD o altri supporti ottici. Se **wbadmin ottenere versioni** viene eseguito nello stesso computer in cui è stato creato il backup, questo parametro non è necessaria. Tuttavia, questo parametro è obbligatorio per ottenere informazioni su un backup creato da un altro computer.|
|-machine|Specifica il computer che si desidera visualizzare dettagli backup per. Utilizzarlo quando nello stesso percorso di archiviazione dei backup di più computer. Deve essere utilizzato quando **- backupTarget** specificato.|

## <a name="remarks"></a>Note

Per elencare gli elementi disponibili per il ripristino da un backup specifico, utilizzare **wbadmin ottenere elementi**.

## <a name="BKMK_examples"></a>Esempi

Per visualizzare un elenco di backup disponibili che vengono archiviati nel volume h, digitare:
```
wbadmin get versions -backupTarget:h:
```
Per visualizzare un elenco dei backup disponibili archiviati nella cartella condivisa remota \\ @ no__t-1servername\share per il computer Server01, digitare:
```
wbadmin get versions -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Altri riferimenti

-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   [Get-WBBackupTarget](https://technet.microsoft.com/library/jj902447.aspx) cmdlet