---
title: Creazione di volumi in Spazi di archiviazione diretta
description: Come creare volumi in Spazi di archiviazione diretta usando l'interfaccia di amministrazione di Windows e PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 06/06/2019
ms.openlocfilehash: 8c17671f2f15d1373973dcf2fbafc753f0a163a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402884"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Creazione di volumi in Spazi di archiviazione diretta

> Si applica a: Windows Server 2019, Windows Server 2016

Questo argomento descrive come creare volumi in un cluster Spazi di archiviazione diretta usando l'interfaccia di amministrazione di Windows, PowerShell o Gestione cluster di failover.

> [!TIP]
> Se non lo hai già fatto, consulta prima [Pianificazione dei volumi in Spazi di archiviazione diretta](plan-volumes.md).

## <a name="create-a-three-way-mirror-volume"></a>Creazione di un volume mirror a tre vie

Per creare un volume mirror a tre vie nell'interfaccia di amministrazione di Windows: 

1. Nell'interfaccia di amministrazione di Windows connettersi a un cluster Spazi di archiviazione diretta e quindi selezionare **volumi** dal riquadro **strumenti** .
2. Nella pagina volumi selezionare la scheda **inventario** , quindi selezionare **Crea volume**.
3. Nel riquadro **Crea volume** immettere un nome per il volume e lasciare la **resilienza** come **mirroring a tre vie**.
4. In **dimensioni su HDD**specificare le dimensioni del volume. Ad esempio, 5 TB (terabyte).
5. Selezionare **Create**.

A seconda delle dimensioni, la creazione del volume può richiedere alcuni minuti. Le notifiche in alto a destra consentiranno di stabilire quando viene creato il volume. Il nuovo volume verrà visualizzato nell'elenco inventario.

Guarda un breve video su come creare un volume mirror a tre vie.

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>Creare un volume di parità con accelerazione con mirroring

La parità con accelerazione speculare riduce il footprint del volume nel disco rigido. Ad esempio, un volume mirror a tre vie significherebbe che per ogni 10 terabyte di dimensione saranno necessari 30 terabyte come footprint. Per ridurre l'overhead in footprint, creare un volume con parità con accelerazione del mirroring. In questo modo si riduce il footprint da 30 terabyte a soli 22 terabyte, anche con soli 4 server, eseguendo il mirroring del 20% dei dati più attivo e usando la parità, che è più efficiente allo spazio, per archiviare il resto. È possibile modificare questo rapporto di parità e mirroring per migliorare le prestazioni rispetto alla capacità per il proprio carico di lavoro. Ad esempio, la parità del 90% e il mirroring del 10% producono una riduzione delle prestazioni, ma semplifica ulteriormente il footprint.

Per creare un volume con la parità con accelerazione speculare nell'interfaccia di amministrazione di Windows:

1. Nell'interfaccia di amministrazione di Windows connettersi a un cluster Spazi di archiviazione diretta e quindi selezionare **volumi** dal riquadro **strumenti** .
2. Nella pagina volumi selezionare la scheda **inventario** , quindi selezionare **Crea volume**.
3. Nel riquadro **Crea volume** immettere un nome per il volume.
4. In **resilienza**selezionare **parità con accelerazione del mirroring**.
5. In **percentuale parità**selezionare la percentuale di parità.
6. Selezionare **Create**.

Guarda un breve video su come creare un volume di parità con accelerazione speculare.

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>Apri volume e Aggiungi file

Per aprire un volume e aggiungere file al volume nell'interfaccia di amministrazione di Windows:

1. Nell'interfaccia di amministrazione di Windows connettersi a un cluster Spazi di archiviazione diretta e quindi selezionare **volumi** dal riquadro **strumenti** .
2. Nella pagina volumi selezionare la scheda **inventario** .
2. Nell'elenco di volumi selezionare il nome del volume che si desidera aprire.

    Nella pagina dettagli volume è possibile visualizzare il percorso del volume.

