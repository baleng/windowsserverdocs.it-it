---
title: 'secedit: analizza'
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fd12d5055853a97b6bd253a83798d35effaa1f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371174"
---
# <a name="seceditanalyze"></a>secedit: analizza



Consente di analizzare le impostazioni correnti di sistemi con le impostazioni di base che vengono archiviate in un database. Per esempi di come è possibile utilizzare questo comando, vedere [esempi](#BKMK_Examples).

## <a name="syntax"></a>Sintassi

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

### <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|db|Obbligatorio.</br>Specifica il percorso e il nome di un database che contiene la configurazione memorizzata con cui verrà eseguita l'analisi.</br>Se il nome di file specifica un database che non ha un modello di sicurezza (come indicato dal file di configurazione) associato, il `/cfg \<configuration file name>` essere specificata anche l'opzione della riga di comando.|
|config.|Facoltativo.</br>Specifica il percorso e il nome del modello di protezione che verrà importato nel database per l'analisi.</br>Questa opzione /cfg è valida solo quando utilizzato con il `/db \<database file name>` parametro. Se non viene specificato, l'analisi viene eseguita con le configurazioni già memorizzate nel database.|
|overwrite|Facoltativo.</br>Specifica se il modello di sicurezza nel parametro /cfg sovrascriverà qualsiasi modello o modello composito, che viene archiviato nel database anziché aggiungere i risultati al modello archiviato.</br>Questa opzione della riga di comando è valido solo quando il `/cfg \<configuration file name>` parametro viene utilizzato anche. Se non viene specificato, il modello nel parametro /cfg viene aggiunto al modello archiviato.|
|log|Facoltativo.</br>Specifica il percorso e il nome del file di log da utilizzare nel processo.|
|quiet|Facoltativo.</br>Disattiva l'output dello schermo. È possibile visualizzare i risultati di analisi tramite l'analisi e configurazione della protezione snap-in a Microsoft Management Console (MMC).|

## <a name="remarks"></a>Note

I risultati dell'analisi vengono archiviati in un'area separata del database e possono essere visualizzati nella configurazione della protezione e analisi snap-in MMC.

Se il percorso del file di log non viene specificato, viene usato il file di logpredefinito, ovvero systemroot\*\Documents and Settings AccountUtente<em>\My Documents\Security\Logs\*DatabaseName</em>. log.

In Windows Server 2008, `Secedit /refreshpolicy` è stato sostituito con `gpupdate`. Per informazioni su come aggiornare le impostazioni di sicurezza, vedere [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Esempi

Eseguire l'analisi per i parametri di sicurezza nel database di protezione, SecDbContoso.sdb, creato utilizzando la configurazione della protezione e snap-in analisi. Indirizzare l'output al file SecAnalysisContosoFY11 con cui viene richiesto, consente di verificare il comando eseguito correttamente.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
Si direbbe che l'analisi ha rivelato alcune carenze, quindi il modello di sicurezza SecContoso. inf è stato modificato. Eseguire nuovamente il comando per rendere effettive le modifiche, indirizzando l'output al file esistente SecAnalysisContosoFY11 senza richiesta.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>Altri riferimenti

-   [Secedit](secedit.md)
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)