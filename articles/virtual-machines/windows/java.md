---
title: Creare e gestire una macchina virtuale di Azure tramite Java | Microsoft Docs
description: Usare Java e Azure Resource Manager per distribuire una macchina virtuale e tutte le relative risorse di supporto.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b9e739a07c5863577285fb3a221b372b385c6762
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="82c05-103">Creare e gestire macchine virtuali Windows in Azure tramite Java</span><span class="sxs-lookup"><span data-stu-id="82c05-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="82c05-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="82c05-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="82c05-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Java.</span><span class="sxs-lookup"><span data-stu-id="82c05-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="82c05-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="82c05-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82c05-107">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="82c05-107">Create a Maven project</span></span>
> * <span data-ttu-id="82c05-108">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="82c05-108">Add dependencies</span></span>
> * <span data-ttu-id="82c05-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="82c05-109">Create credentials</span></span>
> * <span data-ttu-id="82c05-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="82c05-110">Create resources</span></span>
> * <span data-ttu-id="82c05-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="82c05-111">Perform management tasks</span></span>
> * <span data-ttu-id="82c05-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="82c05-112">Delete resources</span></span>
> * <span data-ttu-id="82c05-113">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="82c05-113">Run the application</span></span>

<span data-ttu-id="82c05-114">L'esecuzione di questi passaggi richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="82c05-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="82c05-115">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="82c05-115">Create a Maven project</span></span>

1. <span data-ttu-id="82c05-116">Installare [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), se non lo si è già fatto.</span><span class="sxs-lookup"><span data-stu-id="82c05-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="82c05-117">Installare [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="82c05-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="82c05-118">Creare una nuova cartella e il progetto:</span><span class="sxs-lookup"><span data-stu-id="82c05-118">Create a new folder and the project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="82c05-119">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="82c05-119">Add dependencies</span></span>

1. <span data-ttu-id="82c05-120">Nella cartella `testAzureApp` aprire il file `pom.xml` e aggiungere la configurazione della build al &lt;progetto&gt; per abilitare la compilazione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="82c05-120">Under the `testAzureApp` folder, open the `pom.xml` file and add the build configuration to &lt;project&gt; to enable the building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="82c05-121">Aggiungere le dipendenze necessarie per accedere ad Azure SDK per Java.</span><span class="sxs-lookup"><span data-stu-id="82c05-121">Add the dependencies that are needed to access the Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="82c05-122">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="82c05-122">Save the file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="82c05-123">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="82c05-123">Create credentials</span></span>

<span data-ttu-id="82c05-124">Prima di iniziare questo passaggio, assicurarsi di avere accesso a un'[entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="82c05-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="82c05-125">È inoltre necessario registrare l'ID dell'applicazione, la chiave di autenticazione e l'ID del tenant che saranno necessari in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="82c05-125">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="82c05-126">Creare il file di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="82c05-126">Create the authorization file</span></span>

1. <span data-ttu-id="82c05-127">Creare un file denominato `azureauth.properties` e aggiungervi queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="82c05-127">Create a file named `azureauth.properties` and add these properties to it:</span></span>

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

    <span data-ttu-id="82c05-128">Sostituire **&lt;subscription-id&gt;** con l'identificatore della sottoscrizione, **&lt;application-id&gt;** con l'identificatore dell'applicazione Active Directory, **&lt;authentication-key&gt;** con la chiave dell'applicazione e **&lt;tenant-id&gt;** con l'identificatore del tenant.</span><span class="sxs-lookup"><span data-stu-id="82c05-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

2. <span data-ttu-id="82c05-129">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="82c05-129">Save the file.</span></span>
3. <span data-ttu-id="82c05-130">Impostare una variabile di ambiente denominata AZURE_AUTH_LOCATION nella shell con il percorso completo al file di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="82c05-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with the full path to the authentication file.</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="82c05-131">Creare il client di gestione</span><span class="sxs-lookup"><span data-stu-id="82c05-131">Create the management client</span></span>

