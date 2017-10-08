---
title: aaaCreate e gestire un Azure macchina virtuale utilizzando c# | Documenti Microsoft
description: Utilizzare toodeploy c# e Azure Resource Manager una macchina virtuale e tutte le risorse di supporto.
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
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="8a20c-103">Creare e gestire macchine virtuali Windows in Azure tramite C#</span><span class="sxs-lookup"><span data-stu-id="8a20c-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="8a20c-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a20c-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="8a20c-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale tramite C#.</span><span class="sxs-lookup"><span data-stu-id="8a20c-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="8a20c-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8a20c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a20c-107">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a20c-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="8a20c-108">Installare il pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-108">Install hello package</span></span>
> * <span data-ttu-id="8a20c-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="8a20c-109">Create credentials</span></span>
> * <span data-ttu-id="8a20c-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="8a20c-110">Create resources</span></span>
> * <span data-ttu-id="8a20c-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="8a20c-111">Perform management tasks</span></span>
> * <span data-ttu-id="8a20c-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="8a20c-112">Delete resources</span></span>
> * <span data-ttu-id="8a20c-113">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-113">Run hello application</span></span>

<span data-ttu-id="8a20c-114">Sono necessari circa 20 minuti toodo questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="8a20c-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="8a20c-115">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a20c-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="8a20c-116">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="8a20c-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="8a20c-117">Selezionare **lo sviluppo desktop .NET** hello pagina carichi di lavoro e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="8a20c-118">In hello riepilogo, è possibile vedere che **gli strumenti di sviluppo di .NET Framework 4 a 4.6** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8a20c-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="8a20c-119">Se già stato installato Visual Studio, è possibile aggiungere hello .NET il carico di lavoro hello utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a20c-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="8a20c-120">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="8a20c-121">In **modelli** > **Visual c#**selezionare **applicazione Console (.NET Framework)**, immettere *myDotnetProject* per nome hello del progetto, il percorso di selezione hello del progetto di hello, Hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="8a20c-122">Installare il pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-122">Install hello package</span></span>

<span data-ttu-id="8a20c-123">Pacchetti NuGet sono hello più semplice modo tooinstall hello librerie necessario toofinish questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="8a20c-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="8a20c-124">librerie di hello tooget che è necessario in Visual Studio, eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="8a20c-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="8a20c-125">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="8a20c-126">Nella console di hello, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a20c-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="8a20c-127">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="8a20c-127">Create credentials</span></span>

<span data-ttu-id="8a20c-128">Prima di iniziare questo passaggio, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8a20c-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="8a20c-129">È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="8a20c-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="8a20c-130">Creare il file di autorizzazione hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-130">Create hello authorization file</span></span>

1. <span data-ttu-id="8a20c-131">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="8a20c-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="8a20c-132">File con nome hello *azureauth.properties*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="8a20c-133">Aggiungere le proprietà di autorizzazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a20c-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="8a20c-134">Sostituire  **&lt;id sottoscrizione&gt;**  con l'identificatore della sottoscrizione,  **&lt;id applicazione&gt;**  con hello applicazione Active Directory identificatore,  **&lt;chiave di autenticazione&gt;**  con chiave applicazione hello e  **&lt;id tenant&gt;**  con tenant hello identificatore.</span><span class="sxs-lookup"><span data-stu-id="8a20c-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="8a20c-135">Salvare il file di azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="8a20c-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="8a20c-136">Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con file di tooauthorization hello percorso completo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="8a20c-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="8a20c-137">Ad esempio, consente hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="8a20c-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="8a20c-138">Creare il client di gestione hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-138">Create hello management client</span></span>

1. <span data-ttu-id="8a20c-139">Aprire il file Program.cs hello per progetto hello creato e quindi aggiungerle utilizzando istruzioni esistente toohello all'inizio del file hello:</span><span class="sxs-lookup"><span data-stu-id="8a20c-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="8a20c-140">client di gestione di hello toocreate, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="8a20c-141">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="8a20c-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="8a20c-142">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-142">Create hello resource group</span></span>

<span data-ttu-id="8a20c-143">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a20c-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="8a20c-144">i valori per toospecify hello applicazione e creare il gruppo di risorse hello, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="8a20c-145">Creare set di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-145">Create hello availability set</span></span>

