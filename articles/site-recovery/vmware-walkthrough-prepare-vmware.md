---
title: aaaPrepare VMware risorse locali per la replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello che è necessario per la replica dei carichi di lavoro in esecuzione in macchine virtuali VMware tooAzure archiviazione"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Passaggio 6: Preparazione locale VMware replica tooAzure

Utilizzare le istruzioni di hello in toointeract i server di VMware in questo articolo tooprepare locale con Azure Site Recovery e preparare le macchine virtuali VMWare per l'installazione del servizio di mobilità hello. agente di servizio di mobilità Hello installare su tutte le macchine virtuali in locale che si desidera tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Eseguire la preparazione per l'individuazione automatica

Site Recovery individua automaticamente le macchine virtuali eseguite in host vSphere ESXi (con o senza server vCenter). Per l'individuazione automatica, esigenze di ripristino del sito di un host tooaccess account e i server:

1. toouse un account dedicato, creare un ruolo (a livello di vCenter hello, con autorizzazioni di hello descritte nella tabella hello riportata di seguito. Assegnare un nome all'account, ad esempio **Azure_Site_Recovery**.
2. Quindi, creare un utente nel server host/vCenter di vSphere hello e assegnare hello ruolo toohello utente. Questo account utente viene specificato durante la distribuzione di Site Recovery.


### <a name="vmware-account-permissions"></a>Autorizzazioni dell'account VMware

Il ripristino del sito deve tooVMware di accesso per hello processo server tooautomatically individuare le macchine virtuali e per il failover e failback di macchine virtuali.

- **Eseguire la migrazione**: se si desidera solo toomigrate le macchine virtuali VMware tooAzure, senza mai failback essi, è possibile utilizzare un account di VMware con un ruolo di sola lettura. Un ruolo di questo tipo può eseguire il failover, ma non arrestare i computer di origine protetti. Ciò non è necessario per la migrazione.
- **Replicare/Ripristina**: se si desidera account hello di toodeploy replica completa (replicate, failover, eseguire il failback) deve essere in grado di toorun operazioni quali la creazione e la rimozione di dischi, accensione e così via di macchine virtuali.
- **Individuazione automatica**: è necessario almeno un account di sola lettura.


**Attività** | **Account/ruolo necessario** | **Autorizzazioni** | **Dettagli**
--- | --- | --- | ---
**Individuazione automatica delle VM VMware da parte del server di elaborazione** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** dell'oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).
**Failover** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti) dell'oggetto.<br/><br/> È utile ai fini della migrazione, ma non per la replica completa, il failover e il failback.
**Failover e failback** | È consigliabile creare un ruolo (Azure_Site_Recovery) con le autorizzazioni necessarie hello e quindi assegnare hello ruolo tooa VMware utente o gruppo | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = Azure_Site_Recovery<br/><br/> Datastore (Archivio dati) -> Allocate space (Alloca spazio), Browse datastore (Sfoglia archivio dati), Low level file operations (Operazioni file di livello basso), Remove file (Rimuovi file), Update virtual machine files (Aggiorna file macchina virtuale)<br/><br/> Network (Rete) -> Network assign (Assegnazione rete)<br/><br/> Risorse -> pool tooresource assegnare macchina virtuale, eseguire la migrazione spenta macchina virtuale, eseguire la migrazione nella macchina virtuale è spenta<br/><br/> Tasks (Attività) -> Create task (Crea attività), Update task (Aggiorna attività)<br/><br/> Virtual machine (Macchina virtuale) -> Configuration (Configurazione)<br/><br/> Virtual machine (Macchina virtuale) -> Interact (Interagisci) -> Answer question (Rispondi alla domanda), Device connection (Connessione dispositivo), Configure CD media (Configura supporto CD), Configure floppy media (Configura supporto floppy), Power off (Spegni), Power on (Accendi), VMware tools install (Installazione strumenti VMware)<br/><br/> Virtual machine (Macchina virtuale) -> Inventory (Inventario) -> Create (Crea), Register (Registra), Unregister (Annulla registrazione)<br/><br/> Virtual machine (Macchina virtuale) -> Provisioning -> Allow virtual machine download (Consenti download macchina virtuale), Allow virtual machine files upload (Consenti upload file macchina virtuale)<br/><br/> Macchina virtuale -> Snapshots -> Remove snapshots | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** dell'oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Preparazione per l'installazione push del servizio di mobilità hello

servizio di mobilità Hello deve essere installato in tutte le macchine virtuali desiderate tooreplicate. Esistono numerosi modi tooinstall hello servizio, inclusa l'installazione manuale, l'installazione push dal server di elaborazione hello Site Recovery e l'installazione utilizzando i metodi, ad esempio System Center Configuration Manager.

Se si desidera che l'installazione push toouse, è necessario un account che il ripristino del sito è possibile utilizzare tooaccess hello VM tooprepare.

- È possibile usare un account di dominio o locale
- Per Windows, se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. toodo, in hello registrare in **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, aggiungere una voce DWORD hello **LocalAccountTokenFilterPolicy**, con un valore pari a 1.
- Se si desidera una voce del Registro di sistema di hello tooadd per Windows da CLI, digitare:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Per Linux, account hello devono essere radice nel server di hello origine Linux.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 7: creare un insieme di credenziali](vmware-walkthrough-create-vault.md)
