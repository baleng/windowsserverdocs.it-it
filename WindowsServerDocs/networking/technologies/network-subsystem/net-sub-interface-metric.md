---
title: Configurare l'ordine delle interfacce di rete
description: Questo argomento fa parte della Guida all'ottimizzazione delle prestazioni del sottosistema di rete per Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4368d0709a22e9c122245c6a0131c5c9bee894a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405535"
---
# <a name="configure-the-order-of-network-interfaces"></a>Configurare l'ordine delle interfacce di rete

>Si applica a: Windows Server (Canale semestrale), Windows Server 2016

In Windows Server 2016 e Windows 10, è possibile usare la metrica dell'interfaccia per configurare l'ordine delle interfacce di rete.

Questa operazione è diversa rispetto alle versioni precedenti di Windows e Windows Server, che consentiva di configurare l'ordine di binding delle schede di rete tramite l'interfaccia utente o i comandi **INetCfgComponentBindings:: MoveBefore** e  **INetCfgComponentBindings:: MoveAfter**. Questi due metodi per ordinare le interfacce di rete non sono disponibili in Windows Server 2016 e Windows 10.

In alternativa, è possibile utilizzare il nuovo metodo per impostare l'ordine enumerato delle schede di rete configurando la metrica dell'interfaccia di ogni scheda. È possibile configurare la metrica dell'interfaccia usando il comando [set-NetIPInterface](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface) di Windows PowerShell.

Quando si scelgono le route del traffico di rete e si configura il parametro **InterfaceMetric** del comando **set-NetIPInterface** , la metrica complessiva utilizzata per determinare le preferenze di interfaccia è la somma della metrica di route e metrica dell'interfaccia. In genere, la metrica dell'interfaccia fornisce la preferenza a una particolare interfaccia, ad esempio l'uso di Wired se sono disponibili sia wired che wireless.

Nell'esempio di comando di Windows PowerShell riportato di seguito viene illustrato l'utilizzo di questo parametro.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

L'ordine in cui gli adapter vengono visualizzati in un elenco è determinato dalla metrica dell'interfaccia IPv4 o IPv6.  Per altre informazioni, vedere [funzione GetAdaptersAddresses](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

Per i collegamenti a tutti gli argomenti di questa guida, vedere [ottimizzazione delle prestazioni del sottosistema di rete](net-sub-performance-top.md).
