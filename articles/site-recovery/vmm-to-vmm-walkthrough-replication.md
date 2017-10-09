---
title: aaaSet un criterio di replica per il sito secondario con tooa di replica Hyper-V con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset i criteri per la macchina virtuale Hyper-V replica tooa VMM secondario del sito con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Passaggio 8: Configurare un criterio di replica

Dopo aver configurato [mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md), utilizzare tooset questo articolo di un criterio di replica per Hyper-V macchina virtuale (VM) replica tooa sito secondario, utilizzando [Azure Site Recovery](site-recovery-overview.md).

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Prima di iniziare

- Quando si crea un criterio di replica, tutti gli host tramite criteri di hello devono avere hello stesso sistema operativo. Hello cloud VMM può contenere host Hyper-V che eseguono versioni diverse di Windows Server, ma in questo caso, è necessario più criteri di replica.
- È possibile eseguire hello la replica iniziale offline.

## <a name="configure-replication-settings"></a>Configurare le impostazioni di replica

1. toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.

    ![Rete](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. In **Criteri di creazione e associazione**specificare il nome dei criteri. Hello tipo di origine e di destinazione deve essere **Hyper-V**.
3. In **versione dell'host Hyper-V**, selezionare il sistema operativo è in esecuzione nell'host di hello.
4. In **tipo di autenticazione** e **porta di autenticazione**, specificare come viene autenticato il traffico tra hello primario e i server host Hyper-V di ripristino. Selezionare **Certificato** a meno che non sia configurato un ambiente Kerberos funzionante. Azure Site Recovery configura automaticamente i certificati per l'autenticazione HTTPS. Non è necessario toodo nulla manualmente. Per impostazione predefinita, porte 8083 e 8084 (per i certificati) sono aperte in hello Windows Firewall nei server host Hyper-V di hello. Se si seleziona **Kerberos**, verrà usato un ticket Kerberos per l'autenticazione reciproca dei server host hello. Questa impostazione è rilevante solo per i server host Hyper-V in esecuzione su Windows Server 2012 R2.
5. In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).
6. In **conservazione del punto di ripristino**, specificare in ore, per quanto tempo il periodo di memorizzazione hello verrà per ogni punto di ripristino. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di una finestra.
7. In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello. Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot. Se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine. Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.
8. In **Compressione trasferimento dati**specificare se i dati replicati che vengono trasferiti devono essere compressi.
9. Selezionare **Elimina replica VM**, toospecify che hello macchina virtuale di replica deve essere eliminata se si disabilita la protezione per la macchina virtuale di origine hello. Se si abilita questa impostazione, quando si disabilita la protezione per la macchina virtuale viene rimosso dalla console di Site Recovery hello di origine di hello, le impostazioni di Site Recovery per VMM hello vengono rimosse dalla console VMM hello e hello replica viene eliminata.
10. In **il metodo di replica iniziale**, se si esegue la replica in rete hello, specificare se toostart hello la replica iniziale o la pianificazione. larghezza di banda toosave, potrebbe essere necessario tooschedule è di fuori dell'orario di disponibilità. Fare quindi clic su **OK**.

     ![Criteri di replica](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Quando si crea un nuovo criterio automaticamente associato hello cloud VMM. In **Criteri di replica** fare clic su **OK**. È possibile associare altri cloud VMM (e hello macchine virtuali in essi contenuti) con questo criterio di replica in **replica** > Nome criterio > **associare Cloud VMM**.

     ![Criteri di replica](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Preparare la replica iniziale offline

È possibile eseguire la replica offline per la copia di dati iniziale hello. Per prepararla, procedere come segue:

* Nel server di origine hello, specificare il percorso dal quale hello esportazione dei dati avrà luogo. Assegnare il controllo completo per le autorizzazioni di condivisione e NTFS, il servizio VMM toohello nel percorso di esportazione hello. Nel server di destinazione hello, specificare il percorso da cui importare i dati di hello si verificherà. Assegnare hello delle stesse autorizzazioni su questo percorso di importazione.
* Se hello importare o percorso di esportazione è condiviso, assegnare l'appartenenza al gruppo Administrator, Power User, Print Operator o Server Operators per l'account del servizio VMM hello nel computer remoto hello in cui hello condiviso si trova.
* Se si utilizza qualsiasi host tooadd account RunAs, su hello importare ed esportare i percorsi, assegnare di lettura e delle autorizzazioni di scrittura toohello account RunAs in VMM.
* Hello importazione ed esportazione di condivisioni non deve trovarsi in qualsiasi computer utilizzato come server host Hyper-V, perché la configurazione di loopback non è supportata da Hyper-V.
* In Active Directory, in ogni server host Hyper-V che contiene le macchine virtuali da tooprotect, abilitare e configurare la delega vincolata tootrust hello computer remoti in cui hello importazione e l'esportazione percorsi si trovano, come indicato di seguito:
  1. Nel controller di dominio hello, aprire **Active Directory Users and Computers**.
  2. Nella console di hello, fare clic su **DomainName** > **computer**.
  3. Nome del server host Hyper-V hello rapida > **proprietà**.
  4. In hello **delega** scheda, fare clic su **computer attendibile per i servizi solo di delega toospecified**.
  5. Fare clic su **Usa un qualsiasi protocollo di autenticazione**.
  6. Fare clic su **Aggiungi** > **Utenti e computer**.
  7. Nome del computer di hello che ospita il percorso di esportazione hello hello di tipo > **OK**. Tenere premuto CTRL hello hello l'elenco dei servizi disponibili e fare clic su **cifs** > **OK**. Ripetere per il nome del computer hello hello tale percorso di importazione hello host. Ripetere l'operazione per eventuali altri server host Hyper-V.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 9: abilitare la replica](vmm-to-vmm-walkthrough-enable-replication.md).
