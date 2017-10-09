---
title: "funzionalità di sicurezza aaaAzure utilizzate con macchine virtuali di Azure | Documenti Microsoft"
description: " Panoramica della funzionalità di sicurezza di Azure di base hello che può essere utilizzato con macchine virtuali di Azure. Assegnare le macchine virtuali Azure è hello flessibilità della virtualizzazione senza toobuy e mantenere hello l'hardware fisico esegue hello macchina virtuale. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Informazioni generali sulla sicurezza di Macchine virtuali di Azure
Macchine virtuali di Azure consente di distribuire in modo flessibile un'ampia gamma di soluzioni di elaborazione. Grazie al supporto per Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP e Servizi BizTalk di Azure, è possibile distribuire qualsiasi carico di lavoro, in qualunque linguaggio, praticamente su tutti i sistemi operativi.

Fornisce una macchina virtuale di Azure è hello flessibilità della virtualizzazione senza toobuy e mantenere hardware fisico hello che esegue macchine virtuali hello.  È possibile compilare e distribuire le applicazioni con garanzia hello che i dati siano protetti e sicuro nel nostro datacenter estremamente sicuro.

Con Azure è possibile creare soluzioni conformi con sicurezza avanzata che:

* Proteggono le macchine virtuali da virus e malware
* Applicano la crittografia ai dati sensibili
* Proteggono il traffico di rete
* Identificano e rilevano minacce
* Soddisfano i requisiti di conformità

obiettivo di Hello di questo articolo è tooprovide una panoramica delle funzionalità di sicurezza di Azure core hello che può essere utilizzato con le macchine virtuali. È possibile utilizzare collegamenti tooarticles che forniscono i dettagli di ogni funzionalità in modo per ulteriori informazioni.  

Hello core macchina virtuale di Azure sicurezza funzionalità toobe illustrate in questo articolo:

* Antimalware
* Modulo di protezione hardware
* Crittografia dischi delle macchine virtuali
* Backup di una macchina virtuale
* Azure Site Recovery
* Reti virtuali
* Gestione e reporting dei criteri di sicurezza
* Conformità

## <a name="antimalware"></a>Antimalware
Con Azure, è possibile utilizzare il software antimalware di fornitori di sicurezza, ad esempio Microsoft, Symantec, Trend Micro e Kaspersky tooprotect delle macchine virtuali dal file dannosi, adware e altre minacce. Vedere hello articoli toofind sezione altre informazioni su soluzioni dei partner.

Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure è una funzionalità di protezione in tempo reale che aiuta a identificare e rimuovere virus, spyware e altro software dannoso.  Microsoft Antimalware fornisce avvisi configurabili quando noto tooinstall di tentativi di software dannoso o indesiderato stesso o eseguito nei sistemi di Azure.

Microsoft Antimalware è una soluzione singolo agente per le applicazioni e gli ambienti di tenant, toorun progettato in background hello senza intervento umano. È possibile distribuire la protezione in base alle esigenze di hello i carichi di lavoro dell'applicazione, con una base sicura-per impostazione predefinita o configurazione personalizzata, ad esempio il monitoraggio antimalware avanzata.

Quando si distribuisce e abilita Microsoft Antimalware, hello seguenti funzionalità di base sono disponibile:

* Protezione in tempo reale - attività di monitor in servizi Cloud e macchine virtuali toodetect e blocco di esecuzione di malware.
* Funzionalità di analisi pianificata - esegue periodicamente destinazione analisi malware toodetect, inclusi i programmi in esecuzione.
* Correzione del malware: interviene automaticamente sul malware rilevato, ad esempio eliminando o mettendo in quarantena i file dannosi e pulendo le voci dannose del Registro di sistema.
* Aggiornamenti firma - automaticamente installa hello più recente protezione firme (definizioni di virus) tooensure dati sono aggiornata sulla frequenza predeterminata.
* Motore antimalware Aggiorna automaticamente gli aggiornamenti hello motore Antimalware Microsoft.
* Piattaforma antimalware Aggiorna automaticamente gli aggiornamenti hello piattaforma Microsoft Antimalware.
* Attiva la protezione dati - report tooAzure telemetria metadati sulle minacce rilevate risorse sospette tooensure rapida risposta e Abilita firma sincrono in tempo reale del recapito e tramite hello Microsoft Active Protection System (MAPS).
* Esempi di reporting: viene fornita e segnala gli esempi toohello Microsoft Antimalware service toohelp perfezionare servizio hello e abilitare la risoluzione dei problemi.
* Esclusioni: consente l'applicazione e servizio amministratori tooconfigure determinati file, i processi e unità tooexclude di protezione e l'analisi per motivi di prestazioni e altri.
* Raccolta di eventi antimalware - registra l'integrità del servizio antimalware hello, le attività sospette e azioni di correzione nel registro eventi di sistema operativo hello e li raccoglie in account di archiviazione di Azure del cliente hello.

