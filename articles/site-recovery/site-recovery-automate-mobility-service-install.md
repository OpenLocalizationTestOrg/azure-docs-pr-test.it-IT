---
title: "hello aaaDeploy servizio di mobilità di ripristino del sito con DSC di automazione di Azure | Documenti Microsoft"
description: "Viene descritto come toouse Automation DSC per Azure tooautomatically distribuire il servizio di mobilità di Azure Site Recovery hello e l'agente di Azure per la VM VMware e server fisico replica tooAzure"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="f1581-103">Distribuzione di servizio di mobilità hello con DSC di automazione di Azure per la replica della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f1581-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="f1581-104">In Operations Management Suite offriamo una soluzione completa per il backup e il ripristino di emergenza che può essere usata nell'ambito del piano di continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="f1581-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="f1581-105">Il percorso è iniziato da Hyper-V con la replica Hyper-V,</span><span class="sxs-lookup"><span data-stu-id="f1581-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="f1581-106">Ma abbiamo toosupport espanso un programma di installazione eterogenea poiché i clienti dispongono di più piattaforme e hypervisor nel cloud a loro.</span><span class="sxs-lookup"><span data-stu-id="f1581-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="f1581-107">Se si eseguono i carichi di lavoro di VMware e/o di server fisici oggi, un server di gestione esegue tutti di hello componenti di Azure Site Recovery nell'ambiente toohandle hello comunicazioni e i dati della replica con Azure, quando la destinazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="f1581-108">Distribuire il servizio di mobilità di ripristino del sito di hello tramite DSC di automazione</span><span class="sxs-lookup"><span data-stu-id="f1581-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="f1581-109">Per iniziare, è bene riepilogare le operazioni eseguite da questo server di gestione.</span><span class="sxs-lookup"><span data-stu-id="f1581-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="f1581-110">il server di gestione di Hello esegue diversi ruoli del server.</span><span class="sxs-lookup"><span data-stu-id="f1581-110">hello management server runs several server roles.</span></span> <span data-ttu-id="f1581-111">Uno di questi ruoli è la *configurazione*, che coordina la comunicazione e gestisce i processi di ripristino e replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="f1581-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="f1581-112">Inoltre, hello *processo* ruolo funge da gateway replica.</span><span class="sxs-lookup"><span data-stu-id="f1581-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="f1581-113">Questo ruolo riceve i dati di replica dai computer di origine protetta ottimizzata con la memorizzazione nella cache, la compressione e crittografia e lo invia tooan account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="f1581-114">Una delle funzioni hello per ruolo processo hello è anche un'installazione toopush macchine tooprotected del servizio di mobilità hello ed eseguire l'individuazione automatica delle macchine virtuali VMware.</span><span class="sxs-lookup"><span data-stu-id="f1581-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="f1581-115">Se è presente un failback da Azure, hello *destinazione master* ruolo gestirà i dati di replica hello come parte di questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="f1581-116">Per i computer protetti hello, si affidano hello *servizio di mobilità*.</span><span class="sxs-lookup"><span data-stu-id="f1581-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="f1581-117">Questo componente è tooevery distribuito machine (VM VMware o server fisico) che si desidera tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f1581-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="f1581-118">Scrive dati nel computer di hello acquisisce e li inoltra a server di gestione toohello (ruolo di processo).</span><span class="sxs-lookup"><span data-stu-id="f1581-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="f1581-119">Quando si gestiscono la continuità aziendale, è importante toounderstand i carichi di lavoro, l'infrastruttura e hello componenti coinvolti.</span><span class="sxs-lookup"><span data-stu-id="f1581-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="f1581-120">È quindi possibile soddisfare i requisiti di hello per l'obiettivo del tempo di ripristino (RTO) e un obiettivo del punto di ripristino (RPO).</span><span class="sxs-lookup"><span data-stu-id="f1581-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="f1581-121">In questo contesto, hello servizio di mobilità è tooensuring chiave che i carichi di lavoro siano protetti nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="f1581-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="f1581-122">Come possiamo garantire nel modo migliore che la configurazione sia affidabile e protetta usando alcuni componenti di Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="f1581-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="f1581-123">In questo articolo viene fornito un esempio di come è possibile utilizzare Azure Automation DSC Desired State Configuration (), insieme a Site Recovery, tooensure che:</span><span class="sxs-lookup"><span data-stu-id="f1581-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="f1581-124">il servizio di mobilità Hello e agente VM di Azure sono computer che eseguono Windows toohello distribuita che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f1581-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="f1581-125">servizio di mobilità Hello e agente VM di Azure sono sempre in esecuzione quando la destinazione di replica hello Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1581-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1581-126">Prerequisites</span></span>
* <span data-ttu-id="f1581-127">Un programma di installazione di repository toostore hello richiesto</span><span class="sxs-lookup"><span data-stu-id="f1581-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="f1581-128">Una passphrase tooregister di repository toostore hello richiesto con il server di gestione di hello</span><span class="sxs-lookup"><span data-stu-id="f1581-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="f1581-129">Per ogni server di gestione viene generata una passphrase univoca.</span><span class="sxs-lookup"><span data-stu-id="f1581-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="f1581-130">Se si intende toodeploy più server di gestione, è necessario tooensure tale hello passphrase viene archiviata nel file passphrase.txt hello corretto.</span><span class="sxs-lookup"><span data-stu-id="f1581-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="f1581-131">Windows Management Framework (WMF) 5.0 installato nei computer hello che si desidera tooenable per la protezione dati (un requisito per DSC di automazione)</span><span class="sxs-lookup"><span data-stu-id="f1581-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="f1581-132">Se si vuole toouse DSC per Windows macchine che dispongono di WMF 4.0 installato, vedere la sezione hello [DSC di utilizzo in ambienti disconnessi](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="f1581-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="f1581-133">il servizio di mobilità Hello può essere installato tramite riga di comando hello e accetta diversi argomenti.</span><span class="sxs-lookup"><span data-stu-id="f1581-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="f1581-134">Sono necessari i file binari hello toohave (dopo estrarli il programma di installazione) e archiviarli in una posizione in cui è possibile recuperare tramite una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="f1581-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="f1581-135">Passaggio 1: estrazione dei file binari</span><span class="sxs-lookup"><span data-stu-id="f1581-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="f1581-136">tooextract hello i file necessari per il programma di installazione, passare toohello seguenti directory nel server di gestione:</span><span class="sxs-lookup"><span data-stu-id="f1581-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="f1581-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="f1581-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="f1581-138">In questa cartella dovrebbe essere presente un file MSI denominato:</span><span class="sxs-lookup"><span data-stu-id="f1581-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="f1581-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="f1581-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="f1581-140">Utilizzare hello installer hello tooextract di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f1581-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="f1581-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="f1581-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="f1581-142">Selezionare tutti i file e li inviano tooa compressa (zip).</span><span class="sxs-lookup"><span data-stu-id="f1581-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="f1581-143">È ora i file binari hello che è necessario il programma di installazione di tooautomate hello del servizio di mobilità hello tramite DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="f1581-144">Passphrase</span><span class="sxs-lookup"><span data-stu-id="f1581-144">Passphrase</span></span>
<span data-ttu-id="f1581-145">Successivamente, è necessario toodetermine in cui si desidera tooplace questa cartella compressa.</span><span class="sxs-lookup"><span data-stu-id="f1581-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="f1581-146">È possibile utilizzare un account di archiviazione di Azure, come illustrato più avanti, toostore hello passphrase è necessario per l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="f1581-147">agente Hello verrà quindi registrato con il server di gestione hello come parte del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="f1581-148">passphrase Hello ottenuti quando è stato distribuito il server di gestione di hello può essere salvata i file di testo tooa come passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="f1581-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="f1581-149">Posizionare la cartella compressa hello sia hello passphrase in un contenitore dedicato in hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Percorso della cartella](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="f1581-151">Se si preferiscono tookeep questi file in una condivisione in rete, è possibile farlo.</span><span class="sxs-lookup"><span data-stu-id="f1581-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="f1581-152">È sufficiente tooensure che le risorse DSC hello che verrà utilizzato in un secondo momento può accedere e possono ottenere il programma di installazione di hello e la passphrase.</span><span class="sxs-lookup"><span data-stu-id="f1581-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="f1581-153">Passaggio 2: Creare una configurazione DSC hello</span><span class="sxs-lookup"><span data-stu-id="f1581-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="f1581-154">il programma di installazione di Hello dipende da WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="f1581-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="f1581-155">Per hello macchina toosuccessfully applicare la configurazione di hello DSC di automazione, WMF 5.0 deve toobe presente.</span><span class="sxs-lookup"><span data-stu-id="f1581-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="f1581-156">ambiente Hello utilizza hello seguente esempio di configurazione DSC:</span><span class="sxs-lookup"><span data-stu-id="f1581-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="f1581-157">configurazione di Hello eseguirà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f1581-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="f1581-158">le variabili di Hello indicherà configurazione hello in tooget hello binari per il servizio di mobilità hello e agente VM di Azure hello, in cui tooget hello passphrase e toostore hello di output.</span><span class="sxs-lookup"><span data-stu-id="f1581-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="f1581-159">Hello configurazione importerà risorsa xPSDesiredStateConfiguration DSC hello, in modo che è possibile utilizzare `xRemoteFile` file hello toodownload dal repository hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="f1581-160">configurazione di Hello creerà una directory in cui i file binari hello toostore.</span><span class="sxs-lookup"><span data-stu-id="f1581-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="f1581-161">risorsa archive Hello estrarrà file hello dalla cartella compressa hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="f1581-162">il nome di risorsa di installazione del pacchetto Hello installerà il servizio di mobilità hello hello UNIFIEDAGENT. Programma di installazione EXE con gli argomenti specifici hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="f1581-163">(le variabili hello costruire argomenti hello necessaria tooreflect toobe modificato ambiente).</span><span class="sxs-lookup"><span data-stu-id="f1581-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="f1581-164">il pacchetto di Hello AzureAgent risorse installerà l'agente VM di Azure hello, che è consigliabile in ogni macchina virtuale in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="f1581-165">agente VM di Azure Hello rende possibili tooadd estensioni toohello VM dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="f1581-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="f1581-166">Hello risorsa del servizio o risorse assicurerà che hello correlate a servizi di mobilità e hello servizi di Azure sono sempre in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f1581-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="f1581-167">Salvare la configurazione di hello come **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="f1581-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="f1581-168">Tenere presente che tooreplace hello CSIP nel server di gestione vera e propria hello tooreflect configurazione, in modo che verrà connessa correttamente hello agente e utilizzerà la passphrase corretta hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="f1581-169">Passaggio 3: Caricare tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="f1581-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="f1581-170">Poiché configurazione hello DSC apportate importerà un modulo di risorse DSC necessari (xPSDesiredStateConfiguration), è necessario tooimport in automazione di tale modulo prima di caricare la configurazione DSC hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="f1581-171">Accedi con account di automazione, tooyour Sfoglia troppo**asset** > **moduli**, fare clic su **Sfoglia raccolta**.</span><span class="sxs-lookup"><span data-stu-id="f1581-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="f1581-172">Qui è possibile cercare il modulo hello e importarlo tooyour account.</span><span class="sxs-lookup"><span data-stu-id="f1581-172">Here you can search for hello module and import it tooyour account.</span></span>

![Importazione del modulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="f1581-174">Al termine, andare tooyour macchina in cui i moduli di gestione risorse di Azure hello installati e procedere della configurazione DSC tooimport hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="f1581-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="f1581-175">Cmdlet di importazione</span><span class="sxs-lookup"><span data-stu-id="f1581-175">Import cmdlets</span></span>
<span data-ttu-id="f1581-176">In PowerShell, accedi tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="f1581-177">Modificare l'ambiente di hello cmdlet tooreflect e acquisire le informazioni sull'account di automazione in una variabile:</span><span class="sxs-lookup"><span data-stu-id="f1581-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="f1581-178">Caricare hello configurazione tooAutomation DSC usando hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f1581-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="f1581-179">Compilare la configurazione hello in DSC di automazione</span><span class="sxs-lookup"><span data-stu-id="f1581-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="f1581-180">Successivamente, è necessario configurazione hello toocompile in DSC di automazione, in modo che è possibile avviare tooregister tooit di nodi.</span><span class="sxs-lookup"><span data-stu-id="f1581-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="f1581-181">Ottenere questo risultato eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f1581-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="f1581-182">L'operazione può richiedere alcuni minuti, in quanto si distribuisce sostanzialmente servizio di pull DSC di hello configurazione toohello ospitato.</span><span class="sxs-lookup"><span data-stu-id="f1581-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="f1581-183">Dopo aver compilato la configurazione hello, è possibile recuperare informazioni sul processo hello tramite PowerShell (Get-AzureRmAutomationDscCompilationJob) o tramite hello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1581-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Recuperare il processo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="f1581-185">Si dispone ora correttamente pubblicata e caricato il tooAutomation di configurazione DSC DSC.</span><span class="sxs-lookup"><span data-stu-id="f1581-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="f1581-186">Passaggio 4: Caricare le macchine tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="f1581-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="f1581-187">Uno dei prerequisiti di hello per il completamento di questo scenario è che i computer Windows vengono aggiornati con la versione più recente di hello di WMF.</span><span class="sxs-lookup"><span data-stu-id="f1581-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="f1581-188">È possibile scaricare e installare la versione corretta di hello per la piattaforma di hello [area Download](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="f1581-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="f1581-189">Si creerà un metaconfig si applicherà tooyour nodi DSC.</span><span class="sxs-lookup"><span data-stu-id="f1581-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="f1581-190">toosucceed con questo oggetto, è necessario tooretrieve hello endpoint URL e hello chiave primaria per l'account di automazione selezionato in Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="f1581-191">È possibile trovare questi valori in **chiavi** su hello **tutte le impostazioni** pannello hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Valori chiave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="f1581-193">In questo esempio, è necessario un server fisico di Windows Server 2012 R2 che si desidera tooprotect tramite il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="f1581-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="f1581-194">Verificare la presenza di eventuali operazioni di ridenominazione di file nel Registro di sistema hello in sospeso</span><span class="sxs-lookup"><span data-stu-id="f1581-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="f1581-195">Prima di iniziare server hello tooassociate con endpoint di hello DSC di automazione, è consigliabile verificare la disponibilità di eventuali operazioni di ridenominazione di file nel Registro di sistema hello in sospeso.</span><span class="sxs-lookup"><span data-stu-id="f1581-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="f1581-196">Potrebbe impedire che il programma di installazione di hello completamento a causa di tooa il riavvio in sospeso.</span><span class="sxs-lookup"><span data-stu-id="f1581-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="f1581-197">Eseguire hello tooverify cmdlet che non vi sia alcun riavvio in sospeso nel server di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1581-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="f1581-198">Se questa risulta vuota, verrà tooproceed OK.</span><span class="sxs-lookup"><span data-stu-id="f1581-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="f1581-199">In caso contrario, è necessario risolvere il problema riavviando server hello durante una finestra di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="f1581-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="f1581-200">configurazione di hello tooapply nel server di hello, avviare hello PowerShell Integrated Scripting Environment (ISE) ed eseguire lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="f1581-201">Questa è essenzialmente una configurazione locale di DSC che indicare hello Gestione configurazione locale del motore tooregister con hello servizio DSC di automazione e recuperare la configurazione specifica hello (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="f1581-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="f1581-202">Questa configurazione genera hello Gestione configurazione locale tooregister motore stesso con DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="f1581-203">Viene inoltre determinato funzionamento motore hello, come procedere se è presente una deviazione della configurazione (ApplyAndAutoCorrect) e come deve procedere con la configurazione di hello se è necessario un riavvio.</span><span class="sxs-lookup"><span data-stu-id="f1581-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="f1581-204">Dopo aver eseguito questo script, il nodo hello deve iniziare tooregister con DSC di automazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Registrazione del nodo in corso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="f1581-206">Se si torna indietro toohello portale di Azure, è possibile visualizzare il nodo appena registrato hello è ora presente nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Nodo registrato nel portale di hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="f1581-208">Nel server di hello, è possibile eseguire hello tooverify cmdlet che hello nodo sia stato registrato correttamente PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="f1581-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="f1581-209">Dopo la configurazione di hello è stata estratta e applicata toohello server, è possibile verificare questa eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f1581-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="f1581-210">output di Hello mostra che il server hello è estratta correttamente la configurazione:</span><span class="sxs-lookup"><span data-stu-id="f1581-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Output](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="f1581-212">Inoltre, l'installazione del servizio di mobilità hello include il proprio log in cui è reperibile in *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="f1581-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="f1581-213">La procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="f1581-213">That’s it.</span></span> <span data-ttu-id="f1581-214">È ora correttamente distribuito e registrazione del servizio di mobilità hello computer hello che si desidera tooprotect tramite il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="f1581-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="f1581-215">DSC verrà assicurarsi che i servizi necessario hello sono sempre in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f1581-215">DSC will make sure that hello required services are always running.</span></span>

![Distribuzione completata](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="f1581-217">Dopo che il server di gestione di hello rileva una distribuzione corretta di hello, è possibile configurare la protezione e abilitare la replica nella macchina hello tramite il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="f1581-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="f1581-218">Uso di DSC in ambienti non connessi</span><span class="sxs-lookup"><span data-stu-id="f1581-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="f1581-219">Se i computer non connesso toohello Internet, è possibile affidarsi toodeploy DSC e configurare il servizio di mobilità hello sui carichi di lavoro hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f1581-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="f1581-220">È possibile creare istanze del server di pull DSC nel proprio ambiente tooessentially funzionalità hello stesso che si ottiene da Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f1581-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="f1581-221">Ovvero, i client hello effettuerà il pull configurazione hello (dopo la registrazione) toohello DSC endpoint.</span><span class="sxs-lookup"><span data-stu-id="f1581-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="f1581-222">Tuttavia, un'altra opzione è toomanually push hello DSC configurazione tooyour macchine, locale o remoto.</span><span class="sxs-lookup"><span data-stu-id="f1581-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="f1581-223">Si noti che in questo esempio, un parametro aggiunto hello nome del computer.</span><span class="sxs-lookup"><span data-stu-id="f1581-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="f1581-224">i file remoti Hello si trovano in una condivisione remota deve essere accessibile dai computer hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f1581-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="f1581-225">fine Hello dello script di hello attivarne configurazione hello e quindi avvia il computer di destinazione toohello tooapply hello DSC configurazione.</span><span class="sxs-lookup"><span data-stu-id="f1581-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f1581-226">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1581-226">Prerequisites</span></span>
<span data-ttu-id="f1581-227">Verificare che sia installato il modulo di PowerShell xPSDesiredStateConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="f1581-228">Per i computer Windows in cui è installato WMF 5.0, è possibile installare modulo xPSDesiredStateConfiguration hello eseguendo i seguenti cmdlet nei computer di destinazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="f1581-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="f1581-229">È anche possibile scaricare e salvare il modulo hello nel caso in cui è necessario toodistribute è tooWindows macchine che dispongono di WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="f1581-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="f1581-230">Eseguire questo cmdlet su un computer in cui è presente PowerShellGet (WMF 5.0):</span><span class="sxs-lookup"><span data-stu-id="f1581-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="f1581-231">Inoltre, per WMF 4.0, assicurarsi che hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) viene installato nei computer hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="f1581-232">Hello configurazione seguente può essere inserita tooWindows macchine che dispongono di WMF 5.0 e WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="f1581-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="f1581-233">Se si desidera tooinstantiate il proprio server di pull DSC le funzionalità di hello toomimic rete aziendale che è possibile ottenere da Automation DSC, vedere [configurando un server di pull web DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="f1581-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="f1581-234">Facoltativo: distribuire una configurazione DSC usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1581-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="f1581-235">In questo articolo è incentrata su come creare la propria tooautomatically configurazione DSC distribuire il servizio di mobilità hello e agente VM di Azure - hello e assicurarsi che vengano eseguiti in macchine hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="f1581-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="f1581-236">È necessario anche un modello di gestione risorse di Azure che consente di distribuire questo DSC configurazione tooa account nuovo o esistente automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f1581-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="f1581-237">modello Hello utilizzerà gli asset di automazione toocreate parametri di input contenenti variabili hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="f1581-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="f1581-238">Dopo aver distribuito il modello di hello, è possibile semplicemente fare riferimento toostep 4 in tooonboard questa guida per i computer.</span><span class="sxs-lookup"><span data-stu-id="f1581-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="f1581-239">modello Hello eseguirà seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f1581-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="f1581-240">Usare un account di Automazione esistente e crearne uno nuovo</span><span class="sxs-lookup"><span data-stu-id="f1581-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="f1581-241">Accettare i parametri di input per:</span><span class="sxs-lookup"><span data-stu-id="f1581-241">Take input parameters for:</span></span>
   * <span data-ttu-id="f1581-242">ASRRemoteFile - percorso hello in cui sono memorizzati l'installazione del servizio di mobilità hello</span><span class="sxs-lookup"><span data-stu-id="f1581-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="f1581-243">ASRPassphrase - percorso hello in cui sono memorizzati file passphrase.txt hello</span><span class="sxs-lookup"><span data-stu-id="f1581-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="f1581-244">ASRCSEndpoint - indirizzo IP di hello del server di gestione</span><span class="sxs-lookup"><span data-stu-id="f1581-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="f1581-245">Importare il modulo PowerShell di hello xPSDesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f1581-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="f1581-246">Creare e compilare una configurazione DSC hello</span><span class="sxs-lookup"><span data-stu-id="f1581-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="f1581-247">Hello tutti i passaggi precedenti, viene eseguito nell'ordine corretto hello, in modo che è possibile avviare l'onboarding di computer per la protezione.</span><span class="sxs-lookup"><span data-stu-id="f1581-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="f1581-248">modello di Hello, con le istruzioni per la distribuzione, si trova in [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="f1581-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="f1581-249">Distribuire il modello di hello tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f1581-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="f1581-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1581-250">Next steps</span></span>
<span data-ttu-id="f1581-251">Dopo aver distribuito gli agenti di servizi di mobilità hello, è possibile [abilitare la replica](site-recovery-vmware-to-azure.md) per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="f1581-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
