---
title: 'Guida introduttiva: Installazione manuale di SAP HANA a istanza singola nelle macchine virtuali di Azure | Microsoft Docs'
description: Guida introduttiva per l'installazione manuale di SAP HANA a istanza singola nelle macchine virtuali di Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Guida introduttiva: Installazione manuale di SAP HANA a istanza singola nelle macchine virtuali di Azure
## <a name="introduction"></a>Introduzione
Questa guida consente di configurare SAP HANA a istanza singola nelle macchine virtuali di Azure quando si installano manualmente SAP NetWeaver 7.5 e SAP HANA 1.0 SP12. Hello di questa guida è attiva la distribuzione di SAP HANA in Azure. Questa guida non sostituisce la documentazione SAP. 

>[!Note]
>Questa guida descrive le distribuzioni di SAP HANA in macchine virtuali di Azure. Per informazioni sulla distribuzione di SAP HANA in istanze HANA di grandi dimensioni, vedere [Uso di SAP nelle macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Prerequisiti
La guida presuppone che l'utente abbia familiarità con le nozioni di base sull'infrastruttura distribuita come servizio (IaaS) come:
 * Come toodeploy le macchine virtuali o reti virtuali tramite hello portale di Azure o PowerShell.
 * Hello Azure multipiattaforma interfaccia della riga di comando (CLI), inclusi i modelli di hello opzione toouse JavaScript Object Notation (JSON).

Questo guida presuppone che l'utente abbia familiarità anche con le nozioni seguenti:
* SAP HANA e SAP NetWeaver e come tooinstall usarle in locale.
* Installazione e uso delle istanze di applicazione SAP HANA e SAP in Azure.
* Hello concetti e le procedure seguenti:
   * Pianificazione della distribuzione SAP in Azure, inclusi la pianificazione della rete virtuale di Azure e l'uso dell'archiviazione di Azure. Vedere [SAP NetWeaver in macchine virtuali di Azure: guida alla pianificazione e all'implementazione](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Distribuzione toodeploy principi e le modalità di macchine virtuali in Azure. Vedere [Distribuzione di macchine virtuali di Azure per SAP](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Disponibilità elevata per SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services) ed ERS (Evaluated Receipt Settlement) in Azure. Vedere [Disponibilità elevata per SAP NetWeaver in macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * I dettagli sull'efficienza tooimprove all'utilizzo di un'installazione più SID di ASCS/SCS in Azure. Vedere [Creare una configurazione di SAP NetWeaver a più SID](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Principi di esecuzione di SAP NetWeaver basato su macchine virtuali Linux in Azure. Vedere [Esecuzione di SAP NetWeaver nelle VM SUSE Linux di Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Questa guida fornisce le impostazioni specifiche per Linux in macchine virtuali di Azure e informazioni dettagliate su come tooproperly allegare tooLinux dischi di archiviazione di Azure le macchine virtuali.

Attualmente, le macchine virtuali di Azure sono certificate da SAP solo per le configurazioni per passare a SAP HANA. Le configurazioni con scalabilità orizzontale con il carico di lavoro SAP HANA non sono ancora supportate. Per la disponibilità elevata di SAP HANA nei casi di configurazioni per passare a un livello superiore, vedere [Disponibilità elevata di SAP HANA nelle macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Se si cerca tooget un'istanza di SAP HANA o S/4HANA o sistema BW/4HANA distribuita in un tempo molto veloce, è necessario considerare utilizzo hello di [SAP Cloud accessorio libreria](http://cal.sap.com). In [questa guida](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h) è disponibile la documentazione sulla distribuzione ad esempio di un sistema S/4HANA tramite SAP CAL in Azure. È sufficiente toohave è una sottoscrizione di Azure e un utente SAP che può essere registrato con SAP Cloud accessorio libreria.

## <a name="additional-resources"></a>Risorse aggiuntive
### <a name="sap-hana-backup"></a>Backup di SAP HANA
Per informazioni sul backup dei database SAP HANA nelle macchine virtuali di Azure, vedere:
* [Guida del backup di SAP HANA in macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Backup di SAP HANA di Azure a livello di file](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [Backup di SAP HANA basato su snapshot di archiviazione](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>SAP Cloud Appliance Library
Per informazioni sull'utilizzo di SAP Cloud accessorio libreria toodeploy S/4HANA o BW/4HANA, vedere [BW/4HANA in Microsoft Azure o distribuire SAP S/4HANA](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>Sistemi operativi supportati di SAP HANA
Per informazioni sui sistemi operativi supportati di SAP HANA, vedere [SAP Support Note #2235581 - SAP HANA: Supported Operating Systems](https://launchpad.support.sap.com/#/notes/2235581/E) (Nota di supporto SAP n. 2235581: SAP HANA: sistemi operativi supportati). Le macchine virtuali di Azure supportano soltanto alcuni di questi sistemi operativi. Hello seguenti sistemi operativi sono supportati toodeploy SAP HANA in Azure: 

* SUSE Linux Enterprise Server 12.x
* Red Hat Enterprise Linux 7.2

Per altra documentazione SAP su SAP HANA e sui diversi sistemi operativi Linux, vedere:

* [SAP Support Note #171356 - SAP Software on Linux:  General Information](https://launchpad.support.sap.com/#/notes/1984787) (Nota di supporto SAP n. 171356: informazioni generali sul software SAP in Linux)
* [SAP Support Note #1944799 - SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html) (Nota di supporto SAP n. 1944799: linee guida di SAP HANA per l'installazione del sistema operativo SLES)
* [SAP Support Note #2205917 - SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E) (Nota di supporto SAP n. 2205917: impostazioni del sistema operativo consigliate per il database di SAP HANA per SLES 12 for SAP Applications)
* [SAP Support Note #1984787 - SUSE Linux Enterprise Server 12:  Installation Notes](https://launchpad.support.sap.com/#/notes/1984787) (Nota di supporto SAP n. 1984787: SUSE Linux Enterprise Server 12: note di installazione)
* [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Nota di supporto SAP n. 1391070: soluzioni UUID Linux)
* [SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879) (Nota di supporto SAP #2009879: linee guida di SAP HANA per il sistema operativo Red Hat Enterprise Linux, RHEL)
* [2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E) (2292690 - SAP HANA DB: impostazioni del sistema operativo consigliate per RHEL 7)

### <a name="sap-monitoring-in-azure"></a>Monitoraggio SAP in Azure
Per informazioni sul monitoraggio SAP in Azure, vedere:

* [Nota SAP 2191498](https://launchpad.support.sap.com/#/notes/2191498/E). Questa nota descrive il monitoraggio avanzato SAP con macchine virtuali Linux in Azure. 
* [Nota SAP 1102124](https://launchpad.support.sap.com/#/notes/1102124/E). Questa nota include informazioni su SAPOSCOL in Linux. 
* [Nota SAP 2178632](https://launchpad.support.sap.com/#/notes/2178632/E). Questa nota descrive le metriche di monitoraggio principali per SAP in Microsoft Azure.

### <a name="azure-vm-types"></a>Tipi di macchine virtuali di Azure
I tipi di macchine virtuali di Azure e gli scenari di carico di lavoro supportati da SAP usati con SAP HANA sono documentati nelle [piattaforme IaaS certificate SAP](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

Tipi di macchine Virtuali Azure che sono certificati da SAP per SAP NetWeaver o hello S/4HANA livello dell'applicazione sono documentati in [SAP nota 1928533 - applicazioni SAP in Azure: tipi di prodotti supportati e macchina virtuale di Azure](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Integrazione di SAP-Linux-Azure è supportata solo in Gestione risorse di Azure e non il modello di distribuzione classica hello. 

## <a name="manual-installation-of-sap-hana"></a>Installazione manuale di SAP HANA
Questa guida viene descritto come toomanually installare SAP HANA in macchine virtuali di Azure in due modi diversi:

* Utilizzando SAP Software Provisioning Manager (SWPM) come parte di un'installazione distribuita NetWeaver nel passaggio "Installa l'istanza del database" hello
* Utilizzando hello SAP HANA database dello strumento di gestione del ciclo di vita, HDBLCM e quindi installare NetWeaver

È inoltre possibile utilizzare SWPM tooinstall tutti i componenti (SAP HANA, il server applicazioni SAP hello e istanza ASCS hello) in una singola macchina virtuale, come descritto in questo [annuncio sul blog di SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Questa opzione non è descritta in questa Guida rapida, ma i problemi che è necessario prendere in considerazione sono hello hello stesso.

Prima di iniziare un'installazione, è consigliabile leggere hello "Preparazione Azure le macchine virtuali per l'installazione manuale di SAP HANA" sezione più avanti in questa Guida. In questo modo, è possibile evitare diversi errori di base che possono verificarsi quando si usa solo una configurazione predefinita della VM di Azure.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Passaggi principali per l'installazione di SAP HANA quando si usa SAP SWPM
Questa sezione elenca i passaggi principali hello per un'installazione di SAP HANA manuale, è a istanza singola, quando si usa l'installazione di SAP SWPM tooperform la versione distribuita di SAP NetWeaver 7.5. in modo più dettagliato nelle schermate più avanti in questa guida sono illustrati i singoli passaggi Hello.

1. Creare una rete virtuale di Azure che includa le due macchine virtuali di test.
2. Distribuire hello due macchine virtuali di Azure con sistemi operativi (in questo esempio, SUSE Linux Enterprise Server (SLES) e SLES per SAP applicazioni 12 SP1), in base a modello di gestione risorse di Azure toohello.
3. Collegare Azure due standard o premium archiviazione (dischi, ad esempio, 500 GB o di 75 GB) toohello applicazione macchina virtuale del server.
4. Collegare dischi di archiviazione premium, HANA DB toohello server VM. Per informazioni dettagliate, vedere hello "disco sezione" configurazione più avanti in questa Guida.
5. A seconda dei requisiti di dimensione o velocità effettiva, collegare più dischi e quindi creare volumi con striping utilizzando Gestione volume logico o uno strumento di amministrazione di più dispositivi (MDADM) a livello di hello del sistema operativo all'interno di hello macchina virtuale.
6. Creare sistemi di file XFS su dischi collegato hello o volumi logici.
7. Montare hello nuovo XFS file System a livello di hello del sistema operativo. Utilizzare un file system per tutto il software SAP hello. Utilizzare hello altri sistemi di file per directory /sapmnt hello e backup, ad esempio. Nel server SAP HANA DB hello, montare i sistemi di file XFS hello nei dischi di archiviazione premium hello come /hana e /usr/sap. Questo processo è necessario tooprevent hello radice file system, che non è grande nelle macchine virtuali di Azure, Linux evitarne il riempimento.
8. Immettere indirizzi IP locali hello del test di hello macchine virtuali nel file hosts di hello/e così via.
9. Immettere hello **nofail** parametro nel file hello e così via/fstab.
10. Impostare i parametri del kernel Linux in base a versione del sistema operativo Linux toohello in uso. Per ulteriori informazioni, vedere le note SAP di appropriato hello che illustrano HANA e hello la sezione "Parametri Kernel" in questa Guida.
11. Aggiungere spazio di swapping.
12. Facoltativamente, è possibile installare un desktop con interfaccia grafico nel test hello macchine virtuali. In alternativa, usare un'installazione SAPinst remota.
13. Scaricare il software SAP hello da hello SAP Service Marketplace.
14. Installare l'istanza di SAP ASCS hello nel server di app hello macchina virtuale.
15. Directory condivisa di /sapmnt hello tra hello testare le macchine virtuali con NFS. server applicazioni Hello VM è NFS hello.
16. Installare l'istanza di database hello, incluse HANA, tramite SWPM nel server di database hello macchina virtuale.
17. Installare il server di applicazione principali hello (PAS) nel server di applicazione hello VM.
18. Avviare la console di gestione SAP (SAP MC). Connettersi ad esempio all'interfaccia utente grafica di SAP o HANA Studio.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Passaggi principali per l'installazione di SAP HANA quando si usa HDBLCM
Questa sezione elenca i passaggi principali hello per un'installazione di SAP HANA manuale, è a istanza singola, quando si usa l'installazione di SAP HDBLCM tooperform la versione distribuita di SAP NetWeaver 7.5. in modo più dettagliato nelle schermate in questa guida sono illustrati i singoli passaggi Hello.

1. Creare una rete virtuale di Azure che includa le due macchine virtuali di test.
2. Distribuire due macchine virtuali di Azure con sistemi operativi (in questo esempio, SLES e SLES per SAP applicazioni 12 SP1) in base a modello di gestione risorse di Azure toohello.
3. Collegare Azure due standard o premium archiviazione (dischi, ad esempio, 500 GB o di 75 GB) toohello app macchina virtuale del server.
4. Collegare dischi di archiviazione premium, HANA DB toohello server VM. Per informazioni dettagliate, vedere hello "disco sezione" configurazione più avanti in questa Guida.
5. A seconda dei requisiti di dimensione o velocità effettiva, creare volumi con striping tramite Gestione volume logico o uno strumento di amministrazione di più dispositivi (MDADM) a livello di hello del sistema operativo all'interno di hello VM collegare più dischi.
6. Creare sistemi di file XFS su dischi collegato hello o volumi logici.
7. Montare hello nuovo XFS file System a livello di hello del sistema operativo. Utilizzare un file system per tutto il software SAP hello e utilizzare hello un'altra per directory /sapmnt hello e backup, ad esempio. Nel server SAP HANA DB hello, montare i sistemi di file XFS hello nei dischi di archiviazione premium hello come /hana e /usr/sap. Questo processo è necessario toohelp evitare hello radice file system, che non è di grandi dimensioni nelle macchine virtuali di Azure di Linux, esaurisca.
8. Immettere indirizzi IP locali hello del test di hello macchine virtuali nel file hosts di hello/e così via.
9. Immettere hello **nofail** parametro nel file hello e così via/fstab.
10. Impostare i parametri del kernel in base a versione del sistema operativo Linux toohello in uso. Per ulteriori informazioni, vedere le note SAP di appropriato hello che illustrano HANA e hello la sezione "Parametri Kernel" in questa Guida.
11. Aggiungere spazio di swapping.
12. Facoltativamente, è possibile installare un desktop con interfaccia grafico nel test hello macchine virtuali. In alternativa, usare un'installazione SAPinst remota.
13. Scaricare il software SAP hello da hello SAP Service Marketplace.
14. Creare un gruppo, sapsys, con ID 1001, di gruppo nel server di database HANA hello VM.
15. Installare SAP HANA nel server di database hello VM usando HANA Database Lifecycle Manager (HDBLCM).
16. Installare l'istanza di SAP ASCS hello nel server di app hello macchina virtuale.
17. Directory condivisa di /sapmnt hello tra hello testare le macchine virtuali con NFS. server applicazioni Hello VM è NFS hello.
18. Installare l'istanza di database hello, incluse HANA, tramite SWPM nel server di database HANA hello macchina virtuale.
19. Installare il server di applicazione principali hello (PAS) nel server di applicazione hello VM.
20. Avviare SAP MC. Connettersi tramite l'interfaccia utente grafica di SAP o HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Preparare le macchine virtuali di Azure per l'installazione manuale di SAP HANA
In questa sezione vengono trattati hello seguenti argomenti:

* Aggiornamenti del sistema operativo
* Configurazione dei dischi
* Parametri del kernel
* File system
* file hosts di Hello/e così via
* file Hello e così via/fstab

### <a name="os-updates"></a>Aggiornamenti del sistema operativo
Prima di installare software aggiuntivo, verificare se sono disponibili aggiornamenti e correzioni del sistema operativo Linux. Installando una patch, potrebbe essere in grado di tooavoid desk di supporto toohello una chiamata.

Assicurarsi di usare:
* SUSE Linux Enterprise Server per applicazioni SAP.
* Red Hat Enterprise Linux per applicazioni SAP o Red Hat Enterprise Linux per SAP HANA. 

Se hai già fatto, registrare la distribuzione del sistema operativo hello con la sottoscrizione di Linux da fornitore Linux hello. Si noti che in SUSE sono disponibili immagini del sistema operativo per le applicazioni SAP che includono già i servizi e vengono registrate automaticamente.

Di seguito è riportato un esempio di verifica di patch disponibili per SUSE Linux utilizzando hello **zypper** comando:

 `sudo zypper list-patches`

A seconda della natura hello del problema, patch sono classificate in base a categoria e gravità. I valori usati comunemente per la categoria sono: **sicurezza**, **consigliato**, **facoltativo**, **funzionalità**, **documento** o **yast**.
I valori usati comunemente per la gravità sono: **critica**, **importante**, **moderata**, **bassa** o **non specificata**.

Hello **zypper** comando Cerca solo per gli aggiornamenti di hello necessario i pacchetti installati. È possibile ad esempio usare il comando seguente:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

È possibile aggiungere il parametro hello `--dry-run` tootest hello aggiornamento senza aggiornare effettivamente sistema hello.


### <a name="disk-setup"></a>Configurazione dei dischi
sistema di file Hello radice in una VM Linux di Azure prevede un limite di dimensioni. È pertanto necessario tooattach disco aggiuntivo spazio tooan macchina virtuale di Azure per l'esecuzione di SAP. Per il server applicazioni SAP macchine virtuali di Azure, utilizzare hello dei dischi di archiviazione standard Azure potrebbe essere sufficienti. Tuttavia, per le macchine virtuali SAP HANA DBMS Azure usare hello dei dischi di archiviazione Premium di Azure per le implementazioni di produzione e non di produzione è obbligatorio.

In base a hello [i requisiti di archiviazione di SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), viene suggerito hello seguente configurazione di archiviazione Premium di Azure: 

| SKU di VM | RAM |  /hana/data and /hana/log <br /> con striping con LVM o MDADM | /hana/shared | volume /root | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 GB | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

Nella configurazione del disco consigliate hello, volume di dati HANA hello e di log vengono posizionate in hello stesso insieme di dischi di archiviazione di Azure premium con striping con LVM o MDADM. Non è necessario toodefine qualsiasi ridondanza RAID di livello perché archiviazione Premium di Azure mantiene tre immagini dei dischi hello per garantire la ridondanza. Verificare di aver configurato spazio di archiviazione sufficiente, toomake consultare hello [i requisiti di archiviazione di SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) e [SAP HANA Server Guida all'installazione e aggiornamento](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Considerare anche i dischi di archiviazione premium di Azure diversi volumi di velocità effettiva di disco rigido virtuale (VHD) diverso di hello di hello come documentato [archiviazione Premium a prestazioni elevate e gestiti i dischi per le macchine virtuali](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

È possibile aggiungere che ulteriore spazio di archiviazione premium dischi di macchine virtuali DBMS di toohello HANA per l'archiviazione dei backup del log delle transazioni o di database.

Per ulteriori informazioni su hello due strumenti principali utilizzati tooconfigure lo striping, vedere hello seguenti articoli:

* [Configurare RAID software in Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configurare LVM in una macchina virtuale Linux in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Per ulteriori informazioni sul collegamento di dischi di macchine virtuali tooAzure che eseguono Linux come sistema operativo guest, vedere [aggiungere una VM Linux di tooa disco](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Archiviazione Premium di Azure consente disco toodefine modalità di memorizzazione nella cache. Per i set di striping hello tenendo /hana/data e /hana/log, la cache del disco deve essere disabilitata. Per hello (dischi), altri volumi hello la memorizzazione nella cache in modalità deve essere impostata troppo**ReadOnly**.

Per altre informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../../storage/common/storage-premium-storage.md).

modelli JSON di esempio toofind per la creazione di macchine virtuali, andare troppo[modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).
modello di macchina virtuale-simple-sles Hello è un modello di base. Include una sezione di archiviazione, con un disco dati di 100 GB aggiuntivo. Questo modello può essere usato come base. È possibile adattare configurazione specifica di hello modello tooyour.

>[!Note]
>Si tratta di importanti tooattach hello archiviazione di Azure disco utilizzando un UUID, come documentato [esegue SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Nell'ambiente di test hello, due dischi di archiviazione di Azure standard sono stati server di applicazioni SAP toohello collegato macchina virtuale, come illustrato nella seguente schermata hello. Un disco è archiviato tutto il software SAP hello (incluso SAP HANA 7.5 NetWeaver e SAP GUI) per l'installazione. si è verificata secondo disco Hello che saranno disponibile per i requisiti aggiuntivi (ad esempio, dati di backup e di test) sufficiente spazio libero e per hello /sapmnt directory (ovvero, i profili SAP) toobe condivisi tra tutte le macchine virtuali che appartengono toohello landscape SAP stesso.

![Finestra dei dischi del server applicazioni SAP HANA con due dischi dati e le relative dimensioni](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>Parametri del kernel
SAP HANA richiede le impostazioni specifiche Linux kernel, che non fanno parte di immagini della raccolta di Azure standard hello e devono essere impostate manualmente. A seconda che si utilizzi SUSE o Red Hat, è possibile che i parametri di hello potrebbero essere diversi. Note su SAP Hello elencati in precedenza forniscono informazioni su questi parametri. Nelle schermate di hello illustrate, SUSE Linux 12 SP1 è stato usato. 

SLES per la fase GA 12 di applicazioni SAP e SLES per SAP applicazioni 12 SP1 dispongono di un nuovo strumento **adm ottimizzati**, che sostituisce hello precedente **sapconf** strumento. Per **tuned-adm** è disponibile un profilo di SAP HANA specifico. sistema di hello tootune per SAP HANA, immettere il seguente di hello come utente radice:

   `tuned-adm profile sap-hana`

Per ulteriori informazioni su **adm ottimizzati**, vedere hello [documentazione SUSE sulle adm ottimizzati](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

Nella seguente schermata di hello, è possibile visualizzare come **adm ottimizzati** hello modificata `transparent_hugepage` e `numa_balancing` necessario che i valori, in base toohello le impostazioni di SAP HANA.

![strumento adm ottimizzati Hello cambia i valori in base a toorequired impostazioni SAP HANA](./media/hana-get-started/image005.jpg)

Utilizzare permanente, impostazioni del kernel SAP HANA hello toomake **grub2** SLES 12. Per ulteriori informazioni su **grub2**, visitare toohello [struttura dei File di configurazione](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sezione della documentazione SUSE hello.

Hello schermata riportata di seguito viene illustrato come impostazioni kernel hello sono state modificate nel file di configurazione hello e quindi compilate utilizzando **grub2 mkconfig**:

![Impostazioni di kernel modificato nel file di configurazione hello e compilati con grub2 mkconfig](./media/hana-get-started/image006.jpg)

Un'altra opzione consiste impostazioni hello toochange utilizzando YaST e hello **caricatore di avvio** > **parametri Kernel** impostazioni:

![scheda Impostazioni di parametri del Kernel Hello nel caricatore di avvio YaST](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>File system
Hello schermata seguente mostra due sistemi di file che sono stati creati nel server app hello SAP VM nella parte superiore di due dischi di archiviazione Azure standard hello. Entrambi i sistemi di file sono di tipo XFS e sono montato troppo/sapdata e /sapsoftware.

Si è toostructure non obbligatorio del file System in questo modo. Sono disponibili altre opzioni per la struttura di spazio su disco hello. aspetto più importante Hello è tooprevent hello radice file system in esaurimento dello spazio disponibile.

![Due sistemi di file creati nel server di applicazioni SAP hello VM](./media/hana-get-started/image008.jpg)

Per quanto riguarda hello SAP HANA DB VM, durante l'installazione di un database, quando si utilizza SAPinst (SWPM) e hello **tipico** opzione di installazione, tutto ciò che viene installata in /hana e /usr/sap. il percorso predefinito Hello del backup del log di SAP HANA hello è in /usr/sap. Nuovamente, perché è importante tooprevent hello radice file system in esaurimento dello spazio di archiviazione, assicurarsi che vi sia spazio libero sufficiente in /hana e /usr/sap prima di installare utilizzando SWPM SAP HANA.

Per una descrizione del layout di file system standard hello di SAP HANA, vedere hello [SAP HANA Server Guida all'installazione e aggiornamento](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Sistemi aggiuntive del file creati nel server di applicazioni SAP hello VM](./media/hana-get-started/image009.jpg)

Quando si installa SAP NetWeaver in un SLES/SLES standard per l'immagine della raccolta di Azure di 12 applicazioni SAP, viene visualizzato un messaggio che indica che non vi è alcun spazio di swapping, come illustrato nella seguente schermata hello. toodismiss questo messaggio, è possibile aggiungere manualmente un file di scambio con **gg**, **mkswap**, e **swapon**. toolearn, cercare "Aggiunta di un file di swapping manualmente" nella hello [Using hello YaST Partitioner](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) sezione della documentazione SUSE hello.

Un'altra opzione è lo spazio di swapping tooconfigure utilizzando hello agente VM Linux. Per ulteriori informazioni, vedere hello [Guida dell'utente dell'agente Linux Azure](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Messaggio popup che segnala la presenza di spazio di swapping insufficiente](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>file hosts di Hello/e così via
Prima di iniziare tooinstall SAP, assicurarsi di includere i nomi host hello e gli indirizzi IP di macchine virtuali SAP hello in file /etc/hosts hello. Distribuire tutte le macchine virtuali SAP hello all'interno di una rete virtuale di Azure e quindi utilizzare hello gli indirizzi IP interni, come illustrato di seguito:

![I nomi host e gli indirizzi IP delle macchine virtuali SAP hello elencati nel file /etc/hosts hello](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>file Hello e così via/fstab

È utile tooadd hello **nofail** toohello fstab file dei parametri. In questo modo, se si verificano problemi con i dischi hello hello VM non di blocco nel processo di avvio hello. Tuttavia, tenere presente che potrebbe non essere disponibile ulteriore spazio su disco e i processi potrebbero esaurirsi sistema file radice di hello. Se /hana non è presente, SAP HANA non viene avviato.

![Aggiungere hello nofail parametro toohello fstab file](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Desktop GNOME con interfaccia grafica in SLES 12/SLES for SAP Applications 12
In questa sezione vengono trattati hello seguenti argomenti:

* Installazione desktop GNOME hello e xrdp in SLES 12/SLES per 12 applicazioni SAP
* Esecuzione della console SAP MC basata su Java con Firefox in SLES 12/SLES for SAP Applications 12

È anche possibile usare strumenti alternativi, ad esempio Xterminal o VNC (non descritti in questa guida).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Installazione desktop GNOME hello e xrdp in SLES 12/SLES per 12 applicazioni SAP
Se si dispone di un background di Windows, è possibile usare una grafica desktop direttamente all'interno di hello macchine virtuali Linux SAP toorun Firefox, SAPinst, SAP GUI, MC SAP o Studio HANA facilmente e connettersi toohello VM tramite hello Remote Desktop Protocol (RDP) da un computer Windows. Interfacce utente grafiche dipende da informazioni sull'aggiunta di criteri aziendali di sistemi basati su Linux tooproduction e non di produzione, è opportuno tooinstall GNOME sul server. tooinstall hello GNOME desktop un SLES 12/SLES Azure per la macchina virtuale di 12 applicazioni SAP:

1. Installare desktop GNOME hello immettendo hello comando (ad esempio, in una finestra PuTTY) seguente:

   `zypper in -t pattern gnome-basic`

2. Installare xrdp tooallow toohello una connessione macchina virtuale tramite RDP:

   `zypper in xrdp`

3. Modificare /etc/sysconfig/windowmanager e impostare hello predefinito finestra Gestione tooGNOME:

   `DEFAULT_WM="gnome"`

4. Eseguire **chkconfig** toomake certi che xrdp venga avviato automaticamente dopo il riavvio:

   `chkconfig -level 3 xrdp on`

5. Se si dispone di un problema con hello connessione RDP, provare a toorestart (dalla finestra PuTTY, ad esempio):

   `/etc/xrdp/xrdp.sh restart`

6. Se un'operazione di riavvio xrdp indicato nella precedente hello passaggio non funziona, verificare la presenza di un file .pid:

   `check /var/run` 

   Cercare `xrdp.pid`. Se si ritiene, rimuoverlo e riprovare toorestart.

### <a name="starting-sap-mc"></a>Avvio di SAP MC
Dopo aver installato desktop GNOME hello, avvio hello grafica MC basati su Java di SAP da Firefox durante l'esecuzione in un Azure SLES 12/SLES per la macchina virtuale di 12 applicazioni SAP potrebbe essere visualizzato un errore a causa di hello mancante Java browser plug-in.

hello toostart di URL Hello MC SAP è `<server>:5<instance_number>13`.

Per ulteriori informazioni, vedere [hello iniziale basato sul Web Console di gestione di SAP](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Hello schermata seguente Mostra messaggio di errore hello viene visualizzata quando hello Java browser plug-in è manca:

![Messaggio di errore che indica la mancanza del plug-in Java nel browser](./media/hana-get-started/image013.jpg)

Problema di hello toosolve unidirezionale è hello tooinstall plug-in mancante utilizzando YaST, come illustrato nella seguente schermata hello:

![Utilizzando tooinstall YaST plug-in mancante](./media/hana-get-started/image014.jpg)

Quando sarà necessario immettere l'URL della Console Gestione SAP hello, viene visualizzato un messaggio che chiede di tooactivate hello plug-in:

![Finestra di dialogo con la richiesta di attivazione del plug-in](./media/hana-get-started/image015.jpg)

È anche possibile che venga visualizzato un altro messaggio di errore relativo a un file mancante, javafx.properties. Si tratta requisito toohello correlati di Oracle Java 1.8 per SAP GUI 7.4. (Vedere la [Nota SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424)). Versione di IBM Java hello né pacchetto openjdk hello recapitati con SLES/SLES per 12 applicazioni SAP include file di javafx.properties necessari hello. soluzione hello è toodownload e installare Java SE 8 da Oracle.

Per informazioni su un problema simile di openjdk openSUSE, vedere il thread di discussione hello [SAPGui 7.4 Java per openSUSE 42.1 Leap](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Installazione manuale di SAP HANA: SWPM
serie di Hello di schermate in questa sezione illustra i passaggi principali hello per l'installazione di SAP NetWeaver 7.5 e SAP HANA SP12 quando si utilizza SWPM (SAPinst). Come parte di un'installazione NetWeaver 7.5, SWPM inoltre possibile installare database HANA hello come una singola istanza.

Nell'ambiente di test di esempio è stato installato un solo server applicazioni ABAP (Advanced Business Application Programming). Come illustrato nella seguente schermata hello, abbiamo utilizzato hello **System distribuito** opzione hello tooinstall ASCS e istanze del server principale dell'applicazione in una macchina virtuale di Azure e SAP HANA come sistema di database hello in un'altra macchina virtuale di Azure.

![ASCS e istanze del server primario applicazione installate utilizzando l'opzione Distributed System hello](./media/hana-get-started/image012.jpg)

Dopo che sia installato nel server di app hello macchina virtuale e istanza ASCS hello impostato troppo "verde" hello SAP Management Console (illustrata nella seguente schermata hello), hello /sapmnt directory (directory di profilo SAP hello inclusi) deve essere condivisa con macchina virtuale del server SAP HANA DB hello. passaggio di installazione Hello DB deve accedere a informazioni toothis. accesso tooprovide modo migliore di Hello è toouse NFS, che possono essere configurate tramite YaST.

![Istanza di SAP Console di gestione con hello ASCS installato nel server di app hello macchina virtuale e imposta troppo "verde"](./media/hana-get-started/image016.jpg)

Nel server di app hello VM, hello/sapmnt directory devono essere condivise tramite NFS utilizzando hello **rw** e **no_root_squash** opzioni. Hello valori predefiniti sono **ro** e **root_squash**, che potrebbe causare tooproblems quando si installa l'istanza del database hello.

![Condivisione directory /sapmnt hello tramite NFS utilizzando le opzioni di hello rw e no_root_squash](./media/hana-get-started/image017b.jpg)

Come illustrato nella schermata successiva hello, hello /sapmnt condivisione dalla macchina virtuale del server app hello necessario configurarle nel server SAP HANA DB hello VM utilizzando **Client NFS** (e YaST).

![condivisione /sapmnt Hello configurato utilizzando il Client NFS](./media/hana-get-started/image018b.jpg)

installazione di un 7.5 NetWeaver distribuito tooperform (**istanza Database**), come hello illustrato nella seguente schermata, accedere alla macchina virtuale del server SAP HANA DB toohello e avviare SWPM.

![L'installazione di un'istanza del database nella macchina virtuale del server SAP HANA DB toohello di firma e avviando SWPM](./media/hana-get-started/image019.jpg)

Dopo aver selezionato **tipico** installazione e supporto di installazione toohello percorso hello, immettere un DB SID, nome host hello, del numero di istanza hello e password dell'amministratore di sistema hello DB.

![pagina Hello sign-in Amministrazione sistema di database SAP HANA](./media/hana-get-started/image035b.jpg)

Immettere la password di hello per schema DBACOCKPIT hello:

![casella di immissione della password Hello per schema DBACOCKPIT hello](./media/hana-get-started/image036b.jpg)

Immettere una domanda per la password dello schema di hello SAPABAP1:

![Immettere una domanda per la password dello schema di hello SAPABAP1](./media/hana-get-started/image037b.jpg)

Al termine di ogni attività, un segno di spunta verde viene visualizzato fase tooeach successiva del processo di installazione DB hello. messaggio Hello "esecuzione di... Database Instance has completed" (Esecuzione dell'istanza di database ... completata).

![Finestra in cui viene visualizzata l'attività completata con il messaggio di conferma](./media/hana-get-started/image023.jpg)

Al termine dell'installazione, hello SAP Console di gestione deve inoltre hello DB istanza visualizzata come "green" e visualizzare l'elenco completo di hello dei processi di SAP HANA (hdbindexserver hdbcompileserver e così via).

![Finestra della console di gestione SAP con l'elenco dei processi di SAP HANA](./media/hana-get-started/image024.jpg)

Hello schermata riportata di seguito vengono illustrate hello parti della struttura di file hello nella directory /hana/shared hello SWPM creato durante l'installazione HANA hello. Poiché non esiste alcuna opzione toospecify un percorso diverso, è importante toomount ulteriore spazio su disco nella directory /hana hello prima dell'installazione di SAP HANA hello utilizzando SWPM. Sistema di file radice hello impedisce di insufficienza di spazio libero.

![struttura di Hello /hana/shared directory file creato durante l'installazione HANA](./media/hana-get-started/image025.jpg)

Questa schermata Mostra struttura dei file della directory /usr/sap hello hello:

![struttura del file Hello /usr/sap directory](./media/hana-get-started/image026.jpg)

al termine dell'installazione di distributed hello ABAP Hello è istanza del server principale dell'applicazione hello tooinstall:

![Istanza server principale dell'applicazione ABAP installazione che mostra come passaggio finale hello](./media/hana-get-started/image027b.jpg)

Dopo che l'istanza del server principale dell'applicazione hello e interfaccia utente grafica SAP sono installati, usare hello **DBA Cockpit** tooconfirm transazione che l'installazione di SAP HANA hello viene completata correttamente:

![Finestra DBA Cockpit (Pannello di controllo DBA) di conferma dell'installazione](./media/hana-get-started/image028b.jpg)

Come passaggio finale, si installa toofirst Studio HANA nella macchina virtuale del server applicazioni SAP hello e quindi connettere l'istanza di SAP HANA toohello che è in esecuzione nel server di database hello VM:

![L'installazione di SAP HANA Studio nel server di applicazioni SAP hello VM](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Installazione manuale di SAP HANA: HDBLCM
In aggiunta tooinstalling SAP HANA come parte di un'installazione distribuita utilizzando SWPM, è possibile installare in primo luogo, hello HANA autonomo tramite HDBLCM. Sarà quindi possibile installare ad esempio SAP NetWeaver 7.5. schermate di Hello in questa sezione illustrano il funzionamento di questo processo.

Per ulteriori informazioni su strumento HANA HDBLCM hello, vedere:

* [Scegliendo hello corretti HDBLCM di SAP HANA per l'attività](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools (Strumenti di SAP HANA Lifecycle Management)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide (Guida all'installazione e all'aggiornamento del server SAP HANA)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

impostazione di ID per hello di gruppo tooavoid problemi predefinito `\<HANA SID\>adm user` (creato dallo strumento HDBLCM hello), definire un nuovo gruppo denominato `sapsys` utilizzando l'ID del gruppo `1001` prima di installare SAP HANA tramite HDBLCM:

![Nuovo gruppo "sapsys" definito con ID gruppo 1001](./media/hana-get-started/image030.jpg)

Quando si avvia hello HDBLCM prima volta, viene visualizzato un menu di avvio semplice. Seleziona elemento 1, **installare nuovo sistema**, come illustrato nella seguente schermata hello:

![Opzione "Installa nuovo sistema" nella finestra di avvio HDBLCM hello](./media/hana-get-started/image031.jpg)

Hello schermata riportata di seguito consente di visualizzare tutte le opzioni chiave hello selezionato in precedenza.

> [!IMPORTANT]
> Directory denominate per log HANA e volumi di dati, nonché il percorso di installazione di hello (hana/condivisi in questo esempio) e /usr/sap, non deve essere parte del file system di hello radice. Queste directory appartengono toohello i dischi di dati di Azure che sono stato collegato toohello VM (descritto nella sezione hello "disco setup"). Questo approccio consente di impedire l'insufficienza di spazio di sistema di file radice hello. Nella seguente schermata di hello, è possibile visualizzare tale amministratore di sistema HANA hello di ID utente `1005` e fa parte di hello `sapsys` gruppo (ID `1001`) che è stato definito prima dell'installazione di hello.

![Elenco di tutti i componenti chiave di SAP HANA selezionati in precedenza](./media/hana-get-started/image032.jpg)

È possibile controllare hello `\<HANA SID\>adm user` (`azdadm` nella seguente schermata hello) nella directory hello e così via/passwd dettagli:

![HANA \<HANA SID\>dettagli utente adm elencato in hello e così via/passwd directory](./media/hana-get-started/image033.jpg)

Dopo l'installazione di SAP HANA utilizzando HDBLCM, è possibile visualizzare la struttura di file hello in SAP HANA Studio, come illustrato nella seguente schermata hello. schema di SAPABAP1 Hello, che include tutte le tabelle di SAP NetWeaver hello, non è ancora disponibile.

![Struttura di file di SAP HANA in SAP HANA Studio](./media/hana-get-started/image034.jpg)

Dopo l'installazione di SAP HANA, è possibile installare SAP NetWeaver. Come hello illustrato nella schermata seguente, l'installazione di hello è stata eseguita come un'installazione distribuita utilizzando SWPM (come descritto nella sezione precedente hello). Quando si installa l'istanza del database hello utilizzando SWPM, si immette hello stessi dati utilizzando HDBLCM (ad esempio, nome host, HANA SID e il numero di istanza). SWPM quindi utilizza installazione HANA esistente hello e aggiunge più schemi.

![Installazione distribuita eseguita tramite SWPM](./media/hana-get-started/image035b.jpg)

Hello schermata seguente mostra fase dell'installazione di hello SWPM dove inserire i dati sullo schema DBACOCKPIT hello:

![passaggio di installazione SWPM Hello in cui viene immesso i dati dello schema DBACOCKPIT](./media/hana-get-started/image036b.jpg)

Immettere i dati sullo schema SAPABAP1 hello:

![Immissione di dati sullo schema SAPABAP1 hello](./media/hana-get-started/image037b.jpg)

Al termine dell'installazione dell'istanza del database SWPM hello, è possibile visualizzare schema SAPABAP1 hello in SAP HANA Studio:

![schema di Hello SAPABAP1 in SAP HANA Studio](./media/hana-get-started/image038b.jpg)

Infine, completamento server di applicazioni SAP hello e le installazioni di SAP GUI, è possibile verificare istanza HANA DB hello utilizzando hello **DBA Cockpit** transazione:

![istanza di Hello HANA DB verificato con hello transazione Pannello di controllo amministratore di database](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Download del software SAP
È possibile scaricare software dal hello SAP Service Marketplace, come illustrato nella seguente schermate hello.

Download di NetWeaver 7.5 per Linux/HANA:

 ![Finestra di installazione e aggiornamento del servizio SAP per il download di NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Download di HANA SP12 Platform Edition:

 ![Finestra di installazione e aggiornamento del servizio SAP per il download di HANA SP12 Platform Edition](./media/hana-get-started/image002.jpg)