Altre informazioni: informazioni su tooprotect software antimalware toolearn le macchine virtuali, vedere:

* [Microsoft Antimalware per Servizi cloud e Macchine virtuali di Azure](azure-security-antimalware.md)
* [Distribuzione di soluzioni antimalware in macchine virtuali di Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Come tooinstall e configurare Trend Micro Deep Security come servizio in una macchina virtuale Windows](../virtual-machines/windows/classic/install-trend.md)
* [Come tooinstall e configurare Symantec Endpoint Protection in una macchina virtuale Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Soluzioni per la sicurezza in hello Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Modulo di protezione hardware
Le protezioni con crittografia e autenticazione possono essere migliorate aumentando la sicurezza delle chiavi. È possibile semplificare hello gestione e protezione delle chiavi e segreti critici archiviandole in insieme di credenziali chiave di Azure. Insieme di credenziali chiave fornisce hello opzione toostore le chiavi di standard di livello 2 di 140-2 tooFIPS certificate di moduli di protezione hardware. Le chiavi di crittografia di SQL Server per backup o [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx) possono essere tutte archiviate nell'insieme di credenziali delle chiavi con qualsiasi chiave o segreto delle applicazioni. Le autorizzazioni e accedere agli elementi di toothese protetti viene gestiti tramite [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Altre informazioni:

* [Cos'è l'insieme di credenziali chiave di Azure?](../key-vault/key-vault-whatis.md)
* [Introduzione all'insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-get-started.md)
* [Blog sull'insieme di credenziali delle chiavi di Azure](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Crittografia dischi delle macchine virtuali
Crittografia dischi di Azure è una nuova funzionalità che consente di crittografare i dischi delle macchine virtuali di Azure in Windows e Linux. Crittografia disco Azure utilizza standard di settore hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funzionalità di Windows e hello [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt) funzionalità di crittografia del volume tooprovide Linux per hello del sistema operativo e i dischi dati hello.

soluzione hello è integrato con insieme credenziali chiavi Azure toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia disco hello nella sottoscrizione di insieme di credenziali delle chiavi, assicurando che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.

Altre informazioni:

* [Azure Disk Encryption per le macchine virtuali IaaS Windows e Linux](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Crittografia dischi di Azure per le macchine virtuali di Windows e Linux](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Crittografare una macchina virtuale](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Backup di una macchina virtuale
Backup di Azure è una soluzione scalabile che protegge i dati delle applicazioni senza investimenti di capitale e con costi operativi minimi. Gli errori delle applicazioni possono danneggiare i dati e gli errori umani possono comportare l'introduzione di bug nelle applicazioni. Con Backup di Azure, le macchine virtuali che eseguono Windows e Linux sono protette.

Altre informazioni:

* [Informazioni su Backup di Azure](../backup/backup-introduction-to-azure-backup.md)
* [Percorso di apprendimento di Backup di Azure](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Servizio Backup di Azure: Domande frequenti](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Una parte importante della strategia BCDR dell'organizzazione è pensare a come si verificano tookeep carichi di lavoro aziendali e App di backup e in esecuzione quando pianificato e interruzioni non pianificate. Azure Site Recovery consente di orchestrare la replica, il failover e il ripristino di carichi di lavoro e app in modo che siano disponibili da una località secondaria in caso di inattività di quella primaria.

Site Recovery:

* **Consente di semplificare la strategia di BCDR** -Site Recovery rende replica toohandle semplice, failover e ripristino di più carichi di lavoro di business e applicazioni da un'unica posizione. Site Recovery orchestra la replica e il failover, ma non intercetta i dati dell'applicazione né raccoglie le relative informazioni.
* **Offre una modalità di replica flessibile** : con Site Recovery è possibile replicare i carichi di lavoro in esecuzione in macchine virtuali Hyper-V, macchine virtuali VMware e server fisici Windows o Linux.
* **Supporta il failover e ripristino** -Site Recovery fornisce i test failover drill di ripristino di emergenza toosupport senza modificare gli ambienti di produzione. È anche possibile eseguire failover pianificati senza perdita di dati per interruzioni previste o il failover non pianificato con perdita di dati minima, in base alla frequenza di replica, per emergenze impreviste. Dopo il failover, è possibile eseguire il failback tooyour i siti primari. Site Recovery fornisce i piani di ripristino che possono includere script e cartelle di lavoro di automazione di Azure per personalizzare il failover e il ripristino di applicazioni multilivello.
* **Elimina i Data Center secondario** , è possibile replicare tooa secondario nel sito locale o tooAzure. Uso di Azure come destinazione di ripristino di emergenza Elimina hello costi e complessità di gestione di un sito secondario. I dati replicati vengono archiviati nell'archiviazione di Azure.
* **Si integra con le tecnologie BCDR esistenti** : Site Recovery interagisce con altre funzionalità BCDR dell'applicazione. Ad esempio, è possibile utilizzare il ripristino del sito tooprotect hello Server SQL back-end di carichi di lavoro aziendali. Ciò include il supporto nativo per il failover di SQL Server AlwaysOn toomanage hello dei gruppi di disponibilità.

Altre informazioni:

* [Che cos'è Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
* [Funzionamento di Azure Site Recovery](../site-recovery/site-recovery-components.md)
* [Quali carichi di lavoro è possibile proteggere con Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Reti virtuali
La connettività di rete è indispensabile per le macchine virtuali. toosupport tale requisito, Azure richiede toobe macchine virtuali connesse tooan rete virtuale di Azure. Una rete virtuale di Azure è un costrutto logico basato sull'infrastruttura di rete di Azure fisica hello. Ogni rete virtuale di Azure logica è isolata da tutte le altre reti virtuali di Azure. Questo isolamento contribuisce a garantire che il traffico di rete nelle distribuzioni non è accessibile tooother i clienti di Microsoft Azure.

Altre informazioni:

* [Panoramica della sicurezza di rete di Azure](security-network-overview.md)
* [Panoramica di Rete virtuale.](../virtual-network/virtual-networks-overview.md)
* [Funzionalità di rete e relazioni per gli scenari aziendali](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Gestione e reporting dei criteri di sicurezza
Centro sicurezza di Azure consente di impedire, rilevare e rispondere toothreats e fornisce che maggiore visibilità e controllare i sicurezza hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Il Centro sicurezza di Azure consente di ottimizzare e monitorare la sicurezza delle macchine virtuali offrendo:

* [Consigli sulla sicurezza](../security-center/security-center-recommendations.md) per le macchine virtuali, ad esempio come applicare gli aggiornamenti del sistema, configurare gli endpoint ACL, abilitare antimalware, abilitare i gruppi di sicurezza di rete e applicare la crittografia del disco.
* Monitoraggio dello stato di hello delle macchine virtuali

Altre informazioni:

* [Introduzione tooAzure Centro sicurezza](../security-center/security-center-intro.md)
* [Domande frequenti sul Centro sicurezza di Azure](../security-center/security-center-faq.md)
* [Pianificazione e gestione del Centro sicurezza di Azure](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Conformità
Macchine virtuali di Azure ha ottenuto le certificazioni per FISMA, FedRAMP, HIPAA, PCI DSS Livello 1 e altri importanti programmi di conformità. Questa certificazione rende più semplice per i propri requisiti di conformità toomeet applicazioni Azure e per il tooaddress business un'ampia gamma di requisiti normativi nazionali e internazionali.

Altre informazioni:

* [Centro protezione Microsoft - Conformità](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Trusted Cloud: sicurezza, privacy e conformità di Microsoft Azure](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
