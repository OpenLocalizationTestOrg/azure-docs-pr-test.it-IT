---
title: Automazione della distribuzione di applicazioni con le estensioni delle macchine virtuali | Microsoft Docs
description: Macchine virtuali di Azure - Esercitazione DotNet Core
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f2996eef71b39c6240fac5484854f72d3e657d0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="7a556-103">Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="7a556-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="7a556-104">Dopo che tutti i requisiti dell'infrastruttura di Azure sono stati identificati e convertiti in un modello di distribuzione, è necessario occuparsi della distribuzione effettiva delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7a556-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="7a556-105">Per distribuzione delle applicazioni si intende l'installazione effettiva dei file binari delle applicazioni nelle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a556-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="7a556-106">Per l'esempio Music Store, è necessario installare e configurare .Net Core e IIS in ogni macchina virtuale,</span><span class="sxs-lookup"><span data-stu-id="7a556-106">For the Music Store sample, .Net Core and IIS need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="7a556-107">nonché installare i file binari di Music Store nella macchina virtuale e creare il database di Music Store.</span><span class="sxs-lookup"><span data-stu-id="7a556-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="7a556-108">Questo documento descrive in che modo le estensioni delle macchine virtuali possono automatizzare la distribuzione e la configurazione di applicazioni nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a556-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="7a556-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="7a556-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="7a556-110">Per ottenere risultati ottimali, pre-distribuire un'istanza della soluzione alla propria sottoscrizione di Azure ed esercitarsi con il modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a556-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="7a556-111">Il modello completo è disponibile in [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows) (Distribuzione di Music Store in Windows).</span><span class="sxs-lookup"><span data-stu-id="7a556-111">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="7a556-112">Script di configurazione</span><span class="sxs-lookup"><span data-stu-id="7a556-112">Configuration script</span></span>
<span data-ttu-id="7a556-113">Le estensioni delle macchine virtuali sono programmi specializzati che vengono eseguiti sulle macchine virtuali per automatizzare le attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7a556-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="7a556-114">Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker.</span><span class="sxs-lookup"><span data-stu-id="7a556-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="7a556-115">L'estensione script personalizzata può essere usata per eseguire uno script su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7a556-115">The Custom Script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="7a556-116">Nel caso dell'esempio Music Store, l'estensione script personalizzata viene usata per configurare le macchine virtuali Windows e installare l'applicazione Music Store.</span><span class="sxs-lookup"><span data-stu-id="7a556-116">With the Music Store sample, it is up to the custom script extension to configure the Windows virtual machines and install the Music Store application.</span></span>

<span data-ttu-id="7a556-117">Prima di vedere in che modo le estensioni delle macchine virtuali sono dichiarate in un modello di Azure Resource Manager, esaminare lo script che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="7a556-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="7a556-118">Questo script configura la macchina virtuale Windows in modo da ospitare l'applicazione Music Store.</span><span class="sxs-lookup"><span data-stu-id="7a556-118">This script configures the Windows virtual machine to host the Music Store application.</span></span> <span data-ttu-id="7a556-119">Durante l'esecuzione, lo script installa tutto il software necessario, installa l'applicazione Music Store dal controllo del codice sorgente e prepara il database.</span><span class="sxs-lookup"><span data-stu-id="7a556-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

