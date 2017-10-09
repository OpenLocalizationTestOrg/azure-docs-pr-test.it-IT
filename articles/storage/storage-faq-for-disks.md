---
title: Domande frequenti sui dischi delle macchine virtuali IaaS di Azure | Microsoft Docs
description: Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)

Questo articolo risponde alle domande frequenti su Managed Disks e Archiviazione Premium di Azure.

## <a name="managed-disks"></a>Managed Disks

**Che cos'è Azure Managed Disks?**

Managed Disks è una funzionalità che semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure, gestendo l'account di archiviazione per conto dell'utente. Per ulteriori informazioni, vedere hello [Panoramica di dischi gestiti](storage-managed-disks-overview.md).

**Se si crea un disco gestito Standard da un disco rigido virtuale esistente da 80 GB, qual è il costo?**

Un disco gestito standard creato da un disco rigido virtuale di 80 GB viene considerato come dimensione disponibile su disco standard successiva hello, che è un disco S10. Vengono addebitati in base toohello S10 disco sui prezzi. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).

**Sono previsti costi di transazione per i dischi gestiti Standard?**

Sì. Sì, ogni transazione prevede un addebito. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).

**Per un disco gestito standard, addebitata per dimensioni effettive di hello dei dati di hello su disco hello o per la capacità di hello il provisioning del disco hello?**

Vengono addebitati in base alle capacità di hello il provisioning del disco hello. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).

**In che modo il prezzo della versione Premium dei dischi gestiti è diverso da quello dei dischi non gestiti?**

Hello sui prezzi dei dischi premium gestiti hello come i dischi premium non gestito.

**È possibile modificare hello archiviazione tipo di account (Standard o Premium) di dischi personali gestiti?**

Sì. Per cambiare tipo di account di archiviazione hello i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.

**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**

Sì. È possibile esportare i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.

**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito con una sottoscrizione diversa?**

No.

**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito in un'area diversa?**

No.

**Ci sono limitazioni di scalabilità per i clienti che usano dischi gestiti?**

Dischi gestiti Elimina i limiti di hello associati agli account di archiviazione. Tuttavia, il numero di hello di dischi gestiti per ogni sottoscrizione è limitata too2, 000 per impostazione predefinita. È possibile chiamare il supporto tooincrease questo numero.

**È possibile fare uno snapshot incrementale di un disco gestito?**

No. funzionalità di snapshot corrente Hello crea una copia completa di un disco gestito. Tuttavia, si pianificare toosupport snapshot incrementali in hello future.

**Le macchine virtuali in un set di disponibilità possono essere composte da una combinazione di dischi gestiti e non gestiti?**

No. Hello macchine virtuali in un set di disponibilità deve utilizzare dischi gestiti o tutti i dischi non gestiti. Quando si crea un set di disponibilità, è possibile scegliere quale tipo di disco desiderato toouse.

**È l'opzione predefinita di dischi gestiti hello in hello portale di Azure?**

Non attualmente, ma sarà utilizzata l'impostazione predefinita, hello in futuro hello.

**È possibile creare un disco vuoto gestito?**

Sì. È possibile creare un disco vuoto. Un disco gestito può essere creato in modo indipendente da una macchina virtuale, ad esempio, senza collegarlo tooa macchina virtuale.

**Numero di domini di errore hello è supportato per un set di disponibilità che usa dischi gestiti novità**

A seconda area hello set di disponibilità hello che utilizza dischi gestiti in cui si trova, numero di domini di errore hello supportato è 2 o 3.

**È come account di archiviazione standard hello per configurare diagnostica?**

Si imposta un account di archiviazione privato per la diagnostica della macchina virtuale. In futuro hello, contiamo tooswitch Diagnostica dischi tooManaged anche.

**Che tipo di supporto per il controllo degli accessi in base al ruolo è disponibile per Managed Disks?**

Managed Disks supporta tre ruoli predefiniti principali:

* Proprietario: può gestire tutto, compresi gli accessi
* Collaboratore: può gestire tutto ad eccezione degli accessi
* Lettore: può visualizzare tutto, ma non apportare modifiche

**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**

È possibile ottenere una firma di accesso condiviso di sola lettura URI per hello gestito su disco e usarlo toocopy hello contenuto tooa archiviazione privato locale o account di archiviazione.

**È possibile creare una copia del proprio disco gestito?**

