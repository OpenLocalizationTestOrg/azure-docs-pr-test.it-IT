---
title: aaaCreate e gestire un linguaggio per macchina virtuale utilizzando Azure | Documenti Microsoft
description: Utilizzare toodeploy Java e Azure Resource Manager una macchina virtuale e tutte le risorse di supporto.
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
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="55f3c-103">Creare e gestire macchine virtuali Windows in Azure tramite Java</span><span class="sxs-lookup"><span data-stu-id="55f3c-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="55f3c-104">Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="55f3c-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="55f3c-105">Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Java.</span><span class="sxs-lookup"><span data-stu-id="55f3c-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="55f3c-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="55f3c-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="55f3c-107">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="55f3c-107">Create a Maven project</span></span>
> * <span data-ttu-id="55f3c-108">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="55f3c-108">Add dependencies</span></span>
> * <span data-ttu-id="55f3c-109">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="55f3c-109">Create credentials</span></span>
> * <span data-ttu-id="55f3c-110">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="55f3c-110">Create resources</span></span>
> * <span data-ttu-id="55f3c-111">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="55f3c-111">Perform management tasks</span></span>
> * <span data-ttu-id="55f3c-112">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="55f3c-112">Delete resources</span></span>
> * <span data-ttu-id="55f3c-113">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-113">Run hello application</span></span>

<span data-ttu-id="55f3c-114">Sono necessari circa 20 minuti toodo questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="55f3c-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="55f3c-115">Creare un progetto Maven</span><span class="sxs-lookup"><span data-stu-id="55f3c-115">Create a Maven project</span></span>

1. <span data-ttu-id="55f3c-116">Installare [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), se non lo si è già fatto.</span><span class="sxs-lookup"><span data-stu-id="55f3c-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="55f3c-117">Installare [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="55f3c-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="55f3c-118">Creare un nuovo progetto di cartella e hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-118">Create a new folder and hello project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="55f3c-119">Aggiungere le dipendenze</span><span class="sxs-lookup"><span data-stu-id="55f3c-119">Add dependencies</span></span>

1. <span data-ttu-id="55f3c-120">In hello `testAzureApp` cartella, aprire hello `pom.xml` file e aggiungere la configurazione di compilazione hello troppo&lt;progetto&gt; compilazione hello tooenable dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="55f3c-120">Under hello `testAzureApp` folder, open hello `pom.xml` file and add hello build configuration too&lt;project&gt; tooenable hello building of your application:</span></span>

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

2. <span data-ttu-id="55f3c-121">Aggiungere le dipendenze di hello che sono necessari tooaccess hello Azure SDK per Java.</span><span class="sxs-lookup"><span data-stu-id="55f3c-121">Add hello dependencies that are needed tooaccess hello Azure Java SDK.</span></span>

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

3. <span data-ttu-id="55f3c-122">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-122">Save hello file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="55f3c-123">Creare le credenziali</span><span class="sxs-lookup"><span data-stu-id="55f3c-123">Create credentials</span></span>

<span data-ttu-id="55f3c-124">Prima di iniziare questo passaggio, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55f3c-124">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="55f3c-125">È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="55f3c-125">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="55f3c-126">Creare il file di autorizzazione hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-126">Create hello authorization file</span></span>

1. <span data-ttu-id="55f3c-127">Creare un file denominato `azureauth.properties` e aggiungere tooit queste proprietà:</span><span class="sxs-lookup"><span data-stu-id="55f3c-127">Create a file named `azureauth.properties` and add these properties tooit:</span></span>

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

    <span data-ttu-id="55f3c-128">Sostituire  **&lt;id sottoscrizione&gt;**  con l'identificatore della sottoscrizione,  **&lt;id applicazione&gt;**  con hello applicazione Active Directory identificatore,  **&lt;chiave di autenticazione&gt;**  con chiave applicazione hello e  **&lt;id tenant&gt;**  con tenant hello identificatore.</span><span class="sxs-lookup"><span data-stu-id="55f3c-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

2. <span data-ttu-id="55f3c-129">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-129">Save hello file.</span></span>
3. <span data-ttu-id="55f3c-130">Impostare una variabile di ambiente denominata AZURE_AUTH_LOCATION nella shell con file di autenticazione toohello hello percorso completo.</span><span class="sxs-lookup"><span data-stu-id="55f3c-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with hello full path toohello authentication file.</span></span>

### <a name="create-hello-management-client"></a><span data-ttu-id="55f3c-131">Creare il client di gestione hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-131">Create hello management client</span></span>

1. <span data-ttu-id="55f3c-132">Aprire hello `App.java` file `src\main\java\com\fabrikam` e assicurarsi che l'istruzione di pacchetto è nella parte superiore di hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-132">Open hello `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at hello top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="55f3c-133">In istruzione package hello, Aggiungi queste istruzioni import:</span><span class="sxs-lookup"><span data-stu-id="55f3c-133">Under hello package statement, add these import statements:</span></span>
   
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

2. <span data-ttu-id="55f3c-134">le credenziali di Active Directory hello toocreate toomake richieste, è necessario aggiungere questo codice toohello principale metodo hello classe App:</span><span class="sxs-lookup"><span data-stu-id="55f3c-134">toocreate hello Active Directory credentials that you need toomake requests, add this code toohello main method of hello App class:</span></span>
   
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

## <a name="create-resources"></a><span data-ttu-id="55f3c-135">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="55f3c-135">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="55f3c-136">Creare il gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-136">Create hello resource group</span></span>

<span data-ttu-id="55f3c-137">Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55f3c-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="55f3c-138">i valori per toospecify hello applicazione e creare il gruppo di risorse hello, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-138">toospecify values for hello application and create hello resource group, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="55f3c-139">Creare set di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-139">Create hello availability set</span></span>

