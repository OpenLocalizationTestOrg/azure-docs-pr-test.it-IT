---
title: Creare e gestire una macchina virtuale di Azure tramite C# | Microsoft Docs
description: Usare C# e Azure Resource Manager per distribuire una macchina virtuale e tutte le relative risorse di supporto.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="b6e0c-103">Creare e gestire macchine virtuali Windows in Azure tramite C#</span><span class="sxs-lookup"><span data-stu-id="b6e0c-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="b6e0c-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="b6e0c-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale tramite C#.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="b6e0c-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b6e0c-107">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6e0c-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="b6e0c-108">Installare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="b6e0c-108">Install the package</span></span>
> * <span data-ttu-id="b6e0c-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="b6e0c-109">Create credentials</span></span>
> * <span data-ttu-id="b6e0c-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="b6e0c-110">Create resources</span></span>
> * <span data-ttu-id="b6e0c-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-111">Perform management tasks</span></span>
> * <span data-ttu-id="b6e0c-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="b6e0c-112">Delete resources</span></span>
> * <span data-ttu-id="b6e0c-113">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-113">Run the application</span></span>

<span data-ttu-id="b6e0c-114">L'esecuzione di questi passaggi richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="b6e0c-115">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6e0c-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="b6e0c-116">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="b6e0c-117">Selezionare **Sviluppo per desktop .NET** nella pagina Carichi di lavoro e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="b6e0c-118">Nel riepilogo si noti che **Strumenti di sviluppo per .NET Framework 4-4.6** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="b6e0c-119">Se Visual Studio è già stato installato, è possibile aggiungere il carico di lavoro .NET usando l'utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="b6e0c-120">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="b6e0c-121">In **Modelli** > **Visual C#** selezionare **App console (.NET Framework)**, immettere *myDotnetProject* come nome del progetto, selezionare il percorso del progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="b6e0c-122">Installare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="b6e0c-122">Install the package</span></span>

<span data-ttu-id="b6e0c-123">I pacchetti NuGet sono il modo più semplice per installare le librerie necessarie per completare questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="b6e0c-124">Per ottenere le librerie necessarie in Visual Studio, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="b6e0c-125">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="b6e0c-126">Nella console digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="b6e0c-127">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="b6e0c-127">Create credentials</span></span>

<span data-ttu-id="b6e0c-128">Prima di iniziare questo passaggio, assicurarsi di avere accesso a un'[entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b6e0c-129">È inoltre necessario registrare l'ID dell'applicazione, la chiave di autenticazione e l'ID del tenant che saranno necessari in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="b6e0c-130">Creare il file di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-130">Create the authorization file</span></span>

1. <span data-ttu-id="b6e0c-131">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="b6e0c-132">Assegnare al file il nome *azureauth.properties* e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="b6e0c-133">Aggiungere le proprietà di autorizzazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="b6e0c-134">Sostituire **&lt;subscription-id&gt;** con l'identificatore della sottoscrizione, **&lt;application-id&gt;** con l'identificatore dell'applicazione Active Directory, **&lt;authentication-key&gt;** con la chiave dell'applicazione e **&lt;tenant-id&gt;** con l'identificatore del tenant.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="b6e0c-135">Salvare il file azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="b6e0c-136">Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con il percorso completo verso il file di autorizzazione creato.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="b6e0c-137">Ad esempio, è possibile usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="b6e0c-138">Creare il client di gestione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-138">Create the management client</span></span>

1. <span data-ttu-id="b6e0c-139">Aprire il file Program.cs per il progetto creato e quindi aggiungere le istruzioni using seguenti alle istruzioni esistenti all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="b6e0c-140">Per creare i client di gestione, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="b6e0c-141">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="b6e0c-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="b6e0c-142">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-142">Create the resource group</span></span>

<span data-ttu-id="b6e0c-143">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b6e0c-144">Per specificare i valori per l'applicazione e creare il gruppo di risorse, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="b6e0c-145">Creare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="b6e0c-145">Create the availability set</span></span>

<span data-ttu-id="b6e0c-146">I [set di disponibilità](tutorial-availability-sets.md) semplificano la manutenzione delle macchine virtuali usate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="b6e0c-147">Per creare il set di disponibilità, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="b6e0c-148">Creare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="b6e0c-148">Create the public IP address</span></span>

<span data-ttu-id="b6e0c-149">Un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario per comunicare con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="b6e0c-150">Per creare l'indirizzo IP pubblico della macchina virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="b6e0c-151">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="b6e0c-151">Create the virtual network</span></span>

