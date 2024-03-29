---
title: Utilizzando il comando add-ImageGroup
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ca88671-51de-4924-b969-88f3dfd84270
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e870bd5435e1aa2b155fee880d32c0d784ac398
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363685"
---
# <a name="using-the-add-imagegroup-command"></a>Utilizzando il comando add-ImageGroup

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

aggiunge un gruppo di immagini a un server di servizi di distribuzione Windows.
## <a name="syntax"></a>Sintassi
```
wdsutil [Options] /add-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
## <a name="parameters"></a>Parametri
|Parametro|Descrizione|
|-------|--------|
mediaGroup: <Image group name>|Specifica il nome del gruppo di immagini da aggiungere.|
|[/Server:<Server name>]|Specifica il nome del server. Può essere il nome NetBIOS oppure il nome di dominio completo. Se non si specifica alcun nome server, verrà utilizzato il server locale.|
## <a name="BKMK_examples"></a>Esempi
Per aggiungere un gruppo di immagini, digitare uno dei seguenti:
```
wdsutil /add-ImageGroumediaGroup:ImageGroup2
wdsutil /verbose /add-ImageGroumediaGroup:"My Image Group" /Server:MyWDSServer
```
#### <a name="additional-references"></a>Riferimenti aggiuntivi
[Chiave di sintassi della riga di comando](command-line-syntax-key.md)
[utilizzando il comando get-AllImageGroups](using-the-get-allimagegroups-command.md)
[utilizzando il comando get-ImageGroup](using-the-get-imagegroup-command.md)
[utilizzando il comando remove-ImageGroup](using-the-remove-imagegroup-command.md)
[sottocomando: set-ImageGroup](subcommand-set-imagegroup.md)
