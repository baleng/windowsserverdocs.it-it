---
title: Ripristino della foresta di Active Directory-generazione di pool di RID
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: aa1f5e8b40aa43fa2601bc6f11efe2fcd4ccd05e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369064"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>Ripristino della foresta di Active Directory: generazione del valore dei pool di RID disponibili 

>Si applica a: Windows Server 2016, Windows Server 2012 e 2012 R2, Windows Server 2008 e 2008 R2

Utilizzare la seguente procedura per aumentare il valore dei pool di ID relativi (RID) che il master operazioni RID verrà allocato dopo il ripristino del controller di dominio. Aumentando il valore dei pool di RID disponibili, è possibile assicurarsi che nessun controller di dominio allochi un RID per un'entità di sicurezza creata dopo il backup utilizzato per ripristinare il dominio. 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Informazioni sui pool di Active Directory RID e rIDAvailablePool

Ogni dominio dispone di un oggetto **CN = RID Manager $, CN = System, DC**=<*Domain_name*>. Questo oggetto ha un attributo denominato **rIDAvailablePool**. Questo valore dell'attributo gestisce lo spazio RID globale per un intero dominio. Il valore è un numero intero grande con parti superiori e inferiori. La parte superiore definisce il numero di entità di sicurezza che possono essere allocate per ogni dominio (0x3FFFFFFF o solo oltre 1 miliardo). La parte inferiore è il numero di RID allocati nel dominio. 
  
> [!NOTE]
> In Windows Server 2016 e 2012, il numero di entità di sicurezza che è possibile allocare viene aumentato a oltre 2 miliardi. Per ulteriori informazioni, vedere [gestione del rilascio di RID](https://technet.microsoft.com/library/jj574229.aspx). 
  
- Valore di esempio: 4611686014132422708  
- Parte bassa: 2100 (inizio del pool di RID successivo da allocare)  
- Parte superiore: 1073741823 (numero totale di RID che è possibile creare in un dominio)  
  
Quando si aumenta il valore dell'Integer grande, si aumenta il valore della parte inferiore. Se ad esempio si aggiunge 100.000 al valore di esempio 4611686014132422708 per la somma 4611686014132522708, la nuova parte bassa sarà 102100. Ciò indica che il successivo pool di RID che verrà allocato dal master RID inizierà con 102100 anziché 2100. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Per aumentare il valore dei pool di RID disponibili mediante ADSIEdit e il calcolatore

1. Aprire Server Manager, fare clic su **strumenti** e quindi su **ADSI Edit**.
2. Fare clic con il pulsante destro del mouse, scegliere **Connetti a** e Connetti Esegui il contesto dei nomi predefinito e fare clic su **OK**.
   ![ADSI Edit @ no__t-1 
3. Individuare il percorso del nome distinto seguente: **CN = RID Manager $, CN = System, DC = <domain name>** .
   ![ADSI Edit @ no__t-1 
3. Fare clic con il pulsante destro del mouse e selezionare le proprietà di CN = RID Manager $. 
4. Selezionare l'attributo **rIDAvailablePool**, fare clic su **modifica**, quindi copiare il valore Integer grande negli Appunti.
   ![ADSI Edit @ no__t-1  
5. Avviare il calcolatore e scegliere **modalità scientifica**dal menu **Visualizza** . 
6. Aggiungere 100.000 al valore corrente.
   ![ADSI Edit @ no__t-1 
7. Usare Ctrl + c oppure il comando **Copy** dal menu **Edit (modifica** ) per copiare il valore negli Appunti. 
8. Incollare questo nuovo valore nella finestra di dialogo modifica di ADSIEdit. 
   ![ADSI Edit @ no__t-1 
9. Fare clic su **OK** nella finestra di dialogo e **applicare** nella finestra delle proprietà per aggiornare l'attributo **rIDAvailablePool** . 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>Per aumentare il valore dei pool di RID disponibili mediante LDP  
  
1. Al prompt dei comandi digitare il comando seguente e quindi premere INVIO:  
   **LDP**  
2. Fare clic su **connessione**, fare clic su **Connetti**, digitare il nome di gestione rid, quindi fare clic su **OK**. 
   ![LDP @ NO__T-1
3. Fare clic su **connessione**, su **Binding**, selezionare **associa con credenziali** e digitare le credenziali amministrative, quindi fare clic su **OK**. 
   ![LDP @ NO__T-1
4. Fare clic su **Visualizza**, su **albero** e quindi digitare il percorso del nome distinto seguente:  CN = RID Manager $, CN = System, DC =*nome dominio*  
   ![LDP @ NO__T-1
5. Fare clic su **Sfoglia**e quindi su **modifica**. 
6. Aggiungere 100.000 al valore corrente di **rIDAvailablePool** , quindi digitare la somma in **values**. 
7. In **DN**Digitare `cn=RID Manager$,cn=System,dc=` *< nome di dominio @ no__t-3*. 
8. In **attributo modifica voce**Digitare `rIDAvailablePool`. 
9. Selezionare **Sostituisci** come operazione, quindi fare clic su **invio**.
   ![LDP @ NO__T-1 
10. Fare clic su **Esegui** per eseguire l'operazione. Fare clic su **Chiudi**.
11. Per convalidare la modifica, fare clic su **Visualizza**, su **albero**, quindi digitare il percorso del nome distinto seguente:   CN = RID Manager $, CN = System, DC =*nome dominio*.   Controllare l'attributo **rIDAvailablePool** . 
   ![LDP @ NO__T-1

## <a name="next-steps"></a>Passaggi successivi

- [Guida al ripristino della foresta di Active Directory](AD-Forest-Recovery-Guide.md)
- [Ripristino della foresta di Active Directory - Procedure](AD-Forest-Recovery-Procedures.md)