Clienti di uno snapshot di propri dischi gestiti e quindi utilizzare un altro disco gestito toocreate snapshot hello.

**I dischi non gestiti sono ancora supportati?**

Sì. Sì, sono supportati sia i dischi gestiti che quelli non gestiti. È consigliabile usare dischi gestiti per i nuovi carichi di lavoro e la migrazione dei dischi di toomanaged i carichi di lavoro corrente.


**Se si crea un disco da 128 GB e quindi aumentare hello dimensioni too130 GB, verrà addebitato dimensioni del disco successiva hello (512 GB)?**

Sì.

**È possibile creare dischi gestiti per l'archiviazione con ridondanza locale, l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza della zona?**

Attualmente Azure Managed Disks supporta solo dischi gestiti per l'archiviazione con ridondanza locale.

**È possibile ridurre/ridimensionare i dischi gestiti?**

No. Questa funzionalità non è attualmente supportata. 

**È possibile modificare proprietà del nome computer hello quando specializzata (non creati tramite l'utilità preparazione sistema hello o generalizzata) disco del sistema operativo è tooprovision usato una macchina virtuale?**

No. È possibile aggiornare una proprietà del nome computer hello. Hello nuova macchina virtuale eredita da padre hello VM, che è stato disco del sistema operativo utilizzato toocreate hello. 

**Dove trovare i modelli per Gestione risorse di Azure esempio toocreate macchine virtuali con dischi gestiti?**
* [Elenco di modelli che usano Managed Disks](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Managed Disks e crittografia del servizio di archiviazione 

**La crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo disco gestito?**

Sì.

**Che gestisce le chiavi di crittografia hello?**

Microsoft gestisce le chiavi di crittografia hello.

**È possibile disabilitare la crittografia del servizio di archiviazione per i dischi gestiti?**

No.

**La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**

No. È disponibile in tutte le aree di hello in cui i dischi gestiti è disponibili. Managed Disks è disponibile in tutte le aree pubbliche e in Germania.

**Come si può determinare se un disco gestito è crittografato?**

È possibile scoprire hello ora di creazione un disco gestito dal portale di Azure hello, hello CLI di Azure e PowerShell. Se hello viene eseguita dopo il 9 giugno 2017, il disco è crittografato. 

**Come è possibile crittografare i dischi esistenti creati prima del 10 giugno 2017?**

A partire da 10 giugno 2017, dischi gestiti tooexisting nuovi dati vengono crittografati automaticamente. È inoltre pianificare i dati esistenti tooencrypt e crittografia hello avverrà in modo asincrono in background hello. Se è necessario crittografare i dati esistenti adesso, creare una copia del disco. I nuovi dischi verranno crittografati.

* [Copiare i dischi gestiti tramite hello CLI di Azure](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Copiare i dischi gestiti tramite PowerShell](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Le immagini e gli snapshot gestiti vengono crittografati?**

Sì. Tutte le immagini e gli snapshot gestiti creati dopo il 9 giugno 2017 vengono crittografati automaticamente. 

**È possibile convertire le macchine virtuali con dischi non gestiti che si trovano sugli account di archiviazione o sono stati crittografati in precedenza toomanaged dischi?**

Sì

**Un disco rigido virtuale esportato da un disco gestito o uno snapshot verrà crittografato?**

No. Ma se si esporta un disco rigido virtuale tooan crittografate account di archiviazione da un disco gestito crittografato o di uno snapshot, quindi viene crittografato. 

## <a name="premium-disks-managed-and-unmanaged"></a>Dischi Premium, gestiti e non gestiti

**Se una macchina virtuale usa una serie di dimensioni che supporta Archiviazione Premium, ad esempio DSv2, è possibile collegare dischi dati sia Premium che Standard?** 

Sì.

**È possibile collegare sia premium e standard dischi tooa dimensioni serie di dati non supporta l'archiviazione Premium, ad esempio la serie D, Dv2, G o F**

No. È possibile collegare solo i tooVMs dischi dati standard che non usano una serie di dimensioni che supporta l'archiviazione Premium.

**Se si crea un disco dati Premium da un disco rigido virtuale esistente da 80 GB, qual è il costo?**

Un disco dati premium creato da un disco rigido virtuale di 80 GB viene considerato come dimensioni del disco premium disponibile con Avanti hello, che è un disco P10. Vengono addebitati in base toohello P10 disco sui prezzi.

**Sono presenti i costi di transazione toouse archiviazione Premium?**

È previsto un costo fisso per ogni dimensione di disco con provisioning di un certo numero di IOPS e di una certa velocità effettiva. Hello altri costi sono la larghezza di banda in uscita e la capacità di snapshot, se applicabile. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).

**Quali sono i limiti di hello per IOPS e la velocità effettiva che è possibile ottenere dalla cache di hello disco?**

limiti combinati per cache di Hello e unità SSD locale per una serie di dominio Active Directory sono 4.000 IOPS per ogni core e 33 MB al secondo per ogni core. Hello serie GS offre 5.000 IOPS per ogni core e 50 MB al secondo per i componenti di base.

**È supportata da unità SSD locale per una macchina virtuale i dischi gestiti hello?**

Hello SSD locale temporanea di archiviazione è incluso in una macchina virtuale i dischi gestiti. Questa archiviazione temporanea non comporta costi aggiuntivi. È consigliabile non utilizzare questo toostore SSD locale i dati delle applicazioni perché non è persistente nell'archiviazione Blob di Azure.

**Sono presenti eventuali ripercussioni per hello, utilizzare di TRIM su dischi premium?**

Non viene utilizzato toohello svantaggio di TRIM su dischi premium di Azure o i dischi standard.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Dimensioni dei nuovi dischi, gestiti e non gestiti

**Che cos'è hello disco massime supportate per il sistema operativo e i dischi dati?**

tipo di partizione Hello che supporta Azure per un disco del sistema operativo è il record di avvio principale hello (MBR). formato MBR Hello supporta dimensioni di un disco di too2 TB. dimensione massima di Hello che supporta Azure per un disco del sistema operativo è di 2 TB. Azure supporta backup too4 TB per i dischi dati. 

**Che cos'è hello pagina blob massime supportate?**

Hello pagina blob massime che supporta Azure è 8 TB (8.191 GB). Maggiore di 4 TB (4.095 GB) collegati tooa macchina virtuale come dischi del sistema operativo o di dati BLOB di pagine non è supportato.

**Necessario toouse una nuova versione di strumenti di Azure toocreate, allegare, ridimensionare e caricare dischi superiori a 1 TB?**

È necessario tooupgrade il toocreate gli strumenti di Azure esistente, collegare o ridimensionare i dischi di dimensioni superiori a 1 TB. tooupload file disco rigido virtuale locale direttamente tooAzure come un blob di pagine o un disco non gestito, è necessario set di strumenti più recenti toouse hello:

|Strumenti di Azure      | Versioni supportate                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Numero di versione 4.1.0: versione di giugno 2017 o successiva|
|Interfaccia della riga di comando di Azure v1     | Numero di versione 0.10.13: versione di maggio 2017 o successiva|
|AzCopy           | Numero di versione 6.1.0: versione di giugno 2017 o successiva|

supporto di Hello per v2 CLI di Azure e Azure Storage Explorer sarà presto disponibile. 

**Le dimensioni del disco P4 e P6 sono supportate per i dischi gestiti o i BLOB di pagine?**

No. Le dimensioni del disco P4 (32 GB) e P6 (64 GB) sono supportate solo per i dischi gestiti. Il supporto per dischi non gestiti e BLOB di pagine sarà disponibile a breve.

**Se il premio esistente gestiti disco minore di 64 GB è stato creato prima il disco di piccole dimensioni hello è stato abilitato (circa 15 giugno 2017), come la fatturazione?**

Dischi di piccole dimensioni premium esistenti minore di 64 GB continuare toobe fatturato secondo toohello P10 piano tariffario. 

**Come è possibile passare a livelli disco hello di dischi di piccole dimensioni premium minore di 64 GB da P10 tooP4 o P6?**

È possibile creare uno snapshot di dischi di piccole dimensioni e quindi creare un hello di commutatore tooautomatically disco prezzi tooP4 livello o P6 in base alle dimensioni di hello il provisioning. 


## <a name="what-if-my-question-isnt-answered-here"></a>Cosa fare se non è disponibile una risposta alla domanda?

Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto. È possibile pubblicare una domanda alla fine di hello di questo articolo in commenti hello. tooengage con il team di archiviazione di Azure hello e altri membri della community su questo articolo, utilizzare hello MSDN [forum di Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

funzionalità toorequest, inviare toohello le richieste e idee [forum sul feedback su archiviazione di Azure](https://feedback.azure.com/forums/217298-storage).