<span data-ttu-id="b6e0c-152">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="b6e0c-153">Per creare una subnet e una rete virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="b6e0c-154">Creare l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b6e0c-154">Create the network interface</span></span>

<span data-ttu-id="b6e0c-155">Una macchina virtuale richiede un'interfaccia di rete per comunicare nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="b6e0c-156">Per creare un'interfaccia di rete, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-156">To create a network interface, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="b6e0c-157">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b6e0c-157">Create the virtual machine</span></span>

<span data-ttu-id="b6e0c-158">Dopo avere creato tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="b6e0c-159">Per creare la macchina virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-159">To create the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="b6e0c-160">Questa esercitazione illustra come creare una macchina virtuale in cui è in esecuzione una versione del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="b6e0c-161">Per altre informazioni sulla selezione di altre immagini, vedere [Esplorare e selezionare immagini delle macchine virtuali di Azure con Windows PowerShell e l'interfaccia della riga di comando di Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="b6e0c-162">Se si desidera usare un disco esistente invece di un'immagine del marketplace, usare questo codice:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="b6e0c-163">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-163">Perform management tasks</span></span>

<span data-ttu-id="b6e0c-164">Durante il ciclo di vita di una macchina virtuale si eseguono attività di gestione come l'avvio, l'arresto o l'eliminazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="b6e0c-165">È inoltre possibile creare codice per automatizzare le attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="b6e0c-166">Quando si deve eseguire un'operazione con la macchina virtuale, è necessario ottenere un'istanza della stessa:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="b6e0c-167">Ottenere informazioni sulla VM</span><span class="sxs-lookup"><span data-stu-id="b6e0c-167">Get information about the VM</span></span>

<span data-ttu-id="b6e0c-168">Per ottenere informazioni sulla macchina virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="b6e0c-169">Arrestare la VM</span><span class="sxs-lookup"><span data-stu-id="b6e0c-169">Stop the VM</span></span>

<span data-ttu-id="b6e0c-170">È possibile arrestare una macchina virtuale e mantenere tutte le sue impostazioni, pur continuando a vedersela addebitata oppure è possibile arrestare una macchina virtuale e deallocarla.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="b6e0c-171">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="b6e0c-172">Per arrestare la macchina virtuale senza deallocarla, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="b6e0c-173">Per deallocare la macchina virtuale, sostituire la chiamata PowerOff con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="b6e0c-174">Avviare la VM</span><span class="sxs-lookup"><span data-stu-id="b6e0c-174">Start the VM</span></span>

<span data-ttu-id="b6e0c-175">Per avviare la macchina virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="b6e0c-176">Ridimensionare la VM</span><span class="sxs-lookup"><span data-stu-id="b6e0c-176">Resize the VM</span></span>

<span data-ttu-id="b6e0c-177">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="b6e0c-178">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="b6e0c-179">Per modificare le dimensioni della macchina virtuale, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="b6e0c-180">Aggiungere un disco dati alla VM</span><span class="sxs-lookup"><span data-stu-id="b6e0c-180">Add a data disk to the VM</span></span>

<span data-ttu-id="b6e0c-181">Per aggiungere un disco dati alla macchina virtuale, aggiungere questo codice al metodo Main per aggiungere un disco dati di 2 GB, un LUN pari a 0 e un tipo di caching di ReadWrite:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="b6e0c-182">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="b6e0c-182">Delete resources</span></span>

<span data-ttu-id="b6e0c-183">Poiché vengono applicati addebiti per le risorse usate in Azure, è sempre consigliabile eliminare le risorse che non sono più necessarie.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="b6e0c-184">Per eliminare le macchine virtuali e tutte le risorse di supporto, è sufficiente eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="b6e0c-185">Per eliminare il gruppo di risorse, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="b6e0c-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="b6e0c-186">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="b6e0c-186">Run the application</span></span>

<span data-ttu-id="b6e0c-187">L'esecuzione completa dell'applicazione console dall'inizio alla fine richiederà circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="b6e0c-188">Per eseguire l'applicazione console, fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="b6e0c-189">Prima di premere **INVIO** per avviare l'eliminazione delle risorse, è consigliabile dedicare alcuni minuti alla verifica della creazione delle risorse nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="b6e0c-190">Fare clic sullo stato della distribuzione per visualizzare le informazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="b6e0c-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6e0c-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6e0c-191">Next steps</span></span>
* <span data-ttu-id="b6e0c-192">Per usare un modello per creare una macchina virtuale, vedere le informazioni contenute in [Distribuire una macchina virtuale di Azure con C# e un modello di Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="b6e0c-193">Altre informazioni sull'uso delle [librerie di Azure per .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="b6e0c-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