4. Nella parte superiore della pagina selezionare **Apri**. Verrà avviato lo strumento file nell'interfaccia di amministrazione di Windows.
5. Passare al percorso del volume. Qui è possibile esplorare i file nel volume.
6. Selezionare **carica**e quindi selezionare un file da caricare.
7. Usare il pulsante **indietro** del browser per tornare al riquadro strumenti nell'interfaccia di amministrazione di Windows.

Guarda un breve video su come aprire un volume e aggiungere file.

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>Attivare la deduplicazione e la compressione

La deduplicazione e la compressione sono gestite per ogni volume. La deduplicazione e la compressione utilizzano un modello di post-elaborazione, il che significa che non sarà possibile visualizzare Risparmi fino a quando non viene eseguito. In tal caso, funzionerà su tutti i file, anche quelli presenti in precedenza.

1. Nell'interfaccia di amministrazione di Windows connettersi a un cluster Spazi di archiviazione diretta e quindi selezionare **volumi** dal riquadro **strumenti** .
2. Nella pagina volumi selezionare la scheda **inventario** .
3. Nell'elenco di volumi selezionare il nome del volume che si desidera gestire.
4. Nella pagina dettagli volume fare clic sull'opzione **deduplicazione e compressione**.
5. Nel riquadro Abilita deduplicazione selezionare la modalità di deduplicazione.

    Anziché le impostazioni complesse, l'interfaccia di amministrazione di Windows consente di scegliere tra profili pronti per diversi carichi di lavoro. Se non si è certi, usare l'impostazione predefinita.

6. Seleziona **Abilita**.

Guarda un breve video su come attivare la deduplicazione e la compressione.

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>Creare volumi con PowerShell

Ti consigliamo di usare il cmdlet **New-Volume** per creare i volumi per Spazi di archiviazione diretta. Offre l'esperienza più semplice e rapida. Questo cmdlet singolo crea automaticamente il disco virtuale, lo divide in partizioni e lo formatta, crea il volume con il nome corrispondente e lo aggiunge ai volumi condivisi del cluster, tutto in un unico, semplice passaggio.

Il cmdlet **New-Volume** prevede quattro parametri che dovrai sempre fornire:

- **FriendlyName** Qualsiasi stringa desiderata, ad esempio *"volume1"*
- **FileSystem** **CSVFS_ReFS** (scelta consigliata) o **CSVFS_NTFS**
- **StoragePoolFriendlyName:** Nome del pool di archiviazione, ad esempio *"S2D in clustername"*
- **Dimensioni:** Dimensioni del volume, ad esempio *"10 TB"*

   > [!NOTE]
   > Windows, incluso PowerShell, conta con numeri binari (in base 2), mentre le unità sono spesso etichettate con numeri decimali (in base 10). Questo spiega perché un'unità da "un terabyte", definita come 1.000.000.000.000 byte, viene visualizzata in Windows come circa "909 GB". Si tratta di un comportamento previsto. Durante la creazione di volumi tramite **New-Volume**, devi specificare il parametro **Size** in numeri binari (in base 2). Ad esempio, se specifichi "909GB" o "0,909495TB", verrà creato un volume di circa 1.000.000.000.000 byte.

### <a name="example-with-2-or-3-servers"></a>Esempio: Con 2 o 3 server

Per semplificare le cose, se la distribuzione include solo due server, Spazi di archiviazione diretta userà automaticamente il mirroring a 2 vie per la resilienza. Se la distribuzione include solo tre server, userà automaticamente il mirroring a 3 vie.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Esempio: Con più di 4 server

Se disponi di quattro o più server, puoi utilizzare il parametro facoltativo **ResiliencySettingName** per scegliere il tipo di resilienza.

-   **ResiliencySettingName** **Mirror** o **parità**.

Nell'esempio seguente, *"Volume2"* usa il mirroring a 3 vie e *"Volume3"* usa la doppia parità (spesso detta "codifica di cancellazione").

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Esempio: Uso di livelli di archiviazione

Nelle distribuzioni con tre tipi di unità, un volume può comprendere i livelli SSD e HDD per risiedere parzialmente su ciascuno. Analogamente, nelle distribuzioni con quattro o più server, un volume può combinare mirroring e doppia parità per risiedere parzialmente su ciascuno.

