---
title: prompt
description: Informazioni su come personalizzare il prompt dei comandi.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d98e965-02eb-46ad-9d0a-5dc44830373e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2df80d3af6344644a68b1b2d01ba48fbf41f1581
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372023"
---
# <a name="prompt"></a>prompt



Modifica il prompt dei comandi cmd. exe. Se utilizzata senza parametri, la **richiesta** Reimposta il prompt dei comandi sull'impostazione predefinita, che corrisponde alla lettera di unità corrente e alla directory seguita dal simbolo di maggiore di ( **>** ).

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
prompt [<Text>]
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|\<Text >|Specifica il testo e le informazioni che si desidera includere nel prompt dei comandi.|
|/?|Visualizza la guida al prompt dei comandi.|

## <a name="remarks"></a>Note

È possibile personalizzare il prompt dei comandi per visualizzare il testo desiderato, incluse informazioni quali il nome della directory corrente, l'ora e la data e il numero di versione di Microsoft Windows.

Nella tabella seguente sono elencate le combinazioni di caratteri che è possibile includere anziché o in aggiunta a una o più stringhe di caratteri nel parametro di *testo* . L'elenco include una breve descrizione del testo o delle informazioni aggiunte da ogni combinazione di caratteri al prompt dei comandi.  

| Carattere |                                 Descrizione                                 |
|-----------|-----------------------------------------------------------------------------|
|    $q     |                               = (segno di uguale)                                |
|    $$     |                               $ (segno di dollaro)                               |
|    $t     |                                Ora corrente                                 |
|    $d     |                                Data corrente                                 |
|    $p     |                           Unità e percorso correnti                            |
|    $v     |                           Numero di versione di Windows                            |
|    $n     |                                Unità corrente                                |
|    $g     |                            > (segno di maggiore di)                            |
|    $l     |                             < (segno minore di)                              |
|    $b     |                              \| (simbolo pipe)                               |
|    $_     |                               ENTER-AVANZAMENTO RIGA                                |
|    $e     |                         Codice di escape ANSI (codice 27)                          |
|    $h     | BACKSPACE (per eliminare un carattere che è stato scritto nella riga di comando) |
|    $a     |                                & (e commerciale)                                |
|    $c     |                            (parentesi aperte)                             |
|    $f     |                            ) (parentesi destra)                            |
|    $s     |                                    spazio                                    |

Quando sono abilitate le estensioni dei comandi (impostazione predefinita), il comando **Richiedi** supporta i caratteri di formattazione seguenti:  

|Carattere|Descrizione|
|---------|-----------|
|$+|Zero o più segni di addizione ( **+** ), a seconda della profondità dello stack di directory **push** (un carattere per ogni livello inserito).|
|$m|Nome remoto associato alla lettera di unità corrente o alla stringa vuota se l'unità corrente non è un'unità di rete.|

Se si include il carattere **$p** nel parametro di testo, il disco viene letto dopo aver immesso ogni comando (per determinare l'unità e il percorso correnti). Questa operazione può richiedere più tempo, soprattutto per le unità disco floppy.

## <a name="BKMK_examples"></a>Esempi

Per impostare un prompt dei comandi a due righe con l'ora e la data correnti nella prima riga e il segno di maggiore rispetto alla riga successiva, digitare:
```
prompt $d$s$s$t$_$g 
```
Il prompt viene modificato nel modo seguente, in cui la data e l'ora sono correnti:
```
Fri 06/01/2007  13:53:28.91
>
```
Per impostare il prompt dei comandi per la visualizzazione come una freccia (`-->`), digitare:
```
prompt --$g
```
Per modificare manualmente il prompt dei comandi nell'impostazione predefinita, ovvero l'unità e il percorso correnti seguiti dal segno di maggiore di, digitare:
```
prompt $p$g
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
