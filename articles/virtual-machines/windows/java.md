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
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Creare e gestire macchine virtuali Windows in Azure tramite Java

Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure. Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale usando Java. Si apprenderà come:

> [!div class="checklist"]
> * Creare un progetto Maven
> * Aggiungere le dipendenze
> * Creare le credenziali
> * Creare le risorse
> * Eseguire le attività di gestione
> * Eliminare le risorse
> * Eseguire un'applicazione hello

Sono necessari circa 20 minuti toodo questi passaggi.

## <a name="create-a-maven-project"></a>Creare un progetto Maven

1. Installare [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), se non lo si è già fatto.
2. Installare [Maven](http://maven.apache.org/download.cgi).
3. Creare un nuovo progetto di cartella e hello:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Aggiungere le dipendenze

1. In hello `testAzureApp` cartella, aprire hello `pom.xml` file e aggiungere la configurazione di compilazione hello troppo&lt;progetto&gt; compilazione hello tooenable dell'applicazione:

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

2. Aggiungere le dipendenze di hello che sono necessari tooaccess hello Azure SDK per Java.

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

3. Salvare il file hello.

## <a name="create-credentials"></a>Creare le credenziali

Prima di iniziare questo passaggio, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.

### <a name="create-hello-authorization-file"></a>Creare il file di autorizzazione hello

1. Creare un file denominato `azureauth.properties` e aggiungere tooit queste proprietà:

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

    Sostituire  **&lt;id sottoscrizione&gt;**  con l'identificatore della sottoscrizione,  **&lt;id applicazione&gt;**  con hello applicazione Active Directory identificatore,  **&lt;chiave di autenticazione&gt;**  con chiave applicazione hello e  **&lt;id tenant&gt;**  con tenant hello identificatore.

2. Salvare il file hello.
3. Impostare una variabile di ambiente denominata AZURE_AUTH_LOCATION nella shell con file di autenticazione toohello hello percorso completo.

### <a name="create-hello-management-client"></a>Creare il client di gestione hello

1. Aprire hello `App.java` file `src\main\java\com\fabrikam` e assicurarsi che l'istruzione di pacchetto è nella parte superiore di hello:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. In istruzione package hello, Aggiungi queste istruzioni import:
   
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

2. le credenziali di Active Directory hello toocreate toomake richieste, è necessario aggiungere questo codice toohello principale metodo hello classe App:
   
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

## <a name="create-resources"></a>Creare le risorse

### <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).

i valori per toospecify hello applicazione e creare il gruppo di risorse hello, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Creare set di disponibilità hello

[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.

set di disponibilità hello toocreate, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Creare l'indirizzo IP pubblico hello

Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.

toocreate hello indirizzo IP pubblico per la macchina virtuale hello, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Creare una rete virtuale hello

Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).

toocreate una subnet e una rete virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:

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

### <a name="create-hello-network-interface"></a>Creare l'interfaccia di rete hello

Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.

toocreate un'interfaccia di rete, aggiungere questo blocco try toohello di codice nel metodo main hello:

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

### <a name="create-hello-virtual-machine"></a>Creare una macchina virtuale hello

Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.

toocreate hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:

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
> Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello. toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se si desidera toouse un disco esistente anziché un'immagine del marketplace, è possibile utilizzare questo codice: 

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

## <a name="perform-management-tasks"></a>Eseguire le attività di gestione

Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale. Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.

Quando è necessario toodo con hello VM, è necessario tooget un'istanza. Aggiungere questo blocco try toohello di codice del metodo principale di hello:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Ottenere informazioni su hello VM

tooget informazioni hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:

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

### <a name="stop-hello-vm"></a>Arrestare VM hello

È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo. Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.

macchina virtuale di hello toostop senza deallocarlo, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello spento chiamata:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Avviare hello VM

toostart hello macchina virtuale, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Ridimensionare hello VM

Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione. Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).  

toochange dimensioni della macchina virtuale hello, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Aggiungere un toohello disco dati VM

tooadd una macchina virtuale su disco toohello per dati con 2 GB di dimensioni, dispone di un LUN pari a 0 e un tipo di memorizzazione nella cache di lettura/scrittura, aggiungere questo blocco try toohello di codice nel metodo main hello:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Eliminare le risorse

Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari. Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.

1. risorsa hello toodelete gruppo, aggiungere questo blocco try toohello di codice nel metodo main hello:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Salvare il file di App.java hello.

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish.

1. toorun hello applicazione, utilizzare il comando di Maven:

    ```
    mvn compile exec:java
    ```

2. Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure. Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.


## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sull'utilizzo di hello [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

