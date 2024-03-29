---
title: Copia reg
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a82b17b631d4242fa6affdec0ff67b5b09380550
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371785"
---
# <a name="reg-copy"></a>Copia reg



Copia una voce del Registro di sistema in una posizione specificata nel computer locale o remoto.

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|\<KeyName1 >|Specifica il percorso completo della sottochiave da copiare. Per specificare un computer remoto, includere il nome del computer (nel formato \\ @ no__t-1ComputerName @ no__t-2 come parte del *nome*della pagina. Se si omette \\ @ no__t-1ComputerName \, l'operazione viene impostata sul computer locale per impostazione predefinita. Il *KeyName* deve includere una chiave radice valido. Le chiavi radice valide per il computer locale sono: HKLM, HKCU, HKCR, HKU e HKCC. Se viene specificato un computer remoto, le chiavi radice valide sono: HKLM e HKU.|
|\<KeyName2 >|Specifica il percorso completo della destinazione della sottochiave. Per specificare un computer remoto, includere il nome del computer (nel formato \\ @ no__t-1ComputerName @ no__t-2 come parte del *nome*della pagina. Se si omette \\ @ no__t-1ComputerName \, l'operazione viene impostata sul computer locale per impostazione predefinita. Il *KeyName* deve includere una chiave radice valido. Le chiavi radice valide per il computer locale sono: HKLM, HKCU, HKCR, HKU e HKCC. Se viene specificato un computer remoto, le chiavi radice valide sono: HKLM e HKU.|
|/s|Copia tutte le sottochiavi e le voci nella sottochiave specificata.|
|/f|Copia la sottochiave senza chiedere conferma.|
|/?|Visualizza la Guida per **reg** Copia al prompt dei comandi.|

## <a name="remarks"></a>Note

-   Reg non chiede conferma per la copia di una sottochiave.
-   Nella tabella seguente sono elencati i valori restituiti per il **Copia reg** operazione.

|Value|Descrizione|
|-----|-----------|
|0|Riuscito|
|1|Errore|

## <a name="BKMK_examples"></a>Esempi

Per copiare tutte le sottochiavi e valori della chiave MyApp chiave SalvaMiaApp, digitare:
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
Per copiare tutti i valori nella chiave MyCo nel computer denominato ZODIAC nella chiave MyCo1 del computer corrente, digitare:
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)