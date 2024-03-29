---
title: Creare una raccolta di Servizi Desktop remoto
description: Informazioni su come aggiungere un host sessione Desktop remoto e programmi RemoteApp alla distribuzione di Servizi Desktop remoto.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 11/08/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae9767e3-864a-4eb2-96c0-626759ce6d60
author: lizap
manager: dongill
ms.openlocfilehash: cec1ae43b51b17da5617f95e13b839d4ecfbb40c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404009"
---
# <a name="create-a-remote-desktop-services-collection-for-desktops-and-apps-to-run"></a>Creare una raccolta di Servizi Desktop remoto per desktop e l'esecuzione di app

>Si applica a: Windows Server (Canale semestrale), Windows Server 2019, Windows Server 2016

Per creare una raccolta di sessioni di Servizi Desktop remoto usare la procedura seguente. Una raccolta di sessioni contiene app e desktop che si vuole rendere disponibili agli utenti. Dopo aver creato la raccolta, è possibile pubblicarla in modo che gli utenti possano accedervi.

Prima di creare una raccolta è necessario scegliere il tipo di raccolta necessario: sessioni desktop in pool o sessioni desktop personali. 

- **Usare le sessioni desktop in pool per la virtualizzazione basata sulla sessione**: è possibile sfruttare la potenza di calcolo di Windows Server per offrire un ambiente multisessione conveniente come base per i carichi di lavoro quotidiani degli utenti.
- **Usare le sessioni desktop personali per creare un'infrastruttura desktop virtuale (VDI)** : è possibile sfruttare il client di Windows per offrire una compatibilità tra app, alte prestazioni e quella familiarità che gli utenti si aspettano dalla loro esperienza desktop di Windows.
 
Con una sessione in pool vari utenti accedono a un pool condiviso di risorse, mentre con una sessione desktop personale a ogni utente viene assegnato il proprio desktop dall'interno del pool. La sessione in pool offre una riduzione complessiva dei costi mentre le sessioni personali consentono agli utenti di personalizzare la propria esperienza desktop.

Se è necessario condividere applicazioni con uso elevato di grafica ospitate, è possibile combinare i desktop delle sessioni personali con una GPU virtualizzata RemoteFX configurata per le accelerazioni grafiche. In alternativa, è possibile combinare i desktop di sessione personale con la nuova funzionalità di assegnazione di dispositivi discreti (DDA) per offrire inoltre un supporto alle applicazioni con grafica accelerata ospitate. Consultare la sezione [Quale tecnologia per la virtualizzazione della grafica è adatta alle tue esigenze?](rds-graphics-virtualization.md) per altre informazioni.


Indipendentemente dal tipo di raccolta scelto è possibile popolare tali raccolte con RemoteApp, che consente agli utenti di accedere e lavorare con programmi e risorse da qualsiasi dispositivo supportato, come se il programma fosse in esecuzione in locale.

## <a name="create-a-pooled-desktop-session-collection"></a>Creare una raccolta di sessioni desktop in pool

1.  In Server Manager, fare clic su **Servizi Desktop remoto > raccolte > attività > creare insiemi di sessioni**.  
2.  Immettere un nome per la raccolta, ad esempio **ContosoAps**.  
3.  Selezionare il server Host sessione Desktop remoto creato (ad esempio, Contoso-Shr1).  
4.  Accettare il valore predefinito **gruppi di utenti**.  
5.  Immettere il percorso della condivisione file creata per i dischi dei profili utente per questa raccolta (ad esempio, **\Contoso-Cb1\UserDisksr**).   
6.  Fare clic su **Crea**. Quando viene creata la raccolta, fare clic su **Chiudi**.  


## <a name="create-a-personal-desktop-session-collection"></a>Creare una raccolta di sessioni desktop personali

Usare il cmdlet New-RDSessionCollection per creare una raccolta di sessioni desktop personali. I tre parametri seguenti offrono le informazioni di configurazione necessarie per i desktop sessione personali:

- **-PersonalUnmanaged**: specifica il tipo di raccolta di sessioni che consente di assegnare utenti a un server host sessione personale. Se non specifichi questo parametro, la raccolta verrà creata come una tradizionale raccolta di host sessione Desktop remoto, in cui gli utenti vengono assegnati al successivo host sessione disponibile al momento dell'accesso.
- **-GrantAdministrativePrivilege**: se usi **-PersonalUnmanaged**, questo parametro specifica che all'utente assegnato all'host sessione devono essere concessi privilegi amministrativi. Se non usi questo parametro, agli utenti verranno concessi solo i privilegi utente standard.
- **-AutoAssignUser**: se usi **-PersonalUnmanaged**, questo parametro specifica che i nuovi utenti che si connettono tramite Gestore connessione Desktop remoto devono essere automaticamente assegnati a un host sessione non assegnato. Se non sono presenti host sessione non assegnati nella raccolta, l'utente vedrà un messaggio di errore. Se non si usa questo parametro, è necessario [assegnare manualmente gli utenti a un host sessione](rds-manage-personal-collection.md#manually-assign-a-user-to-a-personal-session-host) prima che del loro accesso.

È possibile usare i cmdlet di PowerShell per gestire le raccolte di sessioni desktop personali. Consultare la sezione [Gestire raccolte di sessioni desktop personali](rds-manage-personal-collection.md) per altre informazioni.

## <a name="publish-remoteapp-programs"></a>Pubblicare i programmi RemoteApp
Per pubblicare le app e le risorse nella raccolta usare la procedura seguente:

1.  In Server Manager, selezionare la nuova raccolta (**ContosoApps**).  
2.  In programmi RemoteApp, fare clic su **programmi RemoteApp pubblicare**.  
3. Selezionare i programmi che si desidera pubblicare e quindi fare clic su **Pubblica**.  
