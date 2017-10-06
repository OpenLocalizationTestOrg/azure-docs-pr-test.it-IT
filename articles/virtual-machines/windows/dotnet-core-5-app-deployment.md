---
title: Distribuzione dell'applicazione con estensioni di macchine virtuali aaaAutomating | Documenti Microsoft
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
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="9bc85-103">Distribuzione di applicazioni con i modelli di Azure Resource Manager per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="9bc85-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="9bc85-104">Una volta tutti i requisiti infrastrutturali Azure sono stati identificati e convertiti in un modello di distribuzione, distribuzione di applicazione reale hello deve toobe risolti.</span><span class="sxs-lookup"><span data-stu-id="9bc85-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="9bc85-105">Distribuzione dell'applicazione qui fa riferimento a file binari dell'applicazione effettivo hello tooinstalling su risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc85-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="9bc85-106">Per esempio negozio hello, .net Core e IIS devono toobe installato e configurato in ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9bc85-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="9bc85-107">Hello negozio file binari necessari toobe installato nella macchina virtuale hello e database dell'archivio di musica hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9bc85-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="9bc85-108">Questo documento illustra in dettaglio come estensioni di macchine virtuali consente di automatizzare la distribuzione e configurazione tooAzure macchine virtuali dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9bc85-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="9bc85-109">Tutte le dipendenze e le configurazioni univoche sono evidenziate.</span><span class="sxs-lookup"><span data-stu-id="9bc85-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="9bc85-110">Per un'esperienza ottimale hello, pre-distribuire un'istanza di hello soluzione tooyour sottoscrizione di Azure e di lavoro nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="9bc85-111">è disponibili qui: modello completa Hello [musica archivio distribuzione in Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="9bc85-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="9bc85-112">Script di configurazione</span><span class="sxs-lookup"><span data-stu-id="9bc85-112">Configuration script</span></span>
<span data-ttu-id="9bc85-113">Estensioni di macchine virtuali sono programmi specializzati eseguite sui automazione configurazione tooprovide di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9bc85-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="9bc85-114">Le estensioni sono disponibili per molti scopi specifici, ad esempio un programma antivirus, la configurazione della registrazione e la configurazione di Docker.</span><span class="sxs-lookup"><span data-stu-id="9bc85-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="9bc85-115">Hello estensione Script personalizzato può essere utilizzato toorun qualsiasi a fronte di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9bc85-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="9bc85-116">Con l'esempio hello Negozio, è backup di macchine virtuali toohello script personalizzato estensione tooconfigure hello Windows e installare un'applicazione hello Negozio.</span><span class="sxs-lookup"><span data-stu-id="9bc85-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="9bc85-117">Prima che riporta in dettaglio come estensioni di macchine virtuali vengono dichiarate in un modello di gestione risorse di Azure, esaminare script hello che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="9bc85-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="9bc85-118">Questo script configura hello toohost di macchina virtuale Windows hello applicazione Negozio.</span><span class="sxs-lookup"><span data-stu-id="9bc85-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="9bc85-119">Durante l'esecuzione, script hello installa il software necessario tutte, installare un'applicazione hello musica archivio dal controllo del codice sorgente e preparare i database di hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="9bc85-120">Questo esempio è fornito a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="9bc85-120">This sample is for demonstration purposes.</span></span>

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

## <a name="vm-script-extension"></a><span data-ttu-id="9bc85-121">Estensione script della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9bc85-121">VM Script Extension</span></span>
<span data-ttu-id="9bc85-122">Le estensioni VM possibile eseguire in una macchina virtuale in fase di compilazione con l'inclusione di risorse di estensione hello nel modello di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="9bc85-123">Hello estensione può essere aggiunta con hello Visual Studio Aggiunta guidata risorsa o tramite l'inserimento di un oggetto JSON valido nel modello hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="9bc85-124">risorse di estensione dello Script Hello è annidata all'interno di hello risorsa macchina virtuale. può essere visto nell'esempio seguente hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="9bc85-125">Seguire questo esempio di collegamento toosee hello JSON all'interno di modello di gestione risorse hello- [estensione della macchina virtuale Script](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="9bc85-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="9bc85-126">Si noti che in hello seguito JSON che hello script viene archiviato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="9bc85-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="9bc85-127">Questo script può essere incluso anche nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc85-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="9bc85-128">Inoltre, i modelli di gestione risorse di Azure consentono hello script esecuzione stringa toobe costruito in modo che i valori di parametri di modello possono essere usati come parametri per l'esecuzione dello script.</span><span class="sxs-lookup"><span data-stu-id="9bc85-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="9bc85-129">In questo caso i dati vengono forniti durante la distribuzione di modelli di hello e questi valori possono quindi essere utilizzati durante l'esecuzione di script hello.</span><span class="sxs-lookup"><span data-stu-id="9bc85-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="9bc85-130">Come indicato in precedenza, è anche possibile toostore script personalizzato nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc85-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="9bc85-131">Sono disponibili due opzioni per l'archiviazione di risorse di script hello nell'archiviazione blob. rendere pubblico contenitore/script hello e seguire hello stesso approccio sopra, o può anche essere conservato nell'archiviazione blob privato che richiede il tooprovide hello storageAccountName e storageAccountKey toohello CustomScriptExtension definizione di risorsa.</span><span class="sxs-lookup"><span data-stu-id="9bc85-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="9bc85-132">Nel seguente esempio hello è stato effettuato un passaggio ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="9bc85-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="9bc85-133">Sebbene sia possibile tooprovide nome account di archiviazione hello e la chiave come parametro o variabile durante la distribuzione, i modelli di gestione risorse forniscono hello `listKeys` funzione che è possibile ottenere l'account di archiviazione hello chiave a livello di codice e inserirlo in toohello modello per l'utente in fase di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9bc85-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="9bc85-134">Nell'esempio hello CustomScriptExtension definizione di risorsa seguente, lo script personalizzato è già stato caricato tooan account di archiviazione di Azure denominato `mystorageaccount9999` che esiste in un altro gruppo di risorse denominato `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="9bc85-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="9bc85-135">Quando si distribuisce un modello che contiene la risorsa, hello `listKeys` funzione a livello di codice ottiene chiave dell'account di archiviazione per l'account di archiviazione hello hello `mystorageaccount9999` nel gruppo di risorse hello `mysa999rgname` e lo inserisce nel modello toohello per noi.</span><span class="sxs-lookup"><span data-stu-id="9bc85-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

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

<span data-ttu-id="9bc85-136">vantaggio principale di Hello di questo approccio è che non richiede toochange è il modello o i parametri di distribuzione nell'evento hello di hello Modifica chiave account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9bc85-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="9bc85-137">Per ulteriori informazioni sull'uso delle estensioni hello script personalizzato, vedere [le estensioni degli script personalizzati con modelli di gestione risorse](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9bc85-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="9bc85-138">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="9bc85-138">Next Step</span></span>
<hr>

[<span data-ttu-id="9bc85-139">Explore More Azure Resource Manager Templates</span><span class="sxs-lookup"><span data-stu-id="9bc85-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

