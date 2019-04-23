---
title: bitsadmin getdisplayname
description: Argomento i comandi di Windows per **bitsadmin getdisplayname** -recupera il nome visualizzato del processo specificato.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1ef16f54b7b825e4293a3870d8181985b83843b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857602"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



Recupera il nome visualizzato del processo specificato.

## <a name="syntax"></a>Sintassi

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|Job|Nome visualizzato o il GUID del processo|

## <a name="BKMK_examples"></a>Esempi

L'esempio seguente recupera il nome visualizzato per il processo denominato *myDownloadJob*.
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
Altri riferimenti

[Chiave sintassi della riga di comando](command-line-syntax-key.md)