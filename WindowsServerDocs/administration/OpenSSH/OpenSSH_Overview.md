---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH, SSH, Win32-OpenSSH
title: OpenSSH in Windows
ms.product: w10
ms.openlocfilehash: c6563fbe4fe69acad4d295a3f7fe166e92d38444
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280054"
---
# <a name="openssh-in-windows"></a>OpenSSH in Windows

OpenSSH è la versione open source degli strumenti di Secure Shell (SSH) utilizzata dagli amministratori di Linux e altre non-Windows per la gestione di multi-piattaforma di sistemi remoti. OpenSSH è stato aggiunto a Windows a partire da autunno del 2018 e inclusa in Windows 10 e Windows Server 2019. 

SSH è basato su un'architettura client-server in cui il sistema che sta lavorando l'utente è il client e il sistema remoto gestito è il server. OpenSSH include una gamma di componenti e gli strumenti progettati per offrire un approccio sicuro e diretto all'amministrazione di sistema remoto, tra cui:

* sshd.exe, ovvero il componente server SSH che deve essere in esecuzione nel sistema gestito in modalità remota 
* SSH.exe, ovvero il componente client SSH che viene eseguito nel sistema locale dell'utente
* SSH keygen.exe genera, gestisce e converte le chiavi di autenticazione per SSH 
* SSH agent.exe archivia le chiavi private utilizzate per l'autenticazione con chiave pubblica
* SSH add.exe aggiunge le chiavi private all'elenco consentito dal server
* SSH keyscan.exe facilita la raccolta di chiavi pubbliche SSH host da un numero di host
* SFTP.exe è il servizio che fornisce il protocollo Secure File Transfer Protocol e viene eseguito tramite SSH
* SCP.exe è un'utilità di copia di file che viene eseguito su SSH

Documentazione in questa sezione è incentrata sulla modalità di utilizzo OpenSSH in Windows, tra cui installazione e casi di configurazione e l'uso di Windows specifiche. Di seguito sono riportati gli argomenti:
* Installazione e disinstallazione di OpenSSH per Windows 10 e Windows Server 2019

Documentazione dettagliata aggiuntiva per le funzionalità comuni di OpenSSH è disponibile online nella [OpenSSH.com](https://www.openssh.com/manual.html). 

Il master [OpenSSH progetto open source](https://www.openssh.com) è gestito da sviluppatori in progetto OpenBSD. È il fork di questo progetto di Microsoft [GitHub](https://github.com/PowerShell/openssh-portable).
Commenti e suggerimenti su Windows OpenSSH sia gradita e può essere fornito mediante la creazione di problemi di GitHub nel nostro [repository GitHub di OpenSSH](https://github.com/PowerShell/openssh-portable). 