1. <span data-ttu-id="82c05-132">Aprire il file `App.java` in `src\main\java\com\fabrikam` e verificare che questa istruzione package si trovi all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="82c05-132">Open the `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at the top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="82c05-133">Sotto l'istruzione package aggiungere queste istruzioni import:</span><span class="sxs-lookup"><span data-stu-id="82c05-133">Under the package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="82c05-134">Per creare le credenziali di Active Directory necessarie per effettuare richieste, aggiungere il codice seguente al metodo main della classe App:</span><span class="sxs-lookup"><span data-stu-id="82c05-134">To create the Active Directory credentials that you need to make requests, add this code to the main method of the App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="82c05-135">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="82c05-135">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="82c05-136">Creare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="82c05-136">Create the resource group</span></span>

<span data-ttu-id="82c05-137">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82c05-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="82c05-138">Per specificare i valori per l'applicazione e creare il gruppo di risorse, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-138">To specify values for the application and create the resource group, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="82c05-139">Creare il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="82c05-139">Create the availability set</span></span>

<span data-ttu-id="82c05-140">I [set di disponibilità](tutorial-availability-sets.md) semplificano la manutenzione delle macchine virtuali usate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="82c05-140">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="82c05-141">Per creare il set di disponibilità, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-141">To create the availability set, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a><span data-ttu-id="82c05-142">Creare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="82c05-142">Create the public IP address</span></span>

<span data-ttu-id="82c05-143">Un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario per comunicare con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="82c05-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="82c05-144">Per creare l'indirizzo IP pubblico per la macchina virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-144">To create the public IP address for the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="82c05-145">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="82c05-145">Create the virtual network</span></span>

<span data-ttu-id="82c05-146">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82c05-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="82c05-147">Per creare una subnet e una rete virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-147">To create a subnet and a virtual network, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="82c05-148">Creare l'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="82c05-148">Create the network interface</span></span>

<span data-ttu-id="82c05-149">Una macchina virtuale richiede un'interfaccia di rete per comunicare nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="82c05-149">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="82c05-150">Per creare un'interfaccia di rete, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-150">To create a network interface, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="82c05-151">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="82c05-151">Create the virtual machine</span></span>

<span data-ttu-id="82c05-152">Dopo avere creato tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="82c05-152">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="82c05-153">Per creare la macchina virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-153">To create the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="82c05-154">Questa esercitazione illustra come creare una macchina virtuale in cui è in esecuzione una versione del sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="82c05-154">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="82c05-155">Per altre informazioni sulla selezione di altre immagini, vedere [Esplorare e selezionare immagini delle macchine virtuali di Azure con Windows PowerShell e l'interfaccia della riga di comando di Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82c05-155">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="82c05-156">Se si desidera usare un disco esistente invece di un'immagine del marketplace, usare questo codice:</span><span class="sxs-lookup"><span data-stu-id="82c05-156">If you want to use an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="82c05-157">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="82c05-157">Perform management tasks</span></span>

<span data-ttu-id="82c05-158">Durante il ciclo di vita di una macchina virtuale si eseguono attività di gestione come l'avvio, l'arresto o l'eliminazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="82c05-158">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="82c05-159">È inoltre possibile creare codice per automatizzare le attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="82c05-159">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="82c05-160">Quando si deve eseguire un'operazione con la macchina virtuale, è necessario ottenere un'istanza della VM.</span><span class="sxs-lookup"><span data-stu-id="82c05-160">When you need to do anything with the VM, you need to get an instance of it.</span></span> <span data-ttu-id="82c05-161">Aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-161">Add this code to the try block of the main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="82c05-162">Ottenere informazioni sulla VM</span><span class="sxs-lookup"><span data-stu-id="82c05-162">Get information about the VM</span></span>

<span data-ttu-id="82c05-163">Per ottenere informazioni sulla macchina virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-163">To get information about the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a><span data-ttu-id="82c05-164">Arrestare la VM</span><span class="sxs-lookup"><span data-stu-id="82c05-164">Stop the VM</span></span>

<span data-ttu-id="82c05-165">È possibile arrestare una macchina virtuale e mantenere tutte le sue impostazioni, pur continuando a vedersela addebitata oppure è possibile arrestare una macchina virtuale e deallocarla.</span><span class="sxs-lookup"><span data-stu-id="82c05-165">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="82c05-166">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="82c05-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="82c05-167">Per arrestare la macchina virtuale senza deallocarla, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-167">To stop the virtual machine without deallocating it, add this code to the try block in the main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

<span data-ttu-id="82c05-168">Per deallocare la macchina virtuale, sostituire la chiamata PowerOff con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="82c05-168">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```java
vm.deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="82c05-169">Avviare la VM</span><span class="sxs-lookup"><span data-stu-id="82c05-169">Start the VM</span></span>

<span data-ttu-id="82c05-170">Per avviare la macchina virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-170">To start the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="82c05-171">Ridimensionare la VM</span><span class="sxs-lookup"><span data-stu-id="82c05-171">Resize the VM</span></span>

<span data-ttu-id="82c05-172">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="82c05-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="82c05-173">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="82c05-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="82c05-174">Per modificare le dimensioni della macchina virtuale, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-174">To change size of the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="82c05-175">Aggiungere un disco dati alla VM</span><span class="sxs-lookup"><span data-stu-id="82c05-175">Add a data disk to the VM</span></span>

<span data-ttu-id="82c05-176">Per aggiungere un disco dati alla macchina virtuale con dimensioni di 2 GB, un numero di unità logica pari a 0 e una memorizzazione nella cache di tipo ReadWrite, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-176">To add a data disk to the virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code to the try block in the main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="82c05-177">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="82c05-177">Delete resources</span></span>

<span data-ttu-id="82c05-178">Poiché vengono applicati addebiti per le risorse usate in Azure, è sempre consigliabile eliminare le risorse che non sono più necessarie.</span><span class="sxs-lookup"><span data-stu-id="82c05-178">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="82c05-179">Per eliminare le macchine virtuali e tutte le risorse di supporto, è sufficiente eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="82c05-179">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="82c05-180">Per eliminare il gruppo di risorse, aggiungere questo codice al blocco try nel metodo main:</span><span class="sxs-lookup"><span data-stu-id="82c05-180">To delete the resource group, add this code to the try block in the main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="82c05-181">Salvare il file App.java.</span><span class="sxs-lookup"><span data-stu-id="82c05-181">Save the App.java file.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="82c05-182">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="82c05-182">Run the application</span></span>

<span data-ttu-id="82c05-183">L'esecuzione completa dell'applicazione console dall'inizio alla fine richiederà circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="82c05-183">It should take about five minutes for this console application to run completely from start to finish.</span></span>

1. <span data-ttu-id="82c05-184">Per eseguire l'applicazione, usare questo comando di Maven:</span><span class="sxs-lookup"><span data-stu-id="82c05-184">To run the application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="82c05-185">Prima di premere **INVIO** per avviare l'eliminazione delle risorse, è consigliabile dedicare alcuni minuti alla verifica della creazione delle risorse nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="82c05-185">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="82c05-186">Fare clic sullo stato della distribuzione per visualizzare le informazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="82c05-186">Click the deployment status to see information about the deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82c05-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82c05-187">Next steps</span></span>
* <span data-ttu-id="82c05-188">Altre informazioni sull'uso delle [librerie di Azure per Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="82c05-188">Learn more about using the [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

