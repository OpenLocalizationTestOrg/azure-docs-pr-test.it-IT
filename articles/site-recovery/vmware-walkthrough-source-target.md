---
title: aaaSet backup hello origine e di destinazione per VMware replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di macchine virtuali VMware tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Passaggio 8: Impostare hello origine e di destinazione per tooAzure replica VMware

In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure di macchine virtuali VMware, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurare un ambiente di origine hello

Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare le macchine virtuali.

1. Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.
2. Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.
3. In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.
4. Scaricare i file di installazione di hello installazione unificata di Site Recovery.
5. Scaricare la chiave di registrazione dell'insieme di credenziali di hello. che sarà necessaria quando si esegue l'Installazione unificata. chiave di Hello è valida per cinque giorni dopo la generazione è.

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrare il server di configurazione di hello nell'insieme di credenziali hello

Seguito hello prima di avviare, quindi eseguire il programma di installazione unificata tooinstall hello configurazione server, il server di elaborazione hello e il server di destinazione master hello.
    - Ottenere una breve panoramica video

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Nel server di configurazione hello VM, verificare che l'orologio di sistema hello è sincronizzato con un [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deve corrispondere. Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.
    - Eseguire l'installazione come amministratore locale nel server di configurazione hello macchina virtuale.
    - Assicurarsi che sia abilitato TLS 1.0 su hello macchina virtuale.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Connettere i server tooVMware

macchine virtuali toodiscover Azure Site Recovery tooallow in esecuzione nell'ambiente locale, è necessario tooconnect il Server VMware vCenter o l'host ESXi vSphere con il ripristino del sito. Si noti seguenti hello prima di iniziare:

- Se si aggiunge il server vCenter hello o vSphere host tooSite ripristino con un account senza privilegi di amministratore nel server di hello, account hello necessita di questi privilegi abilitati:
    - Datacenter (Data center), Datastore (Archivio dati), Folder (Cartella), Host, Network (Rete), Resource (Risorsa), Virtual machine (Macchina virtuale) e vSphere Distributed Switch (Switch distribuito vSphere).
    - server vCenter Hello necessita di autorizzazioni di viste di archiviazione.
- Quando si aggiunge VMware server tooSite ripristino, può richiedere 15 minuti o più per tali tooappear nel portale di hello.

### <a name="add-hello-account-for-automatic-discovery"></a>Aggiungere account hello per l'individuazione automatica

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Configurare una connessione

Connettersi tooservers come indicato di seguito:

1. Selezionare **+ vCenter** toostart la connessione a un server VMware vCenter o un host VMware vSphere ESXi.
2. In **aggiungere vCenter**, specificare un nome descrittivo per il server vCenter o l'host di vSphere hello e quindi specificare l'indirizzo IP hello o il nome FQDN del server di hello.
3. Lasciare la porta hello 443, a meno che i server VMware sono toolisten configurato per le richieste su una porta diversa. Selezionare l'account hello tooconnect toohello VMware vCenter server o di vSphere ESXi. Fare clic su **OK**.
4. Il ripristino del sito si connette a server tooVMware hello utilizzando le impostazioni specificate e individua le macchine virtuali.

> [!NOTE]
> Se si aggiunge un host con un account che non dispone dei privilegi di amministratore nel server vCenter o l'host di hello o un server, verificare che account hello avere questi privilegi abilitati: Data Center, l'archivio dati, cartella, Host, rete, risorsa, la macchina virtuale, e vSphere Switch distribuiti. Inoltre, è necessario hello archiviazione viste privilegio abilitato server hello VMware vCenter.


## <a name="set-up-hello-target-environment"></a>Configurare un ambiente di destinazione hello

Prima configurare un ambiente di destinazione hello, verificare di che disporre di un account di archiviazione di Azure e una configurazione di rete virtuale.

1. Fare clic su **Prepare infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.
2. Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.
3. Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.

   ![Destinazione](./media/vmware-walkthrough-source-target/gs-target.png)
4. Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete**, toocreate un inline di account o rete di gestione risorse.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 9: configurare un criterio di replica](vmware-walkthrough-replication.md)
