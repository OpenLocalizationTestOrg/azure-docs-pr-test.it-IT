---
title: aaaProtect Active Directory e DNS con Azure Site Recovery | Documenti Microsoft
description: Questo articolo viene descritto come tooimplement una soluzione di ripristino di emergenza per Active Directory mediante Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Proteggere Active Directory e DNS con Azure Site Recovery
Applicazioni aziendali, ad esempio SharePoint, Dynamics AX e SAP dipendono da Active Directory e un toofunction infrastruttura DNS, in modo corretto. Quando si crea una soluzione di ripristino di emergenza per le applicazioni, è importante tooremember che è necessario tooprotect e il ripristino di Active Directory e DNS prima di hello altri componenti dell'applicazione, tooensure che aspetti funzionano correttamente quando si verifica un'emergenza.

Site Recovery è un servizio di Azure che fornisce il ripristino di emergenza orchestrando la replica, il failover e il ripristino delle macchine virtuali. Il ripristino del sito supporta numerosi scenari di replica tooconsistently proteggere e facilmente il failover le macchine virtuali e applicazioni tooprivate, public o hoster cloud.

Con Site Recovery è possibile creare un piano di ripristino di emergenza interamente automatizzato per Active Directory. In caso di interruzione, è possibile avviare un failover in pochi secondi da qualsiasi luogo e fare in modo che Active Directory sia operativo in pochi minuti. Se distribuiti Active Directory per più applicazioni, ad esempio SharePoint e SAP nel sito primario e si desidera toofail sulla sito completo hello, è possibile eseguire un failover di Active Directory prima di utilizzare il ripristino del sito e quindi eseguire il failover hello altre applicazioni utilizzo di piani di ripristino specifico dell'applicazione.

Questo articolo spiega come hello toocreate una soluzione di ripristino di emergenza per Active Directory, come tooperform pianificato, non pianificato e i test failover usando un piano di ripristino di un solo clic, prerequisiti e le configurazioni supportate.  È necessario conoscere Active Directory e Azure Site Recovery prima di iniziare.

## <a name="replicating-domain-controller"></a>Replica del controller di dominio

