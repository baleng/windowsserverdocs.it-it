---
title: Configurare il reindirizzamento cartelle nel server di destinazione Windows Server Essentials
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe77ba67-128c-4fc3-9361-30fa6af42516
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6709aa2a342efd5837cf340b645961499baff6a5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433014"
---
# <a name="configure-folder-redirection-on-the-windows-server-essentials-destination-server"></a>Configurare il reindirizzamento cartelle nel server di destinazione Windows Server Essentials

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Eseguire questa attività se il reindirizzamento cartelle è abilitato sul server di origine.  
  
 Eliminare prima la vecchia impostazione di Criteri di gruppo per il reindirizzamento cartelle. Usare quindi il Dashboard di Windows Server Essentials per abilitare il reindirizzamento cartelle nel Server di destinazione.  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>Per eliminare la vecchia impostazione di Criteri di gruppo per il reindirizzamento cartelle  
  
1. Nel server di destinazione aprire lo strumento di amministrazione **Gestione Criteri di gruppo**.  
  
2. In **Gestione Criteri di gruppo**espandere **Foresta:** <em>YourNetworkDomainName</em>espandere **Domini**espandere *YourNetworkDomainName*, quindi **Oggetti Criteri di gruppo**.  
  
3. Fare clic con il pulsante destro del mouse su **Reindirizzamento cartelle Criteri di gruppo SBS**e quindi scegliere **Elimina**.  
  
4. Fare clic con il pulsante destro del mouse su **Modelli di sicurezza Criteri di gruppo SBS** e quindi scegliere **Elimina**.  
  
5. Leggere l'avviso e quindi fare clic su **Sì**.  
  
6. Chiudere **Gestione Criteri di gruppo**.  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>Per abilitare il reindirizzamento cartelle sul server di destinazione  
  
1. Nel Server di destinazione, aprire il Dashboard di Windows Server Essentials.  
  
2. Sulla barra di spostamento fare clic su **Dispositivi**.  
  
3. Nel riquadro **Attività dispositivo** fare clic su **Implementa criteri di gruppo**.  
  
4. Nella pagina **Abilita criteri di gruppo per reindirizzamento cartelle** selezionare le cartelle da reindirizzare e quindi fare clic su **Avanti**.  
  
5. Nella pagina **Abilita impostazioni dei criteri di sicurezza** fare clic su **Fine**.  
  
   Per applicare la modifica al reindirizzamento cartelle, gli utenti di rete devono disconnettere i computer e quindi riconnettersi. Questo garantisce il trasferimento di tutte le cartelle reindirizzate al server di destinazione.
