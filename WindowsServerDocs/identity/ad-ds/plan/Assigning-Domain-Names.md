---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: Assegnazione di nomi di dominio
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 357c136f108c6d8e9e2a15dd9449ab61663079e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408993"
---
# <a name="assigning-domain-names"></a>Assegnazione di nomi di dominio

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

È necessario assegnare un nome a ogni dominio del piano. I domini Active Directory Domain Services (AD DS) hanno due tipi di nomi: Nomi Domain Name System (DNS) e nomi NetBIOS. In generale, entrambi i nomi sono visibili agli utenti finali. I nomi DNS dei domini Active Directory includono due parti, un prefisso e un suffisso. Quando si creano nomi di dominio, determinare innanzitutto il prefisso DNS. Si tratta della prima etichetta nel nome DNS del dominio. Il suffisso viene determinato quando si seleziona il nome del dominio radice della foresta. Nella tabella seguente sono elencate le regole di denominazione dei prefissi per i nomi DNS.  
  
|Regola|Spiegazione|  
|--------|---------------|  
|Selezionare un prefisso che probabilmente non diventi obsoleto.|Evitare nomi come una linea di prodotti o un sistema operativo che potrebbero cambiare in futuro. Si consiglia di usare nomi geografici.|  
|Selezionare un prefisso che includa solo i caratteri Internet standard.|A-Z, a-z, 0-9 e (-), ma non interamente numerici.|  
|Includere almeno 15 caratteri nel prefisso.|Se si sceglie una lunghezza del prefisso di 15 caratteri o meno, il nome NetBIOS sarà uguale al prefisso.|  
  
Per ulteriori informazioni, vedere convenzioni di denominazione in Active Directory per computer, domini, siti e unità organizzative ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Anche se Dcpromo.exe in Windows Server 2008 e Windows Server 2003 consentono di creare un nome di dominio DNS con etichetta singola, questa scelta non è consigliata per diversi motivi. In Windows Server 2008 R2, Dcpromo.exe non consente di creare un nome di dominio DNS con etichetta singola. Per ulteriori informazioni, vedere [https://go.microsoft.com/fwlink/?LinkId=92467.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
Se il nome NetBIOS corrente del dominio non è appropriato per rappresentare l'area o non soddisfa le regole di denominazione dei prefissi, selezionare un nuovo prefisso. In questo caso, il nome NetBIOS del dominio è diverso dal prefisso DNS del dominio.  
  
Per ogni nuovo dominio distribuito, selezionare un prefisso appropriato per l'area e che soddisfi le regole di denominazione dei prefissi. È consigliabile che il nome NetBIOS del dominio corrisponda al prefisso DNS.  
  
Documentare il prefisso DNS e i nomi NetBIOS selezionati per ogni dominio nella foresta. È possibile aggiungere le informazioni sul nome DNS e NetBIOS al foglio di lavoro "pianificazione del dominio" creato per documentare il piano per i domini nuovi e aggiornati. Per aprirlo, scaricare Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip da Job Aids per Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) e aprire "Domain Planning" (DSSLOGI_5. doc).  
  