<span data-ttu-id="55f3c-140">[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="55f3c-140">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="55f3c-141">set di disponibilità hello toocreate, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-141">toocreate hello availability set, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a><span data-ttu-id="55f3c-142">Creare l'indirizzo IP pubblico hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-142">Create hello public IP address</span></span>

<span data-ttu-id="55f3c-143">Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="55f3c-144">toocreate hello indirizzo IP pubblico per la macchina virtuale hello, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-144">toocreate hello public IP address for hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="55f3c-145">Creare una rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-145">Create hello virtual network</span></span>

<span data-ttu-id="55f3c-146">Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55f3c-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="55f3c-147">toocreate una subnet e una rete virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-147">toocreate a subnet and a virtual network, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-network-interface"></a><span data-ttu-id="55f3c-148">Creare l'interfaccia di rete hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-148">Create hello network interface</span></span>

<span data-ttu-id="55f3c-149">Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-149">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="55f3c-150">toocreate un'interfaccia di rete, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-150">toocreate a network interface, add this code toohello try block in hello main method:</span></span>

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

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="55f3c-151">Creare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-151">Create hello virtual machine</span></span>

<span data-ttu-id="55f3c-152">Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="55f3c-152">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="55f3c-153">toocreate hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-153">toocreate hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="55f3c-154">Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-154">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="55f3c-155">toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="55f3c-155">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="55f3c-156">Se si desidera toouse un disco esistente anziché un'immagine del marketplace, è possibile utilizzare questo codice:</span><span class="sxs-lookup"><span data-stu-id="55f3c-156">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span> 

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

## <a name="perform-management-tasks"></a><span data-ttu-id="55f3c-157">Eseguire le attività di gestione</span><span class="sxs-lookup"><span data-stu-id="55f3c-157">Perform management tasks</span></span>

<span data-ttu-id="55f3c-158">Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="55f3c-158">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="55f3c-159">Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="55f3c-159">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="55f3c-160">Quando è necessario toodo con hello VM, è necessario tooget un'istanza.</span><span class="sxs-lookup"><span data-stu-id="55f3c-160">When you need toodo anything with hello VM, you need tooget an instance of it.</span></span> <span data-ttu-id="55f3c-161">Aggiungere questo blocco try toohello di codice del metodo principale di hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-161">Add this code toohello try block of hello main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="55f3c-162">Ottenere informazioni su hello VM</span><span class="sxs-lookup"><span data-stu-id="55f3c-162">Get information about hello VM</span></span>

<span data-ttu-id="55f3c-163">tooget informazioni hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-163">tooget information about hello virtual machine, add this code toohello try block in hello main method:</span></span>

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
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a><span data-ttu-id="55f3c-164">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-164">Stop hello VM</span></span>

<span data-ttu-id="55f3c-165">È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo.</span><span class="sxs-lookup"><span data-stu-id="55f3c-165">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="55f3c-166">Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.</span><span class="sxs-lookup"><span data-stu-id="55f3c-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="55f3c-167">macchina virtuale di hello toostop senza deallocarlo, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-167">toostop hello virtual machine without deallocating it, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

<span data-ttu-id="55f3c-168">Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello spento chiamata:</span><span class="sxs-lookup"><span data-stu-id="55f3c-168">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="55f3c-169">Avviare hello VM</span><span class="sxs-lookup"><span data-stu-id="55f3c-169">Start hello VM</span></span>

<span data-ttu-id="55f3c-170">toostart hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-170">toostart hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="55f3c-171">Ridimensionare hello VM</span><span class="sxs-lookup"><span data-stu-id="55f3c-171">Resize hello VM</span></span>

<span data-ttu-id="55f3c-172">Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="55f3c-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="55f3c-173">Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="55f3c-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="55f3c-174">toochange dimensioni della macchina virtuale hello, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-174">toochange size of hello virtual machine, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="55f3c-175">Aggiungere un toohello disco dati VM</span><span class="sxs-lookup"><span data-stu-id="55f3c-175">Add a data disk toohello VM</span></span>

<span data-ttu-id="55f3c-176">tooadd una macchina virtuale su disco toohello per dati con 2 GB di dimensioni, dispone di un LUN pari a 0 e un tipo di memorizzazione nella cache di lettura/scrittura, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-176">tooadd a data disk toohello virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code toohello try block in hello main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="55f3c-177">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="55f3c-177">Delete resources</span></span>

<span data-ttu-id="55f3c-178">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="55f3c-178">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="55f3c-179">Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="55f3c-179">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="55f3c-180">risorsa hello toodelete gruppo, aggiungere questo blocco try toohello di codice nel metodo main hello:</span><span class="sxs-lookup"><span data-stu-id="55f3c-180">toodelete hello resource group, add this code toohello try block in hello main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="55f3c-181">Salvare il file di App.java hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-181">Save hello App.java file.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="55f3c-182">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="55f3c-182">Run hello application</span></span>

<span data-ttu-id="55f3c-183">Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish.</span><span class="sxs-lookup"><span data-stu-id="55f3c-183">It should take about five minutes for this console application toorun completely from start toofinish.</span></span>

1. <span data-ttu-id="55f3c-184">toorun hello applicazione, utilizzare il comando di Maven:</span><span class="sxs-lookup"><span data-stu-id="55f3c-184">toorun hello application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="55f3c-185">Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="55f3c-185">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="55f3c-186">Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="55f3c-186">Click hello deployment status toosee information about hello deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55f3c-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="55f3c-187">Next steps</span></span>
* <span data-ttu-id="55f3c-188">Ulteriori informazioni sull'utilizzo di hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="55f3c-188">Learn more about using hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

