---
ms.assetid: bbb5b68f-00ad-4715-8176-0c2769b706c4
title: Guida alla distribuzione di ADFS in Windows Server 2012 R2
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5507cd567114d17c6500655ee210b70bd9ea1ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408417"
---
# <a name="deploying-a-federation-server-farm"></a>Distribuzione di una server farm di federazione


Per distribuire una server farm federativa, completare le attività dell'elenco di controllo nell'ordine indicato. In presenza di un collegamento di riferimento a un argomento concettuale, dopo aver consultato quest'ultimo tornare a questo elenco di controllo, in modo da poter continuare con le attività rimanenti.  
  
![deploying federato server farm @ no__t-1Checklist: Distribuzione di una server farm federativa @ no__t-0  
  
||Attività|Riferimenti|  
|-|--------|-------------|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Esaminare i concetti e le considerazioni importanti quando si prepara la distribuzione di Active Directory Federation Services \(AD FS @ no__t-1. **Nota:**|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Guida alla progettazione di AD FS server farm federate ![deploying in Windows server 2012 R2](../../ad-fs/design/AD-FS-Design-Guide-in-Windows-Server-2012-R2.md)<br /><br />![deploying federati server farm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[informazioni sui concetti chiave ad FS](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
||Se si decide di usare Microsoft SQL Server come archivio di configurazione di AD FS, assicurarsi di distribuire un'istanza funzionale di SQL Server.|Avviso [SQL Server](https://technet.microsoft.com/sqlserver) **:** In Windows Server 2012 R2 se si vuole creare una farm AD FS e usare SQL Server per archiviare i dati di configurazione, è possibile usare SQL Server 2008 e versioni successive, incluso SQL Server 2012.|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Aggiungere il computer a un dominio di Active Directory|![deploying federato server farm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[aggiungere un computer a un dominio](Join-a-Computer-to-a-Domain.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Registrare Secure Socket Layer \(SSL\) certificato per ADFS.|![deploying federato server farm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[registrare un certificato SSL per ad FS](Enroll-an-SSL-Certificate-for-AD-FS.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Installare il servizio ruolo AD FS.|![deploying federato server farm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[installare il servizio ruolo ad FS](Install-the-AD-FS-Role-Service.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Configurare un server federativo.|![deploying federato server farm](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[configurare un server federativo](Configure-a-Federation-Server.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Passaggio facoltativo: Configurare un server federativo con Device Registration Service \(DRS @ no__t-1.|![deploying federato server farm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[configurare un server federativo con Device Registration Service](Configure-a-federation-server-with-Device-Registration-Service.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Aggiungere un host \(A\) e alias \(CNAME\) record di risorse di sistema di nome di dominio aziendale \(DNS\) per il servizio federativo e il servizio DRS.|![deploying federati server farm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[configurare il DNS aziendale per i servizio federativo e DRS](Configure-Corporate-DNS-for-the-Federation-Service-and-DRS.md)|  
|![distribuzione di federazione di server farm](media/icon_checkboxo.gif)|Verificare che un server federativo sia operativo.|![deploying federato server farm](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[verificare che un server federativo sia operativo](Verify-That-a-Federation-Server-Is-Operational.md)|  
  

## <a name="see-also"></a>Vedere anche  
[Distribuzione di AD FS](../../ad-fs/AD-FS-Deployment.md)  

[Guida alla distribuzione di Windows Server 2012 R2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
  

