---
title: stato gestione-BDE
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 235db54ef2361c0e95c66b15a15be7f188fb74d9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373861"
---
# <a name="manage-bde-status"></a>Manage-bde: stato



Fornisce le seguenti informazioni su tutte le unità del computer. Se sono protette con BitLocker:
-   Size
-   Versione di BitLocker
-   Stato di conversione
-   Percentuale crittografata
-   Metodo di crittografia
-   Stato di protezione
-   Stato di blocco
-   Campo di identificazione
-   Protezioni con chiave

Per esempi di come è possibile utilizzare questo comando, vedere [esempi](#BKMK_Examples).

## <a name="syntax"></a>Sintassi

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|\<Drive >|Rappresenta una lettera di unità seguita da due punti.|
|-protectionaserrorlevel|Fa sì che lo strumento da riga di comando Manage-bde inviare il codice restituito pari a 0 quando il volume è protetto e 1 quando il volume è protetto; più comunemente utilizzata per gli script batch per determinare se un'unità protetta da BitLocker. È inoltre possibile utilizzare **-p** come una versione abbreviata di questo comando.|
|-computername|Specifica che verrà utilizzato Gestione bde.exe per modificare la protezione BitLocker su un computer diverso. È inoltre possibile utilizzare **- cn** come una versione abbreviata di questo comando.|
|\<Nome >|Rappresenta il nome del computer in cui si desidera modificare la protezione BitLocker. I valori accettati includono nome NetBIOS del computer e l'indirizzo IP del computer.|
|-? o /?|Visualizza una breve guida al prompt dei comandi.|
|-Help o-h|Visualizza la Guida completa al prompt dei comandi.|

## <a name="BKMK_Examples"></a>Esempi

Nell'esempio seguente viene illustrato l'utilizzo di **-stato** comando per visualizzare lo stato dell'unità C.
```
manage-bde –status C:
```

#### <a name="additional-references"></a>Altri riferimenti

-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)