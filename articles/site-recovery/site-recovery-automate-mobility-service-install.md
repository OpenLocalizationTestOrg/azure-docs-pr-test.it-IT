---
title: Distribuire il servizio Site Recovery Mobility con Automation DSC di Azure | Documentazione Microsoft
description: Descrive come usare Automation DSC di Azure per distribuire automaticamente il servizio Mobility di Azure Site Recovery e l'agente di Azure per le macchine virtuali VMware e la replica del server fisico in Azure
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
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="2eacf-103">Distribuire il servizio Mobility di Azure con Automation DSC di Azure per la replica della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="2eacf-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="2eacf-104">In Operations Management Suite offriamo una soluzione completa per il backup e il ripristino di emergenza che può essere usata nell'ambito del piano di continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="2eacf-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="2eacf-105">Il percorso è iniziato da Hyper-V con la replica Hyper-V,</span><span class="sxs-lookup"><span data-stu-id="2eacf-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="2eacf-106">poi è proseguito per supportare una configurazione eterogenea perché i clienti hanno più hypervisor e piattaforme nei loro cloud.</span><span class="sxs-lookup"><span data-stu-id="2eacf-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="2eacf-107">Se attualmente si eseguono carichi di lavoro VMware e/o server fisici, un server di gestione esegue tutti i componenti di Azure Site Recovery nell'ambiente per gestire la comunicazione e la replica dei dati con Azure, quando questo è la destinazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="2eacf-108">Distribuire il servizio Site Recovery Mobility usando Automation DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="2eacf-109">Per iniziare, è bene riepilogare le operazioni eseguite da questo server di gestione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="2eacf-110">Il server di gestione esegue diversi ruoli del server.</span><span class="sxs-lookup"><span data-stu-id="2eacf-110">The management server runs several server roles.</span></span> <span data-ttu-id="2eacf-111">Uno di questi ruoli è la *configurazione*, che coordina la comunicazione e gestisce i processi di ripristino e replica dei dati.</span><span class="sxs-lookup"><span data-stu-id="2eacf-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="2eacf-112">Inoltre, il ruolo di *elaborazione* funge da gateway di replica.</span><span class="sxs-lookup"><span data-stu-id="2eacf-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="2eacf-113">Questo ruolo riceve i dati di replica da computer di origine protetti, li ottimizza attraverso il caching, la compressione e la crittografia e li invia a un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="2eacf-114">Una delle funzioni del ruolo di elaborazione è anche quella di eseguire il push dell'installazione del servizio Mobility nei computer protetti ed eseguire l'individuazione automatica delle VM VMware.</span><span class="sxs-lookup"><span data-stu-id="2eacf-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="2eacf-115">In caso di failback da Azure, il ruolo di *destinazione master* gestirà i dati di replica come parte di questa operazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="2eacf-116">Per i computer protetti, ci si affida al *servizio Mobility*.</span><span class="sxs-lookup"><span data-stu-id="2eacf-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="2eacf-117">Questo componente viene distribuito in ogni computer, ovvero VM VMware o server fisico, di cui si vuole eseguire la replica in Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="2eacf-118">Acquisisce scritture di dati sul computer e le inoltra al server di gestione (ruolo di elaborazione).</span><span class="sxs-lookup"><span data-stu-id="2eacf-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="2eacf-119">Nell'ambito della continuità aziendale è importante comprendere i carichi di lavoro, l'infrastruttura e i componenti coinvolti.</span><span class="sxs-lookup"><span data-stu-id="2eacf-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="2eacf-120">È quindi possibile soddisfare i requisiti per gli obiettivi del tempo di ripristino (RTO) e gli obiettivi del punto di ripristino (RPO).</span><span class="sxs-lookup"><span data-stu-id="2eacf-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="2eacf-121">In questo contesto, il servizio Mobility è fondamentale per garantire che i carichi di lavoro siano protetti nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="2eacf-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="2eacf-122">Come possiamo garantire nel modo migliore che la configurazione sia affidabile e protetta usando alcuni componenti di Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="2eacf-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="2eacf-123">In questo articolo viene fornito un esempio di come è possibile usare Automation Desired State Configuration (DSC) di Azure insieme a Site Recovery per assicurarsi che:</span><span class="sxs-lookup"><span data-stu-id="2eacf-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="2eacf-124">Il servizio Mobility e l'agente VM di Azure vengano distribuiti ai computer Windows che si desidera proteggere.</span><span class="sxs-lookup"><span data-stu-id="2eacf-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="2eacf-125">Il servizio Mobility e l'agente VM di Azure siano sempre in esecuzione quando Azure è la destinazione della replica.</span><span class="sxs-lookup"><span data-stu-id="2eacf-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2eacf-126">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2eacf-126">Prerequisites</span></span>
* <span data-ttu-id="2eacf-127">Un repository per archiviare la configurazione necessaria</span><span class="sxs-lookup"><span data-stu-id="2eacf-127">A repository to store the required setup</span></span>
* <span data-ttu-id="2eacf-128">Un repository per archiviare la passphrase necessaria per la registrazione al server di gestione</span><span class="sxs-lookup"><span data-stu-id="2eacf-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="2eacf-129">Per ogni server di gestione viene generata una passphrase univoca.</span><span class="sxs-lookup"><span data-stu-id="2eacf-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="2eacf-130">Se si intende distribuire più server di gestione, è necessario assicurarsi che la passphrase corretta venga archiviata nel file passphrase txt.</span><span class="sxs-lookup"><span data-stu-id="2eacf-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="2eacf-131">La soluzione Windows Management Framework (WMF) 5.0 installata sui computer di cui che si vuole abilitare la protezione (requisito per Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="2eacf-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="2eacf-132">Se si desidera usare DSC per computer Windows su cui è installato WMF 4.0, vedere la sezione [Uso di DSC in ambienti non connessi](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="2eacf-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="2eacf-133">Il servizio Mobility può essere installato tramite la riga di comando e accetta diversi argomenti.</span><span class="sxs-lookup"><span data-stu-id="2eacf-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="2eacf-134">Ecco perché è necessario disporre dei file binari (dopo averli estratti dalla configurazione) e archiviarli in un punto in cui è possibile recuperarli usando una configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="2eacf-135">Passaggio 1: estrazione dei file binari</span><span class="sxs-lookup"><span data-stu-id="2eacf-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="2eacf-136">Per estrarre i file necessari per la configurazione, accedere alla directory seguente nel server di gestione:</span><span class="sxs-lookup"><span data-stu-id="2eacf-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="2eacf-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="2eacf-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="2eacf-138">In questa cartella dovrebbe essere presente un file MSI denominato:</span><span class="sxs-lookup"><span data-stu-id="2eacf-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="2eacf-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="2eacf-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="2eacf-140">Per estrarre il programma di installazione usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2eacf-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="2eacf-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="2eacf-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="2eacf-142">Selezionare tutti i file e inviarli a una cartella compressa.</span><span class="sxs-lookup"><span data-stu-id="2eacf-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="2eacf-143">Ora sono disponibili i file binari necessari per automatizzare la configurazione del servizio Mobility con Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="2eacf-144">Passphrase</span><span class="sxs-lookup"><span data-stu-id="2eacf-144">Passphrase</span></span>
<span data-ttu-id="2eacf-145">È quindi necessario scegliere dove si vuole posizionare la cartella compressa.</span><span class="sxs-lookup"><span data-stu-id="2eacf-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="2eacf-146">È possibile usare un account di archiviazione di Azure, come illustrato più avanti, per archiviare la passphrase necessaria per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="2eacf-147">L'agente verrà quindi registrato con il server di gestione come parte del processo.</span><span class="sxs-lookup"><span data-stu-id="2eacf-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="2eacf-148">La passphrase ottenuta durante la distribuzione del server di gestione può essere salvata in un file txt come passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="2eacf-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="2eacf-149">Inserire sia la cartella compressa sia la passphrase in un contenitore dedicato nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Percorso della cartella](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="2eacf-151">Se si preferisce, è possibile mantenere questi file in una condivisione all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="2eacf-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="2eacf-152">È sufficiente garantire che la risorsa DSC che verrà usata in un secondo momento disponga dell'accesso e possa usare la configurazione e la passphrase.</span><span class="sxs-lookup"><span data-stu-id="2eacf-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="2eacf-153">Passaggio 2: creazione della configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="2eacf-154">Il programma di configurazione dipende da WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="2eacf-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="2eacf-155">Affinché il computer applichi correttamente la configurazione tramite Automation DSC, è necessario che sia presente la soluzione WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="2eacf-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="2eacf-156">Nell'ambiente la configurazione DSC di esempio usata è la seguente:</span><span class="sxs-lookup"><span data-stu-id="2eacf-156">The environment uses the following example DSC configuration:</span></span>

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
<span data-ttu-id="2eacf-157">La configurazione eseguirà le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2eacf-157">The configuration will do the following:</span></span>

* <span data-ttu-id="2eacf-158">Le variabili indicheranno alla configurazione dove ottenere i file binari per il servizio Mobility e l'agente VM di Azure, la passphrase e il percorso in cui archiviare l'output.</span><span class="sxs-lookup"><span data-stu-id="2eacf-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="2eacf-159">La configurazione importerà la risorsa DSC xPSDesiredStateConfiguration in modo da poter usare `xRemoteFile` per scaricare i file dal repository.</span><span class="sxs-lookup"><span data-stu-id="2eacf-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="2eacf-160">La configurazione creerà la directory in cui si vuole archiviare i dati binari.</span><span class="sxs-lookup"><span data-stu-id="2eacf-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="2eacf-161">La risorsa di archiviazione estrarrà i file dalla cartella compressa.</span><span class="sxs-lookup"><span data-stu-id="2eacf-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="2eacf-162">La risorsa Install del pacchetto installerà il servizio Mobility dal programma di installazione UNIFIEDAGENT.EXE con gli argomenti specifici.</span><span class="sxs-lookup"><span data-stu-id="2eacf-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="2eacf-163">Le variabile che costruiscono gli argomenti devono essere modificate per riflettere l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="2eacf-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="2eacf-164">La risorsa AzureAgent del pacchetto installerà l'agente VM di Azure, consigliato su tutte le VM eseguite in Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="2eacf-165">L'agente VM di Azure rende inoltre possibile aggiungere estensioni alla VM dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="2eacf-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="2eacf-166">Una o più risorse del servizio garantiranno che i servizi Mobility correlati e i servizi di Azure siano sempre in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="2eacf-167">Salvare la configurazione come **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="2eacf-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="2eacf-168">È necessario ricordarsi di sostituire il valore CSIP nella configurazione per riflettere il server di gestione effettivo, in modo che l'agente venga connesso e che usi la passphrase corretta.</span><span class="sxs-lookup"><span data-stu-id="2eacf-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="2eacf-169">Passaggio 3: caricamento su Automation DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="2eacf-170">Dal momento che la configurazione DSC creata importerà il modulo di risorse DSC xPSDesiredStateConfiguration richiesto, è necessario importare il modulo in Automation prima di caricare la configurazione DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="2eacf-171">Accedere all'account di Automazione, andare su **Asset** > **Moduli** e fare clic su **Esplora raccolta**.</span><span class="sxs-lookup"><span data-stu-id="2eacf-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="2eacf-172">Qui è possibile cercare il modulo e importarlo nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="2eacf-172">Here you can search for the module and import it to your account.</span></span>

![Importazione del modulo](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="2eacf-174">Al termine passare al computer su cui sono installati i moduli di Azure Resource Manager e continuare a importare la configurazione DSC appena creata.</span><span class="sxs-lookup"><span data-stu-id="2eacf-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="2eacf-175">Cmdlet di importazione</span><span class="sxs-lookup"><span data-stu-id="2eacf-175">Import cmdlets</span></span>
<span data-ttu-id="2eacf-176">In PowerShell accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="2eacf-177">Modificare i cmdlet in modo da riflettere l'ambiente e acquisire le informazioni sull'account di Automation in forma di variabile:</span><span class="sxs-lookup"><span data-stu-id="2eacf-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="2eacf-178">Caricare la configurazione di Automation DSC usando il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="2eacf-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="2eacf-179">Compilare la configurazione in Automation DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="2eacf-180">È quindi necessario compilare la configurazione in Automation DSC, in modo che sia possibile iniziare a registrare i nodi su di essa.</span><span class="sxs-lookup"><span data-stu-id="2eacf-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="2eacf-181">Questo risultato si ottiene eseguendo il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="2eacf-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="2eacf-182">Questa operazione può richiedere alcuni minuti poiché si sta distribuendo la configurazione al servizio di pull DSC ospitato.</span><span class="sxs-lookup"><span data-stu-id="2eacf-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="2eacf-183">Al termine della configurazione, è possibile recuperare le informazioni sul processo tramite PowerShell (Get-AzureRmAutomationDscCompilationJob) o usando il [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2eacf-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![Recuperare il processo](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="2eacf-185">La configurazione DSC in Automation DSC è stata ora pubblicata e caricata correttamente.</span><span class="sxs-lookup"><span data-stu-id="2eacf-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="2eacf-186">Passaggio 4: caricamento di computer in Automation DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="2eacf-187">Uno dei prerequisiti per il completamento di questo scenario è che la versione della soluzione WMF nei computer Windows sia aggiornata.</span><span class="sxs-lookup"><span data-stu-id="2eacf-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="2eacf-188">È possibile scaricare e installare la versione corretta per la piattaforma dall' [Area download](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="2eacf-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="2eacf-189">Si creerà ora una metaconfig per DSC che sarà applicata ai nodi.</span><span class="sxs-lookup"><span data-stu-id="2eacf-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="2eacf-190">Per un risultato positivo è necessario recuperare l'URL e la chiave primaria dell'endpoint per l'account di automazione selezionato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2eacf-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="2eacf-191">Questi valori si trovano in **Chiavi** nel pannello **Tutte le impostazioni** dell'account di Automazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Valori chiave](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="2eacf-193">In questo esempio è presente un server fisico Windows Server 2012 R2 che si desidera proteggere con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2eacf-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="2eacf-194">Verificare la presenza di eventuali operazioni di ridenominazione di file in sospeso nel Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="2eacf-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="2eacf-195">Prima di iniziare ad associare il server con l'endpoint Automation DSC, è consigliabile controllare le operazioni di ridenominazione dei file in sospeso nel Registro di sistema,</span><span class="sxs-lookup"><span data-stu-id="2eacf-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="2eacf-196">in quanto un riavvio in sospeso potrebbe impedire il completamento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="2eacf-197">Per verificare che non vi sia alcun riavvio in sospeso nel server, eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="2eacf-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="2eacf-198">Se non è presente, è possibile continuare.</span><span class="sxs-lookup"><span data-stu-id="2eacf-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="2eacf-199">In caso contrario, è necessario riavviare il server in una finestra di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="2eacf-200">Per applicare la configurazione sul server, avviare PowerShell Integrated Scripting Environment (ISE) ed eseguire lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="2eacf-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="2eacf-201">Lo script è essenzialmente una configurazione locale per DSC che indicherà al motore di gestione configurazione locale di eseguire la registrazione con il servizio Automation DSC e recuperare la configurazione specifica (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="2eacf-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="2eacf-202">Questa configurazione causerà la registrazione del motore di gestione configurazione locale con Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="2eacf-203">Inoltre determinerà come il motore deve funzionare, come comportarsi in presenza di una differenza nella configurazione (ApplyAndAutoCorrect) e come procedere con la configurazione se è richiesto un riavvio.</span><span class="sxs-lookup"><span data-stu-id="2eacf-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="2eacf-204">Dopo l'esecuzione dello script, il nodo dovrebbe iniziare la registrazione ad Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Registrazione del nodo in corso](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="2eacf-206">Se si torna al portale di Azure, si può notare che il nodo appena registrato è ora presente nel portale.</span><span class="sxs-lookup"><span data-stu-id="2eacf-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Nodo registrato nel portale](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="2eacf-208">Per verificare che la registrazione del nodo sia stata eseguita correttamente, è possibile eseguire il cmdlet PowerShell seguente sul server:</span><span class="sxs-lookup"><span data-stu-id="2eacf-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="2eacf-209">Dopo che il pull della configurazione è stato eseguito e la configurazione è stata applicata al server, procedere alla verifica eseguendo il seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2eacf-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="2eacf-210">L'output mostra che il server ha eseguito correttamente il pull della configurazione:</span><span class="sxs-lookup"><span data-stu-id="2eacf-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Output](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="2eacf-212">Inoltre, la configurazione del servizio Mobility dispone di un proprio log in *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="2eacf-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="2eacf-213">La procedura è terminata.</span><span class="sxs-lookup"><span data-stu-id="2eacf-213">That’s it.</span></span> <span data-ttu-id="2eacf-214">Il servizio Mobility è stato distribuito e registrato correttamente sul computer che si desidera proteggere tramite Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2eacf-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="2eacf-215">DSC si assicurerà che i servizi necessari siano sempre in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-215">DSC will make sure that the required services are always running.</span></span>

![Distribuzione completata](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="2eacf-217">Una volta che il server di gestione ha rilevato la corretta distribuzione, procedere per configurare la protezione e abilitare la replica nel computer con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2eacf-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="2eacf-218">Uso di DSC in ambienti non connessi</span><span class="sxs-lookup"><span data-stu-id="2eacf-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="2eacf-219">Se i computer non sono connessi a Internet, è comunque possibile fare affidamento su DSC per distribuire e configurare il servizio Mobility sui carichi di lavoro da proteggere.</span><span class="sxs-lookup"><span data-stu-id="2eacf-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="2eacf-220">È possibile creare istanze del server di pull DSC nel proprio ambiente per fornire essenzialmente le stesse funzionalità ottenute da Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="2eacf-221">Ciò significa che, dopo la registrazione, i client eseguiranno il pull della configurazione sull'endpoint DSC.</span><span class="sxs-lookup"><span data-stu-id="2eacf-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="2eacf-222">Tuttavia, un'altra opzione consiste nel push manuale della configurazione sui computer locali o remoti.</span><span class="sxs-lookup"><span data-stu-id="2eacf-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="2eacf-223">Notare che in questo esempio esiste un parametro aggiunto per il nome del computer.</span><span class="sxs-lookup"><span data-stu-id="2eacf-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="2eacf-224">I file remoti si trovano ora in una condivisione remota che deve essere accessibile ai computer che si desidera proteggere.</span><span class="sxs-lookup"><span data-stu-id="2eacf-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="2eacf-225">La fine dello script esegue la configurazione e quindi inizia ad applicare la configurazione DSC al computer di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2eacf-226">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2eacf-226">Prerequisites</span></span>
<span data-ttu-id="2eacf-227">Assicurarsi che sia installato il modulo xPSDesiredStateConfiguration di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2eacf-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="2eacf-228">Per i computer Windows su cui è installata la soluzione WMF 5.0, è possibile installare il modulo xPSDesiredStateConfiguration eseguendo il cmdlet seguente nei computer di destinazione:</span><span class="sxs-lookup"><span data-stu-id="2eacf-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="2eacf-229">È inoltre possibile scaricare e salvare il modulo nel caso in cui sia necessario distribuirlo ai computer Windows con WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="2eacf-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="2eacf-230">Eseguire questo cmdlet su un computer in cui è presente PowerShellGet (WMF 5.0):</span><span class="sxs-lookup"><span data-stu-id="2eacf-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="2eacf-231">Anche per WMF 4.0, assicurarsi che sui computer sia installato [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) .</span><span class="sxs-lookup"><span data-stu-id="2eacf-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="2eacf-232">È possibile eseguire il push della configurazione seguente sui computer Windows con WMF 5.0 e WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="2eacf-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="2eacf-233">Se si vuole creare un'istanza del server di pull DSC sulla rete aziendale per riprodurre le funzionalità disponibili in Automation DSC, vedere [Configurazione di un server di pull Web DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="2eacf-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="2eacf-234">Facoltativo: distribuire una configurazione DSC usando il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2eacf-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="2eacf-235">Questo articolo ha illustrato come è possibile creare la propria configurazione DSC per distribuire automaticamente il servizio Mobility e l'agente VM di Azure e assicurarsi che siano in esecuzione sui computer da proteggere.</span><span class="sxs-lookup"><span data-stu-id="2eacf-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="2eacf-236">È disponibile anche un modello di Azure Resource Manager che consente di distribuire questa configurazione DSC a un account di Automazione di Azure nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="2eacf-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="2eacf-237">Il modello userà i parametri di input per creare gli asset di automazione che conterranno le variabili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="2eacf-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="2eacf-238">Una volta distribuito il modello, è possibile fare riferimento al passaggio 4 di questa guida per caricare i computer.</span><span class="sxs-lookup"><span data-stu-id="2eacf-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="2eacf-239">Il modello eseguirà le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2eacf-239">The template will do the following:</span></span>

1. <span data-ttu-id="2eacf-240">Usare un account di Automazione esistente e crearne uno nuovo</span><span class="sxs-lookup"><span data-stu-id="2eacf-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="2eacf-241">Accettare i parametri di input per:</span><span class="sxs-lookup"><span data-stu-id="2eacf-241">Take input parameters for:</span></span>
   * <span data-ttu-id="2eacf-242">ASRRemoteFile - il percorso in cui è stata memorizzata la configurazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="2eacf-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="2eacf-243">ASRPassphrase - il percorso in cui è stato memorizzato il file passphrase.txt</span><span class="sxs-lookup"><span data-stu-id="2eacf-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="2eacf-244">ASRCSEndpoint - l'indirizzo IP del server di gestione</span><span class="sxs-lookup"><span data-stu-id="2eacf-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="2eacf-245">Importare il modulo xPSDesiredStateConfiguration di PowerShell</span><span class="sxs-lookup"><span data-stu-id="2eacf-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="2eacf-246">Creare e compilare la configurazione DSC</span><span class="sxs-lookup"><span data-stu-id="2eacf-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="2eacf-247">Tutti i passaggi precedenti verranno eseguiti nell'ordine corretto in modo da poter iniziare il caricamento dei computer per la protezione.</span><span class="sxs-lookup"><span data-stu-id="2eacf-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="2eacf-248">Il modello con le istruzioni per la distribuzione si trova in [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="2eacf-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="2eacf-249">Distribuire il modello tramite PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2eacf-249">Deploy the template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2eacf-250">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2eacf-250">Next steps</span></span>
<span data-ttu-id="2eacf-251">Dopo avere distribuito gli agenti del servizio Mobility, è possibile [abilitare la replica](site-recovery-vmware-to-azure.md) per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2eacf-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
