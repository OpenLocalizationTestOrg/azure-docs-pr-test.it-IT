---
title: " Gestire un server VMware vCenter in Azure Site Recovery | Microsoft Docs"
description: Questo articolo descrive come aggiungere e gestire un server VMware vCenter in Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Gestire un server VMware vCenter in Azure Site Recovery
Questo articolo illustra hello varie operazioni di ripristino del sito che possono essere eseguite in VMware vCenter.

## <a name="prerequisites"></a>Prerequisiti

**Supporto per host VMware vCenter e VMware vSphere ESX** | **Dettagli** |
|--- | --- |
|**Server VMware locali** | Uno o più server VMware vSphere, che eseguono la versione 6.0, 5.5 o 5.1 con gli ultimi aggiornamenti. I server devono trovarsi nella stessa rete del server di configurazione hello (o server di elaborazione separato) hello.<br/><br/> È consigliabile un vCenter host toomanage server che eseguono 6.0 o 5.5 con gli aggiornamenti più recenti di hello. Quando si distribuisce la versione 6.0, sono supportate solo le funzionalità disponibili nella versione 5.5.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Preparare un account per l'individuazione automatica
Il ripristino del sito deve tooVMware di accesso per hello processo server tooautomatically individuare le macchine virtuali e per il failover e il failback di macchine virtuali.

* **Eseguire la migrazione**: se si vuole solo toomigrate tooAzure di macchine virtuali VMware, senza mai failback essi, è possibile utilizzare un account di VMware con un ruolo di sola lettura. Un ruolo di questo tipo può eseguire il failover, ma non arrestare i computer di origine protetti. Ciò non è necessario per la migrazione.
* **Replicare/Ripristina**: se si desidera account hello di toodeploy replica completa (replicate, failover, eseguire il failback) deve essere in grado di toorun operazioni quali la creazione e la rimozione di dischi, accensione del computer virtuale.
* **Individuazione automatica**: è necessario almeno un account di sola lettura.


|**Attività** | **Account/ruolo necessario** | **Autorizzazioni** | **Dettagli**|
|--- | --- | --- | ---|
|**Individuazione automatica delle macchine virtuali VMware da parte del server di elaborazione** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).|
|**Failover** | È necessario almeno un utente di sola lettura | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = sola lettura | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti) dell'oggetto.<br/><br/> È utile ai fini della migrazione, ma non per la replica completa, il failover e il failback.|
|**Failover e failback** | È consigliabile creare un ruolo (AzureSiteRecoveryRole) con le autorizzazioni necessarie hello e quindi assegnare hello ruolo tooa VMware utente o gruppo | Oggetto di Data Center -> Propaga tooChild oggetto ruolo = AzureSiteRecoveryRole<br/><br/> Datastore (Archivio dati) -> Allocate space (Alloca spazio), Browse datastore (Sfoglia archivio dati), Low level file operations (Operazioni file di livello basso), Remove file (Rimuovi file), Update virtual machine files (Aggiorna file macchina virtuale)<br/><br/> Network (Rete) -> Network assign (Assegnazione rete)<br/><br/> Risorse -> pool tooresource assegnare macchina virtuale, eseguire la migrazione spenta macchina virtuale, eseguire la migrazione nella macchina virtuale è spenta<br/><br/> Tasks (Attività) -> Create task (Crea attività), Update task (Aggiorna attività)<br/><br/> Virtual machine (Macchina virtuale) -> Configuration (Configurazione)<br/><br/> Virtual machine (Macchina virtuale) -> Interact (Interagisci) -> Answer question (Rispondi alla domanda), Device connection (Connessione dispositivo), Configure CD media (Configura supporto CD), Configure floppy media (Configura supporto floppy), Power off (Spegni), Power on (Accendi), VMware tools install (Installazione strumenti VMware)<br/><br/> Virtual machine (Macchina virtuale) -> Inventory (Inventario) -> Create (Crea), Register (Registra), Unregister (Annulla registrazione)<br/><br/> Virtual machine (Macchina virtuale) -> Provisioning -> Allow virtual machine download (Consenti download macchina virtuale), Allow virtual machine files upload (Consenti upload file macchina virtuale)<br/><br/> Macchina virtuale -> Snapshots -> Remove snapshots | Utente assegnato al livello Data Center e dispone di accesso tooall hello oggetti nel Data Center hello.<br/><br/> accesso toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** oggetto, gli oggetti figlio toohello (host vSphere, archivi dati, le macchine virtuali e reti).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Creare un Server di vCenter tooVMware di tooconnect account / VMware vSphere EXSi host
1. Account di accesso in hello configurazione server e avviare hello cspsconfigtool.exe utilizzando hello collegamento sul Desktop hello.
2. Fare clic su **Aggiungi Account** su hello **Gestisci Account** scheda.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Fornire i dettagli dell'account hello e fare clic su OK tooadd hello account. Hello account deve disporre dei privilegi di hello elencati in hello [preparare un account per l'individuazione automatica](#prepare-an-account-for-automatic-discovery) sezione.

  >[!NOTE]
  Sono necessari circa 15 minuti per hello account informazioni toobe sincronizzati backup con il servizio Site Recovery hello.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Associare un host VMware vCenter/vSphere di VMware ESX (Aggiungi vCenter)
* Nel portale di Azure hello, passare troppo*YourRecoveryServicesVault* > **infrastruttura di Site Recovery** > **i server di configurazione,**  >  *ConfigurationServer*
* Nella pagina dettagli del server di configurazione hello fare clic su hello + vCenter pulsante.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modificare le credenziali utilizzate tooconnect toohello vCenter server / host ESXi vSphere

1. Account di accesso in configurazione hello server e avviare cspsconfigtool.exe hello
2. Fare clic su **Aggiungi Account** su hello **Gestisci Account** scheda.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Fornire dettagli hello del nuovo account e fare clic su OK tooadd hello account. Hello account deve disporre dei privilegi di hello elencati in hello [preparare un account per l'individuazione automatica](#prepare-an-account-for-automatic-discovery) sezione.
4. Nel portale di Azure hello, passare troppo*YourRecoveryServicesVault* > **infrastruttura di Site Recovery** > **i server di configurazione,**  >  *ConfigurationServer*
5. Nella pagina dettagli del server di configurazione hello fare clic su hello **aggiornamento del Server** pulsante.
6. Al termine del processo di aggiornamento dei server hello, selezionare hello vCenter Server tooopen hello vCenter pagina di riepilogo.
7. Account seleziona hello appena aggiunto in hello **account dell'host vCenter server/vSphere** campo e fare clic su hello **salvare** pulsante.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Eliminare un server vCenter in Azure Site Recovery
1. Nel portale di Azure hello, passare troppo*YourRecoveryServicesVault* > **infrastruttura di Site Recovery** > **i server di configurazione,**  >  *ConfigurationServer*
2. Nella pagina dei dettagli del server di configurazione hello selezionare hello vCenter Server tooopen hello vCenter pagina di riepilogo.
3. Fare clic su hello **eliminare** pulsante toodelete hello vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Se è necessario toomodify hello vCenter indirizzo IP o FQDN, dettagli della porta, sarà necessario toodelete hello vCenter Server e aggiungerlo di nuovo nuovamente.
