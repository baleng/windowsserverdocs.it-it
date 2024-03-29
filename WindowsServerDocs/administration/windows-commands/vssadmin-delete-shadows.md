---
title: Vssadmin Elimina ombre
description: Descrizione del comando vssadmin delete Shadows.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9779da98ecb43245fe206390d9b70471f15d706e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362609"
---
# <a name="vssadmin-delete-shadows"></a>Vssadmin Elimina ombre

>Si applica a: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Elimina le copie shadow di un volume specificato.

## <a name="syntax"></a>Sintassi

```PowerShell
vssadmin delete shadows /for=<ForVolumeSpec> [/oldest | /all | /shadow=<ShadowID>] [/quiet]
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---|---|
|/for = \<ForVolumeSpec >|Specifica la copia shadow del volume che verrà eliminata.|
|/oldest|Elimina solo la copia shadow meno recente.|
|/all|Elimina tutte le copie shadow del volume specificato.|
|/Shadow = \<ShadowID >|Elimina la copia shadow specificata da IDShadow. Per ottenere l'ID della copia shadow, usare il comando **vssadmin list shadows** . Quando si immette un ID copia shadow, usare il formato seguente, dove ogni *X* rappresenta un carattere esadecimale:<br><br>XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX|
|/quiet|Specifica che il comando non visualizzerà i messaggi durante l'esecuzione.|

## <a name="remarks"></a>Note

È possibile eliminare solo le copie shadow con il tipo accessibile dal client.

## <a name="examples"></a>Esempi

Per eliminare la copia shadow meno recente del volume C, immettere questo comando:

```PowerShell
vssadmin delete shadows /for=c: /oldest
```

## <a name="additional-references"></a>Altri riferimenti

* [Chiave sintassi della riga di comando](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771080(v%3dws.11))
* [Vssadmin](vssadmin.md)
* [Ombreggiatura elenco Vssadmin](vssadmin-list-shadows.md)