---
title: Abilitare il reindirizzamento cartelle nel server1 di destinazione Windows Server Essentials
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
H1: Abilitare il reindirizzamento cartelle nel Server di destinazione Windows Server Essentials
ms.assetid: f67d195e-36f6-495a-8361-6d5faa889441
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 50995f0d03b400d6e44d16389afc69e5f25465ac
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432976"
---
# <a name="enable-folder-redirection-on-the-windows-server-essentials-destination-server1"></a>Abilitare il reindirizzamento cartelle nel server1 di destinazione Windows Server Essentials

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

È possibile eseguire questa attività se il reindirizzamento cartelle è abilitato sul server di origine.  
  
 In primo luogo, usare il Dashboard di Windows Server Essentials per abilitare il reindirizzamento cartelle nel Server di destinazione. Eliminare quindi la vecchia impostazione di Criteri di gruppo per il reindirizzamento cartelle.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>Per abilitare il reindirizzamento cartelle sul server di destinazione  
  
1.  Nel Server di destinazione, aprire il Dashboard di Windows Server Essentials.  
  
2.  Sulla barra di spostamento fare clic su **DISPOSITIVI**.  
  
3.  Nel riquadro **Attività dispositivo** fare clic su **Implementa criteri di gruppo**.  
  
4.  Nella pagina **Abilita criteri di gruppo per reindirizzamento cartelle** selezionare le cartelle da reindirizzare e quindi fare clic su **Avanti**.  
  
5.  Nella pagina **Abilita impostazioni dei criteri di sicurezza** fare clic su **Fine**.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Per eliminare la vecchia impostazione di Criteri di gruppo per il reindirizzamento cartelle  
  
1. Nel server di destinazione aprire lo strumento di amministrazione **Gestione Criteri di gruppo**.  
  
2. In **Gestione Criteri di gruppo**espandere **Foresta:** <em>YourNetworkDomainName</em>espandere **Domini**espandere *YourNetworkDomainName*, quindi **Oggetti Criteri di gruppo**.  
  
3. Fare clic con il pulsante destro del mouse su **Reindirizzamento cartelle di W7PVP**e quindi scegliere **Elimina**.  
  
4. Leggere l'avviso e quindi fare clic su **Sì**.  
  
5. Chiudere **Gestione Criteri di gruppo**.  
  
   Per applicare la modifica al reindirizzamento cartelle, gli utenti di rete devono disconnettere i computer e quindi riconnettersi. Questo garantisce il trasferimento di tutte le cartelle reindirizzate al server di destinazione.
