---
title: wmic
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e9840bc20ddf6193241fe36055698e2bd3222496
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361880"
---
# <a name="wmic"></a>wmic



Visualizza le informazioni WMI all'interno di una shell comandi interattiva.

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
command </parameter>
```

## <a name="sub-commands"></a>Comandi secondari

I comandi secondari seguenti sono sempre disponibili:

|Sottocomando|Descrizione|
|-----------|-----------|
|classe|Viene eseguito l'escape dalla modalità alias predefinita di WMIC per accedere direttamente alle classi nello schema WMI.|
|path|Viene eseguito l'escape dalla modalità alias predefinita di WMIC per accedere direttamente alle istanze nello schema WMI.|
|Contesto|Consente di visualizzare i valori correnti di tutti i commutatori globali.|
|[uscire \| uscita]|Chiude la shell dei comandi WMIC.|

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|</parameter>|\<Concise Description, inizia con un verbo. >|
|</param2>|\<Another concise, inizia con un verbo. >|


## <a name="BKMK_examples"></a>Esempi

Per visualizzare i valori correnti di tutte le opzioni globali, digitare:
```
wmic context
```
Viene visualizzato un output simile al seguente:
```
NAMESPACE    : root\cimv2
ROLE         : root\cli
NODE(S)      : BOBENTERPRISE
IMPLEVEL     : IMPERSONATE
[AUTHORITY   : N/A]
AUTHLEVEL    : PKTPRIVACY
LOCALE       : ms_409
PRIVILEGES   : ENABLE
TRACE        : OFF
RECORD       : N/A
INTERACTIVE  : OFF
FAILFAST     : OFF
OUTPUT       : STDOUT
APPEND       : STDOUT
USER         : N/A
AGGREGATE    : ON
```
Per modificare l'ID lingua usato dalla riga di comando in inglese (ID impostazioni locali 409), digitare:
```
wmic /locale:ms_409
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)