---
title: i nodi del cluster HPC Pack aaaAutoscale | Documenti Microsoft
description: Automaticamente aumentare e ridurre il numero di hello dei nodi di calcolo cluster HPC Pack in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Aumentare e ridurre le risorse di cluster HPC Pack hello in Azure in base a carico di lavoro cluster toohello automaticamente
Se si distribuiscono nodi di "Potenziamento" di Azure nel cluster HPC Pack o si crea un cluster HPC Pack nelle macchine virtuali di Azure, è possibile aumentare o ridurre le risorse cluster hello, ad esempio nodi o core in base al carico di lavoro hello in cluster hello automaticamente. Scalabilità delle risorse cluster hello in questo modo consente toouse le risorse di Azure in modo più efficiente e controllare i costi.

Questo articolo illustra due modalità di HPC Pack fornisce le risorse di calcolo tooautoscale:

* proprietà del cluster HPC Pack Hello **AutoGrowShrink**

* Hello **AzureAutoGrowShrink.ps1** script di HPC PowerShell

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Attualmente è possibile solo aumentare e ridurre automaticamente i nodi di calcolo HPC Pack che eseguono un sistema operativo Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Impostare la proprietà di hello AutoGrowShrink cluster
### <a name="prerequisites"></a>Prerequisiti

* **HPC Pack 2012 R2 Update 2 o versioni successive cluster** -nodo head del cluster hello può essere distribuito in locale o in una macchina virtuale di Azure. Vedere [configurazione di un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget avviato con un nodo head locale e i nodi di "Potenziamento" di Azure. Vedere hello [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly distribuire un cluster HPC Pack nelle macchine virtuali di Azure.

* **Per un cluster con un nodo head in Azure (modello di distribuzione di Resource Manager)**: a partire da HPC Pack 2016, l'autenticazione del certificato in un'applicazione Azure Active Directory viene usata per aumentare o ridurre automaticamente le macchine virtuali del cluster distribuite tramite Azure Resource Manager. Configurare un certificato come segue:

  1. Dopo la distribuzione di cluster, la connessione dal nodo head tooone di Desktop remoto.

  2. Caricamento del nodo head di hello certificato (in formato PFX con la chiave privata) tooeach e installare tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.

  3. Avviare PowerShell di Azure come amministratore ed eseguire hello seguenti comandi in un nodo head:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Se l'account è in più di un tenant di Azure Active Directory o di sottoscrizione di Azure, è possibile eseguire l'esempio hello tooselect hello corretto tenant e una sottoscrizione di comando:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Eseguire hello successivo comando tooview hello selezionato tenant e sottoscrizione:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Eseguire lo script seguente hello

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    dove

    **DisplayName**: nome visualizzato dell'applicazione Azure Active. Se un'applicazione hello non esiste, viene creato in Azure Active Directory.

    **Home page** -hello home page di un'applicazione hello. È possibile configurare un URL fittizi, come hello sopra riportato.

    **IdentifierUri** -identificatore dell'applicazione hello. È possibile configurare un URL fittizi, come hello sopra riportato.

    **CertificateThumbprint** -identificazione personale del certificato hello installato nel nodo head di hello nel passaggio 1.

    **TenantId**: ID tenant di Azure Active Directory. È possibile ottenere l'ID Tenant hello dal portale di Azure Active Directory hello **proprietà** pagina.

    Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Per un cluster con un nodo head in Azure (modello di distribuzione classica)** : se si utilizza del cluster di hello toocreate script distribuzione IaaS di HPC Pack hello in hello classico modello di distribuzione, abilitare hello **AutoGrowShrink** cluster proprietà impostando l'opzione AutoGrowShrink hello nel file di configurazione del cluster hello. Per informazioni dettagliate, vedere la documentazione di hello che accompagna hello [download dello script](https://www.microsoft.com/download/details.aspx?id=44949).

    In alternativa, abilitare hello **AutoGrowShrink** proprietà cluster dopo la distribuzione di cluster hello utilizzando HPC PowerShell i comandi descritti nella seguente sezione hello. tooprepare per questo, primo hello completo seguendo i passaggi:

  1. Configurare un certificato di gestione di Azure nel nodo head hello e in hello sottoscrizione di Azure. Per una distribuzione di test, è possibile usare hello predefinito Microsoft HPC Azure certificato autofirmato che consente di installare HPC Pack nel nodo head hello e quindi caricare tale tooyour certificato sottoscrizione di Azure. Per le opzioni e procedure, vedere hello [linee guida della libreria TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Eseguire **regedit** nel nodo head hello passare tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e aggiungere un valore stringa. Impostare il nome di valore hello troppo "Identificazione personale" e l'identificazione personale toohello di dati di valore del certificato hello nel passaggio 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Proprietà di HPC PowerShell commands tooset hello AutoGrowShrink
Di seguito sono tooset i comandi di PowerShell HPC esempio **AutoGrowShrink** tootune e il comportamento di altri parametri. Vedere [AutoGrowShrink parametri](#AutoGrowShrink-parameters) più avanti in questo articolo per l'elenco completo di hello delle impostazioni.

toorun questi comandi, avviare PowerShell HPC nel nodo head del cluster hello come amministratore.

**hello tooenable AutoGrowShrink proprietà**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**hello toodisable AutoGrowShrink proprietà**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**hello toochange aumentare l'intervallo in minuti**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**hello toochange ridurre l'intervallo in minuti**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**configurazione corrente di hello tooview di AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**gruppi di nodi tooexclude da AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Questo parametro è supportato a partire da HPC Pack 2016
>

### <a name="autogrowshrink-parameters"></a>Parametri di AutoGrowShrink 
di seguito Hello sono AutoGrowShrink parametri che è possibile modificare tramite hello **Set HpcClusterProperty** comando.

* **EnableGrowShrink** : passare tooenable o disabilitare hello **AutoGrowShrink** proprietà.
* **ParamSweepTasksPerCore** -numero di sweep parametrico attività toogrow uno dei core. valore predefinito di Hello è toogrow un core per ogni attività.

  > [!NOTE]
  > Modifiche di HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** troppo**TasksPerResourceUnit**. È basato sul tipo di risorsa di processo hello e può essere nodo, socket o core.
  >
  >
* **GrowThreshold** -soglia di attività in coda tootrigger aumento automatico delle dimensioni. valore predefinito di Hello è 1, che significa che se sono presenti 1 o più attività in hello in coda, aumenta automaticamente i nodi.
* **GrowInterval** -intervallo in minuti tootrigger aumento automatico delle dimensioni. intervallo di Hello predefinito è 5 minuti.
* **ShrinkInterval** -intervallo in minuti tootrigger la compattazione automatica. intervallo di Hello predefinito è 5 minuti. |
* **ShrinkIdleTimes** -numero di controlli continua tooshrink tooindicate hello nodi è inattivo. valore predefinito di Hello è pari a 3 volte. Ad esempio, se hello **ShrinkInterval** è 5 minuti, HPC Pack controlla se il nodo hello è inattivo ogni 5 minuti. Se i nodi di hello sono in stato di inattività hello dopo 3 continua controlla (15 minuti), HPC Pack compatta tale nodo.
* **ExtraNodesGrowRatio** -percentuale aggiuntiva di toogrow nodi per i processi di interfaccia MPI (Message Passing). valore predefinito di Hello è 1, il che significa che HPC Pack aumenta nodi % 1 per i processi MPI.
* **GrowByMin** -Switch tooindicate se il criterio di aumento automatico delle dimensioni hello si basa su risorse di hello minime necessarie per il processo di hello. valore predefinito di Hello è false, il che significa che HPC Pack aumenta i nodi per i processi in base alle risorse di hello massimo richiesto per i processi di hello.
* **SoaJobGrowThreshold** -soglia di arrivo SOA richieste tootrigger hello automatico aumento delle dimensioni di processo. valore predefinito di Hello è 50000.

  > [!NOTE]
  > Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** -numero di SOA in ingresso richieste toogrow uno dei core. valore predefinito di Hello è 20000.

  > [!NOTE]
  > Questo parametro è supportato a partire da HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** : i nodi in hello specificati gruppi di nodi non automaticamente aumentare e ridurre.
  
  > [!NOTE]
  > Questo parametro è supportato a partire da HPC Pack 2016.
  >

### <a name="mpi-example"></a>Esempio MPI
Per impostazione predefinita HPC Pack aumenta di 1% nodi aggiuntivi per i processi MPI (**ExtraNodesGrowRatio** è impostato too1). motivo di Hello è MPI potrebbe richiedere più nodi che il processo di hello può essere eseguito solo quando tutti i nodi sono pronti. Quando Azure avvia nodi, in alcuni casi un nodo potrebbe essere necessario più tempo toostart rispetto ad altri, causando toobe altri nodi inattivo durante l'attesa di tale nodo tooget pronto. Aumentando i nodi supplementari, HPC Pack riduce il tempo di attesa delle risorse, riducendo potenzialmente i costi. percentuale di hello tooincrease di nodi aggiuntivi per i processi MPI (ad esempio, % too10), eseguire un comando simile a

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Esempio SOA
Per impostazione predefinita, **SoaJobGrowThreshold** è impostato too50000 e **SoaRequestsPerCore** è impostato too200000. Se si invia un processo SOA con 70000 richieste, ci sarà una sola attività in coda e le richieste in ingresso saranno 70000. In questo caso HPC Pack aumenta 1 core per hello in coda attività e per le richieste in ingresso, aumento delle dimensioni (70000 50000) / core 20000 = 1, in totale aumenta 2 core per questo processo SOA.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Eseguire script AzureAutoGrowShrink.ps1 hello
### <a name="prerequisites"></a>Prerequisiti

* **HPC Pack 2012 R2 Update 1 o versioni successive cluster** : hello **AzureAutoGrowShrink.ps1** script viene installato nella cartella di hello % CCP_HOME % bin. nodo head del cluster Hello può essere distribuito in locale o in una macchina virtuale di Azure. Vedere [configurazione di un cluster ibrido con HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget avviato con un nodo head locale e i nodi di "Potenziamento" di Azure. Vedere hello [script di distribuzione IaaS di HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly distribuire un cluster HPC Pack nelle macchine virtuali di Azure oppure usare un [modello di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **Azure PowerShell 1.4.0** -script hello attualmente dipende da questa versione specifica di Azure PowerShell.
* **Per un cluster con Azure burst nodi** -Esegui script hello in un computer client in cui è installato HPC Pack o nel nodo head hello. Se in esecuzione in un computer client, assicurarsi di impostare hello variabile $env: nodo head di CCP_SCHEDULER toopoint toohello. i nodi di Azure "potenziamento" Hello devono essere aggiunte toohello cluster, ma possono risultare non distribuiti hello.
* **Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione di gestione delle risorse)** -per un cluster di macchine virtuali di Azure distribuite nel modello di distribuzione di gestione risorse di hello, script hello supporta due metodi per l'autenticazione di Azure: Accedi tooyour account Azure script hello toorun ogni ora (eseguendo `Login-AzureRmAccount`, o configurare un tooauthenticate dell'entità servizio con un certificato. HPC Pack fornisce script hello **ConfigARMAutoGrowShrinkCert.ps** toocreate un'entità servizio con certificato. script Hello crea un'applicazione Azure Active Directory (Azure AD) e un'entità servizio e assegna l'entità di servizio toohello ruolo Collaboratore hello. script di hello toorun, avviare Azure PowerShell come amministratore ed eseguire hello seguenti comandi:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Per altre informazioni su **ConfigARMAutoGrowShrinkCert.ps1**, eseguire `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.

* **Per un cluster distribuito in macchine virtuali di Azure (modello di distribuzione classica)** -Esegui script hello nel nodo head hello macchina virtuale, perché dipende da hello **Start-hpciaasnode.ps1** e **Stop-hpciaasnode.ps1**script che vi sono installati. Per questi script è inoltre necessario un certificato di gestione di Azure o un file delle impostazioni di pubblicazione (vedere [Gestire i nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster-node-manage.md)). Verificare che hello tutte le macchine virtuali è necessario del nodo sono già state aggiunte toohello cluster di calcolo. Possono essere nello stato Stopped hello.



### <a name="syntax"></a>Sintassi
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>parameters
* **NodeTemplates** -i nomi di hello nodo modelli toodefine hello ambito per toogrow nodi hello e compatta. Se non specificato (valore predefinito di hello è @()), tutti i nodi hello **AzureNodes** gruppo di nodi sono nell'ambito quando **NodeType** ha un valore di AzureNodes e tutti i nodi in hello **ComputeNodes** gruppo di nodi sono nell'ambito quando **NodeType** ha un valore di ComputeNodes.
* **Le entità Jobtemplate** -processo di nomi di hello modelli toodefine hello ambito toogrow nodi hello.
* **Tipo di nodo** - tipo di nodo toogrow hello e compattazione. I valori supportati sono:

  * **AzureNodes** - Per i nodi di Azure PaaS (burst) in un cluster locale o IaaS di Azure.
  * **ComputeNodes** - Solo per le macchine virtuali dei nodi di calcolo in un cluster IaaS di Azure.

* **NumOfQueuedJobsPerNodeToGrow** -numero di processi in coda necessari toogrow un nodo.
* **NumOfQueuedJobsToGrowThreshold** -processo di aumento delle dimensioni hello soglia numero hello toostart processi in coda.
* **NumOfActiveQueuedTasksPerNodeToGrow** -numero di hello di attività attive in coda necessari toogrow un nodo. Se si specifica un valore maggiore di 0 per **NumOfQueuedJobsPerNodeToGrow** , questo parametro viene ignorato.
* **NumOfActiveQueuedTasksToGrowThreshold** -processo di aumento delle dimensioni hello soglia numero hello toostart attività attive in coda.
* **NumOfInitialNodesToGrow** : hello iniziale numero minimo di nodi toogrow se tutti i nodi di hello nell'ambito sono **non distribuiti** o **arrestato (deallocato)**.
* **GrowCheckIntervalMins** -intervallo hello in minuti tra i controlli toogrow.
* **ShrinkCheckIntervalMins** -intervallo hello in minuti tra i controlli tooshrink.
* **ShrinkCheckIdleTimes** -hello numero di controlli di riduzione continui (separati da **ShrinkCheckIntervalMins**) tooindicate hello nodi sono inattivi.
* **UseLastConfigurations** -hello configurazioni precedenti salvate nel file hello degli argomenti.
* **ArgFile**: nome di hello argomento file utilizzato toosave hello e hello configurazioni toorun hello script di aggiornamento.
* **LogFilePrefix** -hello prefisso del nome del file di log hello. È possibile specificare un percorso. Per impostazione predefinita il log di hello è scritto toohello directory di lavoro corrente.

### <a name="example-1"></a>Esempio 1
Hello seguente esempio mostra come configurare hello Azure burst nodi distribuiti con toogrow il modello AzureNode predefinito e la riduzione automatica. Se tutti i nodi sono inizialmente in hello **non distribuiti** stato, vengono avviati almeno 3 nodi. Se il numero di hello di processi in coda è superiore a 8, script hello avvia nodi fino a quando il numero supera il rapporto hello di processi in coda per **NumOfQueuedJobsPerNodeToGrow**. Se un nodo risulta inattivo in periodi di inattività consecutivi 3 toobe, viene arrestato.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Esempio 2
Hello seguente esempio mostra come configurare hello Azure distribuite con hello modello ComputeNode predefinito toogrow macchine virtuali del nodo di calcolo e la riduzione automatica.
processi di Hello configurati dal modello di processo predefinito di hello definiscono l'ambito di hello del carico di lavoro nel cluster hello. Se tutti i nodi di hello inizialmente vengono arrestati, vengono avviati almeno 5 nodi. Se il numero di hello di attività attive in coda è superiore a 15, script hello avvia nodi fino a quando il numero supera il rapporto di hello di attività attive in coda troppo**NumOfActiveQueuedTasksPerNodeToGrow**. Se un nodo risulta inattivo in 10 periodi di inattività consecutivi toobe, viene arrestato.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