<span data-ttu-id="8a20c-146">[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a20c-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="8a20c-147">set di disponibilità hello toocreate, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="8a20c-148">Creare l'indirizzo IP pubblico hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-148">Create hello public IP address</span></span>

<span data-ttu-id="8a20c-149">Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8a20c-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="8a20c-150">toocreate hello indirizzo IP pubblico per la macchina virtuale hello, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="8a20c-151">Creare una rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-151">Create hello virtual network</span></span>

<span data-ttu-id="8a20c-152">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a20c-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="8a20c-153">toocreate una subnet e una rete virtuale, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="8a20c-154">Creare l'interfaccia di rete hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-154">Create hello network interface</span></span>

<span data-ttu-id="8a20c-155">Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8a20c-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="8a20c-156">toocreate un'interfaccia di rete, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-156">toocreate a network interface, add this code toohello Main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="8a20c-157">Creare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-157">Create hello virtual machine</span></span>

<span data-ttu-id="8a20c-158">Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a20c-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="8a20c-159">toocreate hello macchina virtuale, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

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
> <span data-ttu-id="8a20c-160">Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="8a20c-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="8a20c-161">toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a20c-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="8a20c-162">Se si desidera toouse un disco esistente anziché un'immagine del marketplace, è possibile utilizzare questo codice:</span><span class="sxs-lookup"><span data-stu-id="8a20c-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="8a20c-163">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="8a20c-163">Perform management tasks</span></span>

<span data-ttu-id="8a20c-164">Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8a20c-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="8a20c-165">Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="8a20c-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="8a20c-166">Quando è necessario toodo con hello VM, è necessario tooget un'istanza:</span><span class="sxs-lookup"><span data-stu-id="8a20c-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="8a20c-167">Ottenere informazioni su hello VM</span><span class="sxs-lookup"><span data-stu-id="8a20c-167">Get information about hello VM</span></span>

<span data-ttu-id="8a20c-168">tooget informazioni hello macchina virtuale, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
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
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="8a20c-169">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-169">Stop hello VM</span></span>

<span data-ttu-id="8a20c-170">È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo.</span><span class="sxs-lookup"><span data-stu-id="8a20c-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="8a20c-171">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="8a20c-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="8a20c-172">macchina virtuale di hello toostop senza deallocarlo, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="8a20c-173">Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello spento chiamata:</span><span class="sxs-lookup"><span data-stu-id="8a20c-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="8a20c-174">Avviare hello VM</span><span class="sxs-lookup"><span data-stu-id="8a20c-174">Start hello VM</span></span>

<span data-ttu-id="8a20c-175">toostart hello macchina virtuale, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="8a20c-176">Ridimensionare hello VM</span><span class="sxs-lookup"><span data-stu-id="8a20c-176">Resize hello VM</span></span>

<span data-ttu-id="8a20c-177">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8a20c-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="8a20c-178">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8a20c-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="8a20c-179">toochange dimensioni della macchina virtuale hello, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="8a20c-180">Aggiungere un toohello disco dati VM</span><span class="sxs-lookup"><span data-stu-id="8a20c-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="8a20c-181">tooadd una macchina virtuale toohello disco dati, aggiungere questo tooadd di metodo Main toohello codice un disco dati è di 2 GB di dimensioni, han un LUN pari a 0 e un tipo di memorizzazione nella cache di lettura/scrittura:</span><span class="sxs-lookup"><span data-stu-id="8a20c-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="8a20c-182">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="8a20c-182">Delete resources</span></span>

<span data-ttu-id="8a20c-183">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="8a20c-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="8a20c-184">Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="8a20c-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="8a20c-185">risorsa hello toodelete gruppo, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="8a20c-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="8a20c-186">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="8a20c-186">Run hello application</span></span>

<span data-ttu-id="8a20c-187">Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish.</span><span class="sxs-lookup"><span data-stu-id="8a20c-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="8a20c-188">un'applicazione console hello toorun, fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="8a20c-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="8a20c-189">Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a20c-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="8a20c-190">Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="8a20c-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a20c-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a20c-191">Next steps</span></span>
* <span data-ttu-id="8a20c-192">Sfruttare utilizzando un toocreate modello una macchina virtuale utilizzando informazioni hello [distribuire una macchina virtuale di Azure con c# e un modello di gestione risorse](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a20c-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="8a20c-193">Ulteriori informazioni sull'utilizzo di hello [Azure libraries per .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="8a20c-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

