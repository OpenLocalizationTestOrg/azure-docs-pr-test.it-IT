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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Creare e gestire macchine virtuali Windows in Azure tramite C# #

Una [macchina virtuale di Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) richiede diverse risorse di supporto di Azure. Questo articolo descrive come creare, gestire ed eliminare le risorse della macchina virtuale tramite C#. Si apprenderà come:

> [!div class="checklist"]
> * Creare un progetto di Visual Studio
> * Installare il pacchetto di hello
> * Creare le credenziali
> * Creare le risorse
> * Eseguire le attività di gestione
> * Eliminare le risorse
> * Eseguire un'applicazione hello

Sono necessari circa 20 minuti toodo questi passaggi.

## <a name="create-a-visual-studio-project"></a>Creare un progetto di Visual Studio

1. Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selezionare **lo sviluppo desktop .NET** hello pagina carichi di lavoro e quindi fare clic su **installare**. In hello riepilogo, è possibile vedere che **gli strumenti di sviluppo di .NET Framework 4 a 4.6** viene selezionato automaticamente. Se già stato installato Visual Studio, è possibile aggiungere hello .NET il carico di lavoro hello utilità di avvio di Visual Studio.
2. In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.
3. In **modelli** > **Visual c#**selezionare **applicazione Console (.NET Framework)**, immettere *myDotnetProject* per nome hello del progetto, il percorso di selezione hello del progetto di hello, Hello e quindi fare clic su **OK**.

## <a name="install-hello-package"></a>Installare il pacchetto di hello

Pacchetti NuGet sono hello più semplice modo tooinstall hello librerie necessario toofinish questi passaggi. librerie di hello tooget che è necessario in Visual Studio, eseguire questi passaggi:

1. Fare clic su **Strumenti** > **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.
2. Nella console di hello, digitare il comando seguente:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Creare le credenziali

Prima di iniziare questo passaggio, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). È inoltre necessario registrare l'ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario in un passaggio successivo.

### <a name="create-hello-authorization-file"></a>Creare il file di autorizzazione hello

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*. File con nome hello *azureauth.properties*, quindi fare clic su **Aggiungi**.
2. Aggiungere le proprietà di autorizzazione seguenti:

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

3. Salvare il file di azureauth.properties hello. 
4. Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con file di tooauthorization hello percorso completo che è stato creato. Ad esempio, consente hello comando PowerShell seguente:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Creare il client di gestione hello

1. Aprire il file Program.cs hello per progetto hello creato e quindi aggiungerle utilizzando istruzioni esistente toohello all'inizio del file hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. client di gestione di hello toocreate, aggiungere questo toohello codice metodo Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Creare le risorse

### <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Tutte le risorse devono essere contenute in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).

i valori per toospecify hello applicazione e creare il gruppo di risorse hello, aggiungere questo toohello codice metodo Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Creare set di disponibilità hello

[Set di disponibilità](tutorial-availability-sets.md) rendono più semplice per l'utente nelle macchine virtuali di hello toomaintain utilizzate dall'applicazione.

set di disponibilità hello toocreate, aggiungere questo toohello codice metodo Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Creare l'indirizzo IP pubblico hello

Oggetto [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) è necessario toocommunicate con la macchina virtuale hello.

toocreate hello indirizzo IP pubblico per la macchina virtuale hello, aggiungere questo toohello codice metodo Main:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Creare una rete virtuale hello

Una macchina virtuale deve essere inclusa in una subnet di una [rete virtuale](../../virtual-network/virtual-networks-overview.md).

toocreate una subnet e una rete virtuale, aggiungere questo toohello codice metodo Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Creare l'interfaccia di rete hello

Una macchina virtuale richiede un toocommunicate di interfaccia di rete nella rete virtuale hello.

toocreate un'interfaccia di rete, aggiungere questo toohello codice metodo Main:

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

### <a name="create-hello-virtual-machine"></a>Creare una macchina virtuale hello

Dopo aver creato hello tutte le risorse di supporto, è possibile creare una macchina virtuale.

toocreate hello macchina virtuale, aggiungere questo toohello codice metodo Main:

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
> Questa esercitazione consente di creare una macchina virtuale in esecuzione una versione del sistema operativo di Windows Server hello. toolearn più sulla selezione di altre immagini, vedere [Naviga e selezionare le immagini di macchina virtuale di Azure con Windows PowerShell e hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se si desidera toouse un disco esistente anziché un'immagine del marketplace, è possibile utilizzare questo codice:

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

## <a name="perform-management-tasks"></a>Eseguire le attività di gestione

Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale. Inoltre, è consigliabile toocreate codice tooautomate attività ripetitive o complesse.

Quando è necessario toodo con hello VM, è necessario tooget un'istanza:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Ottenere informazioni su hello VM

tooget informazioni hello macchina virtuale, aggiungere questo toohello codice metodo Main:

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

### <a name="stop-hello-vm"></a>Arrestare VM hello

È possibile arrestare una macchina virtuale e mantenere tutte le relative impostazioni, ma continuare toobe addebitato oppure è possibile arrestare una macchina virtuale e deallocarlo. Quando una macchina virtuale viene deallocata, lo stesso viene fatto per tutte le risorse associate e la fatturazione termina.

macchina virtuale di hello toostop senza deallocarlo, aggiungere questo toohello codice metodo Main:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Se si desidera una macchina virtuale di hello toodeallocate, modificare il codice di toothis hello spento chiamata:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Avviare hello VM

toostart hello macchina virtuale, aggiungere questo toohello codice metodo Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Ridimensionare hello VM

Al momento di decidere le dimensioni della macchina virtuale, è necessario considerare molti aspetti della distribuzione. Per altre informazioni, vedere [Dimensioni delle macchine virtuali](sizes.md).  

toochange dimensioni della macchina virtuale hello, aggiungere questo toohello codice metodo Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Aggiungere un toohello disco dati VM

tooadd una macchina virtuale toohello disco dati, aggiungere questo tooadd di metodo Main toohello codice un disco dati è di 2 GB di dimensioni, han un LUN pari a 0 e un tipo di memorizzazione nella cache di lettura/scrittura:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Eliminare le risorse

Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari. Se si desidera toodelete hello le macchine virtuali e hello tutte le risorse di supporto, si dispone di toodo è gruppo di risorse hello di eliminazione.

risorsa hello toodelete gruppo, aggiungere questo toohello codice metodo Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish. 

1. un'applicazione console hello toorun, fare clic su **avviare**.

2. Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure. Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.

## <a name="next-steps"></a>Passaggi successivi
* Sfruttare utilizzando un toocreate modello una macchina virtuale utilizzando informazioni hello [distribuire una macchina virtuale di Azure con c# e un modello di gestione risorse](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Ulteriori informazioni sull'utilizzo di hello [Azure libraries per .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

