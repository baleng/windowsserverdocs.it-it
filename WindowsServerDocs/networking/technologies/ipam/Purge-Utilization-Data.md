---
title: Ripulire i dati di utilizzo
description: Questo argomento fa parte della Guida di gestione di gestione indirizzi IP (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7b471417d4c44c22f115443f1f2dcca6f351e6f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827942"
---
# <a name="purge-utilization-data"></a>Ripulire i dati di utilizzo

>Si applica a: Windows Server (canale semestrale), Windows Server 2016

È possibile utilizzare questo argomento per informazioni su come eliminare i dati di utilizzo dal database di gestione indirizzi IP.  

È necessario essere un membro del **amministratori IPAM**, il computer locale **gli amministratori** o gruppo equivalente, per eseguire questa procedura.

## <a name="to-purge-the-ipam-database"></a>Ripulire il database di gestione indirizzi IP  
1. Aprire Server Manager e quindi passare all'interfaccia di client di gestione indirizzi IP.
2. Passare a una delle seguenti posizioni: **Blocchi di indirizzi IP**, **inventario degli indirizzi IP**, o **gruppi di intervalli di indirizzi IP**.  
3. Fare clic su **attività**, quindi fare clic su **ripulire i dati di utilizzo**. Il **ripulire i dati di utilizzo** verrà visualizzata la finestra di dialogo.
4. Nella **ripulire utilizzo tutti i dati entro**, fare clic su **selezionare una data**.
5. Scegliere la data per il quale si desidera eliminare tutti i record di database sia in sia prima di tale data.
6. Fare clic su **OK**. Gestione indirizzi IP consente di eliminare tutti i record che è stato specificato.