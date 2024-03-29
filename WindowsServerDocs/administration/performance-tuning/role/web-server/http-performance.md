---
title: Ottimizzazione delle prestazioni per HTTP 1.1/2
description: Suggerimenti per l'ottimizzazione delle prestazioni per HTTP 1.1/2
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: IvanPash; GMonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: f7d7bd5145a0804b9ec86438602dfed7c75a2b02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384975"
---
# <a name="performance-tuning-http-112"></a>Ottimizzazione delle prestazioni HTTP 1.1/2

HTTP/2 ha lo scopo di migliorare le prestazioni sul lato client, ad esempio il tempo di caricamento della pagina in un browser. Sul server può rappresentare un lieve aumento dei costi della CPU. Mentre il server non richiede più una singola connessione TCP per ogni richiesta, parte di tale stato verrà ora mantenuta nel livello HTTP. Inoltre, HTTP/2 ha una compressione di intestazione, che rappresenta un carico aggiuntivo della CPU.

Per alcune situazioni è necessario un fallback HTTP/1.1 (reimpostazione della connessione HTTP/2 e stabilire invece una nuova connessione per l'utilizzo di HTTP/1.1). In particolare, la rinegoziazione TLS e l'autenticazione HTTP (ad eccezione di Basic e digest) richiedono il fallback HTTP/1.1. Anche se questa operazione aggiunge un sovraccarico, queste operazioni implicano già un certo ritardo, quindi non sono particolarmente sensibili alle prestazioni.

## <a name="see-also"></a>Vedere anche
- [Ottimizzazione delle prestazioni del server Web](index.md) 
- [Ottimizzazione delle prestazioni di IIS 10.0](tuning-iis-10.md)