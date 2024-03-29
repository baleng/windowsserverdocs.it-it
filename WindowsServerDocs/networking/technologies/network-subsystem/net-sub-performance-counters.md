---
title: Contatori delle prestazioni di rete
description: Questo argomento fa parte della Guida all'ottimizzazione delle prestazioni del sottosistema di rete per Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ebff972d670f3fd0b8d12959d161bce03ac487e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401851"
---
# <a name="network-related-performance-counters"></a>Contatori delle prestazioni di rete

>Si applica a: Windows Server (Canale semestrale), Windows Server 2016

Questo argomento elenca i contatori rilevanti per la gestione delle prestazioni di rete e contiene le sezioni seguenti.  
  
-   [Utilizzo risorse](#bkmk_ru)  
  
-   [Potenziali problemi di rete](#bkmk_np)  
  
-   [Prestazioni dell'Unione lato ricezione (RSC)](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a>Utilizzo risorse  

I contatori delle prestazioni seguenti sono rilevanti per l'utilizzo delle risorse di rete.  
  
- IPv4, IPv6  
  
  -   Datagrammi ricevuti/sec  
  
  -   Datagrammi inviati/sec  
  
- TCPv4, TCPv6  
  
  -   Segmenti ricevuti/sec  
  
  -   Segmenti inviati/sec  
  
  -   Segmenti ritrasmessi/sec  
  
- Interfaccia di rete (*), scheda di rete (\*)  
  
  - Byte ricevuti/sec  
  
  - Byte inviati/sec  
  
  - Pacchetti ricevuti/sec  
  
  - Pacchetti inviati/sec  
  
  - Lunghezza coda di output  
  
    Questo contatore è la lunghezza della coda di pacchetti di output \(cm pacchetti @ no__t-1. Se è più lungo di 2, si verificano ritardi. È necessario trovare il collo di bottiglia ed eliminarlo, se possibile. Poiché NDIS Accoda le richieste, questa lunghezza deve essere sempre 0.  
  
- Informazioni sul processore  
  
  - % di tempo processore  
  
  - Interruzioni/sec  
  
  - DPC in coda/sec  
  
    Questo contatore è una velocità media a cui sono stati aggiunti DPC alla coda DPC del processore logico. Ogni processore logico ha una propria coda DPC. Questo contatore misura la frequenza con cui vengono aggiunti DPC alla coda, non il numero di DPC nella coda. Viene visualizzata la differenza tra i valori osservati negli ultimi due esempi, divisi per la durata dell'intervallo di campionamento.  
  
##  <a name="bkmk_np"></a>Potenziali problemi di rete  

I contatori delle prestazioni seguenti sono rilevanti per potenziali problemi di rete.  
  
-   Interfaccia di rete (*), scheda di rete (\*)  
  
    -   Pacchetti ricevuti scartati  
  
    -   Errori ricevuti dai pacchetti  
  
    -   Pacchetti in uscita eliminati  
  
    -   Errori dei pacchetti in uscita  
  
-   WFPv4, WFPv6  
  
    -   Pacchetti scartati/sec

-   UDPv4, UDPv6

    -   Errori di datagrammi ricevuti  
  
-   TCPv4, TCPv6  
  
    -   Errori di connessione  
  
    -   Connessioni reimpostate  
  
-   Criteri QoS di rete  
  
    -   Pacchetti eliminati  
  
    -   Pacchetti eliminati/sec  
  
-   Attività scheda di interfaccia di rete per processore  
  
    -   Indicazioni di ricezione risorse insufficienti/sec  
  
    -   Pacchetti di risorse insufficienti/sec  
  
-   Microsoft Winsock BSP  
  
    -   Datagrammi eliminati  
  
    -   Datagrammi eliminati/sec  
  
    -   Connessioni rifiutate  
  
    -   Connessioni rifiutate/sec  
  
##  <a name="bkmk_rsc"></a>Prestazioni dell'Unione lato ricezione (RSC)  

I contatori delle prestazioni seguenti sono rilevanti per le prestazioni di RSC.  
  
-   Scheda di rete(*)  
  
    -   Connessioni TCP Active RSC  
  
    -   Dimensioni medie pacchetto TCP RSC  
  
    -   Pacchetti per TCP RSC Uniti/sec  
  
    -   Eccezioni TCP RSC/sec

Per i collegamenti a tutti gli argomenti di questa guida, vedere [ottimizzazione delle prestazioni del sottosistema di rete](net-sub-performance-top.md).