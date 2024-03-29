---
title: L'appartenenza al dominio è consigliata per i server che eseguono Hyper-V
description: Versione online del testo per questa regola di Best Practices Analyzer.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 48ea52e962f2f476d1428a69bab6c6e38c4ec005
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364920"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>L'appartenenza al dominio è consigliata per i server che eseguono Hyper-V

>Si applica a: Windows Server 2016


  
*Per ulteriori informazioni sulle procedure consigliate e le analisi, vedere* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Proprietà|Dettagli|  
|-|-|  
|**Sistema operativo**|Windows Server 2016|  
|**Prodotto/funzionalità**|Hyper-V|  
|**Gravità**|Avviso|  
|**Categoria**|Configurazione|  
  
Nelle sezioni seguenti, corsivo indica il testo dell'interfaccia Utente visualizzata nello strumento Analizzatore procedure consigliate per questo problema.  
  
## <a name="issue"></a>Problema  
  
*Questo server è membro di un gruppo di lavoro.*  
  
## <a name="impact"></a>Impatto  
  
*Non esiste alcuna gestione centrale per questo server.*  
  
L'aggiunta di questo computer al dominio consente la gestione centralizzata tramite criteri di identità, sicurezza e controllo.  
  
## <a name="resolution"></a>Risoluzione  
  
*Se è disponibile un ambiente di dominio, aggiungere il server al dominio.*  
  
> [!IMPORTANT]  
> Si consiglia di esaminare i carichi di lavoro in esecuzione nelle macchine virtuali del computer per determinare se sono presenti implicazioni relative alla sicurezza per l'aggiunta del computer a un dominio. Se una delle macchine virtuali è un controller di dominio virtualizzato, vedere [considerazioni sulla pianificazione per i controller di dominio virtualizzati](https://go.microsoft.com/fwlink/?LinkId=190192) (https://go.microsoft.com/fwlink/?LinkId=190192).  
  
Per l'aggiunta di un computer a un dominio è necessario disporre delle autorizzazioni per il computer e il dominio:   
- Nel computer è necessario un account utente che sia membro del gruppo Administrators. Accedere con questo tipo di account oppure specificare il nome utente e la password per l'account quando richiesto.   
- Nel dominio è necessario un account utente autorizzato a aggiungere il computer al dominio. Verranno richiesti il nome utente e la password.  
  
Per istruzioni, vedere [aggiungere il computer al dominio](https://go.microsoft.com/fwlink/?LinkId=190193) (https://go.microsoft.com/fwlink/?LinkId=190193).  
  


