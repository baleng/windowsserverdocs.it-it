---
title: 'che Ksetup: addenctypeattr'
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f207d36ff52be4b0dc222d96d62a2ac9e38f573f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375298"
---
# <a name="ksetupaddenctypeattr"></a>che Ksetup: addenctypeattr



Aggiunge l'attributo di tipo di crittografia all'elenco dei possibili tipi per il dominio. Per esempi di come è possibile utilizzare questo comando, vedere [esempi](#BKMK_Examples).

## <a name="syntax"></a>Sintassi

```
ksetup /addenctypeattr <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|\<DomainName >|Nome del dominio a cui si desidera stabilire una connessione. Utilizzare il nome di dominio completo o un modulo semplice del nome, ad esempio corp.contoso.com o contoso.|
|Tipo di crittografia|Deve essere uno dei tipi di crittografia supportati seguenti:</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128-CTS-HMAC-SHA1-96</br>-AES256-CTS-HMAC-SHA1-96|

## <a name="remarks"></a>Note

Per visualizzare il tipo di crittografia per Kerberos ticket di concessione ticket (TGT) e la chiave di sessione, eseguire il **klist** comando e visualizzare l'output.

È possibile impostare o aggiungere più tipi di crittografia separando i tipi di crittografia nel comando con uno spazio. Tuttavia, è possibile eseguire questa operazione solo per un dominio alla volta.

Se il comando ha esito positivo o negativo, viene visualizzato un messaggio di stato.

Per impostare il dominio a cui si desidera connettersi e usare, eseguire il comando **che Ksetup/domain \<DomainName >** .

## <a name="BKMK_Examples"></a>Esempi

Determinare i tipi di crittografia corrente che sono impostati su questo computer:
```
klist
```
Impostare il dominio corp.contoso.com:
```
ksetup /domain corp.contoso.com
```
Aggiungere il tipo di crittografia AES-256-CTS-HMAC-SHA1-96 all'elenco dei possibili tipi per il dominio corp.contoso.com:
```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Impostare l'attributo di tipo di crittografia su AES-256-CTS-HMAC-SHA1-96 per il dominio corp.contoso.com:
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
Verificare che l'attributo del tipo di crittografia sia impostato come previsto per il dominio:
```
ksetup /getenctypeattr corp.contoso.com
```

#### <a name="additional-references"></a>Altri riferimenti

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)