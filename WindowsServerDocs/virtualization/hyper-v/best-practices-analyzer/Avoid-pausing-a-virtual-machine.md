---
title: Evitare la sospensione di una macchina virtuale
description: Versione online del testo per questa regola di Best Practices Analyzer.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 406b24edd4a7e87e32058006590ac7cd37206568
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366446"
---
# <a name="avoid-pausing-a-virtual-machine"></a>Evitare la sospensione di una macchina virtuale

>Si applica a: Windows Server 2016

Per altre informazioni sulle procedure consigliate e sulle analisi, vedere [Eseguire analisi di Best Practice Analyzer e gestire i risultati delle analisi](https://go.microsoft.com/fwlink/p/?LinkID=223177).
  
|Proprietà|Dettagli|  
|-|-|  
|**Sistema operativo**|Windows Server 2016|  
|**Prodotto/funzionalità**|Hyper-V|  
|**Gravità**|Avviso|  
|**Categoria**|Configurazione|  

Nelle sezioni seguenti, corsivo indica il testo dell'interfaccia Utente visualizzata nello strumento Analizzatore procedure consigliate per questo problema.

## <a name="issue"></a>Problema  
  
*Questo server dispone di una o più macchine virtuali in uno stato di sospensione.*  
  
## <a name="impact"></a>Impatto  
  
*A seconda della quantità di memoria disponibile, potrebbe non essere possibile eseguire altre macchine virtuali.*  
  
Le macchine virtuali sospese non rilasciano la memoria allocata, il che significa che la memoria non è disponibile per l'avvio di altre macchine virtuali.  
  
## <a name="resolution"></a>Risoluzione  
  
*If questo comportamento è intenzionale, non è necessaria alcuna azione ulteriore. In caso contrario, provare a riprendere le macchine virtuali o a arrestarle.*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Usare la console di gestione di Hyper-V per riprendere la macchina virtuale  
  
1.  Aprire la console di gestione di Hyper-V. Dal menu **strumenti** di Server Manager fare clic su console di **gestione di Hyper-V**.  
  
2.  Dall'elenco **macchine virtuali** individuare le macchine virtuali con lo stato **sospeso**.  
  
    > [!IMPORTANT]  
    > Lo stato **Paused-Critical** si verifica quando lo spazio libero rimanente nello spazio di archiviazione fisico per la macchina virtuale è insufficiente. Prima di provare a riprendere una macchina virtuale in questo stato, liberare spazio disponibile nell'archiviazione fisica.  
  
3.  Fare clic con il pulsante destro del mouse su ogni nome macchina virtuale, quindi scegliere **Riprendi**. In questo modo la macchina virtuale viene restituita a uno stato di esecuzione. Successivamente, se si desidera arrestare la macchina virtuale, fare di nuovo clic con il pulsante destro del mouse su di essa e scegliere **Arresta**.  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Usare Windows PowerShell per riprendere la macchina virtuale  
  
È possibile eseguire questa operazione in un unico comando usando il filtro e la pipeline dopo avere ottenuto tutte le macchine virtuali nell'host. Digitare:  
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


