---
title: Guida di aaaBackup per SAP HANA in macchine virtuali di Azure | Documenti Microsoft
description: La guida del backup per SAP HANA offre due opzioni principali per il backup di SAP HANA su macchine virtuali di Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: e651091bb5da2698ec8bf80cad405bfce5b192cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-guide-for-sap-hana-on-azure-virtual-machines"></a>Guida del backup di SAP HANA in macchine virtuali di Azure

## <a name="getting-started"></a>Introduzione

Guida al backup Hello per SAP HANA in esecuzione in macchine virtuali di Azure solo descrive gli argomenti specifici di Azure. Per generale SAP HANA backup elementi correlati, vedere la documentazione di SAP HANA hello (vedere _documentazione di backup di SAP HANA_ più avanti in questo articolo).

Hello di questo articolo è attiva due possibilità backup principali per SAP HANA in macchine virtuali di Azure:

- Sistema di file di backup toohello HANA in una macchina virtuale Linux di Azure (vedere [SAP HANA Azure Backup a livello di file](sap-hana-backup-file-level.md))
- Backup HANA basato su snapshot di archiviazione con funzionalità snapshot blob di archiviazione di Azure hello manualmente o servizio di Backup di Azure (vedere [SAP HANA backup basato su snapshot di archiviazione](sap-hana-backup-storage-snapshots.md))

