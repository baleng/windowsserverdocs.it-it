---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: Definizione della pianificazione
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 04576a88825205398f1b555d9f5063ac26e2a76e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408861"
---
# <a name="determining-the-schedule"></a>Definizione della pianificazione

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

È possibile controllare la disponibilità dei collegamenti di sito impostando una pianificazione per i collegamenti di sito. Quando la replica tra due siti attraversa più collegamenti di sito, l'intersezione delle pianificazioni di replica in tutti i collegamenti rilevanti determina la pianificazione della connessione tra i due siti.  
  
Per pianificare l'impostazione della pianificazione dei collegamenti di sito, creare due pianificazioni sovrapposte tra i collegamenti di sito che contengono controller di dominio che vengono replicati direttamente tra loro. Usare la pianificazione predefinita (100-percent) per questi collegamenti, a meno che non si desideri bloccare il traffico di replica durante le ore di picco. Bloccando la replica, si assegna la priorità ad altro traffico, ma si aumenta anche la latenza di replica.  
  
I controller di dominio archiviano l'ora in formato UTC (Coordinated Universal Time). Le impostazioni di ora nelle pianificazioni degli oggetti di collegamento di sito sono conformi all'ora locale del sito e del computer in cui è impostata la pianificazione. Quando un controller di dominio Contatta un computer che si trova in un sito e in un fuso orario diversi, la pianificazione del controller di dominio Visualizza l'impostazione dell'ora in base all'ora locale per il sito del computer.  
  


