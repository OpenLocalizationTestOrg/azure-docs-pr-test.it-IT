---
title: pianificazione della distribuzione di Site Recovery aaaAzure per VMware in Azure | Documenti Microsoft
description: Si tratta di Guida alla utente pianificazione della distribuzione di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery Deployment Planner
Questo articolo è manuale dell'utente hello pianificazione della distribuzione di ripristino del sito di Azure per le distribuzioni di produzione VMware in Azure.

## <a name="overview"></a>Panoramica

Prima di iniziare a proteggere le macchine virtuali VMware (VM) con il ripristino del sito, allocare larghezza di banda sufficiente, in base a tasso di modifica dei dati giornaliera, toomeet l'obiettivo del punto di ripristino desiderata (RPO). Impossibile verificare toodeploy hello del numero corretto di server di configurazione e il processo server locale.

È inoltre necessario tipo corretto di toocreate hello e numero di account di archiviazione di Azure di destinazione. Per creare account di archiviazione Standard o Premium, si considera la crescita nei server di produzione di origine a causa del maggiore utilizzo nel tempo. Si sceglie il tipo di archiviazione hello per ogni macchina virtuale, in base alle caratteristiche del carico di lavoro (ad esempio, operazioni dei / o di lettura/scrittura o al secondo [IOPS varianza dei dati) e limita il ripristino del sito.

anteprima pubblica pianificazione della distribuzione Site Recovery Hello è uno strumento da riga di comando che è attualmente disponibile solo per uno scenario di hello VMware in Azure. In modalità remota, è possibile profilare le macchine virtuali VMware tramite questa larghezza di banda hello toounderstand strumento (senza alcun impatto di produzione qualunque) e i requisiti di archiviazione di Azure per il completamento della replica e failover di test. È possibile eseguire lo strumento hello senza installare tutti i componenti di Site Recovery in locale. Tuttavia, tooget accurato ottenuto i risultati di velocità effettiva, è consigliabile eseguire la pianificazione hello in un Server di Windows che soddisfi hello requisiti minimi hello il ripristino del sito del server di configurazione che è infine necessario toodeploy come uno dei primi passaggi hello nella distribuzione di produzione.

lo strumento di Hello offre hello seguenti dettagli:

**Valutazione della compatibilità**

* Valutazione dell'idoneità delle VM in base a numero di dischi, dimensioni dei dischi, operazioni di I/O al secondo, varianza e tipo di avvio (EFI/BIOS)
* Hello stimato larghezza di banda necessaria per la replica differenziale

**Valutazione della larghezza di banda di rete necessaria rispetto al valore RPO**

* Hello stimato larghezza di banda necessaria per la replica differenziale
* velocità effettiva di Hello che il ripristino del sito è possibile ottenere da tooAzure locale
* numero di Hello di toobatch di macchine virtuali, in base a hello stimato della larghezza di banda toocomplete la replica iniziale in un determinato periodo di tempo

**Requisiti dell'infrastruttura di Azure**

* requisito del tipo (account di archiviazione standard o premium) archiviazione Hello per ogni macchina virtuale
* numero totale di Hello di toobe gli account di archiviazione standard e premium impostato per la replica
* Suggerimenti di denominazione degli account di archiviazione in base alle linee guida di archiviazione di Azure
* posizionamento di account di archiviazione Hello per tutte le macchine virtuali
* numero di Hello di Azure Core toobe imposta prima di failover di test o il failover su sottoscrizione hello
* Hello dimensioni consigliate da macchina virtuale di Azure per ogni macchina virtuale in locale

**Requisiti dell'infrastruttura locale**
* Hello il numero di server di configurazione richiesto e toobe di processo server distribuiti in locale

>[!IMPORTANT]
>
>Poiché l'utilizzo è probabilmente tooincrease nel tempo, tutti hello strumento precedente vengono eseguiti i calcoli, presupponendo un fattore di crescita del 30% in termini di caratteristiche del carico di lavoro e l'utilizzo di un valore del 95 ° percentile di hello tutte le metriche di profilatura (lettura/scrittura IOPS, varianza e pertanto via). Entrambi questi elementi (fattore di crescita e calcolo percentile) sono configurabili. sezione "Considerazioni fattore di crescita" hello, vedere toolearn ulteriori informazioni su fattore di crescita. toolearn ulteriori informazioni su valore percentile, nella sezione hello "Valore Percentile utilizzato per il calcolo hello".
>

## <a name="requirements"></a>Requisiti
strumento di Hello presenta due fasi principali: analisi e generazione del report. È inoltre disponibile una terza opzione toocalculate velocità effettiva solo. requisiti di Hello per server hello dal quale hello misura la velocità effettiva e la profilatura viene avviata vengono presentati in hello nella tabella seguente:

| Requisito server | Descrizione|
|---|---|
|Profilatura e misurazione della velocità effettiva| <ul><li>Sistema operativo: Microsoft Windows Server 2012 R2<br>(idealmente corrispondenti ad almeno hello [dimensioni indicazioni per il server di configurazione di hello](https://aka.ms/asr-v2a-on-prem-components))</li><li>Configurazione del computer: 8 vCPU, 16 GB di RAM, disco rigido da 300 GB</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ Redistributable per Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>TooAzure accesso Internet da questo server</li><li>Account di archiviazione di Azure</li><li>Accesso di amministratore sul server hello</li><li>Almeno 100 GB di spazio libero su disco (presumendo 1000 VM con una media di tre dischi ognuna, profilate per 30 giorni)</li><li>Impostazioni del livelli di VMware vCenter statistiche deve essere impostati too2 o alto livello</li><li>Consentire la porta 443: pianificazione della distribuzione di ripristino automatico di sistema utilizza l'host di server/ESXi toovCenter tooconnect porta</ul></ul>|
| Generazione di report | Un PC o server Windows con Microsoft Excel 2013 o versione successiva |
| Autorizzazioni utente | Autorizzazione di sola lettura per l'account utente hello host ESXi tooaccess hello VMware vCenter server/VMware vSphere utilizzato durante la profilatura |

> [!NOTE]
>
>strumento Hello è possibile profilare solo le macchine virtuali con dischi VMDK e RDM. Non può profilare VM con dischi iSCSI o NFS. Il ripristino del sito supporta iSCSI e i dischi NFS per i server VMware, tuttavia, poiché pianificazione della distribuzione di hello non è presente all'interno di guest hello e i profili solo tramite i contatori delle prestazioni di vCenter, strumento hello non è visibile in questi tipi di disco.
>

## <a name="download-and-extract-hello-public-preview"></a>Scaricare ed estrarre l'anteprima pubblica di hello
1. Scaricare una versione più recente di hello di hello [anteprima pubblica pianificazione della distribuzione di Site Recovery](https://aka.ms/asr-deployment-planner).  
strumento Hello viene compresso in una cartella con estensione zip. versione corrente di Hello dello strumento hello supporta solo scenario di hello VMware in Azure.

2. Copia hello ZIP cartella toohello Windows server da cui si desidera che toorun hello strumento.  
È possibile eseguire lo strumento hello da Windows Server 2012 R2 se hello server dispone di accesso tooconnect toohello vCenter server/vSphere ESXi host di rete che contiene hello toobe di macchine virtuali a profilatura. Tuttavia, è consigliabile eseguire lo strumento hello in un server di cui la configurazione hardware soddisfi hello [delle linee guida di configurazione server ridimensionamento](https://aka.ms/asr-v2a-on-prem-components). Se sono già stati distribuiti componenti Site Recovery in locale, eseguire lo strumento hello dal server di configurazione hello.

 È consigliabile acquisire hello hello configurazione server (che dispone di un server di elaborazione in compilato) in server hello in cui viene eseguito lo strumento hello stessa configurazione hardware. Questa configurazione assicura la velocità effettiva hello ottenuta tale hello strumento report corrispondenze hello velocità effettiva che è possibile ottenere il ripristino del sito durante la replica. calcolo della velocità effettiva di Hello varia a seconda della larghezza di banda di rete disponibili nel server di hello e configurazione hardware del server hello (CPU, memoria e così via). Se si esegue lo strumento hello da qualsiasi altro server, la velocità effettiva hello viene calcolata da tale tooMicrosoft server Azure. Inoltre, poiché configurazione hardware hello del server hello potrebbero essere diversi da quello del server di configurazione di hello, velocità effettiva di hello ottenuta che hello strumento report potrebbe non essere accurata.

3. Estrarre la cartella con estensione zip hello.  
cartella Hello contiene più file e sottocartelle. file eseguibile di Hello è ASRDeploymentPlanner.exe nella cartella padre hello.

    Esempio:  
    Copiare tooE di file con estensione zip hello: \ unità ed estrarre i file.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Capabilities
È possibile eseguire lo strumento da riga di comando di hello (ASRDeploymentPlanner.exe) in uno dei seguenti tre modalità hello:

1. Profilatura  
2. Generazione di report
3. Misurare la velocità effettiva

Strumento di hello in primo luogo, l'esecuzione della profilatura varianza dei dati in modalità toogather VM e IOPS. Successivamente, eseguire report di hello toogenerate strumento hello toofind hello rete larghezza di banda e requisiti di archiviazione.

## <a name="profiling"></a>Profilatura
In modalità di profilatura dello strumento di pianificazione di hello distribuzione si connette toohello vCenter server/vSphere ESXi host toocollect i dati sulle prestazioni hello macchina virtuale.

* Profilatura non influisce sulle prestazioni hello di produzione hello macchine virtuali, perché toothem è viene stabilita alcuna connessione diretta. Tutti i dati sulle prestazioni raccolti dai hello vCenter server/ESXi host vSphere.
* tooensure che vi sia un impatto trascurabile nel server di hello a causa di profilatura, hello strumento query hello vCenter server/ESXi host vSphere una volta ogni 15 minuti. Questo intervallo di query non compromettere la precisione di profilatura, perché lo strumento hello archivia i dati dei contatori delle prestazioni del minuto.

### <a name="create-a-list-of-vms-tooprofile"></a>Creare un elenco di macchine virtuali tooprofile
In primo luogo, è necessario un elenco di hello toobe di macchine virtuali a profilatura. È possibile ottenere tutti i nomi di hello di macchine virtuali in un host ESXi di vCenter server/vSphere mediante hello VMware vSphere PowerCLI comandi hello seguente procedura. In alternativa, è possibile elencare in un nome descrittivo hello o hello di indirizzi IP delle macchine virtuali che si desidera tooprofile manualmente.

1. Accedi toohello tale vSphere VMware PowerCLI viene installato nella VM.
2. Aprire la console di hello VMware vSphere PowerCLI.
3. Verificare che i criteri di esecuzione hello sono abilitato per script hello. Se è disabilitato, avviare la console di hello VMware vSphere PowerCLI in modalità amministratore e quindi abilitarlo eseguendo hello comando seguente:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. È possibile necessità opzione toorun hello comando seguente, se VIServer di connessione non è riconosciuto come nome hello del cmdlet.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget tutti i nomi di hello di macchine virtuali in un server vCenter/vSphere ESXi ospitano e archiviano hello elenco in un file con estensione txt, due comandi hello esecuzione elencati di seguito.
Sostituire &lsaquo;server name&rsaquo;, &lsaquo;user name&rsaquo;, &lsaquo;password&rsaquo; e &lsaquo;outputfile.txt&rsaquo; con i propri input.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Aprire il file di output di hello nel blocco note e copiare quindi i nomi di hello di tutte le macchine virtuali che si desidera tooprofile tooanother file (ad esempio, ProfileVMList.txt), un nome di macchina virtuale per ogni riga. Questo file viene utilizzato come input toohello *- VMListFile* parametro dello strumento da riga di comando hello.

    ![Elenco di nomi di macchina virtuale nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Avviare la profilatura
Dopo aver ottenuto l'elenco di hello di profiling toobe di macchine virtuali, è possibile eseguire lo strumento hello in modalità di profilatura. Ecco elenco hello dei parametri obbligatori e facoltativi di hello strumento toorun in modalità di profilatura.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Nome parametro | Descrizione |
|---|---|
| -Operation | StartProfiling |
| -Server | nome di dominio completo di Hello o indirizzo IP dell'host ESXi di hello vCenter server/vSphere cui le macchine virtuali sono toobe a profilatura.|
| -User | Hello utente nome tooconnect toohello vCenter server/ESXi host vSphere. utente Hello deve toohave accesso in sola lettura, come minimo.|
| -VMListFile | file Hello contenente hello elenco di macchine virtuali toobe il profiling. percorso del file Hello può essere assoluto o relativo. file di Hello deve contenere una VM nome/indirizzo IP per riga. Nome della macchina virtuale specificato nel file hello devono essere hello come nome della macchina virtuale nell'host ESXi di hello vCenter server/vSphere hello.<br>Ad esempio, file hello VMList.txt contiene hello macchine virtuali seguenti:<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | Hello numero di giorni per la quale il profiling è toobe esecuzione. È consigliabile eseguire il profiling per più di 15 giorni tooensure che hello modello di carico di lavoro nel proprio ambiente su hello specificato periodo viene osservata e utilizzato tooprovide un'indicazione accurata. |
| -Directory | Convenzione di denominazione universali hello (facoltativo) (UNC) o toostore di percorso di directory locale generati durante l'analisi di dati di profilatura. Se non viene specificato un nome di directory, directory di hello denominata 'ProfiledData' nel percorso corrente hello da utilizzare come directory predefinita hello. |
| -Password | (Facoltativo) hello password toouse tooconnect toohello vCenter server/ESXi host vSphere. Se non si specifica uno a questo punto, verrà richiesto per tale quando viene eseguito il comando hello.|
| -StorageAccountName | Nome dell'account di archiviazione hello (facoltativo) che è la velocità effettiva di hello toofind utilizzati raggiungibile per la replica dei dati da tooAzure in locale. Hello strumento caricamenti test toothis storage account toocalculate velocità effettiva dei dati.|
| -StorageAccountKey | Chiave dell'account di archiviazione hello (facoltativo) che ha utilizzato l'account di archiviazione tooaccess hello. Passare toohello portale di Azure > gli account di archiviazione ><*nome account di archiviazione*>> Impostazioni > chiavi di accesso > Key1 (o chiave di accesso primaria per l'account di archiviazione classico). |
| -Environment | (Facoltativo) Ambiente dell'account di archiviazione di Azure di destinazione. Può trattarsi di uno di tre valori: AzureCloud, AzureUSGovernment, AzureChinaCloud. Il valore predefinito è AzureCloud. Utilizzare il parametro hello quando l'area di Azure di destinazione è cloud Azure del governo o Azure China. |


Si consiglia di profilare le macchine virtuali per almeno 15 giorni too30. Durante il periodo di profilatura di hello, ASRDeploymentPlanner.exe continua a funzionare normalmente. strumento di Hello accetta input di profilatura in giorni. Se si desidera tooprofile per alcune ore o minuti per un rapido test dello strumento di hello, in anteprima pubblica di hello, è necessario tempo hello tooconvert in misura equivalente di hello di giorni. Ad esempio, tooprofile per 30 minuti, hello input deve essere 30/(60*24) = 0.021 giorni. Hello consentito profilatura tempo minimo è 30 minuti.

Durante la profilatura, è possibile passare facoltativamente un nome di account di archiviazione e la velocità effettiva di hello toofind chiave in grado di ottenere il ripristino del sito in fase di replica dal server di configurazione hello o processo server tooAzure di hello. Se chiave e il nome di account di archiviazione hello non vengono passati durante l'analisi, strumento hello non in grado di calcolare la velocità effettiva ottenibile.

È possibile eseguire più istanze dello strumento hello per vari set di macchine virtuali. Verificare che i nomi di macchina virtuale hello non vengono ripetuti in qualsiasi hello profilatura set. Ad esempio, se si dispongano di profilatura dieci macchine virtuali (VM1 tramite VM10) e dopo alcuni giorni si desidera tooprofile cinque macchine virtuali di un altro (VM11 tramite VM15), è possibile eseguire lo strumento hello da un'altra console della riga di comando per secondo set di macchine virtuali di hello (VM11 tramite VM15). Verificare che secondo set di macchine virtuali di hello non hanno nomi di macchina virtuale dall'istanza di profilatura prima hello o utilizzare una directory di output diverso per la seconda esecuzione hello. Se due istanze dello strumento hello vengono utilizzate per la profilatura hello stesse macchine virtuali e utilizzare hello stessa directory di output, report hello generato non saranno corretti.

Le configurazioni di macchina virtuale vengono acquisite contemporaneamente all'inizio di hello di hello profiling dell'operazione e archiviate in un file denominato VMDetailList.xml. Queste informazioni vengono utilizzate quando viene generato il report hello. Qualsiasi modifica nella configurazione della macchina virtuale (ad esempio, un numero maggiore di schede di rete, dischi o core) dalla fine di toohello hello inizio dell'analisi non viene acquisito. Se una configurazione profilata della macchina virtuale è stata modificata durante il corso hello di profilatura, in anteprima pubblica di hello, ecco hello soluzione tooget VM dettagli durante la generazione di report hello:

* Eseguire il backup VMdetailList.xml ed eliminare file hello dalla posizione corrente.
* Passare - e - la Password utente argomenti in fase di hello della generazione di report.

Hello profilatura comando genera più file in hello profilatura directory. Non eliminare eventuali file hello, perché ciò interessa pertanto la generazione del report.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Esempio 1: Macchine virtuali di profilo per 30 giorni e la velocità effettiva di hello trova da tooAzure locale
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Esempio 2: Profilare le VM per 15 giorni

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Esempio 3: Macchine virtuali di profilo 1 ora per un rapido test dello strumento hello
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Se il server di hello dello strumento hello è in esecuzione in è stata riavviata oppure si è arrestato, o se si chiude hello strumento utilizzando Ctrl + C, i dati di profilatura hello viene mantenuto. Tuttavia, è la possibilità di hello manca ultimi 15 minuti di dati analizzati. In questo caso, eseguire di nuovo lo strumento hello in modalità di profilatura dopo il riavvio del server di hello.
>* Quando vengono passati hello nome di account di archiviazione e la chiave, la velocità effettiva hello misure strumento hello ultimo passaggio di hello di profilatura. Se hello viene chiuso prima del completamento di profilatura della velocità effettiva di hello non viene calcolata. hello di velocità effettiva di hello toofind prima della generazione di report, è possibile eseguire l'operazione GetThroughput hello dalla console della riga di comando hello. In caso contrario, il report generato hello non conterrà dati sulla velocità effettiva hello.


## <a name="generate-a-report"></a>Generare un report
strumento di Hello genera un file di Microsoft Excel con attivazione macro (file XLSM) come output del report hello, che sono riepilogati i requisiti di distribuzione tutti hello. report di Hello è denominato DeploymentPlannerReport_ <*identificatore numerico univoco*> xlsm e hello nella directory specificata.

Al termine dell'analisi, è possibile eseguire lo strumento hello in modalità di generazione di report. Hello nella tabella seguente contiene un elenco di toorun parametri obbligatori e facoltativi di strumento in modalità di generazione di report.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Nome parametro | Descrizione |
|-|-|
| -Operation | GenerateReport |
| -Server |  server vCenter/vSphere Hello completi di nome di dominio o indirizzo IP (utilizzare hello stesso nome o indirizzo IP utilizzato in fase di hello di profilatura) in cui le macchine virtuali il cui tipo di report è toobe generato il profiling hello si trovano. Si noti che, se si utilizza un server vCenter in fase di hello di profilatura, è possibile utilizzare un server di vSphere per la generazione di report e viceversa.|
| -VMListFile | file Hello contenente hello elenco di macchine virtuali profilate che hello report è toobe generato per. percorso del file Hello può essere assoluto o relativo. Hello file deve contenere un nome di macchina virtuale o un indirizzo IP per riga. i nomi di macchina virtuale Hello specificati nel file hello devono essere hello come nomi di macchina virtuale hello hello vCenter server/ESXi host vSphere e quello utilizzato durante l'analisi di corrispondenza.|
| -Directory | (Facoltativo) hello UNC o percorso della directory locale in cui il profiling dati (file generati durante la profilatura) hello viene archiviato. Questi dati sono necessari per la generazione di report hello. Se non è specificato nessun nome, verrà usata la directory "ProfiledData". |
| -GoalToCompleteIR | Hello (facoltativo) numero di ore in cui hello la replica iniziale di hello profilato macchine virtuali deve toobe completato. report generato Hello fornisce hello numero di macchine virtuali per cui è possibile eseguire la replica iniziale in hello specificato tempo. valore predefinito di Hello è 72 ore. |
| -User | (Facoltativo) hello utente toouse tooconnect toohello vCenter/vSphere server dei nomi. nome Hello è utilizzato toofetch hello più recente informazioni di configurazione di macchine virtuali, ad esempio il numero di hello dei dischi, numero di core e numero di schede di rete, nel report hello toouse hello. Se non è specificato il nome di hello, le informazioni di configurazione hello raccolte all'inizio di hello della profilatura Kick Off hello viene utilizzate. |
| -Password | (Facoltativo) hello password toouse tooconnect toohello vCenter server/ESXi host vSphere. Se la password di hello non è specificata come parametro, verrà richiesto per tale in un secondo momento quando viene eseguito il comando hello. |
| -DesiredRPO | (Facoltativo) hello desiderato obiettivo punto di ripristino, in minuti. valore predefinito di Hello è 15 minuti.|
| -Bandwidth | Larghezza di banda in Mbps. prova parametro toouse toocalculate prova RPO che può essere ottenuta hello specificato della larghezza di banda. |
| -StartDate | (Facoltativo) hello data e ora di inizio in MM-GG-YYYY:HH:MM (formato di 24 ore). *StartDate* deve essere specificato con *EndDate*. Quando viene specificato StartDate, report hello viene generato per hello analizzata i dati raccolti tra StartDate ed EndDate. |
| -EndDate | Data di fine (facoltativo) hello e l'ora in MM-GG-YYYY:HH:MM (formato di 24 ore). *EndDate* deve essere specificato con *StartDate*. Quando viene specificato EndDate, report hello viene generato per hello analizzata i dati raccolti tra StartDate ed EndDate. |
| -GrowthFactor | Fattore di crescita hello (facoltativo), espressa come percentuale. valore predefinito di Hello è il 30%. |
| -UseManagedDisks | (Facoltativo) UseManagedDisks: Yes/No. Il valore predefinito è Yes. numero di Hello di macchine virtuali che possono essere inseriti in un singolo account di archiviazione viene calcolato considerando se il Failover o Test failover delle macchine virtuali viene eseguito su un disco gestito anziché un disco non gestito. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Esempio 1: Generare un report con i valori predefiniti quando i dati di profilatura hello sono nell'unità locale hello
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Esempio 2: Generare un report quando i dati di profilatura hello in un server remoto
Deve disporre dell'accesso in lettura/scrittura in directory remota hello.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Esempio 3: Creare un report con un toocomplete specifiche di larghezza di banda e obiettivo IR entro il tempo specificato
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Esempio 4: Creare un report con un fattore di crescita del 5% anziché il 30% di hello predefinito
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Esempio 5: Generare un report con un subset di dati profilati
Ad esempio, si entro 30 giorni di dati analizzati e si desidera toogenerate un report solo per 20 giorni.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Esempio 6: Generare un report per un valore RPO di 5 minuti
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Valore percentile utilizzato per il calcolo hello
**Valore percentile predefinito hello misurazione delle prestazioni raccolti durante l'analisi dello strumento utilizza hello quando genera un report?**

Hello strumento predefinite toohello 95 ° percentile di valori di lettura/scrittura IOPS, scrivere IOPS e varianza dei dati raccolti durante l'analisi di tutte le macchine virtuali hello. Questa metrica assicura tale picco hello 100 percentile le macchine virtuali potrebbe essere visualizzato a causa di eventi temporanei è toodetermine non usato i requisiti di larghezza di banda di origine e account di archiviazione di destinazione. Un evento temporaneo può essere, ad esempio, un processo di backup eseguito una volta al giorno, un'indicizzazione periodica di un database, un'attività di generazione di report analitici o altri eventi simili temporizzati di breve durata.

Utilizzando i valori di 95 ° percentile offre che un'idea delle caratteristiche del carico di lavoro reale offre hello prestazioni ottimali quando i carichi di lavoro hello sono in esecuzione in Azure. Non prevediamo di che è necessario toochange questo numero. Se si modifica il valore di hello (toohello 90 ° percentile, ad esempio), è possibile aggiornare il file di configurazione di hello *ASRDeploymentPlanner.exe.config* in hello cartella predefinita e salvarlo in un nuovo report toogenerate hello esistente a profilatura dati.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Considerazioni sul fattore di crescita
**Perché considerare il fattore di crescita quando si pianificano le distribuzioni**

È tooaccount critico per la crescita le caratteristiche del carico di lavoro, presupponendo che un potenziale incremento nell'utilizzo nel tempo. Dopo aver protezione sul posto, se modificare le caratteristiche del carico di lavoro, è possibile passare tooa altro account di archiviazione per la protezione senza disabilitando e riabilitando la protezione di hello.

Si supponga, ad esempio, che attualmente la VM sia idonea per un account di replica di archiviazione Standard. Su hello prossimi tre mesi, più modifiche sono probabilmente toooccur:

* aumenta il numero di Hello di utenti dell'applicazione hello in esecuzione su hello macchina virtuale.
* Hello risultante maggiore varianza hello VM sarà richiesta l'archiviazione di hello VM toogo toopremium in modo che la replica di Site Recovery è possibile tenere il passo.
* Di conseguenza, si hanno toodisable e abilitare nuovamente l'account di archiviazione premium tooa di protezione.

È consigliabile pianificare la crescita durante la pianificazione della distribuzione e mentre hello predefinita è 30 percento. Si è esperti di hello sulle proiezioni di crescita e modello di utilizzo applicazione ed è possibile modificare questo numero di conseguenza durante la generazione di un report. Inoltre, è possibile generare più report con diversi fattori di crescita con hello stesso profiling dati e determinare quali suggerimenti di larghezza di banda origine e di archiviazione di destinazione soluzione più adatta.

report di Microsoft Excel Hello generato contiene hello le seguenti informazioni:

* [Input](site-recovery-deployment-planner.md#input)
* [Raccomandazioni](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Raccomandazioni con la larghezza di banda disponibile come input](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [Selezione host di archiviazione delle VM](site-recovery-deployment-planner.md#vm-storage-placement)
* [VM compatibili](site-recovery-deployment-planner.md#compatible-vms)
* [VM incompatibili](site-recovery-deployment-planner.md#incompatible-vms)

![Deployment Planner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Misurare la velocità effettiva

velocità effettiva di hello tooestimate che il ripristino del sito è possibile ottenere da tooAzure locale durante la replica, eseguire lo strumento hello in modalità GetThroughput. strumento Hello consente di calcolare la velocità effettiva hello da server hello hello strumento è in esecuzione in. In teoria, questo server si basa sul ridimensionamento manuale di hello configurazione server. Se il ripristino del sito infrastruttura componenti locale è già stato distribuito, eseguire lo strumento hello nel server di configurazione hello.

Aprire una console della riga di comando e passare la distribuzione di Site Recovery toohello cartella dello strumento di pianificazione. Eseguire ASRDeploymentPlanner.exe con i parametri seguenti.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Nome parametro | Descrizione |
|-|-|
| -Operation | GetThroughput |
| -Directory | (Facoltativo) hello UNC o percorso della directory locale in cui il profiling dati (file generati durante la profilatura) hello viene archiviato. Questi dati sono necessari per la generazione di report hello. Se non viene specificato un nome di directory, viene usata la directory "ProfiledData". |
| -StorageAccountName | nome dell'account di archiviazione Hello utilizzati di larghezza di banda di hello toofind utilizzata per la replica dei dati da tooAzure locale. Hello strumento caricamenti test dati toothis storage account toofind hello larghezza di banda utilizzata. |
| -StorageAccountKey | chiave dell'account di archiviazione Hello che ha utilizzato l'account di archiviazione tooaccess hello. Passare toohello portale di Azure > gli account di archiviazione ><*nome account di archiviazione*>> Impostazioni > chiavi di accesso > Key1 (o una chiave di accesso primaria per un account di archiviazione classico). |
| -VMListFile | file Hello che contiene l'elenco hello di profilatura per il calcolo hello banda toobe di macchine virtuali. percorso del file Hello può essere assoluto o relativo. file di Hello deve contenere una VM nome/indirizzo IP per riga. i nomi di macchina virtuale Hello specificati nel file hello devono essere hello come nomi di macchina virtuale hello in hello vCenter server/ESXi host vSphere.<br>Ad esempio, file hello VMList.txt contiene hello macchine virtuali seguenti:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (Facoltativo) Ambiente dell'account di archiviazione di Azure di destinazione. Può trattarsi di uno di tre valori: AzureCloud, AzureUSGovernment, AzureChinaCloud. Il valore predefinito è AzureCloud. Utilizzare il parametro hello quando l'area di Azure di destinazione è cloud Azure del governo o Azure China. |

Hello vengono creati diversi file 64 MB asrvhdfile <> # vhd (dove "#" è il numero di hello di file) nella directory specificata hello. strumento Hello carica hello file toohello storage account toofind hello della velocità effettiva. Dopo che viene misurata la velocità effettiva hello, strumento hello Elimina tutti i file hello dall'account di archiviazione hello e dal server locale hello. Se lo strumento hello viene terminato per qualsiasi motivo, mentre in corso il calcolo della velocità effettiva, non viene eliminato il file hello hello di archiviazione o dal server locale hello. Sarà necessario toodelete li manualmente.

Hello velocità effettiva è misurata in un punto specifico nel tempo ed è hello la velocità effettiva massima che è possibile ottenere il ripristino del sito durante la replica, purché tutti gli altri fattori rimangono uguali hello. Ad esempio, qualsiasi applicazione inizia a utilizzare più larghezza di banda hello stessa rete, la velocità effettiva di hello varia durante la replica. Se si esegue il comando GetThroughput hello da un server di configurazione, lo strumento hello è conoscenza di eventuali macchine virtuali protette e replica in corso. Hello risultati di velocità effettiva misurata hello sono diverso se hello GetThroughput operazione viene eseguita quando hello protetto le macchine virtuali dispone di dati elevati varianza. È consigliabile eseguire strumento hello in diversi punti nel tempo durante la profilatura toounderstand quale velocità effettiva in momenti diversi, è possibile ottenere i livelli. Nel report hello, lo strumento di hello Mostra hello ultimo misurata la velocità effettiva.

### <a name="example"></a>Esempio
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Eseguire lo strumento hello in un server dotato di hello stessa risorsa di archiviazione e le caratteristiche di CPU come server di configurazione hello.
>
> Per la replica, impostare hello hello toomeet consigliati della larghezza di banda RPO 100% del tempo di hello. Dopo aver impostato hello destra della larghezza di banda, se non viene visualizzato un aumento della velocità effettiva hello ottenuta segnalati dallo strumento hello, hello seguenti:
>
>  1. Controllare toodetermine se è presente alcuna rete Quality of Service (QoS) che limitano la velocità effettiva Site Recovery.
>
>  2. Controllare toodetermine se l'insieme di credenziali di Site Recovery in hello più vicino di latenza di rete toominimize Microsoft Azure area fisicamente supportata.
>
>  3. Se è possibile migliorare hardware hello (ad esempio, tooSSD HDD), controllare il toodetermine caratteristiche di archiviazione locale.
>
>  4. Modificare anche le impostazioni di Site Recovery hello nel server di elaborazione hello[aumentare hello quantità di larghezza di banda di rete utilizzata per la replica](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Raccomandazioni con valore RPO desiderato come input

### <a name="profiled-data"></a>Dati profilati

![visualizzazione di dati profilato Hello nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Periodo dei dati profilata**: periodo hello durante cui hello è stata eseguita l'analisi. Per impostazione predefinita, lo strumento hello include tutti i dati di analizzata nel calcolo hello, a meno che non genera report hello per un periodo specifico utilizzando le opzioni di StartDate ed EndDate durante la generazione di report.

**Nome del server**: nome hello o l'indirizzo IP di hello VMware vCenter o l'host ESXi viene generato il report di cui le macchine virtuali.

**Desired RPO**: obiettivo del punto di ripristino hello per la distribuzione. Per impostazione predefinita, hello obbligatorio della larghezza di banda di rete viene calcolato per valori di 15, 30 e 60 minuti. In base alla selezione di hello, i valori hello interessato vengono aggiornati nel foglio hello. Se è stata usata hello *DesiredRPOinMin* parametro durante la generazione di report di hello, visualizzato nel risultato desiderato RPO hello valore.

### <a name="profiling-overview"></a>Panoramica della profilatura

![Risultati del profiling nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/profiling-overview.png)

**Totale macchine virtuali di profiling**: hello numero totale di macchine virtuali i cui dati analizzati sono disponibili. Se hello VMListFile con nomi di tutte le macchine virtuali che non analizzate, tali macchine virtuali non vengono considerati nella generazione del report hello e vengono escluse dal conteggio di macchine virtuali di hello totale profilato.

**Macchine virtuali compatibili**: hello numero di macchine virtuali che possono essere protetti tooAzure tramite il ripristino del sito. È hello il numero totale di macchine virtuali compatibili per cui hello vengono calcolate la larghezza di banda di rete necessarie, numero di account di archiviazione, numero di core di Azure e numero di server di configurazione e i server di elaborazione aggiuntive. sono disponibili nella sezione "Macchine virtuali compatibili" hello Hello dettagli di ogni VM compatibile.

**Macchine virtuali compatibili**: hello numero di macchine virtuali profilate che non sono compatibili per la protezione con il ripristino del sito. motivi Hello per incompatibilità sono indicate nella sezione "Macchine virtuali incompatibile" hello. Se hello VMListFile con nomi di tutte le macchine virtuali non analizzate, tali macchine virtuali sono escluse dal conteggio di macchine virtuali compatibile hello. Queste macchine virtuali sono elencate come "Dati non trovato" alla fine di hello della sezione hello "VMs incompatibile".

**Desired RPO** (RPO desiderato): obiettivo del punto di ripristino desiderato, in minuti. report Hello viene generato per tre valori: 15 (impostazione predefinita), 30 e 60 minuti. indicazione della larghezza di banda Hello in report hello viene modificato in base alla selezione nell'elenco di hello elenco a discesa RPO desiderato nella hello in alto a destra della finestra hello. Se si sono generati report hello utilizzando hello *- DesiredRPO* parametro con un valore personalizzato, questo valore personalizzato verrà visualizzato come valore predefinito di hello nell'elenco di hello elenco a discesa RPO desiderato.

### <a name="required-network-bandwidth-mbps"></a>Larghezza di banda di rete necessaria (Mbps)

![Larghezza di banda di rete richieste nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100% del tempo di hello:** hello consigliato di larghezza di banda in Mbps toobe allocata toomeet del RPO desiderato 100% del tempo di hello. La quantità di larghezza di banda deve essere dedicato per la replica nello stato stazionario delta di tutte le macchine virtuali tooavoid compatibile violazioni RPO.

**toomeet RPO il 90% di tempo hello**: a causa di prezzi a banda larga o per qualsiasi motivo, se non è possibile impostare toomeet di larghezza di banda necessaria hello del RPO desiderato 100% del tempo di hello, è possibile scegliere toogo con una larghezza di banda inferiore, l'impostazione che è possibile soddisfare il RPO desiderato il 90% di tempo hello. implicazioni di hello toounderstand dell'impostazione di larghezza di banda inferiore, hello report include un'analisi di simulazione hello numero e la durata di tooexpect violazioni RPO.

**Velocità effettiva ottenuta:** velocità effettiva di hello dal server di hello in cui sono stati eseguiti hello GetThroughput comando toohello regione di Microsoft Azure in cui si trova l'account di archiviazione hello. Questo numero di velocità effettiva indica il livello stimato hello che è possibile ottenere quando si protegge macchine virtuali compatibili con il ripristino del sito, purché il server di configurazione o le caratteristiche di archiviazione e di rete server processo rimangono hello uguale a quello di hello server di Hello da cui sono stati eseguiti strumento hello.

Per la replica, è consigliabile impostare hello hello toomeet consigliati della larghezza di banda RPO 100% del tempo di hello. Dopo aver impostato la larghezza di banda hello, se non viene visualizzato un aumento della velocità effettiva di hello ottenuta, come indicato dallo strumento hello, eseguire hello seguenti:

1. Controllare toosee se è presente alcuna rete Quality of Service (QoS) che limitano la velocità effettiva Site Recovery.

2. Controllare toosee se l'insieme di credenziali di Site Recovery in hello più vicino di latenza di rete toominimize Microsoft Azure area fisicamente supportata.

3. Se è possibile migliorare hardware hello (ad esempio, tooSSD HDD), controllare il toodetermine caratteristiche di archiviazione locale.

4. Modificare anche le impostazioni di Site Recovery hello nel server di elaborazione hello[aumentare hello quantità larghezza di banda utilizzata per la replica](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Se si esegue lo strumento hello in un server di configurazione o di un server di elaborazione che già dispone di macchine virtuali protetti, eseguire lo strumento hello più volte. Hello ottenuta cambia il numero di velocità effettiva a seconda della quantità di hello di varianza elaborata a questo punto nel tempo.

Per tutte le distribuzioni aziendali di Site Recovery è consigliabile usare [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Account di archiviazione necessari
Hello seguente grafico Mostra numero totale di hello di archiviazione di account (standard e premium) che sono necessari tooprotect tutti hello macchine virtuali compatibili. toolearn dello storage account toouse per ogni macchina virtuale, nella sezione hello "posizione di archiviazione di macchine Virtuali".

![Account di archiviazione richiesto nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Numero di core Azure necessari
Questo risultato è hello totale dei core toobe impostare prima hello di failover o test failover di tutte le macchine virtuali compatibili. Se sono disponibili nella sottoscrizione hello core insufficiente, il ripristino del sito non riesce macchine virtuali toocreate in fase di hello di failover o il failover di test.

![Numero di core Azure nella pianificazione della distribuzione hello richiesto](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Infrastruttura locale necessaria
Questa figura è il numero totale di hello del server di configurazione e toobe server processo aggiuntivo configurato che basterebbe tooprotect tutti hello macchine virtuali compatibili. A seconda di hello supportato [dimensioni indicazioni per il server di configurazione di hello](https://aka.ms/asr-v2a-on-prem-components), strumento hello potrebbe essere consigliabile server aggiuntivi. Hello raccomandazione si basa su hello più grande di varianza al giorno hello o numero massimo di hello di macchine virtuali protette (supponendo una media di tre dischi per ogni macchina virtuale), a seconda del valore viene raggiunto prima nel server di configurazione hello o il server di elaborazione aggiuntive di hello. Nella sezione "Input" hello, sono disponibili dettagli hello di varianza totale per ogni giorno e il numero totale di dischi protetti.

![Infrastruttura locale necessari nella pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Analisi di simulazione
Questa analisi viene quanti la violazione può verificarsi durante la profilatura quando si imposta periodo hello che una larghezza di banda inferiore per hello desiderato RPO toobe soddisfatta solo il 90% di tempo hello. Possono verificarsi una o più violazioni del valore RPO in un giorno. grafico di Hello Mostra punta hello RPO del giorno hello.
In base a questa analisi, è possibile decidere se è accettabile con numero di hello di violazioni di RPO in tutti i giorni e punta RPO raggiunto al giorno hello specificato della larghezza di banda inferiore. Se è accettabile, è possibile allocare larghezza di banda inferiore hello per la replica, in caso contrario allocare hello maggiore larghezza di banda desiderato toomeet suggeriti hello RPO 100% del tempo di hello.

![L'analisi di simulazione in pianificazione della distribuzione hello](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Dimensioni raccomandate per i batch di VM per la replica iniziale
In questa sezione, è consigliabile numero hello di macchine virtuali che possono essere protetti in parallelo toocomplete hello la replica iniziale all'interno di 72 ore con hello suggerito toomeet della larghezza di banda desiderato RPO 100% del tempo di hello viene impostata. Questo valore è configurabile. toochange è in fase di generazione di report, utilizzare hello *GoalToCompleteIR* parametro.

grafico qui Hello Mostra un intervallo di valori di larghezza di banda e una calcolato VM batch dimensioni conteggio toocomplete la replica iniziale in 72 ore, basata sulla media hello rilevato VM hello di dimensioni in tutte le macchine virtuali compatibili.

In anteprima pubblica di hello, report hello non specifica le macchine virtuali devono essere inclusi in un batch. È possibile utilizzare dimensioni disco hello nella toofind sezione hello "VMs compatibile" dimensioni di ciascuna macchina virtuale e selezionarli per un batch oppure è possibile selezionare le macchine virtuali hello in base alle caratteristiche del carico di lavoro noti. tempo di completamento Hello delle modifiche della replica iniziale hello in proporzione, in base alle dimensioni del disco di macchina virtuale effettiva hello, utilizzato spazio su disco e la velocità effettiva di rete disponibile.

![Dimensioni raccomandate per i batch di VM](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Fattore di crescita e valori percentili usati
In questa sezione nella parte inferiore di hello di hello foglio valore percentile di hello viene utilizzato per tutti i contatori delle prestazioni di hello di macchine virtuali hello profilato (valore predefinito è 95 ° percentile) e hello fattore di crescita (valore predefinito è 30 percento) che viene utilizzata in tutti i calcoli di hello.

![Fattore di crescita e valori percentili usati](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Raccomandazioni con la larghezza di banda disponibile come input

![Raccomandazioni con la larghezza di banda disponibile come input](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Si possono verificare situazioni in cui non è possibile impostare una larghezza di banda oltre un dato valore di Mbps per la replica di Site Recovery. lo strumento Hello consente tooinput di larghezza di banda disponibile (utilizzando hello - parametro larghezza di banda durante la generazione di report) e ottenere hello raggiungibile RPO in minuti. Con questo valore RPO raggiungibile, è possibile decidere se è necessario tooset di larghezza di banda aggiuntiva o si OK con presenza di una soluzione di ripristino di emergenza con questo RPO.

![Valore RPO ottenibile per 500 Mbps di larghezza di banda](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Input
foglio di lavoro di Input Hello fornisce che una panoramica di hello profilato ambiente VMware.

![Panoramica di hello profilato ambiente VMware](./media/site-recovery-deployment-planner/Input.png)

**Data di inizio** e **data di fine**: hello date di inizio e fine di hello considerati per la generazione di report di dati di profilatura. Per impostazione predefinita, la data di inizio hello è data hello profilatura inizio, e data di fine hello è hello data dell'ultima analisi. Se viene generato il report di hello con questi parametri può essere hello 'StartDate' e 'EndDate' valori.

**Numero totale di giorni di profilatura**: numero totale di hello dei giorni della profilatura tra hello iniziare e terminare le date per cui hello è generato report.

**Numero di macchine virtuali compatibili**: numero totale di hello di macchine virtuali compatibili per larghezza di banda di rete quali hello necessario, numero necessario di archiviazione di account, Core di Microsoft Azure, i server di configurazione e i server di elaborazione aggiuntive sono calcolato.

**Numero totale dei dischi tra tutte le macchine virtuali compatibili**: numero di hello che viene utilizzato come uno dei hello input toodecide hello numerosi server di configurazione e toobe server processo aggiuntivo nella distribuzione di hello.

**Numero medio dei dischi per ogni macchina virtuale compatibili**: numero medio di hello di dischi calcolata in tutte le macchine virtuali compatibili.

**Dimensioni del disco (GB) di Media**: calcolare le dimensioni di hello media tra tutte le macchine virtuali compatibili.

**Desired RPO (minuti)**: hello predefinito ripristino punto obiettivo hello valore o è passato per il parametro 'DesiredRPO' hello in fase di hello di tooestimate di generazione di report necessarie della larghezza di banda.

**Larghezza di banda (Mbps) desiderato**: hello valore passato per il parametro 'Larghezza di banda' hello in fase di hello di tooestimate di generazione report RPO raggiungibile.

**Varianza dei dati tipico osservato al giorno (GB)**: varianza dei dati Media hello osservati in analisi di tutti i giorni. Questo numero viene utilizzato come uno del numero di hello input toodecide hello del server di configurazione e toobe server processo aggiuntivo nella distribuzione di hello.


## <a name="vm-storage-placement"></a>Selezione host di archiviazione delle VM

![Selezione host di archiviazione delle VM](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Tipo di archiviazione del disco**: entrambi un account di archiviazione standard o premium, che è usato tooreplicate tutti hello macchine virtuali corrispondenti in hello **tooPlace macchine virtuali** colonna.

**Prefisso suggerito**: hello tre caratteri prefisso che può essere utilizzato per la denominazione di account di archiviazione hello. È possibile usare il propria prefisso, ma i suggerimenti dello strumento hello segue hello [convenzione di denominazione per gli account di archiviazione di partizione](https://aka.ms/storage-performance-checklist).

**Suggerito il nome di Account**: nome dell'account di archiviazione hello dopo aver incluso prefisso hello. Sostituire hello nome tra parentesi angolari hello (< e >) con l'input dell'utente personalizzato.

**Account di archiviazione di log**: tutti i log di replica hello vengono archiviati in un account di archiviazione standard. Per le macchine virtuali che eseguono la replica tooa account di archiviazione premium, impostare un account di archiviazione standard aggiuntivi per l'archiviazione dei log. Un singolo account di archiviazione log Standard può essere usato da più account di archiviazione di replica Premium. Le macchine virtuali che vengono replicati toostandard archiviazione account utilizzare hello stesso account di archiviazione per i log.

**Suggerito il nome di Account Log**: il nome dell'account archiviazione log dopo aver incluso prefisso hello. Sostituire hello nome tra parentesi angolari hello (< e >) con l'input dell'utente personalizzato.

**Riepilogo di posizionamento**: un riepilogo di hello totale carico delle macchine virtuali nell'account di archiviazione hello in fase di hello di replica e failover o il failover di test. Include il numero totale di hello di macchine virtuali toohello con mapping account di archiviazione totale di lettura/scrittura IOPS tra tutte le macchine virtuali viene inserite in questo account di archiviazione totale scrittura dischi (replica) IOPS, dimensioni di setup totale in tutti e il numero totale dei dischi.

**Macchine virtuali tooPlace**: un elenco di tutte le macchine virtuali che devono essere posizionate in hello specificato account di archiviazione per ottenere prestazioni ottimali e l'utilizzo di hello.

## <a name="compatible-vms"></a>VM compatibili
![Foglio di calcolo di Excel delle VM compatibili](./media/site-recovery-deployment-planner/compatible-vms.png)

**Nome della macchina virtuale**: hello nome della macchina virtuale o l'indirizzo IP utilizzato in hello VMListFile quando viene generato un report. Questa colonna elenca anche i dischi di hello (VMDK) che sono le macchine virtuali toohello associata. vCenter toodistinguish macchine virtuali con nomi duplicati o indirizzi IP, nomi di hello includono il nome host ESXi hello. Hello host ESXi elencati è hello uno in hello macchina virtuale è stata inserita quando lo strumento hello individuati durante la profilatura periodo hello.

**VM Compatibility** (Compatibilità VM): i valori sono **Yes** e **Yes**\*. **Sì** \* è per le istanze in cui hello VM è un adattamento per [archiviazione Premium di Azure](https://aka.ms/premium-storage-workload). In questo caso, hello profilato elevata varianza o disco IOPS adatta hello P20 o P30 categoria, ma dimensioni hello del disco hello provoca toobe mappato tooa P10 o P20 verso il basso. account di archiviazione Hello decide quale disco di archiviazione premium digitare toomap un disco, in base alla dimensione. ad esempio:
* <128 GB rientrano nella categoria P10.
* 128 GB too512 GB è una P20.
* 512 GB too1024 GB è una P30.
* 1025 GB too2048 GB è una P40.
* 2049 GB too4095 GB è una P50.

Se le caratteristiche del carico di lavoro hello di un disco inserirlo in hello P20 o P30 categoria, ma dimensioni hello ne esegue il mapping a discesa tipo di tooa inferiore premium archiviazione su disco, lo strumento hello contrassegna tale macchina virtuale come **Sì**\*. strumento Hello consiglia inoltre di modificare hello origine disco dimensioni toofit in hello consigliato di tipo di disco di archiviazione premium o modificare hello destinazione disco tipo dopo il failover.

**Storage Type** (Tipo di archiviazione): Standard o Premium.

**Prefisso suggerito**: il prefisso di account di archiviazione di tre caratteri hello.

**Account di archiviazione**: nome hello che usa il prefisso di account di archiviazione suggeriti hello.

**IOPS di lettura/scrittura (con il fattore di crescita)**: hello picco del carico di lavoro lettura/scrittura IOPS su disco hello (valore predefinito è 95 ° percentile), tra cui il fattore di crescita futura hello (valore predefinito è 30 percento). Si noti che hello lettura/scrittura totale di IOPS di una macchina virtuale non sono sempre somma hello di lettura/scrittura di singoli dischi hello della macchina virtuale IOPS, poiché hello punta lettura/scrittura IOPS di hello VM punta hello della somma hello dei relativi singoli dischi lettura/scrittura IOPS ogni minuto di hello periodo di profilatura.

**Varianza dei dati in Mbps (con il fattore di crescita)**: frequenza di varianza hello massimo su disco hello (valore predefinito è 95 ° percentile), tra cui il fattore di crescita futura hello (valore predefinito è 30 percento). Si noti che hello varianza totale dei dati di hello VM non è sempre somma hello di varianza dei dati dei dischi singoli hello della macchina virtuale, perché varianza dei dati hello picco di hello VM è punta hello somma hello di varianza dei relativi singoli dischi ogni minuto di hello profilatura periodo.

**Dimensioni VM di Azure**: hello ideale eseguito il mapping di dimensioni di macchina virtuale di servizi Cloud di Azure per questo locali di macchina virtuale. mapping di Hello basato sulla memoria della macchina virtuale di hello on-premise, numero di dischi/core/NIC e IOPS di lettura/scrittura. indicazione di Hello è sempre dimensioni delle macchine Virtuali di Azure più bassa hello che corrisponde a tutte le caratteristiche di macchina virtuale locale hello.

**Numero di dischi**: hello totale dei dischi della macchina virtuale (VMDK) su hello macchina virtuale.

**Dimensioni (GB) del disco**: hello dimensioni di setup totale di tutti i dischi di VM hello. lo strumento di Hello Mostra anche dimensioni del disco per i singoli dischi hello hello in hello macchina virtuale.

**Core**: hello numero di core CPU in hello macchina virtuale.

**Memoria (MB)**: hello RAM su hello macchina virtuale.

**Le schede NIC**: numero di schede di rete nella macchina virtuale hello hello.

**Tipo di avvio**: è il tipo di avvio di hello macchina virtuale. Può essere BIOS o EFI. Azure Site Recovery supporta attualmente solo il tipo di avvio BIOS. Tutte le macchine virtuali hello del tipo di avvio EFI sono elencate nel foglio di lavoro di macchine virtuali non compatibile.

**Tipo di sistema operativo**: hello è il tipo di sistema operativo della macchina virtuale hello. Può essere Windows, Linux o altro.

## <a name="incompatible-vms"></a>VM incompatibili

![Foglio di calcolo di Excel delle VM incompatibili](./media/site-recovery-deployment-planner/incompatible-vms.png)

**Nome della macchina virtuale**: hello nome della macchina virtuale o l'indirizzo IP utilizzato in hello VMListFile quando viene generato un report. Questa colonna elenca anche VMDK hello che sono le macchine virtuali toohello associata. vCenter toodistinguish macchine virtuali con nomi duplicati o indirizzi IP, nomi di hello includono il nome host ESXi hello. Hello host ESXi elencati è hello uno in hello macchina virtuale è stata inserita quando lo strumento hello individuati durante la profilatura periodo hello.

**Compatibilità di VM**: indica perché non è compatibile per l'utilizzo con il ripristino del sito hello dato macchina virtuale. Hello motivi vengono descritti per ogni disco incompatibile di hello VM e, in base nella pubblicazione [limiti di archiviazione](https://aka.ms/azure-storage-scalbility-performance), può essere una delle seguenti operazioni hello:

* Dimensioni disco superiori a 4095 GB. Archiviazione di Azure attualmente non supporta dischi dati di dimensioni superiori a 4095 GB.
* Disco del sistema operativo superiore a 2048 GB. Archiviazione di Azure attualmente non supporta dischi del sistema operativo di dimensioni superiori a 2048 GB.
* Il tipo di avvio è EFI. Azure Site Recovery supporta attualmente solo macchine virtuali con tipo di avvio BIOS.

* Totale dimensioni della macchina virtuale (replica + TFO) superano limite di dimensioni di account di archiviazione di hello è supportato (35 TB). Questo problema di incompatibilità si verifica in genere quando un singolo disco hello VM presenta una caratteristica di prestazioni che supera hello Azure o il ripristino del sito i limiti massimi supportati per l'archiviazione standard. Tale istanza inserisce hello VM nell'area di archiviazione premium hello. Tuttavia, non è possibile proteggere hello massimo supportato di dimensioni di un account di archiviazione premium sono 35 TB e protetto di una singola macchina virtuale tra più account di archiviazione. Si noti inoltre che quando un failover di test viene eseguito su una macchina virtuale protetta, viene eseguito in hello stesso account di archiviazione in cui è in corso la replica. In questo caso, impostare 2x dimensioni hello del disco di hello per replica tooprogress e toosucceed di failover di test in parallelo.
* Le operazioni di I/O al secondo di origine superano il limite supportato di archiviazione di 5000 operazioni per ogni disco.
* Le operazioni di I/O al secondo di origine superano il limite supportato di archiviazione di 80.000 operazioni per ogni VM.
* Varianza dei dati Media supera supportato il ripristino del sito varianza del limite di 10 MBps per la dimensione media i/o per il disco di hello.
* Varianza totale dei dati tra tutti i dischi sulla VM hello hello massimo supportato il ripristino del sito varianza eccede il limite stabilito di 54 MBps per ogni macchina virtuale.
* Medio scrittura efficace IOPS supera limite di IOPS di ripristino del sito di hello supportato di 840 per disco.
* Archiviazione dello snapshot calcolato superato limite di archiviazione di snapshot di hello supportato di 10 TB.

**IOPS di lettura/scrittura (con il fattore di crescita)**: il carico di picco hello IOPS su disco hello (valore predefinito è 95 ° percentile), tra cui il fattore di crescita futura hello (valore predefinito è 30 percento). Si noti che hello lettura/scrittura totale di IOPS di hello VM non sono sempre somma hello di lettura/scrittura di singoli dischi hello della macchina virtuale IOPS, poiché hello punta lettura/scrittura IOPS di hello VM punta hello della somma hello dei relativi singoli dischi lettura/scrittura IOPS ogni minuto di hello periodo di profilatura.

**Varianza dei dati in Mbps (con il fattore di crescita)**: frequenza di varianza hello massimo su disco hello (95 ° percentile predefinito) tra il fattore di crescita futura hello (valore predefinito 30 percento). Si noti che hello varianza totale dei dati di hello VM non è sempre somma hello di varianza dei dati dei dischi singoli hello della macchina virtuale, perché varianza dei dati hello picco di hello VM è punta hello somma hello di varianza dei relativi singoli dischi ogni minuto di hello profilatura periodo.

**Numero di dischi**: numero totale di VMDK su hello VM hello.

**Dimensioni (GB) del disco**: hello dimensioni di setup totale di tutti i dischi di VM hello. lo strumento di Hello Mostra anche dimensioni del disco per i singoli dischi hello hello in hello macchina virtuale.

**Core**: hello numero di core CPU in hello macchina virtuale.

**Memoria (MB)**: quantità hello di RAM hello macchina virtuale.

**Le schede NIC**: numero di schede di rete nella macchina virtuale hello hello.

**Tipo di avvio**: è il tipo di avvio di hello macchina virtuale. Può essere BIOS o EFI. Azure Site Recovery supporta attualmente solo il tipo di avvio BIOS. Tutte le macchine virtuali hello del tipo di avvio EFI sono elencate nel foglio di lavoro di macchine virtuali non compatibile.

**Tipo di sistema operativo**: hello è il tipo di sistema operativo della macchina virtuale hello. Può essere Windows, Linux o altro.


## <a name="site-recovery-limits"></a>Limiti relativi a Site Recovery

**Destinazione archiviazione di replica** | **Dimensioni medie I/O disco di origine** |**Varianza dati media disco di origine** | **Varianza dati totale giornaliera disco di origine**
---|---|---|---
Archiviazione standard | 8 KB | 2 MBps | 168 GB per disco
Premium, disco P10 | 8 KB | 2 MBps | 168 GB per disco
Premium, disco P10 | 16 KB | 4 MBps | 336 GB per disco
Premium, disco P10 | 32 KB o superiori | 8 MBps | 672 GB per disco
Disco P20 o P30 Premium | 8 KB  | 5 MBps | 421 GB per disco
Disco P20 o P30 Premium | 16 KB o superiori |10 MBps | 842 GB per disco

Si tratta di numeri medi presupponendo una sovrapposizione I/O del 30%. Site Recovery può gestire una velocità effettiva maggiore in base alla percentuale di sovrapposizione, alle dimensioni di scrittura maggiori e all'effettivo I/O del carico di lavoro. Hello numeri precedenti si presuppongono un backlog tipico di circa cinque minuti. ovvero i dati, dopo essere stati caricati, verranno elaborati e verrà creato un punto di ripristino entro cinque minuti.

Questi limiti si basano su test di Microsoft, ma non possono coprire tutte le possibili combinazioni di I/O delle applicazioni. I risultati effettivi possono variare in base alla combinazione di I/O delle applicazioni. Per ottenere risultati ottimali, anche dopo la pianificazione della distribuzione, è sempre consigliabile eseguire test tramite un'immagine di test failover tooget hello prestazioni dell'applicazione completo.

## <a name="updating-hello-deployment-planner"></a>Pianificazione della distribuzione di aggiornamento hello
pianificazione della distribuzione di hello tooupdate, hello seguenti:

1. Scaricare una versione più recente di hello di hello [pianificazione della distribuzione di Azure Site Recovery](https://aka.ms/asr-deployment-planner).

2. Copia hello ZIP tooa server di cartelle che si desidera toorun sul.

3. Estrarre la cartella con estensione zip hello.

4. Effettuare una delle seguenti hello:
 * Se la versione più recente di hello non contiene una correzione di profilatura, profilatura è già in corso della versione corrente di pianificazione hello continuare la profilatura hello.
 * Se la versione più recente di hello contiene una correzione di profilatura, si consiglia di interrompere la profilatura della versione corrente e riavviare la profilatura hello con la nuova versione di hello.

  >[!NOTE]
  >
  >Quando si avvia la profilatura con hello nuova versione, passaggio hello che stesso percorso della directory di output in modo che hello strumento aggiunge dati di profilo in hello file esistenti. Un set completo di dati analizzati sarà utilizzato toogenerate hello report. Se si passa una directory di output diversi, vengono creati nuovi file e dati di profilatura precedente non viene utilizzato il report di hello toogenerate.
  >
  >Ogni nuova pianificazione di distribuzione è un aggiornamento cumulativo del file con estensione zip hello. Non è necessario toocopy hello più recenti toohello precedente cartella dei file. È possibile creare e usare una nuova cartella.


## <a name="version-history"></a>Cronologia delle versioni

### <a name="131"></a>1.3.1
Ultimo aggiornamento: 19 luglio 2017

È stata aggiunta la nuova funzionalità seguente:

* Aggiunta del supporto per dischi di dimensioni superiori a 1 TB nella generazione di report. Ora è possibile utilizzare la replica tooplan di pianificazione della distribuzione per le macchine virtuali che hanno dimensioni disco maggiore di 1 TB (fino a 4095 GB).
Per altre informazioni, vedere il post di blog sul [supporto di dischi di grandi dimensioni in Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/).


### <a name="13"></a>1.3
Ultimo aggiornamento: 9 maggio 2017

È stata aggiunta la nuova funzionalità seguente:

* Aggiunta del supporto di dischi gestiti nella generazione di report. Hello numero di macchine virtuali può essere inserito tooa di archiviazione singolo account viene calcolata in base se gestiti disco è selezionata per il Failover o Test failover.        


### <a name="12"></a>1.2
Ultimo aggiornamento: 7 aprile 2017

Sono state aggiunte le correzioni seguenti:

* Avvio aggiunta digitare check (BIOS o EFI) per ogni macchina virtuale di toodetermine se macchina virtuale hello è compatibile per la protezione di hello.
* Aggiunta del sistema operativo digitare le informazioni per ogni macchina virtuale in macchine virtuali compatibili hello e fogli di lavoro di macchine virtuali non compatibile.
* operazione GetThroughput Hello è ora supportato in aree di hello governo e Cina Microsoft Azure.
* Aggiunte alcune altre verifiche dei prerequisiti per server vCenter ed ESXi.
* Recupero di generazione del report non corretto quando le impostazioni locali è impostato toonon in lingua inglese.


### <a name="11"></a>1.1
Ultimo aggiornamento: 9 marzo 2017

Hello i seguenti problemi:

* strumento Hello non è possibile profilare le macchine virtuali se vCenter hello dispone di due o più macchine virtuali con hello stesso nome o indirizzo IP tra vari host ESXi.
* Copia e la ricerca è disabilitato per i fogli di lavoro hello compatibile macchine virtuali e macchine virtuali non compatibile.

### <a name="10"></a>1.0
Ultimo aggiornamento: 23 febbraio 2017

Pianificazione della distribuzione di ripristino del sito pubblica anteprima di Azure 1.0 offre i seguenti di hello (toobe risolti negli aggiornamenti futuri) problemi noti:

* strumento di Hello funziona solo per gli scenari di VMware in Azure, non per le distribuzioni di Hyper-V in Azure. Per gli scenari di Hyper-V in Azure, utilizzare hello [dello strumento di pianificazione della capacità di Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Hello GetThroughput operazione non è supportata nelle aree di hello governo e Cina Microsoft Azure.
* strumento Hello non è possibile profilare le macchine virtuali se il server vCenter hello dispone di due o più macchine virtuali con hello stesso nome o indirizzo IP tra vari host ESXi. In questa versione, lo strumento hello ignora la profilatura per i nomi di macchina virtuale duplicati o indirizzi IP in hello VMListFile. soluzione alternativa Hello è tooprofile hello macchine virtuali tramite un host ESXi anziché server vCenter hello. È necessario eseguire una sola istanza per ogni host ESXi.