SAP HANA offre un backup API, che consente di strumenti di backup di terze parti toointegrate direttamente con SAP HANA. (Che non è nell'ambito di hello di questa Guida). Al momento non è prevista alcuna integrazione diretta di SAP HANA con il servizio di Backup di Azure basato su tale API.

SAP HANA è ufficialmente supportato sul tipo di macchina virtuale di Azure GS5 come singola istanza con i carichi di lavoro tooOLAP un'ulteriore restrizione (vedere [trovare piattaforme IaaS Certificate](https://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html) nel sito Web SAP hello). Questo articolo verrà aggiornato non appena saranno disponibili nuove offerte per SAP HANA in Azure.

Azure offre anche una soluzione ibrida SAP HANA, in cui SAP HANA viene eseguito in modo non virtualizzato su server fisici. La presente guida del backup di SAP HANA in Azure descrive un ambiente di Azure genuino in cui SAP HANA viene eseguito in una VM di Azure, non su &quot;istanze di grandi dimensioni&quot;. Vedere [SAP HANA (large instances) overview and architecture on Azure](hana-overview-architecture.md) (Panoramica e architettura di SAP HANA (istanze di grandi dimensioni) in Azure) per altre informazioni su questa soluzione di backup per &quot;istanze di grandi dimensioni&quot; basate su snapshot di archiviazione.

Informazioni generali sui prodotti SAP supportati in Azure sono reperibili in [SAP Note 1928533](https://launchpad.support.sap.com/#/notes/1928533) (Nota SAP 1928533).

Hello tre figure seguenti offrono una panoramica di hello opzioni di backup di SAP HANA utilizzando funzionalità native di Azure attualmente e anche mostrano tre potenziali scenari di backup futuri. articoli correlati Hello [SAP HANA Azure Backup a livello di file](sap-hana-backup-file-level.md) e [SAP HANA backup basato su snapshot di archiviazione](sap-hana-backup-storage-snapshots.md) vengono descritte queste opzioni in modo più dettagliato, tra cui dimensioni e considerazioni sulle prestazioni per SAP Backup HANA terabyte di più dimensioni.

![La figura seguente illustra due possibilità per il salvataggio stato macchina virtuale corrente hello](media/sap-hana-backup-guide/image001.png)

Questa figura mostra il possibilità hello di salvataggio hello corrente stato della macchina virtuale, tramite il servizio di Backup di Azure o manuale dello snapshot di dischi di macchina virtuale. Con questo approccio, un &#39; non ha i backup di SAP HANA toomanage. challenge Hello dello scenario di snapshot disco hello è coerenza del file system e uno stato coerente con l'applicazione su disco. argomento di coerenza Hello è descritta nella sezione hello _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_ più avanti in questo articolo. Funzionalità e limitazioni del servizio di Backup di Azure correlate a backup HANA tooSAP viene anche illustrato più avanti in questo articolo.

![La figura seguente illustra le opzioni per l'esecuzione di un SAP HANA file di backup all'interno di hello VM](media/sap-hana-backup-guide/image002.png)

Questa figura mostra le opzioni per eseguire un backup del file SAP HANA all'interno di hello macchina virtuale e quindi archiviati i file di backup HANA da qualche parte else usando strumenti diversi. L'esecuzione di un backup HANA richiede più tempo rispetto a una soluzione di backup basato su snapshot, ma presenta vantaggi riguardanti l'integrità e la coerenza. Altri dettagli sono disponibili più avanti in questo articolo.

![La figura seguente mostra un potenziale scenario futuro di backup di SAP HANA](media/sap-hana-backup-guide/image003.png)

La figura seguente mostra un potenziale scenario futuro di backup di SAP HANA. Se SAP HANA ha consentito l'esecuzione di backup da una replica secondaria, vengono aggiunte altre opzioni per le strategie di backup. Attualmente non è possibile in base tooa post in hello SAP HANA Wiki:

_&quot;È possibile tootake backup sul lato secondario hello?_

_No, attualmente è possibile solo richiedere dati e i backup su lato primario hello del log. Se il backup del log automatico è abilitato, dopo l'acquisizione della proprietà toohello lato secondario, i backup del log hello verranno automaticamente essere scritti.&quot;_

## <a name="sap-resources-for-hana-backup"></a>Risorse SAP per il backup di HANA

### <a name="sap-hana-backup-documentation"></a>Documentazione sul backup di SAP HANA

- [Introduzione tooSAP amministrazione HANA](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/2.0.00/en-US)
- [Planning Your Backup and Recovery Strategy](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) (Pianificazione del backup e strategia di ripristino)
- [Schedule HANA Backup using ABAP DBACOCKPIT](http://www.hanatutorials.com/p/schedule-hana-backup-using-abap.html) (Pianificare il backup di HANA tramite ABAP DBACOCKPIT)
- [Schedule Data Backups (SAP HANA Cockpit)](http://help.sap.com/saphelp_hanaplatform/helpdata/en/6d/385fa14ef64a6bab2c97a3d3e40292/frameset.htm) (Pianificare il backup dei dati (Pannello di controllo di SAP HANA)
- Domande frequenti sul backup di SAP HANA in [Nota SAP 1642148](https://launchpad.support.sap.com/#/notes/1642148)
- Domande frequenti sugli snapshot di archiviazione e dei database di SAP HANA in [Nota SAP 2039883](https://launchpad.support.sap.com/#/notes/2039883)
- File system di rete non appropriati per il backup e il ripristino in [Nota SAP 1820529](https://launchpad.support.sap.com/#/notes/1820529)

### <a name="why-sap-hana-backup"></a>Perché eseguire il backup di SAP HANA?

Archiviazione di Azure offre disponibilità e affidabilità predefinito hello (vedere [tooMicrosoft introduzione di archiviazione di Azure](../../../storage/common/storage-introduction.md) per ulteriori informazioni sull'archiviazione di Azure).

Hello minimo per &quot;backup&quot; è toorely su hello SLA di Azure, mantenendo hello file di dati e log SAP HANA su macchina virtuale del server SAP HANA toohello collegati dischi rigidi virtuali di Azure. Questo approccio vengono illustrati gli errori di macchina virtuale, ma non potenziali dati SAP HANA toohello di danni e i file di log o errori logici, ad esempio l'eliminazione di dati o file accidentalmente. I backup sono necessari anche per motivi legali o di conformità. In breve, è sempre necessario eseguire backup di SAP HANA.

### <a name="how-tooverify-correctness-of-sap-hana-backup"></a>Come tooverify correttezza del backup di SAP HANA
Quando si usano gli snapshot di archiviazione, è consigliabile eseguire un ripristino di prova su un sistema differente. Questo approccio offre un modo tooensure che è un backup corretti e interni processi di lavoro di backup e ripristino come previsto. Mentre questo è un importante ostacolo in locale, è molto più semplice tooaccomplish nel cloud hello fornendo temporaneamente le risorse necessarie per questo scopo.

Tenere presente che eseguire un semplice ripristino e verificare che HANA sia attivo e in esecuzione non è sufficiente. Idealmente, uno deve essere eseguito un toobe controllo coerenza nella tabella, è necessario che il database ripristinato hello correttamente. SAP HANA offre diversi tipi di verifiche della coerenza, descritti nella [Nota SAP 1977584](https://launchpad.support.sap.com/#/notes/1977584).

Informazioni sulla verifica della coerenza hello tabella sono disponibili sul sito Web SAP hello al [tabella e le verifiche di coerenza catalogo](http://help.sap.com/saphelp_hanaplatform/helpdata/en/25/84ec2e324d44529edc8221956359ea/content.htm#loio9357bf52c7324bee9567dca417ad9f8b).

Per il backup di file standard, non è necessario eseguire un ripristino di prova. Sono disponibili due strumenti di SAP HANA che consentono di toocheck quali backup può essere utilizzato per il ripristino: hdbbackupdiag e hdbbackupcheck. Vedere [Manually Checking Whether a Recovery is Possible](https://help.sap.com/saphelp_hanaplatform/helpdata/en/77/522ef1e3cb4d799bab33e0aeb9c93b/content.htm) (Verifica manuale della fattibilità di un ripristino) per altre informazioni su questi strumenti.

### <a name="pros-and-cons-of-hana-backup-versus-storage-snapshot"></a>Vantaggi e svantaggi dei backup di HANA rispetto agli snapshot di archiviazione

SAP &#39; backup t offrono preferenza tooeither HANA e snapshot di archiviazione. Elenca i vantaggi e svantaggi, in modo possibile determinare quali toouse a seconda della situazione hello e tecnologia di archiviazione disponibile (vedere [pianificazione di strategia di Backup e ripristino](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm)).

In Azure, tenere in considerazione il fatto hello che hello non funzionalità snapshot di blob di Azure &#39; t garantire coerenza del file system (vedere [utilizzando gli snapshot di blob con PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/)). la sezione successiva, Hello _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_, vengono fornite alcune considerazioni relative a questa funzionalità.

Dispone inoltre di uno toounderstand hello costi di fatturazione quando si utilizzano spesso degli snapshot blob come descritto in questo articolo: [informazioni sulle modalità costi dovuto agli snapshot](/rest/api/storageservices/understanding-how-snapshots-accrue-charges), non è &#39; t altrettanto ovvie come l'uso di Azure dischi virtuali.

### <a name="sap-hana-data-consistency-when-taking-storage-snapshots"></a>Coerenza dei dati SAP HANA durante l'esecuzione degli snapshot di archiviazione

La coerenza del file system e dell'applicazione è un problema complesso quando si eseguono snapshot di archiviazione. problemi di tooavoid modo più semplici Hello è tooshut verso il basso SAP HANA, o forse macchina virtuale intero hello. L'arresto potrebbe essere eseguibile tramite demo, prototipo o anche tramite un sistema di sviluppo, ma non è un'opzione per un sistema di produzione.

In Azure, uno ha tookeep presente che hello non funzionalità snapshot di blob di Azure &#39; t garantire coerenza del file system. Funziona correttamente, tuttavia utilizzando hello SAP HANA snapshot funzionalità, come un singolo disco virtuale è coinvolto. Ma anche con un singolo disco, gli elementi aggiuntivi toobe selezionata. La [Nota SAP 2039883](https://launchpad.support.sap.com/#/notes/2039883) contiene importanti informazioni sui backup di SAP HANA tramite gli snapshot di archiviazione. Ad esempio, sono indicate che, con file system di hello XFS, è necessario toorun **xfs\_bloccare** prima di avviare una risorsa di archiviazione snapshot coerenza tooguarantee (vedere [xfs\_freeze(8) - uomo di Linux pagina](https://linux.die.net/man/8/xfs_freeze) per informazioni dettagliate su **xfs\_bloccare**).

argomento Hello di verifica di coerenza diventa anche più complessa in un caso in cui un singolo file system si estende su più dischi o volumi. Ad esempio, tramite mdadm o LVM e lo striping. Nota SAP indicato in precedenza stati Hello:

_&quot;Ma tenere presente che il sistema di archiviazione hello è la coerenza di tooguarantee i/o durante la creazione di uno snapshot di archiviazione per ogni volume di dati SAP HANA, ad esempio agli snapshot di un volume di dati specifici del servizio di SAP HANA devono essere un'operazione atomica.&quot;_

Supponendo che esista un file system XFS spanning quattro dischi virtuali Azure, hello passaggi seguenti viene fornito uno snapshot coerente che rappresenta l'area dei dati HANA hello:

- Preparazione dello snapshot HANA
- Bloccare il sistema di file hello (ad esempio, utilizzare **xfs\_bloccare**)
- Creare tutti gli snapshot BLOB necessari in Azure.
- Sbloccare il sistema di file hello
- Conferma snapshot HANA hello

Si consiglia di toouse hello procedura in tutti i casi toobe relativamente hello-safe, indipendentemente da quale file system. In alternativa, se si tratta di un singolo disco o dello striping, usare mdadm o LVM nei diversi dischi.

Si tratta di importanti tooconfirm hello HANA snapshot. Scadenza toohello &quot;Copy-on-Write&quot; SAP HANA possono non richiedere ulteriore spazio su disco in questa modalità di preparazione dello snapshot. &#39; s toostart inoltre non è possibile nuovi backup fino a quando non viene confermato snapshot SAP HANA hello.

Servizio di Azure Backup utilizza tootake estensioni VM di Azure cure hello coerenza del file system. Queste estensioni della macchina virtuale non sono disponibili per l'uso autonomo. Uno dispone ancora di coerenza di SAP HANA toomanage. Vedere l'articolo correlato hello [SAP HANA Azure Backup a livello file](sap-hana-backup-file-level.md) per ulteriori informazioni.

### <a name="sap-hana-backup-scheduling-strategy"></a>Strategia di pianificazione del backup di SAP HANA

articolo di SAP HANA Hello [pianificazione di strategia di Backup e ripristino](https://help.sap.com/saphelp_hanaplatform/helpdata/en/ef/085cd5949c40b788bba8fd3c65743e/content.htm) stati a basic piano backup toodo:

- Snapshot di archiviazione (giornaliero)
- Backup completo dei dati tramite il formato di file o backint (una volta alla settimana)
- Backup automatici dei log

Facoltativamente, è possibile procedere completamente senza snapshot di archiviazione. Questi possono essere sostituiti da backup delta di HANA, ad esempio backup incrementali o differenziali. Vedere [Delta Backups](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm) (Backup delta).

Guida all'amministrazione HANA Hello fornisce un elenco di esempio. Si consiglia di che uno eseguire il recupero temporizzato di SAP HANA tooa hello seguente sequenza di backup utilizzando:

1. Backup completo dei dati
2. Backup differenziale
3. Backup incrementale 1
4. Backup incrementale 2
5. Backup dei log

Per una pianificazione esattamente come toowhen e la frequenza con cui deve verificarsi un tipo di backup specifico, non è possibile toogive generale, è troppo specifiche del cliente e dipende dal numero di modifiche di dati si verifica nel sistema hello. Una base dal lato SAP, che può essere visualizzato come indicazione generale, si consiglia di toomake un backup HANA completo una volta alla settimana.
Per quanto riguarda i backup del log, vedere la documentazione di SAP HANA hello [i backup del Log](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/bb7e33bb571014a03eeabba4e37541/content.htm).

SAP consiglia inoltre di eseguire alcune le attività di manutenzione di hello catalogo di backup tookeep dalla crescita smisurata (vedere [di manutenzione per il catalogo di Backup e archiviazione di Backup](http://help.sap.com/saphelp_hanaplatform/helpdata/en/ca/c903c28b0e4301b39814ef41dbf568/content.htm)).

### <a name="sap-hana-configuration-files"></a>File di configurazione di SAP HANA

Come indicato in domande frequenti hello in [1642148 nota SAP](https://launchpad.support.sap.com/#/notes/1642148), i file di configurazione di SAP HANA hello non fanno parte di un backup HANA standard. Non sono essenziali toorestore un sistema. configurazione HANA Hello è possibile modificare manualmente dopo il ripristino di hello. Nel caso in cui desiderato tooget hello stessa configurazione personalizzata durante il processo di ripristino di hello, è necessario tooback dei file di configurazione HANA hello separatamente.

Se i backup HANA standard sta tooa dedicato di sistema di file di backup HANA, uno è stato possibile anche copiare toohello i file di configurazione hello stesso backup del file System e quindi copiare tutti gli elementi come destinazione di archiviazione finale toohello insieme raffreddare nell'archiviazione blob.

### <a name="sap-hana-cockpit"></a>Pannello di controllo SAP HANA

Pannello di controllo di SAP HANA offre il possibilità hello di monitoraggio e la gestione di SAP HANA tramite un browser. Consente inoltre la gestione dei backup di SAP HANA e pertanto può essere utilizzato come alternativa tooSAP Studio HANA e ABAP DBACOCKPIT (vedere [SAP HANA Cockpit](https://help.sap.com/saphelp_hanaplatform/helpdata/en/73/c37822444344f3973e0e976b77958e/content.htm) per altre informazioni).

![Questa figura mostra hello schermata di amministrazione del Database SAP HANA Pannello di controllo](media/sap-hana-backup-guide/image004.png)

In questa figura mostra hello schermata di amministrazione del Database SAP HANA Pannello di controllo e riquadro backup hello hello a sinistra. Riquadro di backup hello vedere richiede autorizzazioni utente appropriate per l'account di accesso.

![I backup possono essere monitorati nel pannello di controllo di SAP HANA durante l'esecuzione.](media/sap-hana-backup-guide/image005.png)

I backup possono essere monitorati nel Pannello di controllo di SAP HANA mentre sono in corso e, al termine, tutti i dettagli backup hello sono disponibili.

![Esempio di uso di Firefox in una macchina virtuale 12 SLES di Azure con desktop Gnome](media/sap-hana-backup-guide/image006.png)

schermate di Hello precedenti sono state apportate da una macchina virtuale Windows Azure. Questo è un esempio di uso di Firefox in una macchina virtuale 12 SLES di Azure con desktop Gnome, Mostra le pianificazioni dei backup hello opzione toodefine SAP HANA in Pannello di controllo di SAP HANA. Come si può anche osservare, si consiglia di data/ora come prefisso per i file di backup hello. In SAP HANA Studio prefisso predefinito hello è &quot;completa\_dati\_BACKUP&quot; quando si esegue un backup completo del file. Si consiglia l'uso di un prefisso unico.

### <a name="sap-hana-backup-encryption"></a>Crittografia del backup di SAP HANA

SAP HANA offre la crittografia di dati e log. Se non vengono crittografati i dati di SAP HANA e di log, quindi backup hello inoltre non vengono crittografati. È attivo toohello cliente toouse munita di un backup di SAP HANA hello tooencrypt soluzione di terze parti. Vedere [dati e la crittografia del Volume di Log](https://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/01f36fbb5710148b668201a6e95cf2/content.htm) toofind ulteriori informazioni sulla crittografia di SAP HANA.

In Microsoft Azure, un cliente può utilizzare hello tooencrypt funzionalità di crittografia VM IaaS. Ad esempio, una possibile utilizzare dati dedicata dischi collegati toohello macchina virtuale, che vengono utilizzati toostore backup SAP HANA, quindi creare copie di questi dischi.

Servizio di Backup di Azure in grado di gestire le macchine virtuali/dischi crittografati (vedere [la modalità di crittografia delle macchine virtuali con Azure Backup tooback backup e ripristino](../../../backup/backup-azure-vms-encryption.md)).

Un'altra opzione potrebbe essere toomaintain hello SAP HANA VM e i relativi dischi senza crittografia e archiviare i file di backup di hello SAP HANA in un account di archiviazione per cui è stata abilitata la crittografia (vedere [la crittografia del servizio di archiviazione di Azure per i dati inattivi](../../../storage/common/storage-service-encryption.md)) .

## <a name="test-setup"></a>Impostazione del test

### <a name="test-virtual-machine-on-azure"></a>Eseguire il test della macchina virtuale in Azure.

Un'installazione di SAP HANA in una macchina virtuale di Azure GS5 è stata usata per hello seguente test di backup e ripristino.

![In questa figura viene illustrata parte del hello Panoramica del portale Azure per la macchina virtuale di test HANA hello](media/sap-hana-backup-guide/image007.png)

Questa figura mostra parte della panoramica del portale Azure per la macchina virtuale di test HANA hello hello.

### <a name="test-backup-size"></a>Testare la dimensione del backup

![In questa figura è stata ricavata dalla console di backup hello in Studio HANA e Mostra le dimensioni di file di backup hello GB 229 hello HANA server di indicizzazione](media/sap-hana-backup-guide/image008.png)

Una tabella fittizia è riempita con dati tooget una dimensione di backup totale dei dati di più di 200 GB di dati delle prestazioni realistici tooderive. Figura Hello è stata ricavata dalla console di backup hello in Studio HANA e Mostra le dimensioni di file di backup hello GB 229 hello HANA server di indicizzazione. Per i test di hello, hello predefinito backup prefisso "COMPLETE_DATA_BACKUP" in SAP HANA Studio è stato utilizzato. Nei sistemi di produzione reali, deve essere definito un prefisso più utile. Il pannello di controllo SAP HANA suggerisce data/ora.

### <a name="test-tool-toocopy-files-directly-tooazure-storage"></a>Test dello strumento toocopy direttamente i file tooAzure archiviazione

tootransfer SAP HANA i file di backup direttamente nell'archiviazione blob tooAzure o condivisioni di file di Azure, hello blobxfer stato utilizzato lo strumento perché supporta sia le destinazioni e possono essere facilmente integrati negli script di automazione dell'interfaccia della riga di comando tooits di scadenza. Hello blobxfer strumento è disponibile in [GitHub](https://github.com/Azure/blobxfer).

### <a name="test-backup-size-estimation"></a>Testare la stima della dimensione del backup

È importante tooestimate dimensioni del backup hello di SAP HANA. Questa stima consente prestazioni tooimprove definendo hello di dimensione massima del file di backup per un numero di file di backup, scadenza tooparallelism durante la copia di un file. Questi dettagli verranno spiegati più avanti nell'articolo. Inoltre, è necessario stabilire se una procedura completa di backup o un delta toodo backup (incrementale o differenziale).

Fortunatamente, è una semplice istruzione SQL che stima hello dimensioni dei file di backup hello: **selezionare \* da M\_BACKUP\_dimensioni\_STIME** (vedere [ Hello stima dello spazio necessario in hello File System per un Backup dei dati](https://help.sap.com/saphelp_hanaplatform/helpdata/en/7d/46337b7a9c4c708d965b65bc0f343c/content.htm)).

![output di Hello dell'istruzione SQL corrisponde quasi esattamente hello dimensioni reali hello completo di backup dei dati su disco](media/sap-hana-backup-guide/image009.png)

Per il sistema di prova hello, output di hello dell'istruzione SQL corrisponde quasi esattamente hello dimensioni reali hello completo di backup dei dati su disco.

### <a name="test-hana-backup-file-size"></a>Testare la dimensione del file di backup HANA

![console di backup HANA Studio Hello consente una dimensione massima del file di hello toorestrict HANA dei file di backup](media/sap-hana-backup-guide/image010.png)

console di backup HANA Studio Hello consente una dimensione massima del file di hello toorestrict HANA dei file di backup. Nell'ambiente di esempio hello, questa funzionalità rende possibili tooget più backup di più piccoli file anziché un file di backup di 230 GB. Le dimensioni del file ha un impatto significativo sulle prestazioni (vedere l'articolo correlato hello [SAP HANA Azure Backup a livello file](sap-hana-backup-file-level.md)).

## <a name="summary"></a>Riepilogo

In base ai risultati dei test hello hello le tabelle seguenti Mostra i vantaggi e svantaggi delle soluzioni tooback di un database SAP HANA in esecuzione in macchine virtuali di Azure.

**Eseguire il backup di copia e SAP HANA toohello file system file di backup in un secondo momento la destinazione di backup finale di toohello**

|Soluzione                                           |Vantaggi                                 |Svantaggi                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Mantenere i backup di HANA sui dischi della macchina virtuale                      |Nessuno sforzo di gestione aggiuntivo     |Consuma spazio sul disco della macchina virtuale locale           |
|Archiviazione tooblob di Blobxfer strumento toocopy i file di backup |Parallelismo toocopy più file, nell'archiviazione blob sporadico toouse scelta | Manutenzione aggiuntiva dello strumento e script personalizzato | 
|Copia di BLOB tramite Powershell o interfaccia della riga di comando                    |Nessuno strumento aggiuntivo necessario, è possibile procedere con l'esecuzione tramite Azure Powershell o interfaccia della riga di comando |processo manuale, cliente ha tootake cure script e la gestione di copia BLOB per il ripristino|
|Condivisione tooNFS copia                                  |Post-elaborazione dei file di backup in altre VM senza alcun impatto sul server HANA hello|Processo di copia lenta|
|Copia di Blobxfer tooAzure servizio File                |Non consuma spazio sui dischi della macchina virtuale locale|Nessun supporto di scrittura diretto dal backup di HANA, la restrizione sulle dimensioni della condivisione di file è attualmente di 5 TB|
|Agente di Backup di Azure                                 | Soluzione preferibile         | Attualmente non disponibile su Linux    |



**Backup di SAP HANA basato su snapshot di archiviazione**

|Soluzione                                           |Vantaggi                                 |Svantaggi                                  |
|---------------------------------------------------|-------------------------------------|--------------------------------------|
|Servizio Backup di Azure                               | Consente il backup delle macchine virtuali basato su snapshot BLOB | Quando non si utilizza il ripristino a livello di file, richiede la creazione di hello di una nuova macchina virtuale per il processo di ripristino hello, che implica quindi necessario hello di una nuova chiave di licenza di SAP HANA|
|Snapshot BLOB manuali                              | Flessibilità toocreate e ripristino specifici dischi di macchina virtuale senza modificare hello ID univoco di VM|Tutto il lavoro manuale, che ha eseguito dal cliente hello toobe|

## <a name="next-steps"></a>Passaggi successivi
* [SAP HANA Azure Backup a livello di file](sap-hana-backup-file-level.md) descrive l'opzione di backup basato su file hello.
* [Backup di SAP HANA in base agli snapshot di archiviazione](sap-hana-backup-storage-snapshots.md) descrive hello archiviazione basata su snapshot opzione di backup.
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).