> <span data-ttu-id="7a556-120">Questo esempio è fornito a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="7a556-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="7a556-121">Estensione script della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7a556-121">VM Script Extension</span></span>
<span data-ttu-id="7a556-122">Le estensioni delle macchine virtuali possono essere eseguite su una macchina virtuale in fase di compilazione includendo la risorsa dell'estensione nel modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7a556-122">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="7a556-123">È possibile aggiungere l'estensione usando la procedura guidata Aggiungi nuova risorsa di Visual Studio o inserendo una risorsa JSON valida nel modello.</span><span class="sxs-lookup"><span data-stu-id="7a556-123">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="7a556-124">La risorsa dell'estensione script è annidata all'interno della risorsa della macchina virtuale, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7a556-124">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="7a556-125">Fare clic su questo collegamento per vedere l'esempio JSON incluso nel modello di Resource Manager: [Estensione script della macchina virtuale](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="7a556-125">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="7a556-126">Nel codice JSON seguente è possibile notare che lo script è archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a556-126">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="7a556-127">Questo script può essere incluso anche nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a556-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="7a556-128">Inoltre, i modelli di Azure Resource Manager consentono di creare la stringa di esecuzione dello script in modo che i valori dei parametri del modello siano utilizzabili come parametri per l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="7a556-128">Also, Azure Resource Manager templates allow the script execution string to be constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="7a556-129">In questo caso, i dati vengono forniti quando si distribuiscono i modelli e questi valori possono quindi essere usati durante l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="7a556-129">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="7a556-130">Come indicato in precedenza, è anche possibile archiviare gli script personalizzati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a556-130">As mentioned above, it is also possible to store your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="7a556-131">Esistono due possibilità di archiviazione per le risorse di script nell'archivio BLOB: rendere pubblico il contenitore o lo script e seguire l'approccio descritto in precedenza, oppure mantenere l'archivio BLOB privato il che implica indicare storageAccountName e storageAccountKey nella definizione della risorsa CustomScriptExtension.</span><span class="sxs-lookup"><span data-stu-id="7a556-131">There are two options for storing the script resources in blob storage; either make the container/script public and follow the same approach as above, or it can also be kept in private blob storage which requires you to provide the storageAccountName and storageAccountKey to the CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="7a556-132">Nell'esempio seguente è stato effettuato un passaggio in più.</span><span class="sxs-lookup"><span data-stu-id="7a556-132">In the example below we have gone a step further.</span></span> <span data-ttu-id="7a556-133">Sebbene sia possibile indicare il nome e la chiave dell'account di archiviazione come parametro o variabile durante la distribuzione, i modelli di Resource Manager implementano la funzione `listKeys` che può recuperare la chiave dell'account di archiviazione a livello di programmazione e inserirla nel modello in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7a556-133">While it is possible to provide the storage account name and key as a parameter or variable during deployment, Resource Manager templates provide the `listKeys` function that can obtain the storage account key programmatically and insert it in to the template for you at deployment time.</span></span>

<span data-ttu-id="7a556-134">Nell'esempio di definizione di risorsa CustomScriptExtension riportato di seguito, lo script personalizzato è già stato caricato in un account di archiviazione di Azure denominato `mystorageaccount9999` che esiste in un altro gruppo di risorse denominato `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="7a556-134">In the example CustomScriptExtension resource definition below, our custom script has already been uploaded to an Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="7a556-135">Quando si distribuisce un modello contenente questa risorsa, la funzione `listKeys` recupera a livello di programmazione la chiave dell'account di archiviazione per l'account di archiviazione `mystorageaccount9999` nel gruppo di risorse `mysa999rgname` e la inserisce nel modello.</span><span class="sxs-lookup"><span data-stu-id="7a556-135">When we deploy a template containing this resource, the `listKeys` function programmatically obtains the storage account key for the storage account `mystorageaccount9999` in the Resource Group `mysa999rgname` and inserts it in to the template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="7a556-136">Il principale vantaggio di questo approccio è che non è necessario modificare i parametri del modello o della distribuzione nel caso in cui la chiave dell'account di archiviazione venga modificata.</span><span class="sxs-lookup"><span data-stu-id="7a556-136">The main benefit of this approach is that it does not require you to change your template or deployment parameters in the event of the storage account key changing.</span></span>

<span data-ttu-id="7a556-137">Per altre informazioni sull'estensione script personalizzata, vedere [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Estensioni script personalizzate con i modelli di Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="7a556-137">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="7a556-138">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="7a556-138">Next Step</span></span>
<hr>

[<span data-ttu-id="7a556-139">Explore More Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="7a556-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

