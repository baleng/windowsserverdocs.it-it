---
title: Modifiche apportate a Nano Server in Windows Server (Canale semestrale)
description: Nel nuovo modello di manutenzione di Windows Server, Nano Server è solo un sistema operativo contenitore, con alcune modifiche alle funzionalità.
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c12ca84826a92fa045eb84b55e7406392161280b
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "66452799"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Modifiche apportate a Nano Server in Windows Server (Canale semestrale)

>Si applica a: Windows Server, Canale semestrale

Se esegui già Nano Server, il modello di manutenzione [Canale semestrale di Windows Server](../get-started-19/servicing-channels-19.md) ti sarà già familiare, poiché è stato precedentemente fornito dal modello Current Branch for Business (CBB). Il modello di manutenzione Canale semestrale di Windows Server non è altro che lo stesso modello con un nuovo nome. In questo modello, i rilasci degli aggiornamenti di funzionalità di Nano Server sono previsti due o tre volte l'anno.

Tuttavia, a partire da Windows Server versione 1803, Nano Server è disponibile solo come **immagine del sistema operativo di base del contenitore**. Deve essere eseguito come contenitore in un host del contenitore, come un'installazione dei componenti di base del server di Windows Server. L'esecuzione di un contenitore basato su Nano Server in questa versione differisce dalle versioni precedenti per tre aspetti:

- Nano Server è stato ottimizzato per le applicazioni .NET Core.
- Nano Server ha dimensioni ancora minori rispetto alla versione Windows Server 2016.
- PowerShell Core, .NET Core e WMI non sono più inclusi per impostazione predefinita, ma puoi includere i pacchetti di contenitori [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) e [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) durante la creazione del contenitore.
- In Nano Server non è più incluso uno stack di manutenzione. Microsoft pubblica in Docker Hub un contenitore Nano aggiornato che può essere ridistribuito.
- I problemi relativi al nuovo contenitore Nano vengono risolti tramite Docker.
- Puoi ora eseguire contenitori Nano in IoT Core.

## <a name="related-topics"></a>Argomenti correlati

- [Documentazione dei contenitori di Windows](http://aka.ms/windowscontainers)
- [Panoramica del modello di manutenzione Canale semestrale di Windows Server](../get-started-19/servicing-channels-19.md)
