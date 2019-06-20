---
title: Macchine virtuali Oracle Linux supportate in Hyper-V
description: Elenca le funzionalità incluse in ogni versione di Linux integration services
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/01/2017
ms.openlocfilehash: e353ea0b444c07557de99db4472f565decb37349
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447756"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>Macchine virtuali Oracle Linux supportate in Hyper-V

>Si applica a: Windows Server 2016, Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012, Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

La mappa di distribuzione di funzionalità seguente indica le funzionalità presenti in ogni versione. Dopo la tabella sono elencate i problemi noti e soluzioni alternative per ogni distribuzione.

In questa sezione:

* [Serie di Kernel compatibile Red Hat](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_rhc)

* [Unbreakable Enterprise Kernel serie](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_uek)

* [Note](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md#BKMK_notes)

## <a name="table-legend"></a>Legenda tabella

* **Incorporata** -LIS sono inclusi come parte di questa distribuzione Linux. I numeri di versione del modulo del kernel per incorporato LIS (come illustrato da **lsmod**, ad esempio) sono diversi dal numero di versione del pacchetto di download LIS fornita da Microsoft. Una mancata corrispondenza non indica che incorporato LIS è scaduto.

* &#10004; -Funzionalità disponibili

* (*vuoto*)-funzionalità non disponibile

* **R UEK\*x QU\*y** -Unbreakable Enterprise Kernel (UEK) in cui *x* è il numero di versione e *y* è l'aggiornamento trimestrale.

## <a name="BKMK_rhc"></a>Serie di Kernel compatibile Red Hat

Il kernel a 32 bit per la serie di 6. x è PAE attivata. Non esiste alcun supporto predefinito di LIS per Oracle Linux RHCK 6.0-6.3. Kernel di Oracle Linux 7. x sono solo a 64 bit.

| **Funzionalità**                                                                                                              | **Versione di Windows server**   | **7.5-7.6**         | **7.4**             | **6.4 6.8 e 7.0 a 7.3**                                             | **6.4 6.8 e 7.0-7.2**                                             | **RHCK 7.0-7.2**         | **RHCK 6.8**             | **RHCK 6.6, 6.7**        | **RHCK 6.5**              | **RHCK6.4**               |
|--------------------------------------------------------------------------------------------------------------------------|------------------------------|---------------------|---------------------|---------------------------------------------------------------------|---------------------------------------------------------------------|--------------------------|--------------------------|--------------------------|---------------------------|---------------------------|
| **Disponibilità**                                                                                                         |                              | Incorporata            | Incorporata            | [LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106) | [LIS 4.1](https://www.microsoft.com/download/details.aspx?id=51612) | Incorporata                 | Incorporata                 | Incorporata                 | Incorporata                  | Incorporata                  |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                          | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Ora esatta di Windows Server 2016                                                                                        | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Funzionalità di rete](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**              |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Frame jumbo                                                                                                             | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| La codifica VLAN e trunking                                                                                                | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004; (Nota 1 per 6.4 6.8)                                       | &#10004; (Nota 1 per 6.4 6.8)                                       | &#10004;                 | &#10004; Nota 1          | &#10004; Nota 1          | &#10004; Nota 1           | &#10004; Nota 1           |
| Migrazione in tempo reale                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Indirizzo IP statico Injection                                                                                                      | 2016, 2012 R2, 2012          | &#10004; Nota 14    | &#10004; Nota 14    | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| RSS virtuale                                                                                                                     | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| Segmentazione di TCP e gli offload Checksum                                                                                   | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 |                           |                           |
| SR-IOV                                                                                                                   | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Archiviazione](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                    |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Ridimensionamento di VHDX                                                                                                              | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| Fibre Channel virtuale                                                                                                    | 2016, 2012 R2                | &#10004; Nota 2     | &#10004; Nota 2     | &#10004; Nota 2                                                     | &#10004; Nota 2                                                     | &#10004; Nota 2          | &#10004; Nota 2          | &#10004; Nota 2          | &#10004; Nota 2           |                           |
| Backup della macchina virtuale in tempo reale                                                                                              | 2016, 2012 R2                | &#10004;Nota 11,3  | &#10004;Nota 11, 3 | &#10004; Nota 3, 4                                                  | &#10004; Nota 3, 4                                                  | &#10004; Nota 3, 4, 11   | &#10004; Nota 3, 4, 11   | &#10004; Nota 3, 4, 11   | &#10004; Nota 3, 4, 5, 11 | &#10004; Nota 3, 4, 5, 11 |
| Supporto per TRIM                                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 |                          |                           |                           |
| WWN SCSI                                                                                                                 | 2016, 2012 R2                | &#10004;            |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| **[Memoria](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                      |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Supporto PAE Kernel                                                                                                       | 2016, 2012 R2, 2012, 2008 R2 | N/D                 | N/D                 | &#10004; (solo 6. x)                                                 | &#10004; (solo 6. x)                                                 | N/D                      | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Configurazione di gap MMIO                                                                                                | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Memoria dinamica - aggiunta a caldo                                                                                                 | 2016, 2012 R2, 2012          | &#10004;Si noti 8, 9  | &#10004;Si noti 8, 9  | &#10004; Si noti 7, 8, 9, 10 (nota 6 per 6.4 6.7)                      | &#10004; Si noti 7, 8, 9, 10 (nota 6 per 6.4 6.7)                      | &#10004; Nota 6, 7, 8, 9 | &#10004; Nota 6, 7, 8, 9 | &#10004; Nota 6, 7, 8, 9 | &#10004; Nota 6, 7, 8, 9  |                           |
| Memoria dinamica - Ballooning                                                                                              | 2016, 2012 R2, 2012          | &#10004;Si noti 8, 9  | &#10004;Si noti 8, 9  | &#10004; Si noti 7, 9, 10 (nota 6 per 6.4 6.7)                         | &#10004; Si noti 7, 9, 10 (nota 6 per 6.4 6.7)                         | &#10004; Nota 6, 8, 9    | &#10004; Nota 6, 8, 9    | &#10004; Nota 6, 8, 9    | &#10004; Nota 6, 8, 9     | &#10004; Nota 6, 8, 9, 10 |
| Ridimensionamento della memoria di runtime                                                                                                    | 2016                         |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                        |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Dispositivo video specifico Hyper-V                                                                                            | 2016,2012 R2, 2012, 2008 R2  | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  |                           |
| **[Varie](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                 |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Coppia chiave-valore                                                                                                           | 2016, 2012 R2, 2012, 2008 R2 | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004; Nota 12         | &#10004; Nota 12         | &#10004; Nota 12         | &#10004; Nota 12          | &#10004; Nota 12          |
| Interrupt non mascherabile                                                                                                   | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            | &#10004;                 | &#10004;                 | &#10004;                 | &#10004;                  | &#10004;                  |
| Copiare i file dall'host al guest                                                                                             | 2016, 2012 R2                | &#10004;            | &#10004;            | &#10004;                                                            | &#10004;                                                            |                          | &#10004;                 |                          |                           |                           |
| comando lsvmbus                                                                                                          | 2016, 2012 R2, 2012, 2008 R2 |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| Socket di Hyper-V                                                                                                          | 2016                         |                     |                     | &#10004;                                                            | &#10004;                                                            |                          |                          |                          |                           |                           |
| Pass-through/DDA PCI                                                                                                      | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| **[Macchine virtuali di generazione 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                              |                     |                     |                                                                     |                                                                     |                          |                          |                          |                           |                           |
| Avvio UEFI                                                                                                          | 2016, 2012 R2                | &#10004; Nota 13    | &#10004; Nota 13    | &#10004; Nota 13                                                    | &#10004; Nota 13                                                    | &#10004; Nota 13         | &#10004; Nota 13         |                          |                           |                           |
| Avvio protetto                                                                                                              | 2016                         | &#10004;            | &#10004;            |                                                                     |                                                                     |                          |                          |                          |                           |                           |


## <a name="BKMK_uek"></a>Unbreakable Enterprise Kernel serie

Oracle Linux Unbreakable Enterprise Kernel (UEK) è solo a 64 bit e con il supporto incorporato per LIS.

|**Funzionalità**|**Versione di Windows server**|**UEK R4**|**UEK R3 QU3**|**UEK R3 QU2**|**UEK R3 QU1**|
|-|-|-|-|-|-|
|**Disponibilità**||Incorporata|Incorporata|Incorporata|Incorporata|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Ora esatta di Windows Server 2016|2016|||||
|**[Funzionalità di rete](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||
|Frame jumbo|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|La codifica VLAN e trunking|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Migrazione in tempo reale|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Indirizzo IP statico Injection|2016, 2012 R2, 2012|&#10004;|&#10004;|&#10004;||
|RSS virtuale|2016, 2012 R2|&#10004;||||
|Segmentazione di TCP e gli offload Checksum|2016, 2012 R2, 2012, 2008 R2|&#10004;||||
|SR-IOV|2016|||||
|**[Archiviazione](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||
|Ridimensionamento di VHDX|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|Fibre Channel virtuale|2016, 2012 R2|&#10004;|&#10004;|&#10004;||
|Backup della macchina virtuale in tempo reale|2016, 2012 R2|&#10004; Nota 3, 4, 5, 11|&#10004; Nota 3, 4, 5, 11|&#10004; Nota 3, 4, 5, 11||
|Supporto per TRIM|2016, 2012 R2|&#10004;||||
|WWN SCSI|2016, 2012 R2|||||
|**[Memoria](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|
|Supporto PAE Kernel|2016, 2012 R2, 2012, 2008 R2|N/D|N/D|N/D|N/D|
|Configurazione di gap MMIO|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Memoria dinamica - aggiunta a caldo|2016, 2012 R2, 2012|&#10004;||||
|Memoria dinamica - Ballooning|2016, 2012 R2, 2012|&#10004;||||
|Ridimensionamento della memoria di runtime|2016|||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||
|Dispositivo video specifico Hyper-V|2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;||
|**[Varie](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||
|Coppia chiave-valore|2016, 2012 R2, 2012, 2008 R2|&#10004; Nota 11, 12|&#10004; Nota 11, 12|&#10004; Nota 11, 12|&#10004; Nota 11, 12|
|Interrupt non mascherabile|2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Copiare i file dall'host al guest|2016, 2012 R2|&#10004; Nota 11|&#10004; Nota 11|&#10004; Nota 11|&#10004; Nota 11|
|comando lsvmbus|2016, 2012 R2, 2012, 2008 R2|||||
|Socket di Hyper-V|2016|||||
|Pass-through/DDA PCI|2016|||||
|**[Macchine virtuali di generazione 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|
|Avvio UEFI|2016, 2012 R2|&#10004;||||
|Avvio protetto|2016|&#10004;||||

## <a name="BKMK_notes"></a>Note

1. Per questa versione di Oracle Linux, VLAN tag funziona ma trunking VLAN non sono disponibili.

2. Quando si utilizzano dispositivi di virtuale fibre channel, assicurarsi che il numero di unità logica (LUN 0) 0 è stato popolato. Se non è stato popolato LUN 0, una macchina virtuale potrebbe non essere in grado di installare dispositivi di fibre channel in modo nativo.

3. Se sono presenti handle di file aperti durante un'operazione di backup di macchina virtuale, quindi in alcuni casi estremi, i dischi rigidi virtuali backup potrebbero essere necessario essere sottoposto a un controllo di coerenza di sistema di file (fsck) su ripristino.

4. Operazioni di backup Live possano un esito negativo se la macchina virtuale dispone di un dispositivo iSCSI collegati o DAS (noto anche come disco pass-through).

5. Supporto di backup in tempo reale per Oracle Linux 6.4/6.5/UEKR3 QU2 e QU3 è disponibile tramite [Essentials Backup Hyper-V per Linux](https://github.com/LIS/backupessentials/tree/1.0).

6. Supporto della memoria dinamica è disponibile solo nelle macchine virtuali a 64 bit.

7. Aggiunta a caldo Supporto non è abilitato per impostazione predefinita in questa distribuzione. Per abilitare il supporto aggiunto a caldo che è necessario aggiungere una regola di udev in /etc/udev/rules.d/ come indicato di seguito:

   1. Creare un file **/etc/udev/rules.d/100-balloon.rules**. È possibile utilizzare qualsiasi altro nome per il file desiderato.

   2. Aggiungere il contenuto seguente al file: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Riavviare il sistema per consentire l'aggiunta a caldo.

   Durante il download di Linux Integration Services crea questa regola su installazione, la regola è rimossi anche quando LIS viene disinstallato, la regola deve essere ricreato se è necessaria una quantità di memoria dinamica dopo la disinstallazione.

8. Operazioni di memoria dinamica possono non riuscire se il sistema operativo guest è troppo memoria insufficiente. Di seguito sono le procedure consigliate:

   * Memoria di avvio e di memoria minimo deve essere uguale o maggiore rispetto alla quantità di memoria in cui si consiglia il fornitore.

   * Le applicazioni che tendono a consumare l'intera memoria disponibile in un sistema sono limitate all'utilizzo di fino a 80% della RAM disponibile.

9. Se si utilizza la memoria dinamica in un sistema operativo Windows Server 2012 R2 o Windows Server 2016, specificare **memoria di avvio**, **memoria minima**, e **quantità massima di memoria** parametri in multipli di 128 megabyte (MB). In caso contrario, può comportare errori a caldo e non sarà possibile visualizzare qualsiasi memoria aumenta in un sistema operativo guest.

10. Alcune distribuzioni, incluse quelle in uso LIS 3.5 o 4.0, LIS solo supportano Ballooning e non forniscono supporto per l'aggiunta a caldo. In questo caso, è possibile utilizzare la funzionalità memoria dinamica impostando il parametro di memoria di avvio su un valore che corrisponde al parametro di memoria massimo. Questo consente di tutta la memoria necessaria viene aggiunta a caldo alla macchina virtuale in fase di avvio e successivamente in base ai requisiti di memoria dell'host Hyper-V può liberamente allocare o deallocare la memoria dal guest utilizzando Ballooning. Configurare **memoria di avvio** e **memoria minima** uguale o superiore sul valore consigliato per la distribuzione.

11. Daemon di Oracle Linux Hyper-V non vengono installati per impostazione predefinita. Per utilizzare questi daemon, installare il pacchetto daemon Hyper-v. Questo pacchetto di conflitto con scaricato Linux Integration Services e non deve essere installato nei sistemi con LIS scaricato.

12. L'infrastruttura (coppia chiave-VALORE) di coppia chiave/valore potrebbe non funzionare correttamente senza un aggiornamento software Linux. Contattare il fornitore di distribuzione per ottenere l'aggiornamento software nel caso in cui noterete problemi con questa funzionalità.

13. Le macchine virtuali introdotte Server 2012 R2Generation 2 è avvio protetto abilitato per impostazione predefinita e alcune macchine virtuali di Linux non verranno avviate se l'opzione di avvio protetto è disabilitata. È possibile disabilitare l'avvio protetto nel **Firmware** sezione delle impostazioni per la macchina virtuale in **di gestione di Hyper-V** o è possibile disabilitarlo con Powershell:

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Il download di Linux Integration Services può essere applicato alle macchine virtuali di 2 generazione esistente ma non applicare la funzionalità di generazione 2.

14. Inserimento di IP statico potrebbe non funzionare se Gestione di rete è stata configurata per una scheda di rete sintetiche sulla macchina virtuale. Per garantire il corretto funzionamento di IP statico injection assicurarsi che l'amministratore di sistema è spento completamente o è stato disattivato per una scheda di rete specifico tramite il file ifcfg-ethX.


Vedere anche

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [CentOS è supportato e Red Hat Enterprise Linux macchine virtuali in Hyper-V](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Macchine virtuali Debian supportate in Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Macchine virtuali SUSE supportate in Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Macchine virtuali Ubuntu supportate in Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Macchine virtuali FreeBSD supportate in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Forniscono le descrizioni per le macchine virtuali Linux e FreeBSD in Hyper-V](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Le procedure consigliate per l'esecuzione di Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)