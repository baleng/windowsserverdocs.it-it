---
title: Tecnologie di ottimizzazione e offload di rete
description: In questo argomento viene fornita una panoramica delle tecnologie di offload e ottimizzazione di Windows Server 2016 e sono inclusi collegamenti a ulteriori indicazioni su tali tecnologie.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 57e8a61bc54be05a32daa7eabc55a09553cee28a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405684"
---
# <a name="network-offload-and-optimization-technologies"></a>Tecnologie di ottimizzazione e offload di rete

In questo argomento viene illustrata una panoramica delle diverse funzionalità di offload e di ottimizzazione della rete disponibili in Windows Server 2016 e viene illustrato come contribuire a rendere più efficiente la rete. Queste tecnologie includono solo le funzionalità e le tecnologie, le funzionalità e le tecnologie integrate di software e hardware (SH) e le tecnologie e le funzionalità di solo hardware (HO).

Le tre categorie di funzionalità di rete disponibili in Windows Server 2016 sono: 

1.  [Funzionalità e tecnologie solo del software](hpn-software-only-features.md): Queste funzionalità vengono implementate come parte del sistema operativo e sono indipendenti dalle schede di interfaccia di rete sottostanti. A volte queste funzionalità richiedono l'ottimizzazione della scheda di interfaccia di rete per un funzionamento ottimale. Esempi di questi includono funzionalità Hyper-v, ad esempio vmQoS, ACL e funzionalità non Hyper-V come gruppo NIC.   

2.  [Funzionalità e tecnologie integrate di software e hardware (SH)](hpn-software-hardware-features.md): Queste funzionalità includono componenti software e hardware. Il software è strettamente correlato alle funzionalità hardware necessarie per il funzionamento della funzionalità. Esempi di questi includono VMMQ, VMQ, offload con checksum IPv4 di trasmissione e RSS.   

3.  [Funzionalità e tecnologie solo hardware (ho)](hpn-hardware-only-features.md): Queste accelerazioni hardware migliorano le prestazioni di rete insieme al software, ma non fanno parte di alcuna funzionalità software. Alcuni esempi includono la moderazione di interrupt, il controllo di flusso e l'offload di checksum IPv4 sul lato di ricezione. 

4. [Proprietà avanzate NIC](hpn-nic-advanced-properties.md): È possibile gestire le schede di rete e tutte le funzionalità tramite Windows PowerShell usando il cmdlet NetAdapter.  È anche possibile gestire le schede di rete e tutte le funzionalità usando il pannello di controllo della rete (ncpa. cpl). 

>[!TIP]
>- Le funzionalità e le tecnologie sono quindi disponibili in tutte le architetture hardware, indipendentemente dalla velocità di NIC o dalle funzionalità NIC.
>
>- Le funzionalità SH e HO sono disponibili solo quando la scheda di rete supporta le funzionalità o le tecnologie.

---