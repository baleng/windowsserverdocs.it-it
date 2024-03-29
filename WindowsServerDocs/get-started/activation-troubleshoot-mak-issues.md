---
title: Problemi noti relativi all'attivazione tramite codice ad attivazione multipla
description: Questo articolo descrive i problemi comuni che possono verificarsi durante il processo di attivazione tramite codice ad attivazione multipla e fornisce soluzioni e indicazioni
ms.topic: article
ms.date: 10/3/2019
ms.technology: server-general
ms.assetid: ''
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: 25fa6d32571597136580afe062aa8d9c7e2d82b7
ms.sourcegitcommit: 9855d6b59b1f8722f39ae74ad373ce1530da0ccf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71962987"
---
# <a name="mak-activation-known-issues"></a>Attivazione tramite codice ad attivazione multipla: problemi noti

Questo articolo illustra i problemi comuni che possono presentarsi durante le attivazioni tramite codice ad attivazione multipla (MAK, Multiple Activation Key) e offre indicazioni per risolvere tali problemi.

## <a name="how-can-i-tell-whether-my-computer-is-activated"></a>Come posso stabilire se il computer è attivato?

Nel computer client apri il pannello di controllo **Sistema** e cerca il messaggio **Windows è attivato**. In alternativa, esegui Slmgr.vbs e usa l'opzione della riga di comando **/dli**.

## <a name="the-computer-does-not-activate-over-the-internet"></a>Il computer non viene attivato tramite Internet

Verifica che le porte necessarie siano aperte nel firewall. Per un elenco delle porte, vedi la [Guida alla distribuzione dei servizi di attivazione per i contratti multilicenza](http://go.microsoft.com/fwlink/?linkid=150083).

## <a name="internet-and-telephone-activation-fail"></a>L'attivazione tramite Internet o telefono non riesce

Contatta un centro di attivazione Microsoft per la tua area. Per i numeri di telefono dei centri di attivazione Microsoft in tutto il mondo, visita la pagina con i [numeri di telefono dei centri di attivazione delle licenze Microsoft](https://www.microsoft.com/Licensing/existing-customer/activation-centers). Quando esegui la chiamata, verifica di avere a disposizione le informazioni sul contratto multilicenza e la prova di acquisto.

## <a name="slmgrvbs-ato-returns-an-error-code"></a>Slmgr.vbs /ato restituisce un codice di errore

Se Slmgr.vbs restituisce un codice di errore esadecimale, puoi identificare il messaggio di errore corrispondente eseguendo lo script seguente:

```cmd
slui.exe 0x2a 0x <ErrorCode>
```

Per altre informazioni su codici di errore specifici e su come risolverli, vedi [Risoluzione dei codici di errore di attivazione comuni](activation-error-codes.md).
