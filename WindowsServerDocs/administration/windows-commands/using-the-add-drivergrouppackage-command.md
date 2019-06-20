---
title: Utilizzando il comando add-DriverGroupPackage
description: 'Argomento i comandi di Windows per * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad9d180e2cf2110d36ebc82211af3a495a0e0b6b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440736"
---
# <a name="using-the-add-drivergrouppackage-command"></a>Utilizzando il comando add-DriverGroupPackage

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aggiunge un pacchetto di driver a un gruppo di driver.
## <a name="syntax"></a>Sintassi
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>Parametri

|         Parametro         |                                                                                                                                               Descrizione                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /DriverGroup:<Group Name> |                                                                                                                                 Specifica il nome del gruppo di driver.                                                                                                                                 |
|   /Server:<Server name>   |                                                                                  Specifica il nome del server. Questo può essere il nome NetBIOS o il nome FQDN. Se viene specificato alcun nome di server, viene utilizzato il server locale.                                                                                  |
|   /DriverPackage:<Name>   |                                                                      Specifica il nome del pacchetto driver da aggiungere al gruppo. È necessario specificare questa opzione se il pacchetto driver non può essere identificato in modo univoco in base al nome.                                                                       |
|      /PackageId:<ID>      | Specifica l'ID per un pacchetto. Per trovare l'ID del pacchetto, fare clic sul gruppo di driver che contiene il pacchetto (o **tutti i pacchetti** nodo), fare doppio clic su pacchetto e quindi fare clic su **proprietà**. L'ID pacchetto è elencato nel **generali** scheda, ad esempio: **{dd098d20-1850-4fc8-8e35-ea24a1beff5e}** . |

## <a name="BKMK_examples"></a>Esempi
Per aggiungere un pacchetto driver, digitare uno dei seguenti:
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>Riferimenti aggiuntivi
[Sintassi della riga di comando chiave](command-line-syntax-key.md)
[utilizzando il comando add-DriverGroupPackages](using-the-add-drivergrouppackages-command.md)
[utilizzando il comando Aggiungi /InfFile](using-the-add-driverpackage-command.md)
[utilizzando il sottocomando AllDriverPackages Aggiungi](using-the-add-alldriverpackages-subcommand.md)