È necessario toosetup [la replica di Site Recovery](#enable-protection-using-site-recovery) su almeno una macchina virtuale che ospita il Controller di dominio e DNS. Se dispone di [più controller di dominio](#environment-with-multiple-domain-controllers) nell'ambiente in uso, inoltre tooreplicating hello macchina virtuale controller di dominio con il ripristino del sito, è necessario tooset backup un [controllerdidominioaggiuntivo](#protect-active-directory-with-active-directory-replication) nel sito di destinazione hello (Azure o un Data Center secondario locale). 

### <a name="single-domain-controller-environment"></a>Ambiente con singolo controller di dominio
Se si dispone di alcune applicazioni e solo un singolo controller di dominio e si desidera toofail sull'intero sito hello insieme, quindi si consiglia di utilizzare controller di dominio di Site Recovery tooreplicate hello toohello di sito secondario (se sta failover tooAzure o tooa del sito secondario). Hello stesso replicati utilizzabile per macchina virtuale DNS o controller di dominio [failover di test](#test-failover-considerations) anche.

### <a name="environment-with-multiple-domain-controllers"></a>Ambiente con più controller di dominio
Se si dispone di molte applicazioni e in più di un controller di dominio nell'ambiente di hello, o se si intende toofail in alcune applicazioni alla volta, è consigliabile che anche controller di dominio hello tooreplicating virtuale del computer con il ripristino del sito è anche impostare un [controller di dominio aggiuntivo](#protect-active-directory-with-active-directory-replication) nel sito di destinazione hello (Azure o un Data Center secondario locale). Per [failover di test](#test-failover-considerations), utilizzare il controller di dominio replicato da un ripristino del sito e per il failover, il controller di dominio aggiuntivo hello nel sito di destinazione hello. 


Hello nelle sezioni seguenti viene illustrato come protezione tooenable per un controller di dominio in Site Recovery e come tooset un controller di dominio in Azure.

## <a name="prerequisites"></a>Prerequisiti
* Una distribuzione locale del server DNS e di Active Directory.
* Un insieme di credenziali dei servizi Azure Site Recovery in una sottoscrizione di Microsoft Azure.
* Se si esegue la replica tooAzure, eseguire lo strumento di valutazione della macchina virtuale Azure hello in macchine virtuali tooensure ma sono compatibili con macchine virtuali di Azure e servizi di Azure Site Recovery.

## <a name="enable-protection-using-site-recovery"></a>Abilitare la protezione usando Site Recovery
### <a name="protect-hello-virtual-machine"></a>Proteggere una macchina virtuale hello
Abilitare la protezione della macchina virtuale DNS o controller di dominio hello in Site Recovery. Configurare le impostazioni di ripristino del sito in base al tipo di macchina virtuale hello (Hyper-V o VMware). controller di dominio Hello replicate tramite il ripristino del sito viene utilizzato per [failover di test](#test-failover-considerations). Assicurarsi che vengano soddisfatti i seguenti requisiti hello:

1. controller di dominio Hello è un server di catalogo globale
2. controller di dominio Hello deve essere proprietario del ruolo FSMO hello per i ruoli che saranno necessari durante un failover di test (in caso contrario, questi ruoli dovrà toobe [requisito](http://aka.ms/ad_seize_fsmo) dopo il failover hello)

### <a name="configure-virtual-machine-network-settings"></a>Configurare le impostazioni di rete della macchina virtuale
Per la macchina virtuale controller/DNS del dominio hello, configurare le impostazioni di rete in Site Recovery in modo che macchina virtuale hello toohello associata la rete dopo il failover. 

![Impostazioni di rete della VM](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Proteggere Active Directory con la replica di Active Directory
### <a name="site-to-site-protection"></a>Protezione da sito a sito
Creare un controller di dominio nel sito secondario hello. Quando si innalza di livello ruolo controller di dominio di hello server tooa, specificare il nome di hello di hello nello stesso dominio in uso nel sito primario di hello. È possibile utilizzare hello **Active Directory, siti e servizi** snap-dell'oggetto impostazioni tooconfigure nel collegamento di sito hello toowhich hello siti vengono aggiunti. Configurando le impostazioni in un collegamento di sito, è possibile controllare quando viene eseguita la replica tra due o più siti e con quale frequenza. Per altre informazioni, vedere [Pianificazione della replica tra siti](https://technet.microsoft.com/library/cc731862.aspx) .

### <a name="site-to-azure-protection"></a>Protezione da sito ad Azure
Seguire le istruzioni di hello troppo[creare un controller di dominio in una rete virtuale di Azure](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Quando si innalza di livello ruolo controller di dominio di hello server tooa, specificare hello stesso nome di dominio utilizzato nel sito primario di hello.

Quindi [riconfigurare hello DNS server per la rete virtuale hello](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), server DNS di hello toouse in Azure.

![Azure Network](./media/site-recovery-active-directory/azure-network.png)

**DNS nella rete di produzione di Azure**

## <a name="test-failover-considerations"></a>considerazioni sul failover di test
Il failover di test si verifica in una rete isolata dalla rete di produzione, in modo che non si verifichi alcun impatto sui carichi di lavoro di produzione.

La maggior parte delle applicazioni richiedono inoltre presenza hello di un controller di dominio e un toofunction server DNS. Pertanto, prima di un'applicazione hello è stata eseguita il failover, un controller di dominio deve toobe creato in toobe rete hello isolato utilizzato per il failover di test. Hello toodo modo più semplice si tratta di una macchina virtuale DNS o controller di dominio con il ripristino del sito tooreplicate. Quindi eseguire un failover di test della macchina virtuale controller di dominio hello prima di eseguire un failover di test hello del piano di ripristino per un'applicazione hello. Di seguito viene indicato come procedere:

1. [Replicare](site-recovery-replicate-vmware-to-azure.md) hello macchina virtuale DNS o controller di dominio tramite il ripristino del sito.
1. Creare una rete isolata. Qualsiasi rete virtuale creata in Azure per impostazione predefinita è isolata dalle altre reti. È consigliabile che l'intervallo di indirizzi IP hello per la rete è corrisponde a quello della rete di produzione. Non abilitare la connettività da sito a sito in questa rete.
1. Specificare un indirizzo IP DNS nella rete hello creato, come indirizzo IP hello che si prevede di tooget di macchina virtuale DNS hello. Se si esegue la replica tooAzure, quindi fornire l'indirizzo IP hello per macchina virtuale che viene utilizzato in caso di failover in hello **indirizzo IP di destinazione** impostazione in **di calcolo e rete** impostazioni. 

    ![IP di destinazione](./media/site-recovery-active-directory/DNS-Target-IP.png)**IP di destinazione**

    ![Rete di test di Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS nella rete di test di Azure**

> [!TIP]
> Il ripristino del sito tenta toocreate macchine virtuali di test in una subnet con stesso nome e con hello stesso IP a quella fornita **di calcolo e rete** impostazioni della macchina virtuale hello. Se non è disponibile nella rete virtuale di Azure fornito per il failover di test, hello subnet stesso nome macchina virtuale di test viene creato nella prima subnet hello in ordine alfabetico. Se hello IP di destinazione fa parte di hello scelto subnet, il ripristino del sito tenta di macchina virtuale toocreate hello test failover utilizzando l'indirizzo IP di destinazione hello. Se l'indirizzo IP di destinazione hello non fa parte di hello scelto subnet, macchina virtuale di test failover viene creata utilizzando qualsiasi IP disponibile in hello scelto subnet. 
>
>


1. Se si esegue la replica da sito locale tooanother e si usa DHCP, seguire le istruzioni di hello troppo[configurare DNS e DHCP per il failover di test](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Eseguire un failover di test della macchina virtuale controller dominio hello eseguito in una rete isolata hello. Utilizzare più recente disponibile **coerenti con l'applicazione** punto di ripristino di hello macchina virtuale di controller di dominio toodo failover di test di hello. 
1. Eseguire un failover di test per il piano di ripristino hello contenente macchine virtuali di un'applicazione hello. 
1. Al termine il test, **il failover di test di pulizia** nella macchina virtuale controller di dominio hello. Questo passaggio consente di eliminare i controller di dominio hello che è stato creato per il failover di test.


### <a name="removing-reference-tooother-domain-controllers"></a>Rimozione dei controller di dominio di riferimento tooother
Quando si esegue un failover di test, non connettere tutti i controller di dominio hello in rete di test hello. riferimento di hello tooremove altri controller di dominio presenti nell'ambiente di produzione, potrebbe essere troppo[requisire i ruoli FSMO Active Directory](http://aka.ms/ad_seize_fsmo) e [pulizia dei metadati](https://technet.microsoft.com/library/cc816907.aspx) per dominio mancante controller. 



> [!IMPORTANT]
> Alcune delle configurazioni di hello descritte nella seguente sezione hello non sono le configurazioni del controller dominio hello standard o predefinito. Se non si desidera toomake che questi controller di dominio di produzione tooa modifiche, è possibile creare un toobe dedicato di controller di dominio utilizzato per il ripristino del sito di failover di test e rendere toothat queste modifiche.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemi dovuti alle misure di sicurezza della virtualizzazione 

A partire da Windows Server 2012, [sono state integrate misure di sicurezza aggiuntive in Active Directory Domain Services](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Queste misure di sicurezza aiutano a proteggere i controller di dominio virtualizzati rollback degli USN, purché piattaforma hypervisor sottostante hello supporta VM-GenerationID. Azure supporta VM-GenerationID, ciò significa che i controller di dominio che eseguono Windows Server 2012 o macchine virtuali di Azure in un secondo momento misure di sicurezza aggiuntive di hello. 


Quando hello VM-GenerationID viene reimpostato, viene inoltre reimpostato hello invocationID del database di hello AD DS, hello pool di RID viene ignorato e SYSVOL è contrassegnato come non autorevole. Per ulteriori informazioni, vedere [tooActive introduzione virtualizzazione di servizi di Directory dominio](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) e [virtualizzazione sicura di DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Failover tooAzure può causare la reimpostazione dell'ID di generazione VM e che interviene misure di sicurezza aggiuntive di hello all'avvio di macchina virtuale controller di dominio hello in Azure. Questo può comportare un **un ritardo significativo** nella macchina virtuale del controller in grado di toologin toohello dominio utente. Poiché questo controller di dominio viene usato solo in un failover di test, non sono necessari misure di sicurezza della virtualizzazione. tooensure che non cambia l'ID di generazione VM per la macchina virtuale controller di dominio hello, è possibile modificare il valore di hello di too4 DWORD seguente nel controller di dominio locale hello.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Sintomi delle misure di sicurezza della virtualizzazione
 
Se le misure di sicurezza della virtualizzazione sono intervenute dopo un failover di test, è possibile che si verifichi uno o più dei seguenti sintomi:  

Modifica dell'ID di generazione

![Modifica dell'ID di generazione](./media/site-recovery-active-directory/Event2170.png)

Modifica dell'ID di chiamata

![Modifica dell'ID di chiamata](./media/site-recovery-active-directory/Event1109.png)

Condivisioni SYSVOL e Netlogon non disponibili

![Condivisione SYSVOL](./media/site-recovery-active-directory/sysvolshare.png)

![NTFRS Sysvol](./media/site-recovery-active-directory/Event13565.png)

Vengono eliminati tutti i database DFSR

![Eliminazione del database DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Alcune delle configurazioni di hello descritte nella seguente sezione hello non sono le configurazioni del controller dominio hello standard o predefinito. Se non si desidera toomake che questi controller di dominio di produzione tooa modifiche, è possibile creare un toobe dedicato di controller di dominio utilizzato per il ripristino del sito di failover di test e rendere toothat queste modifiche.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Risolvere i problemi del controller di dominio durante il failover di test


In un prompt dei comandi, eseguire hello successivo comando toocheck se NETLOGON e SYSVOL condivise:

    NET SHARE

Nel prompt dei comandi di hello, eseguire hello comando funzionante tooensure che hello controller di dominio seguente.

    dcdiag /v > dcdiag.txt

Nel log di output di hello, cercare tooconfirm testo seguente che hello controller di dominio funziona correttamente. 

* "passed test Connectivity"
* "passed test Advertising"
* "passed test MachineAccount"

Se hello precedente condizioni vengono soddisfatte, è probabile che il controller di dominio hello funziona correttamente. In caso contrario, attenersi alla procedura seguente.


* Eseguire un ripristino autorevole hello del controller di dominio.
    * Sebbene sia [non è consigliabile replica FRS toouse](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), ma se si sta ancora utilizzando hello procedure fornite [qui](https://support.microsoft.com/kb/290762) toodo un ripristino autorevole. È possibile leggere ulteriori informazioni su Burflags parlato nel collegamento precedente hello [qui](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Se si utilizza la replica DFS, quindi seguire i passaggi di hello disponibili [qui](https://support.microsoft.com/kb/2218556) toodo un ripristino autorevole. A tale scopo è anche possibile usare le funzioni di Powershell disponibili in questo [collegamento](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/). 
    
* Ignorare il requisito di sincronizzazione iniziale mediante l'impostazione seguente too0 chiave del Registro di sistema nel controller di dominio locale hello. Se questo valore DWORD non esiste, può essere creato nel nodo "Parameters". Per altre informazioni, vedere [qui](https://support.microsoft.com/kb/2001093).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Disabilitare il requisito di hello che un server di catalogo globale è disponibile toovalidate dell'accesso utente tramite l'impostazione seguente too1 chiave del Registro di sistema nel controller di dominio locale hello. Se questo valore DWORD non esiste, può essere creato nel nodo "Lsa". Per altre informazioni, vedere [qui](http://support.microsoft.com/kb/241789).

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS e controller di dominio su computer diversi
Se DNS non è in hello stessa macchina virtuale come controller di dominio hello, è necessario toocreate una VM DNS per il failover di test hello. Se si trova nella stessa macchina virtuale di hello, è possibile ignorare questa sezione.

È possibile utilizzare un server DNS nuovo e creare tutte le zone hello necessario. Ad esempio, se il dominio di Active Directory è contoso.com, è possibile creare una zona DNS con il nome di hello contoso.com. le voci di Hello corrispondente tooActive Directory devono essere aggiornate nel DNS, come indicato di seguito:

1. Verificare che queste impostazioni sono presenti prima di altre macchine virtuali nel piano di ripristino hello viene visualizzato:
   
   * zona Hello deve essere denominata dopo il nome radice della foresta hello.
   * zona di Hello deve essere file di backup.
   * Hello area deve essere abilitata per gli aggiornamenti di protezione e non sicure.
   * resolver Hello della macchina virtuale controller di dominio hello deve puntare toohello di indirizzo IP della macchina virtuale di hello DNS.
2. Eseguire hello comando seguente nella macchina virtuale controller di dominio:
   
    `nltest /dsregdns`
3. Aggiungere una zona nel server DNS hello, consentire aggiornamenti non protetti e aggiungere una voce per tale tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Passaggi successivi
Lettura [i carichi di lavoro è possibile proteggere?](site-recovery-workload.md) toolearn ulteriori informazioni sulla protezione di carichi di lavoro aziendali con Azure Site Recovery.

