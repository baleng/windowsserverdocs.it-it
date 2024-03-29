---
title: nfsshare
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a952e247ee40f832045d39d0e2164bb2e6613c54
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373206"
---
# <a name="nfsshare"></a>nfsshare



È possibile utilizzare **nfsshare** per controllare le condivisioni NFS (Network File System).

## <a name="syntax"></a>Sintassi

```
nfsshare <ShareName>=<Drive:Path> [-o <Option=value>...]
nfsshare {<ShareName> | <Drive>:<Path> | * } /delete
```

## <a name="description"></a>Descrizione

Senza argomenti, l'utilità da riga di comando **nfsshare** elenca tutte le condivisioni NFS (Network File System) esportate da server per NFS. Con *ShareName* come unico argomento, **nfsshare** elenca le proprietà della condivisione NFS identificata da *ShareName*. Quando vengono specificati *ShareName* e <em>Drive</em> **:** <em>path</em> , **nfsshare** Esporta la cartella identificata da <em>unità</em> **:** <em>percorso</em> come *ShareName*. Quando si utilizza l'opzione **/Delete** , la cartella specificata non viene più resa disponibile ai client NFS.

## <a name="options"></a>Opzioni

Il comando **nfsshare** accetta le opzioni e gli argomenti seguenti:


|             Nome              |                                                                                                                                                                                                                      Definizione                                                                                                                                                                                                                       |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         -o anon = {Yes          |                                                                                                                                                                                                                          non                                                                                                                                                                                                                          |
|  -o RW [= \<Host > [: <Host>]...]  |                       Fornisce accesso in lettura/scrittura alla directory condivisa dagli host o dai gruppi di client specificati dall' *host*. Separare i nomi host e gruppo con i due punti ( **:** ). Se *host* non è specificato, tutti gli host e i gruppi di client (ad eccezione di quelli specificati con l'opzione **ro** ) avranno accesso in lettura/scrittura. Se non è impostata né l'opzione **ro** né l'opzione **RW** , tutti i client avranno accesso in lettura/scrittura alla directory condivisa.                       |
|  -o ro [= \<Host > [: <Host>]...]  | Fornisce accesso in sola lettura alla directory condivisa dagli host o dai gruppi di client specificati dall' *host*. Separare i nomi host e gruppo con i due punti ( **:** ). Se l' *host* non è specificato, tutti i client (eccetto quelli specificati con l'opzione **RW** ) avranno accesso in sola lettura. Se l'opzione **ro** è impostata per uno o più client, ma l'opzione **RW** non è impostata, solo i client specificati con l'opzione **ro** possono accedere alla directory condivisa. |
|       -o codifica = {Big5       |                                                                                                                                                                                                                        EUC-JP                                                                                                                                                                                                                         |
|       -o anongid = \<gid >       |                                                                                     Specifica che gli utenti anonimi (non mappati) accederanno alla directory Share usando *GID* come identificatore del gruppo (GID). Il valore predefinito è-2. Il GID anonimo verrà usato quando si segnala il proprietario di un file di proprietà di un utente non mappato, anche se l'accesso anonimo è disabilitato.                                                                                      |
|      -o anonuid = \<uid >       |                                                                                      Specifica che gli utenti anonimi (non mappati) accederanno alla directory Share usando *UID* come identificatore utente (UID). Il valore predefinito è-2. L'UID anonimo verrà usato quando si segnala il proprietario di un file di proprietà di un utente non mappato, anche se l'accesso anonimo è disabilitato.                                                                                      |
| -o root [= \<Host > [: <Host>]...] |                                                                         Fornisce l'accesso radice alla directory condivisa dagli host o dai gruppi di client specificati dall' *host*. Separare i nomi host e gruppo con i due punti ( **:** ). Se l' *host* non è specificato, tutti i client hanno accesso alla radice. Se l'opzione **radice** non è impostata, nessun client dispone di accesso radice alla directory condivisa.                                                                         |
|            /delete            |                                                                                                                                                       Se viene specificato *ShareName* o <em>Drive</em> **:** <em>path</em> , Elimina la condivisione specificata. Se si specifica \*, Elimina tutte le condivisioni NFS.                                                                                                                                                       |

> [!NOTE]
> Per visualizzare la sintassi completa del comando, al prompt dei comandi digitare:</br>> **nfsshare/?**

# #

Informazioni [di riferimento sui servizi per il file System di rete](services-for-network-file-system-command-reference.md) Vedere anche