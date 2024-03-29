---
title: Ripristino della foresta di Active Directory-pulizia
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: c4e800f380cf75022c03e21b91f3b6f71cf79708
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369238"
---
# <a name="ad-forest-recovery---cleanup"></a>Ripristino della foresta di Active Directory-pulizia

>Si applica a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

 Eseguire i passaggi successivi al ripristino in base alle esigenze:  
  
- Dopo il ripristino dell'intera foresta, è possibile ripristinare la configurazione DNS originale, inclusa la configurazione dei server DNS preferiti e alternativi in ogni controller di dominio. Dopo che i server DNS sono stati configurati come prima del malfunzionamento, verranno ripristinate le funzionalità di risoluzione dei nomi precedenti. Eliminare tutti i record DNS per i controller di dominio che non sono stati ripristinati.  
- Eliminare i record WINS (Windows Internet Name Service) per tutti i controller di dominio che non sono stati ripristinati.  
- È possibile trasferire i ruoli di master operazioni in altri controller di dominio nel dominio o nella foresta e aggiungere altri server di catalogo globale in base alla configurazione prima dell'errore.  
- Poiché l'intera foresta viene ripristinata a uno stato precedente, tutti gli oggetti (ad esempio utenti e computer) aggiunti e tutti gli aggiornamenti (ad esempio, le modifiche della password) apportati agli oggetti esistenti dopo questo punto andranno perduti. Pertanto, è necessario ricreare questi oggetti mancanti e riapplicare gli aggiornamenti mancanti nel modo appropriato.  
- Potrebbe anche essere necessario ripristinare i trust in uscita con domini e foreste esterni, perché queste relazioni di trust esterne non vengono ripristinate automaticamente dai backup.

## <a name="next-steps"></a>Passaggi successivi

- [Guida al ripristino della foresta di Active Directory](AD-Forest-Recovery-Guide.md)
- [Ripristino della foresta di Active Directory - Procedure](AD-Forest-Recovery-Procedures.md)  
