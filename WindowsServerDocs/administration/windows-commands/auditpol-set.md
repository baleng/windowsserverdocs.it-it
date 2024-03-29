---
title: set di Auditpol
description: 'Argomento dei comandi di Windows per **auditpol set** : imposta i criteri di controllo per utente, i criteri di controllo del sistema o le opzioni di controllo.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3c9ec2fab4cad408e0bb845fe157cfdf94f8e09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382401"
---
# <a name="auditpol-set"></a>set di Auditpol

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Imposta i criteri di controllo per utente, i criteri di controllo del sistema o le opzioni di controllo.

## <a name="syntax"></a>Sintassi
```
auditpol /set
[/user[:<username>|<{sid}>][/include][/exclude]]
[/category:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/subcategory:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/option:<option name> /value: <enable>|<disable>]
```
## <a name="parameters"></a>Parametri

|  Parametro   |                                                                                                                                          Descrizione                                                                                                                                           |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /User     |                                        Entità di sicurezza per la quale vengono impostati i criteri di controllo per utente specificati dalla categoria o dalla sottocategoria. È necessario specificare l'opzione category o SubCategory come ID di sicurezza (SID) o nome.                                         |
|   /include   | Specificato con/User; indica che i criteri per utente dell'utente comporteranno la generazione di un controllo anche se non è specificato dai criteri di controllo del sistema. Questa impostazione è l'impostazione predefinita e viene applicata automaticamente se non vengono specificati in modo esplicito i parametri/include e/Exclude. |
|   /Exclude   |                                Specificato con/User; indica che i criteri per utente dell'utente comporteranno l'eliminazione di un controllo indipendentemente dai criteri di controllo del sistema. Questa impostazione viene ignorata per gli utenti che sono membri del gruppo Administrators locale.                                |
|  /Category   |                                                                            Una o più categorie di controllo specificate da un identificatore univoco globale (GUID) o da un nome. Se non viene specificato alcun utente, vengono impostati i criteri di sistema.                                                                             |
| /Subcategory |                                                                                         Una o più sottocategorie di controllo specificate in base al nome o al GUID. Se non viene specificato alcun utente, vengono impostati i criteri di sistema.                                                                                          |
|   /Success   |                 Specifica il controllo di esito positivo. Questa impostazione è l'impostazione predefinita e viene applicata automaticamente se non vengono specificati in modo esplicito i parametri/Success e/Failure. Questa impostazione deve essere utilizzata con un parametro che indica se abilitare o disabilitare l'impostazione.                 |
|   /Failure   |                                                                                  Specifica il controllo degli errori. Questa impostazione deve essere utilizzata con un parametro che indica se abilitare o disabilitare l'impostazione.                                                                                   |
|   /opzione    |                                                                                   Imposta i criteri di controllo per le opzioni CrashOnAuditFail, FullprivilegeAuditing, AuditBaseObjects o AuditBasedirectories.                                                                                    |
|     /SD      |                 Imposta il descrittore di sicurezza utilizzato per delegare l'accesso ai criteri di controllo. Il descrittore di sicurezza deve essere specificato tramite il linguaggio SDDL (Security Descriptor Definition Language). Il descrittore di sicurezza deve avere un elenco di controllo di accesso discrezionale (DACL).                 |
|      /?      |                                                                                                                              Visualizza la guida al prompt dei comandi.                                                                                                                              |

## <a name="remarks"></a>Note
per tutte le operazioni sui set per i criteri per utente e i criteri di sistema, è necessario disporre dell'autorizzazione di controllo completo o di scrittura per tale set di oggetti nel descrittore di sicurezza. È anche possibile eseguire operazioni sui set possedendo il diritto utente **Gestione registro di controllo e protezione** (SeSecurityPrivilege). Tuttavia, questo diritto consente un accesso aggiuntivo che non è necessario per eseguire l'operazione di impostazione.
## <a name="BKMK_examples"></a>Esempi
### <a name="examples-for-the-per-user-audit-policy"></a>Esempi per i criteri di controllo per utente
Per impostare i criteri di controllo per utente per tutte le sottocategorie della categoria di rilevamento dettagliata per l'utente Zaffaronif in modo che tutti i tentativi dell'utente vengano controllati, digitare:
```
auditpol /set /user:mikedan /category:"detailed Tracking" /include /success:enable
```
Per impostare i criteri di controllo per utente per le categorie specificate per nome e GUID e le sottocategorie specificate da GUID per evitare il controllo per eventuali tentativi riusciti o non riusciti, digitare:
```
auditpol /set /user:mikedan /exclude /category:"Object Access","System",{6997984b-797a-11d9-bed3-505054503030} 
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```
Per impostare i criteri di controllo per utente per l'utente specificato per tutte le categorie per l'eliminazione del controllo di tutti i tentativi ma riusciti, digitare:
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```
### <a name="examples-for-the-system-audit-policy"></a>Esempi per i criteri di controllo del sistema
Per impostare i criteri di controllo del sistema per tutte le sottocategorie della categoria di rilevamento dettagliata in modo da includere il controllo solo per i tentativi riusciti, digitare:
```
auditpol /set /category:"detailed Tracking" /success:enable
```
> [!NOTE]
> L'impostazione di errore non viene modificata.
> Per impostare i criteri di controllo del sistema per l'accesso agli oggetti e le categorie di sistema (implicite perché sono elencate le sottocategorie) e le sottocategorie specificate dai GUID per l'eliminazione dei tentativi non riusciti e il controllo dei tentativi riusciti, digitare:
> ```
> auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
> ```
> ### <a name="example-for-auditing-options"></a>Esempio per le opzioni di controllo
> Per impostare le opzioni di controllo sullo stato abilitato per l'opzione CrashOnAuditFail, digitare:
> ```
> auditpol /set /option:CrashOnAuditFail /value:enable
> ```
> #### <a name="additional-references"></a>Riferimenti aggiuntivi
> [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
