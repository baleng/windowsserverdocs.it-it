---
ms.assetid: f0d4cecc-5a03-448c-bef9-86c4730b4eb0
title: Panoramica di bilanciamento del carico di macchine virtuali
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: bhattacharyaz
manager: eldenc
ms.author: subhatt
ms.date: 09/19/2016
ms.openlocfilehash: 125dd7421cc1876c07983016498a9689d8a507ac
ms.sourcegitcommit: a3c9a7718502de723e8c156288017de465daaf6b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/19/2019
ms.locfileid: "65475992"
---
# <a name="virtual-machine-load-balancing-overview"></a>Panoramica di bilanciamento del carico di macchine virtuali

> Si applica a: Windows Server 2019, Windows Server 2016

Un fattore fondamentale per le distribuzioni di cloud privato è il (spese in conto capitale<abbr title="spese in conto capitale">CapEx</abbr>) necessario per passare alla fase di produzione. È molto comune per aggiungere ridondanza per le distribuzioni di cloud privato per evitare la capacità in difetto durante il picco di traffico nell'ambiente di produzione, ma in questo modo aumenta <abbr title="spese in conto capitale">CapEx</abbr>. La necessità di ridondanza è dovuta a un utilizzo non equilibrato nei cloud privati in cui alcuni nodi ospita altre macchine virtuali (<abbr title="macchine virtuali">Macchine virtuali</abbr>) e altri sono sottoutilizzati (ad esempio un server appena riavviato).

<strong>Breve Video introduttivo</strong><br>(6 minuti)<br>
> [!VIDEO https://channel9.msdn.com/Blogs/windowsserver/Virtual-Machine-Load-Balancing-in-Windows-Server-2016/player]

## <a id="what-is-vm-load-balancing"></a>Che cos'è il bilanciamento del carico di macchine virtuali?
<abbr title="Macchina virtuale">VM</abbr> Bilanciamento del carico è una funzionalità inclusa in Windows Server 2019 e Windows Server 2016 che consente di ottimizzare l'utilizzo di nodi in un Cluster di Failover. Identifica i nodi stati overcommit e distribuisce nuovamente <abbr title="macchine virtuali">Macchine virtuali</abbr> da tali nodi ai nodi nel commit. Alcuni degli aspetti più importanti di questa funzionalità sono i seguenti:

* *Si tratta di una soluzione senza tempi di inattività*: <abbr title="Macchine virtuali">Macchine virtuali</abbr> sono in tempo reale-migrati a nodi inattivi.
* *Perfetta integrazione con l'ambiente cluster esistente*: Criteri di errore, come possibili proprietari, domini di errore e anti-affinità vengono rispettati.
* *L'euristica per bilanciamento del carico*: <abbr title="Macchina virtuale">VM</abbr> utilizzo elevato della memoria e utilizzo della CPU del nodo.
* *Controllo granulare*: Abilitata per impostazione predefinita. Può essere attivato su richiesta o a intervalli periodici.
* *Le soglie di aggressività*: Tre valori di soglia disponibili in base alle caratteristiche della distribuzione.

## <a id="feature-in-action"></a>La funzionalità in azione
### <a id="new-node-added"></a>Viene aggiunto un nuovo nodo al Cluster di Failover
![Rappresentazione grafica di un nuovo nodo da aggiungere al Cluster di Failover](media/vm-load-balancing/overview-VM-load-balancing-1.png)

Quando si aggiunta nuove capacità per il Cluster di Failover, il <abbr title="macchina virtuale">VM</abbr> Funzionalità di bilanciamento del carico consente di bilanciare automaticamente la capacità dai nodi esistenti, per il nodo appena aggiunto nell'ordine seguente:

1. La pressione viene valutata sui nodi esistenti nel Cluster di Failover.
2. Tutti i nodi di soglia vengono identificati.
3. I nodi con la più alta pressione vengono identificati per determinare la priorità di bilanciamento del carico.
4. <abbr title="Macchine virtuali">Macchine virtuali</abbr> sono in tempo reale la migrazione (con senza tempi di inattività) da un nodo di soglia per un nodo appena aggiunto nel Cluster di Failover.

### <a id="recurring-load-balancing"></a>Bilanciamento del carico ricorrente
![Rappresentazione grafica di una macchina virtuale ricorrente il bilanciamento del carico](media/vm-load-balancing/overview-VM-load-balancing-2.png)

Quando configurato per il bilanciamento periodica, viene valutata la pressione sui nodi del cluster Bilanciamento del carico ogni 30 minuti. In alternativa, la pressione possa essere valutate su richiesta. Ecco il flusso dei passaggi:

1. La pressione viene valutata in tutti i nodi in un cloud privato.
2. Tutti i nodi supera soglia e quelle successive soglia vengono identificati.
3. I nodi con la più alta pressione vengono identificati per determinare la priorità di bilanciamento del carico.
4. <abbr title="Macchine virtuali">Macchine virtuali</abbr> sono in tempo reale la migrazione (senza alcun tempo di inattività) da un nodo che superano la soglia al nodo sotto la soglia minima.

## <a name="see-also"></a>Vedere anche
* [Approfondimento sul bilanciamento del carico delle macchine virtuali](vm-load-balancing-deep-dive.md)
* [Clustering di failover](failover-clustering-overview.md)
* [Panoramica di Hyper-V](../virtualization/hyper-v/Hyper-V-on-Windows-Server.md)