---
title: chiamare
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d34a41dc-e6c7-4467-bf6a-15cec704833e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: 0e5f9f2b0102c12ee0925bb434fdeddde85e34cd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379723"
---
# <a name="call"></a>chiamare



Chiama un programma batch da un altro senza arrestare il programma batch padre. Il comando **Call** accetta le etichette come destinazione della chiamata.

> [!NOTE]
> La **chiamata** non ha effetto al prompt dei comandi quando viene usata all'esterno di uno script o di un file batch.

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
call [Drive:][Path]<FileName> [<BatchParameters>] [:<Label> [<Arguments>]]
```

## <a name="parameters"></a>Parametri

|           Parametro           |                                                                         Descrizione                                                                          |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive >:] [\<Path >] <FileName> | Specifica il percorso e il nome del programma batch che si desidera chiamare. Il parametro *filename* è obbligatorio e deve avere un'estensione. bat o. cmd. |
|      \<BatchParameters >       |                                            Specifica le informazioni della riga di comando richieste dal programma batch.                                             |
|           : \<Label >           |                                            Specifica l'etichetta a cui si desidera passare un controllo del programma batch.                                             |
|         \<Arguments >          |                     Specifica le informazioni della riga di comando da passare alla nuova istanza del programma batch, a partire da *: Label.*                     |
|              /?               |                                                             Visualizza la guida al prompt dei comandi.                                                             |

## <a name="batch-parameters"></a>Parametri batch

I riferimenti all'argomento dello script batch ( **% 0**, **% 1**,...) sono elencati nelle tabelle seguenti.

**% @ no__t-2** in uno script batch fa riferimento a tutti gli argomenti (ad esempio, **% 1**, **% 2**, **% 3**...)

È possibile utilizzare le seguenti sintassi facoltative come sostituzioni per i parametri batch ( **% n**):

|Parametro batch|Descrizione|
|---------------|-----------|
|% ~ 1|Espande **% 1** e rimuove le virgolette circostanti ("").|
|% ~ F1|Espande **% 1** in un percorso completo.|
|% ~ D1|Espande **% 1** solo a una lettera di unità.|
|% ~ P1|Espande **% 1** solo in un percorso.|
|% ~ N1|Espande **% 1** solo in un nome file.|
|% ~ X1|Espande **% 1** solo in un'estensione del nome di file.|
|% ~ S1|Espande **% 1** in un percorso completo che contiene solo nomi brevi.|
|% ~ a1|Espande **% 1** sugli attributi del file.|
|% ~ T1|Espande **% 1** alla data e all'ora del file.|
|% ~ Z1|Espande **% 1** fino alla dimensione del file.|
|% ~ $PATH: 1|Esegue la ricerca nelle directory elencate nella variabile di ambiente PATH ed espande **% 1** con il nome completo della prima directory trovata. Se il nome della variabile di ambiente non è definito o il file non viene trovato dalla ricerca, questo modificatore espande la stringa vuota.|

La tabella seguente illustra come è possibile combinare i modificatori con i parametri batch per i risultati composti:

|Parametro batch con modificatore|Descrizione|
|-----------------------------|-----------|
|% ~ DP1|Espande **% 1** in una lettera di unità e un solo percorso.|
|% ~ nx1|Espande **% 1** solo in un nome file e un'estensione.|
|% ~ dp $ PATH: 1|Esegue la ricerca nelle directory elencate nella variabile di ambiente PATH per **% 1**, quindi si espande alla lettera di unità e al percorso della prima directory trovata.|
|% ~ ftza1|Espande **% 1** per visualizzare un output simile al comando **dir** .|

Negli esempi precedenti, **% 1** e Path possono essere sostituiti da altri valori validi. La sintassi <strong>%~</strong> viene terminata con un numero di argomento valido. Non è possibile usare i modificatori <strong>%~</strong> con **% @ no__t-4 @ no__t-5**.

## <a name="remarks"></a>Note

-   Uso dei parametri batch

    I parametri batch possono contenere tutte le informazioni che è possibile passare a un programma batch, incluse le opzioni della riga di comando, i nomi file, i parametri batch da **% 0** a **% 9**e le variabili (ad esempio, **% baud%** ).
-   Uso del parametro *Label*

    Utilizzando **Call** con il parametro *Label* , viene creato un nuovo contesto del file batch e viene passato il controllo all'istruzione dopo l'etichetta specificata. La prima volta che viene rilevata la fine del file batch (ovvero dopo il passaggio all'etichetta), il controllo torna all'istruzione successiva all'istruzione **Call** . La seconda volta che viene rilevata la fine del file batch, lo script batch viene terminato.
-   Uso di pipe e simboli di Reindirizzamento

    Non usare pipe ( **|** ) e i simboli di reindirizzamento ( **<** o **>** ) con **Call**.
-   Esecuzione di una chiamata ricorsiva

    È possibile creare un programma batch che chiama se stesso. Tuttavia, è necessario fornire una condizione di uscita. In caso contrario, i programmi batch padre e figlio possono eseguire un ciclo infinito.
-   Utilizzo di estensioni di comando

    Se sono abilitate le estensioni dei comandi, la **chiamata** accetta l' *etichetta* come destinazione della chiamata. La sintassi corretta è la seguente:

    `call :\<Label> <Arguments>`

## <a name="BKMK_examples"></a>Esempi

Per eseguire il programma denominato nuovo. bat da un altro programma batch, digitare il comando seguente nel programma batch padre:
```
call checknew
```
Se il programma batch padre accetta due parametri batch e si desidera che i parametri vengano passati a denominato nuovo. bat, digitare il comando seguente nel programma batch padre:
```
call checknew %1 %2
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
