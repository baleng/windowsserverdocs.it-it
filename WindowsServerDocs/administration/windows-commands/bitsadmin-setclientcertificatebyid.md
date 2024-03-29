---
title: setclientcertificatebyid Bitsadmin
description: Argomento dei comandi di Windows per **BITSAdmin setclientcertificatebyid** specifica l'identificatore del certificato client da usare per l'autenticazione client in una richiesta HTTPS (SSL)
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53b6fa4c65397cf710d0497fbae889afd31ec136
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380732"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>setclientcertificatebyid Bitsadmin



Specifica l'identificatore del certificato client da utilizzare per l'autenticazione del client in una richiesta HTTPS (SSL).

## <a name="syntax"></a>Sintassi

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> hexa-decimal_cert_id>
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|Job|Nome visualizzato o il GUID del processo|
|Store_location|Identifica la posizione di un archivio di sistema da utilizzare per la ricerca del certificato. I valori possibili sono:</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (SERVIZI)</br>5 (UTENTI)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|Il nome dell'archivio certificati. I valori possibili sono:</br>CA (certificati dell'autorità di certificazione)</br>MY (certificati personali)</br>RADICE (certificati radice)</br>SPC (certificato autore del software)|
|Hexadecimal_cert_id|Un numero esadecimale che rappresenta l'hash del certificato|

## <a name="BKMK_examples"></a>Esempi

Nell'esempio seguente viene specificato l'identificatore del certificato client da utilizzare per l'autenticazione del client in una richiesta HTTPS (SSL) per il processo denominato *il mio lavoro*.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByID myJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD 
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)