---
title: Passare un oggetto JSON a un runbook di Automazione di Azure | Microsoft Docs
description: Come passare i parametri a un runbook come un oggetto JSON
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
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="90400-104">Passare un oggetto JSON a un runbook di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="90400-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="90400-105">Può essere utile archiviare i dati che si desidera passare a un runbook in un file JSON.</span><span class="sxs-lookup"><span data-stu-id="90400-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="90400-106">Ad esempio, è possibile creare un file JSON che contiene tutti i parametri da passare a un runbook.</span><span class="sxs-lookup"><span data-stu-id="90400-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="90400-107">A tale scopo, è necessario convertire il JSON in una stringa e quindi convertire la stringa in un oggetto PowerShell prima di passare il relativo contenuto al runbook.</span><span class="sxs-lookup"><span data-stu-id="90400-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="90400-108">In questo esempio si creerà uno script di PowerShell che chiama [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) per avviare un runbook PowerShell, passando il contenuto di JSON al runbook.</span><span class="sxs-lookup"><span data-stu-id="90400-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="90400-109">Il runbook PowerShell avvia una VM di Azure, ottenendo i parametri per la VM dal file JSON che è stato passato.</span><span class="sxs-lookup"><span data-stu-id="90400-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90400-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="90400-110">Prerequisites</span></span>
<span data-ttu-id="90400-111">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="90400-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="90400-112">Sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90400-112">Azure subscription.</span></span> <span data-ttu-id="90400-113">Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="90400-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="90400-114">[Account di Automazione](automation-sec-configure-azure-runas-account.md) che conterrà il runbook ed eseguirà l'autenticazione con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="90400-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="90400-115">Questo account deve avere l'autorizzazione per avviare e arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90400-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="90400-116">Macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="90400-116">An Azure virtual machine.</span></span> <span data-ttu-id="90400-117">La macchina virtuale viene arrestata e avviata, quindi non deve essere una macchina virtuale di produzione.</span><span class="sxs-lookup"><span data-stu-id="90400-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="90400-118">Azure Powershell installato in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="90400-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="90400-119">Per informazioni sulla configurazione di PowerShell, vedere [Come installare e configurare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0).</span><span class="sxs-lookup"><span data-stu-id="90400-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="90400-120">Creare il file JSON</span><span class="sxs-lookup"><span data-stu-id="90400-120">Create the JSON file</span></span>

<span data-ttu-id="90400-121">Digitare il seguente test in un file di testo e salvarlo come `test.json` in un punto qualsiasi nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="90400-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="90400-122">Creare il runbook</span><span class="sxs-lookup"><span data-stu-id="90400-122">Create the runbook</span></span>

<span data-ttu-id="90400-123">Creare un nuovo runbook di PowerShell denominato "Test-Json" in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90400-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="90400-124">Per informazioni su come creare un nuovo runbook di PowerShell, vedere [Il primo runbook PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="90400-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="90400-125">Per accettare i dati JSON, il runbook deve accettare un oggetto come parametro di input.</span><span class="sxs-lookup"><span data-stu-id="90400-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="90400-126">Il runbook può quindi usare le proprietà definite nel file JSON.</span><span class="sxs-lookup"><span data-stu-id="90400-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="90400-127">Salvare e pubblicare il runbook nell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="90400-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="90400-128">Chiamare il runbook da PowerShell</span><span class="sxs-lookup"><span data-stu-id="90400-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="90400-129">Ora è possibile chiamare il runbook dal computer locale tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90400-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="90400-130">Eseguire i comandi di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="90400-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="90400-131">Accedere ad Azure:</span><span class="sxs-lookup"><span data-stu-id="90400-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="90400-132">Viene richiesto di immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="90400-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="90400-133">Ottenere il contenuto del file JSON e convertirlo in una stringa:</span><span class="sxs-lookup"><span data-stu-id="90400-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="90400-134">`JsonPath` è il percorso in cui è stato salvato il file JSON.</span><span class="sxs-lookup"><span data-stu-id="90400-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="90400-135">Convertire i contenuti stringa di `$json` in un oggetto di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="90400-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="90400-136">Creare una tabella hash per i parametri per `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="90400-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="90400-137">Si noti che si imposta il valore di `Parameters` sull'oggetto PowerShell che contiene i valori dal file JSON.</span><span class="sxs-lookup"><span data-stu-id="90400-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="90400-138">Avviare il runbook</span><span class="sxs-lookup"><span data-stu-id="90400-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="90400-139">Il runbook usa i valori del file JSON per avviare una VM.</span><span class="sxs-lookup"><span data-stu-id="90400-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90400-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90400-140">Next steps</span></span>

* <span data-ttu-id="90400-141">Per altre informazioni sulla modifica di runbook di PowerShell e del flusso di lavoro PowerShell con un editor di testo, vedere [Modifica di runbook testuali in Automazione di Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="90400-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="90400-142">Per altre informazioni su come creare o importare un runbook, vedere [Creazione o importazione di un runbook in Automazione di Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="90400-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


