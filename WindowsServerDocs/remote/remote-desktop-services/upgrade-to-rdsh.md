---
title: Aggiornamento del server Host sessione Desktop remoto a Windows Server 2016
description: In questo articolo viene descritto come aggiornare le distribuzioni di Servizi Desktop remoto esistente a Windows Server 2016.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: 784eb7c0ccc37eb31b514fbbeaa9e99c3a39a9e9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387062"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>Aggiornamento del server Host sessione Desktop remoto a Windows Server 2016

>Si applica a: Windows Server (canale semestrale), Windows Server 2019, Windows Server 2016

> [!IMPORTANT]
> Tutte le applicazioni devono essere disinstallate prima dell'aggiornamento e reinstallate dopo l'aggiornamento, per evitare eventuali problemi di compatibilità delle app causati dall'aggiornamento.

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Aggiornamenti del sistema operativo è supportato con ruolo Servizi Desktop REMOTO
Gli aggiornamenti a Windows Server 2016 sono supportati solo da Windows Server 2012 R2 e Windows Server 2016 TP5.

## <a name="upgrading-a-rds-session-based-collection"></a>Aggiornamento di una raccolta basata sulla sessione di Servizi Desktop remoto
Per ridurre al minimo i tempi di inattività, durante l'aggiornamento di una raccolta basata sulla sessione di Servizi Desktop remoto è consigliabile seguire questa procedura:

1. Identifica i server da aggiornare, ad esempio, la metà dei server nella raccolta.
2. Impedisci nuove connessioni a tali server impostando **Consenti nuove connessioni** su false.
3. Disconnetti tutte le sessioni nei server. 
4. Rimuovi i server dalla raccolta.
5. Aggiorna i server a Windows Server 2016.
6. Imposta **Consenti nuove connessioni** su "false" negli altri server della raccolta.
7. Aggiungi i server aggiornati alle raccolte corrispondenti.
8. Rimuovi il set di server rimanente per l'aggiornamento dalla raccolta.
9. Imposta **Consenti nuove connessioni** su "true" nei server aggiornati della raccolta.
10. A questo punto, aggiorna i server rimanenti nella distribuzione seguendo i passaggi precedenti, da 3 a 9.

## <a name="upgrading-a-standalone-rd-session-host-server"></a>Aggiornamento di un server Host sessione Desktop remoto autonomo
Un server Host sessione Desktop remoto autonomo può essere aggiornato in qualsiasi momento.