---
title: Modificare un disco GPT (Tabella di partizione GUID - GUID partition table) in un disco MBR (Record di avvio principale, Master Boot Record)
description: Descrive come modificare un disco con stile di partizione GPT (Tabella di partizione GUID - GUID partition table) in un disco con stile di partizione MBR (Record di avvio principale, Master Boot Record).
ms.date: 06/19/2018
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5cd345230ce5c0fc556bfd8b421d866bd827507b
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812450"
---
# <a name="convert-a-gpt-disk-into-an-mbr-disk"></a>Convertire un disco GPT in un disco MBR

> **Si applica a:** Windows 10, Windows 8.1, Windows Server (canale semestrale), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

I dischi MBR (Master Boot Record) usano la tabella di partizione BIOS standard. I dischi GPT (GUID Partition Table) utilizzano Unified Extensible Firmware Interface (UEFI). I dischi MBR non supportano più di quattro partizioni in ciascun disco. Il metodo di partizione MBR non è consigliato per i dischi più grandi di due terabyte (TB).

È possibile modificare un disco dallo stile di partizione GPT a MBR, purché il disco sia vuoto e non contenga volumi.

> [!NOTE]
> Prima di convertire un disco, eseguire il backup tutti i dati su di esso e chiudere tutti i programmi che accedono al disco.

> [!NOTE]
> Per completare questi passaggi, devi essere un membro del gruppo **Backup Operators** o **Administrators**.

## <a name="converting-using-the-windows-interface"></a>Conversione tramite l'interfaccia di Windows

1.  Eseguire il backup di tutti i volumi sul disco GPT di base che si desidera convertire in un disco MBR.

2.  Se il disco contiene partizioni o volumi, fare clic con il pulsante destro del mouse su ciascuno di essi e quindi fare clic su **Elimina Volume**.

3.  Fare clic con il pulsante destro del mouse sul disco GPT che si desidera convertire in un disco MBR, quindi fare clic su **Converti in disco MBR**.

## <a name="converting-using-a-command-line"></a>Conversione tramite la riga di comando

1.  Eseguire il backup di tutti i volumi sul disco GPT di base che si desidera convertire in un disco MBR.

2.  Aprire un prompt dei comandi con privilegi elevati facendo clic con il pulsante destro del mouse su **Prompt dei comandi** e selezionando **Esegui come amministratore**.

3. Digitare `diskpart`. Se il disco non contiene partizioni, andare al passaggio 6.

4.  Al prompt **DISKPART** digita `list disk`. Prendere nota del numero di disco che si desidera eliminare.

5.  Al prompt **DISKPART** digita `select disk <disknumber>`.

6.  Al prompt **DISKPART** digita `clean`.

    > [!IMPORTANT]
    > L'esecuzione del comando **clean** eliminerà tutte le partizioni o volumi sul disco.

7.  Al prompt **DISKPART** digita `convert mbr`.

|                Value                  |      Descrizione   |
| ------------------------------------- | -----------------  |
|  <strong>disco di elenco</strong>  | Visualizza un elenco di dischi e le relative informazioni, ad esempio le dimensioni, quantità di spazio libero, se il disco è un disco di base o dinamico e se il disco usa lo stile di partizione MBR (Record di avvio principale, Master Boot Record) o GPT (Tabella di partizione GUID, GUID Partition Table). Il disco contrassegnato con un asterisco (\*) ha lo stato attivo. |
| <strong>Selezionare disco</strong> |                                                                                                          Seleziona il disco specificato, dove <em>disknumber</em> è il numero del disco, assegnandogli lo stato attivo.                                                                                                           |
| <strong>Convertire mbr</strong> |                                                                               Converte un disco di base vuoto con lo stile di partizione GPT in un disco di base con lo stile di partizione MBR.                                                                                |

## <a name="see-also"></a>Vedere anche

-   [Notazione della sintassi della riga di comando](https://technet.microsoft.com/library/cc742449(v=ws.11).aspx)