Per facilitare la creazione di tali volumi, Spazi di archiviazione diretta fornisce modelli di livello predefiniti denominati *Performance* e *Capacity*. Questi modelli incapsulano le definizioni per il mirroring a 3 vie nelle unità di capacità più veloci (ove applicabile) e la doppia parità nelle unità di capacità più lente (ove applicabile).

Puoi vederli eseguendo il cmdlet **Get-StorageTier**.

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![Screenshot di PowerShell con livelli di archiviazione](media/creating-volumes/storage-tiers-screenshot.png)

Per creare volumi a livelli, fai riferimento a questi modelli di livello usando i parametri **StorageTierFriendlyNames** e **StorageTierSizes** del cmdlet **New-Volume**. Ad esempio, il cmdlet seguente crea un solo volume che combina il mirroring a 3 vie e la doppia parità in proporzioni di 30:70.

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

## <a name="create-volumes-using-failover-cluster-manager"></a>Creare volumi tramite Gestione cluster di failover

Puoi inoltre creare volumi tramite la *Creazione guidata nuovo disco virtuale (Spazi di archiviazione diretta)* seguita dalla *Creazione guidata Nuovo volume* da Gestione cluster di failover, anche se il flusso di lavoro include molti più passaggi manuali e non è consigliato.

Ci sono tre passaggi principali:

### <a name="step-1-create-virtual-disk"></a>Passaggio 1: Crea disco virtuale

![Nuovo disco virtuale](media/creating-volumes/GUI-Step-1.png)

1. In Gestione cluster di failover, passa a **Archiviazione** -> **Pool**.
2. Seleziona **Nuovo disco virtuale** dal riquadro Azioni a destra o fai clic con il pulsante destro del mouse sul pool e seleziona **Nuovo disco virtuale**.
3. Seleziona il pool di archiviazione e fai clic su **OK**. La *Creazione guidata nuovo disco virtuale (Spazi di archiviazione diretta)* verrà aperta.
4. Utilizza la procedura guidata per denominare il disco virtuale e specificarne le dimensioni.
5. Rivedi le selezioni e fai clic su **Crea**.
6. Assicurati di selezionare la casella contrassegnata **Crea un volume al termine della procedura guidata** prima della chiusura.

### <a name="step-2-create-volume"></a>Passaggio 2: Crea volume

La *Creazione guidata Nuovo volume* verrà aperta.

7. Seleziona il disco virtuale appena creato e fai clic su **Avanti**.
8. Specifica le dimensioni del volume (impostazione predefinita: le stesse dimensioni del disco virtuale) e fai clic su **Avanti**. 
9. Assegna il volume a una lettera di unità o scegli **Non assegnare a una lettera di unità** e fai clic su **Avanti**.
10. Specifica il file system da utilizzare, lascia la dimensione dell'unità di allocazione come *Predefinita*, assegna un nome al volume e fai clic su **Avanti**.
11. Rivedi le selezioni e fai clic su **Crea**, quindi su **Chiudi**.

### <a name="step-3-add-to-cluster-shared-volumes"></a>Passaggio 3: Aggiungi a volumi condivisi cluster

![Aggiungi a volumi condivisi cluster](media/creating-volumes/GUI-Step-2.png)

12. In Gestione cluster di failover, passa a **Archiviazione** -> **Dischi**.
13. Seleziona il disco virtuale appena creato e seleziona **Aggiungi a volumi condivisi cluster** dal riquadro Azioni a destra o fai clic con il pulsante destro del mouse sul disco virtuale e seleziona **Aggiungi a volumi condivisi cluster**.

Non c'è altro da fare. Ripeti il numero di volte necessario per creare altri volumi.

## <a name="see-also"></a>Vedere anche

- [Panoramica di Spazi di archiviazione diretta](storage-spaces-direct-overview.md)
- [Pianificazione di volumi in Spazi di archiviazione diretta](plan-volumes.md)
- [Estensione di volumi in Spazi di archiviazione diretta](resize-volumes.md)
- [Eliminazione di volumi in Spazi di archiviazione diretta](delete-volumes.md)
