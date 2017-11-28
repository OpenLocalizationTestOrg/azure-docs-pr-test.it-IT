---
title: aaaPass un formato JSON dell'oggetto tooan runbook di automazione di Azure | Documenti Microsoft
description: Come toopass parametri tooa runbook come un oggetto JSON
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell, runbook, json, automazione di azure
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="6caa3-104">Passare a un runbook di automazione di Azure tooan oggetto JSON</span><span class="sxs-lookup"><span data-stu-id="6caa3-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="6caa3-105">Può essere utile toostore dati che si desidera toopass tooa runbook in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="6caa3-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="6caa3-106">Ad esempio, è possibile creare un file JSON che contiene tutti i parametri di hello desiderato toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="6caa3-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="6caa3-107">toodo, si tooconvert hello JSON tooa stringa e quindi convertire l'oggetto di PowerShell tooa stringa hello prima di passare il runbook toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="6caa3-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="6caa3-108">In questo esempio, si creerà uno script di PowerShell che chiama [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook di PowerShell, il passaggio di contenuto di hello di hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="6caa3-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="6caa3-109">runbook PowerShell Hello avvia una macchina virtuale di Azure, recupero dei parametri di hello per hello VM da hello JSON che è stato passato.</span><span class="sxs-lookup"><span data-stu-id="6caa3-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6caa3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6caa3-110">Prerequisites</span></span>
<span data-ttu-id="6caa3-111">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="6caa3-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6caa3-112">Sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa3-112">Azure subscription.</span></span> <span data-ttu-id="6caa3-113">Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="6caa3-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="6caa3-114">[Account di automazione](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.</span><span class="sxs-lookup"><span data-stu-id="6caa3-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="6caa3-115">Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="6caa3-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="6caa3-116">Macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa3-116">An Azure virtual machine.</span></span> <span data-ttu-id="6caa3-117">La macchina virtuale viene arrestata e avviata, quindi non deve essere una macchina virtuale di produzione.</span><span class="sxs-lookup"><span data-stu-id="6caa3-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="6caa3-118">Azure Powershell installato in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="6caa3-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="6caa3-119">Vedere [installare e configurare Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) per informazioni su come tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6caa3-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="6caa3-120">Creare file JSON hello</span><span class="sxs-lookup"><span data-stu-id="6caa3-120">Create hello JSON file</span></span>

<span data-ttu-id="6caa3-121">Digitare quanto segue di hello test in un file di testo e salvarlo come `test.json` in un punto qualsiasi nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="6caa3-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="6caa3-122">Creare runbook hello</span><span class="sxs-lookup"><span data-stu-id="6caa3-122">Create hello runbook</span></span>

<span data-ttu-id="6caa3-123">Creare un nuovo runbook di PowerShell denominato "Test-Json" in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa3-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="6caa3-124">toolearn toocreate un nuovo runbook di PowerShell, vedere [il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6caa3-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="6caa3-125">dati JSON hello tooaccept hello runbook deve accettare un oggetto come un parametro di input.</span><span class="sxs-lookup"><span data-stu-id="6caa3-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="6caa3-126">runbook Hello è quindi possibile utilizzare le proprietà di hello definite in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6caa3-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="6caa3-127">Salvare e pubblicare il runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6caa3-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="6caa3-128">Chiamata runbook hello da PowerShell</span><span class="sxs-lookup"><span data-stu-id="6caa3-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="6caa3-129">È ora possibile chiamare hello runbook dal computer locale tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6caa3-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="6caa3-130">Eseguire i seguenti comandi PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="6caa3-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="6caa3-131">Accedi tooAzure:</span><span class="sxs-lookup"><span data-stu-id="6caa3-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="6caa3-132">Si sono tooenter richieste le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="6caa3-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="6caa3-133">Ottenere il contenuto di hello del file JSON hello e convertirlo tooa stringa:</span><span class="sxs-lookup"><span data-stu-id="6caa3-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="6caa3-134">`JsonPath`è il percorso di hello in cui è stato salvato il file JSON di hello.</span><span class="sxs-lookup"><span data-stu-id="6caa3-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="6caa3-135">Convertire il contenuto della stringa hello `$json` tooa PowerShell oggetto:</span><span class="sxs-lookup"><span data-stu-id="6caa3-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="6caa3-136">Creare una tabella hash per i parametri di hello per `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="6caa3-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="6caa3-137">Si noti che è impostato come valore hello `Parameters` toohello PowerShell oggetto che contiene i valori hello dal file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="6caa3-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="6caa3-138">Avviare il runbook hello</span><span class="sxs-lookup"><span data-stu-id="6caa3-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="6caa3-139">Hello runbook vengono utilizzati valori hello hello JSON file toostart una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6caa3-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6caa3-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6caa3-140">Next steps</span></span>

* <span data-ttu-id="6caa3-141">toolearn più sulla modifica di runbook PowerShell e flusso di lavoro di PowerShell con un editor di testo, vedere [modifica testuale runbook in automazione di Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="6caa3-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="6caa3-142">toolearn ulteriori informazioni su creazione e importazione di runbook, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="6caa3-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


