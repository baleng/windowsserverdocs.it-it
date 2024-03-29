---
ms.assetid: e6b72a80-e8b7-4305-be0c-0a290f468d36
title: Distribuzione di Active Directory Domain Services in un'organizzazione con Windows Server 2003
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 7426ba8fa3ea5077510655ea4877d0e0b69226ff
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408909"
---
# <a name="deploying-ad-ds-in-a-windows-server-2003-organization"></a>Distribuzione di Active Directory Domain Services in un'organizzazione con Windows Server 2003

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Se l'organizzazione è in esecuzione Windows Server 2003 Active Directory, è possibile distribuire Windows Server 2008 Active Directory Domain Services (AD DS), entrambi eseguendo un aggiornamento sul posto di alcuni o tutti i sistemi operativi dei controller di dominio a Windows Server 2008 o introducendo i controller di dominio che esegue Windows Server 2008 nell'ambiente.  
  
Prima di poter aggiungere un controller di dominio che esegue Windows Server 2008 a un dominio di Active Directory di Windows Server 2003 esistente, è necessario eseguire **adprep**, uno strumento da riga di comando. Adprep estende lo schema di Active Directory, aggiorna i descrittori di protezione predefinito degli oggetti selezionati e aggiunge i nuovi oggetti di directory come richiesto da alcune applicazioni. Adprep è disponibile sul disco di installazione di Windows Server 2008 (\sources\adprep\adprep.exe). Per ulteriori informazioni, vedere Adprep ([https://go.microsoft.com/fwlink/?LinkId=99215](https://go.microsoft.com/fwlink/?LinkId=99215)).  
  
Nella figura seguente vengono illustrati i passaggi per la distribuzione di Windows Server 2008 Active Directory in un ambiente di rete attualmente in esecuzione Windows Server 2003 Active Directory.  
  
![distribuire un organigramma di windows 2003](media/Deploying-AD-DS-in-a-Windows-Server-2003-Organization/900c4eee-1119-4a9a-9310-755597428b71.gif)  
  
> [!NOTE]  
> Se si desidera impostare il livello di funzionalità del dominio o foresta a Windows Server 2008, tutti i controller di dominio nell'ambiente in uso devono eseguire il sistema operativo Windows Server 2008.  
  
Consolidamento dei domini di risorse e account che vengono aggiornati sul posto da un ambiente Windows Server 2003 come parte della distribuzione di Windows Server 2008 Active Directory potrebbe essere necessario tra insiemi di strutture o intraforest ristrutturazione di dominio. Ristrutturazione dei domini di Active Directory tra foreste consente di ridurre la complessità della rappresentazione dell'organizzazione in Active Directory, e consente di ridurre i costi amministrativi associati. Ristrutturazione dei domini di Active Directory all'interno di un insieme di strutture consente di ridurre il carico amministrativo per l'organizzazione di riduzione del traffico di replica, riducendo la quantità di utente e l'amministrazione di gruppo che è necessario e semplificare l'amministrazione dei criteri di gruppo. Per ulteriori informazioni, vedere la guida alla migrazione di il numero di versione 3.1 ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
Per un elenco delle attività dettagliate che è possibile usare per pianificare e distribuire servizi di dominio Active Directory in un'organizzazione che esegue Windows Server 2003 Active Directory, vedere [Checklist: Distribuzione di servizi di dominio Active Directory in un'organizzazione Windows Server 2003 @ no__t-0.  
  


