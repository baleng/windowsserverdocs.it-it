---
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
title: Fsutil objectid
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 509e58b85842826b71cb1bfed72ae4c7e5337e25
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376828"
---
# <a name="fsutil-objectid"></a>Fsutil objectid
>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Gestisce gli identificatori di oggetto (OID), che sono oggetti interni utilizzati dal servizio client di rilevamento collegamento distribuito (DLT) e dal servizio Replica file (FRS) per tenere traccia di altri oggetti, ad esempio file, directory e collegamenti. Gli identificatori di oggetto sono invisibili alla maggior parte dei programmi e non devono mai essere modificati.

> [!CAUTION]
> Non eliminare, impostare o modificare in altro modo un identificatore di oggetto. L'eliminazione o l'impostazione di un identificatore di oggetto può comportare la perdita di dati da parti di un file, fino a includere interi volumi di dati. Inoltre, è possibile che si verifichi un comportamento negativo nel servizio client di rilevamento dei collegamenti distribuiti (DLT) e nel servizio Replica file (FRS).

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
fsutil objectid [create] <FileName>
fsutil objectid [delete] <FileName>
fsutil objectid [query] <FileName>
fsutil objectid [set] <ObjectID> <BirthVolumeID> <BirthObjectID> <DomainID> <FileName>
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|-------------|---------------|
|creazione|Crea un identificatore di oggetto se il file specificato non ne contiene già uno. Se il file ha già un identificatore di oggetto, questo sottocomando è equivalente al sottocomando della **query** .|
|Elimina|Elimina un identificatore di oggetto.|
|query|Esegue una query su un identificatore di oggetto.|
|set|Imposta un identificatore di oggetto.|
|\<ObjectID >|Imposta un identificatore esadecimale a 16 byte specifico del file che è sicuramente univoco all'interno di un volume. L'identificatore di oggetto viene utilizzato dal servizio client di rilevamento collegamento distribuito (DLT) e dal servizio Replica file (FRS) per identificare i file.|
|\<BirthVolumeID >|Indica il volume in cui si trovava il file quando è stato ottenuto per la prima volta un identificatore di oggetto. Questo valore è un identificatore esadecimale a 16 byte utilizzato dal servizio client DLT.|
|\<BirthObjectID >|Indica l'identificatore di oggetto originale del file (l' *ObjectID* può cambiare quando viene spostato un file). Questo valore è un identificatore esadecimale a 16 byte utilizzato dal servizio client DLT.|
|\<DomainID >|identificatore di dominio esadecimale a 16 byte. Questo valore non è attualmente in uso e deve essere impostato su tutti zeri.|
|\<> FileName|Specifica il percorso completo del file, inclusi il nome file e l'estensione, ad esempio C:\documents\filename.txt.|

## <a name="remarks"></a>Note

-   Qualsiasi file con un identificatore di oggetto ha anche un identificatore di volume di nascita, un identificatore di oggetto di nascita e un identificatore di dominio. Quando si sposta un file, è possibile che l'identificatore dell'oggetto venga modificato, ma che il volume di nascita e gli identificatori di oggetti di nascita rimangano invariati. Questo comportamento consente al sistema operativo Windows di trovare sempre un file, indipendentemente dalla posizione in cui è stato spostato.

## <a name="BKMK_examples"></a>Esempi
Per creare un identificatore di oggetto, digitare:

`fsutil objectid create c:\temp\sample.txt`

Per eliminare un identificatore di oggetto, digitare:

`fsutil objectid delete c:\temp\sample.txt`

Per eseguire una query su un identificatore di oggetto, digitare:

`fsutil objectid query c:\temp\sample.txt`

Per impostare un identificatore di oggetto, digitare:

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

#### <a name="additional-references"></a>Altri riferimenti
[Indicazioni generali sulla sintassi della riga di comando](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


