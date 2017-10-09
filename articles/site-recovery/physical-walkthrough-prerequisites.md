---
title: aaaPrerequisites per la replica di server fisici tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Vengono riepilogati i prerequisiti di hello per la replica dei carichi di lavoro in esecuzione su fisico tooAzure server di Windows/Linux, tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: b0ed53a143079877a2ad21ee17aae5510e0dc058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-physical-server-tooazure-replication"></a>Passaggio 2: Esaminare i prerequisiti di hello per la replica tooAzure server fisico

Esaminare i prerequisiti di hello riepilogati nella tabella hello.


**Prerequisito** | **Dettagli**
--- | ---
**Azzurro** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server di configurazione locale** | È necessario un server fisico (o una VM VMware) che esegue Windows Server 2012 R2 o versione successiva. Questo server viene configurato durante la distribuzione di Site Recovery.<br/><br/> Per il processo di hello predefinito server e server di destinazione master vengono installati anche in questo computer. Quando si aumentano le prestazioni, potrebbe essere necessario un server di elaborazione separato. In caso contrario, contiene hello stessi requisiti del server di configurazione hello.<br/><br/> [Altre informazioni](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)
**VM locali** | Le macchine da tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e conforme con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL** | il server di configurazione di Hello deve accedere agli URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).<br/><br/> Consenti a questo URL per il download di MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Servizio Mobility** | Deve essere installato in ogni server replicato.




## <a name="limitations"></a>Limitazioni

Si notino limitazioni hello riepilogate nella tabella di hello prima di distribuire.

**Limitazione** | **Dettagli**
--- | ---
**Azzurro** | Gli account di archiviazione e rete devono essere in hello stessa area dell'insieme di credenziali di hello<br/><br/> Se si utilizza un account di archiviazione premium, è necessario anche uno standard di archiviare i log di replica toostore account<br/><br/> Non è possibile replicare gli account toopremium centrale e meridionale.
**Server di configurazione locale** | Se si utilizza una VM VMware come computer server di configurazione hello, hello il tipo di adapter VMware VM deve essere VMXNET3. In caso contrario, [installare questo aggiornamento](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> Per una VM VMware, è necessario installare vSphere PowerCLI 6.0.<br/><br> macchina Hello non deve essere un controller di dominio.<br/><br/> macchina di Hello deve essere un indirizzo IP statico.<br/><br/> nome host Hello deve essere di 15 caratteri o meno, e il sistema operativo deve essere in lingua inglese.
**Replicare le macchine** | Verificare le [limitazioni delle VM di Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Non è possibile replicare VM con dischi crittografati o con avvio UEFI/EFI.<br/><br> I cluster di dischi condivisi non sono supportati. Se l'origine hello VM con gruppo NIC, viene convertito tooa singola scheda di rete dopo il failover.<br/><br/> Se le macchine virtuali dispongono di un disco iSCSI, il ripristino del sito converte i file di disco rigido virtuale tooa dopo il failover. Destinazione iSCSI hello può essere raggiunta in hello macchina virtuale di Azure, si connette tooit e vede e hello disco rigido virtuale. In questo caso, è possibile disconnettere destinazione iSCSI hello.<br/><br/> Se si desidera che la coerenza tra più macchine tooenable, che consente alle macchine virtuali in esecuzione hello stesso carico di lavoro toobe recuperati dati coerenti con l'insieme tooa punto, aprire la porta 20004 in hello macchina virtuale.<br/><br/> Windows deve essere installato nell'unità C hello. disco del sistema operativo Hello deve essere base e non dinamici. disco dati Hello può essere dinamica.<br/><br/> Il file /etc/hosts Linux nelle macchine virtuali devono contenere voci che mappa gli indirizzi tooIP nome host locale hello associati a tutte le schede di rete. Hello nome host, i punti di montaggio, nome del dispositivo, i percorsi di sistema e i nomi di file (/ e così via; in /usr.) deve essere solo in inglese.<br/><br/> Sono supportati tipi specifici di [archiviazione Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).<br/><br/>Creare o impostare **disk.enableUUID=true** nelle impostazioni di VM hello. In questo modo un toohello UUID coerenza VMDK, in modo che installa correttamente e assicura che le modifiche delta solo locale tooon indietro trasferiti durante il failback, senza la replica completa.


## <a name="next-steps"></a>Passaggi successivi

- Se si sta eseguendo una distribuzione completa, andare troppo[passaggio 3: pianificare la capacità](physical-walkthrough-capacity.md)
- Se si sta eseguendo una distribuzione di test semplice, andare troppo[passaggio 4: pianificare la rete](physical-walkthrough-network.md).
