---
title: configurazione dell'account di automazione di Azure aaaValidate | Documenti Microsoft
description: "In questo articolo viene descritto come configurazione hello tooconfirm dell'account di automazione è configurato correttamente."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="d15bd-103">Testare l'autenticazione con un account RunAs di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d15bd-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="d15bd-104">Dopo aver creato un account di automazione correttamente, è possibile eseguire tooconfirm un semplice test si è in grado di autenticare toosuccessfully in Gestione risorse di Azure o distribuzione di Azure classica con l'account RunAs automazione appena creato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="d15bd-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="d15bd-105">Autenticazione con l'account RunAs di Automazione</span><span class="sxs-lookup"><span data-stu-id="d15bd-105">Automation Run As authentication</span></span>
<span data-ttu-id="d15bd-106">Utilizzare anche codice di esempio hello seguente[creare un runbook PowerShell](automation-creating-importing-runbook.md) autenticazione tooverify utilizzando hello eseguite come account e anche in tooauthenticate il runbook personalizzati e gestire le risorse di gestione delle risorse con l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="d15bd-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="d15bd-107">Si noti hello cmdlet usato per l'autenticazione runbook hello - **Aggiungi AzureRmAccount**, hello utilizza *ServicePrincipalCertificate* set di parametri.</span><span class="sxs-lookup"><span data-stu-id="d15bd-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="d15bd-108">ed esegue l'autenticazione usando il certificato dell'entità servizio, non le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d15bd-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="d15bd-109">Quando si [eseguire runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate l'account RunAs, un [processo del runbook](automation-runbook-execution.md) viene creato, viene visualizzato il pannello di processo hello e visualizzato lo stato del processo hello in hello **riepilogo**riquadro.</span><span class="sxs-lookup"><span data-stu-id="d15bd-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="d15bd-110">lo stato del processo Hello verrà avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.</span><span class="sxs-lookup"><span data-stu-id="d15bd-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="d15bd-111">Verranno quindi spostati troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d15bd-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="d15bd-112">Al termine del processo del runbook hello, dovremmo vedere lo stato **completato**.</span><span class="sxs-lookup"><span data-stu-id="d15bd-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="d15bd-113">toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="d15bd-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="d15bd-114">In hello **Output** pannello, si noterà ha autenticato e restituisce un elenco di tutte le risorse in tutti i gruppi di risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d15bd-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="d15bd-115">Ricorda però blocco hello tooremove codice che inizia con il commento hello `#Get all ARM resources from all resource groups` quando è riutilizzare codice hello dai runbook.</span><span class="sxs-lookup"><span data-stu-id="d15bd-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="d15bd-116">Autenticazione con l'account RunAs classico</span><span class="sxs-lookup"><span data-stu-id="d15bd-116">Classic Run As authentication</span></span>
<span data-ttu-id="d15bd-117">Utilizzare anche codice di esempio hello seguente[creare un runbook PowerShell](automation-creating-importing-runbook.md) tooverify l'autenticazione tramite hello Classic eseguite come account e anche in tooauthenticate il runbook personalizzati e gestire le risorse nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d15bd-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="d15bd-118">Quando si [eseguire runbook hello](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate l'account RunAs, un [processo del runbook](automation-runbook-execution.md) viene creato, viene visualizzato il pannello di processo hello e visualizzato lo stato del processo hello in hello **riepilogo**riquadro.</span><span class="sxs-lookup"><span data-stu-id="d15bd-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="d15bd-119">lo stato del processo Hello verrà avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toobecome disponibili.</span><span class="sxs-lookup"><span data-stu-id="d15bd-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="d15bd-120">Verranno quindi spostati troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d15bd-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="d15bd-121">Al termine del processo del runbook hello, dovremmo vedere lo stato **completato**.</span><span class="sxs-lookup"><span data-stu-id="d15bd-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="d15bd-122">toosee hello risultati dettagliati di hello runbook, fare clic su hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="d15bd-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="d15bd-123">In hello **Output** pannello, si noterà ha autenticato e restituisce un elenco di tutte le macchine virtuali di Azure da VMName che vengono distribuiti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d15bd-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="d15bd-124">Ricorda però tooremove hello cmdlet **Get-AzureVM** quando è riutilizzare codice hello dai runbook.</span><span class="sxs-lookup"><span data-stu-id="d15bd-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d15bd-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d15bd-125">Next steps</span></span>
* <span data-ttu-id="d15bd-126">tooget avviato con runbook PowerShell, vedere [il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d15bd-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="d15bd-127">toolearn ulteriori informazioni sui grafici per la modifica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d15bd-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
