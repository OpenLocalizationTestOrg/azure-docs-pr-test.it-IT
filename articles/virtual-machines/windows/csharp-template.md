---
title: aaaDeploy una macchina virtuale con c# e un modello di gestione risorse | Documenti Microsoft
description: Informazioni su toouse toohow c# e un toodeploy di modello una macchina virtuale di Azure Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Distribuire una macchina virtuale di Azure con C# e un modello di Azure Resource Manager
In questo articolo illustra come toodeploy un modello di gestione risorse di Azure tramite c#. modello Hello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con una singola subnet.

Per una descrizione dettagliata della risorsa di macchina virtuale hello, vedere [macchine virtuali in un modello di gestione risorse di Azure](template-description.md). Per ulteriori informazioni su tutte le risorse di hello in un modello, vedere [procedura dettagliata di modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Sono necessari circa 10 minuti toodo questi passaggi.

## <a name="create-a-visual-studio-project"></a>Creare un progetto di Visual Studio

In questo passaggio è assicurarsi che Visual Studio è installato e si crea un modello di hello console toodeploy applicazione utilizzata.

1. Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selezionare **lo sviluppo desktop .NET** hello pagina carichi di lavoro e quindi fare clic su **installare**. In hello riepilogo, è possibile vedere che **gli strumenti di sviluppo di .NET Framework 4 a 4.6** viene selezionato automaticamente. Se già stato installato Visual Studio, è possibile aggiungere hello .NET il carico di lavoro hello utilità di avvio di Visual Studio.
2. In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.
3. In **modelli** > **Visual c#**selezionare **applicazione Console (.NET Framework)**, immettere *myDotnetProject* per nome hello del progetto, il percorso di selezione hello del progetto di hello, Hello e quindi fare clic su **OK**.

## <a name="install-hello-packages"></a>Installare i pacchetti hello

Pacchetti NuGet sono hello più semplice modo tooinstall hello librerie necessario toofinish questi passaggi. librerie di hello tooget che è necessario in Visual Studio, eseguire questi passaggi:

1. Fare clic su **Strumenti** > **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.
2. Nella console di hello, digita questi comandi:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Creare file hello

In questo passaggio si crea un file di modello che consente di distribuire risorse hello e un file di parametri che fornisce modelli di toohello valori di parametro. È inoltre possibile creare un file di autorizzazione che è utilizzati tooperform le operazioni di gestione risorse di Azure.

### <a name="create-hello-template-file"></a>Creare il file di modello hello

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*. File con nome hello *CreateVMTemplate.json*, quindi fare clic su **Aggiungi**.
2. Aggiungere questo file toohello di codice JSON che è stato creato:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Salvare il file di CreateVMTemplate.json hello.

### <a name="create-hello-parameters-file"></a>Creare i file dei parametri hello

toospecify i valori per i parametri delle risorse hello definiti nel modello di hello, creare un file di parametri che contiene i valori hello.

1. In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*. File con nome hello *Parameters.json*, quindi fare clic su **Aggiungi**.
2. Aggiungere questo file toohello di codice JSON che è stato creato:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Salvare il file di Parameters.json hello.

### <a name="create-hello-authorization-file"></a>Creare il file di autorizzazione hello

Prima di poter distribuire un modello, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../resource-group-authenticate-service-principal.md). Dall'entità servizio hello, acquisire un token per autenticare le richieste tooAzure Gestione risorse. È inoltre necessario registrare ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario che nel file di autorizzazione hello.

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
4. Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con file di tooauthorization hello percorso completo che è stato creato, ad esempio hello possibile usare il comando PowerShell seguente:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Creare il client di gestione hello

1. Aprire il file Program.cs hello per progetto hello creato e quindi aggiungerle utilizzando istruzioni esistente toohello all'inizio del file hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
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

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

i valori toospecify per un'applicazione hello, aggiungere metodo Main toohello di codice:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Creare un account di archiviazione

parametri e modello hello vengono distribuiti da un account di archiviazione in Azure. In questo passaggio, creare account hello e caricare file hello. 

toocreate hello account, aggiungere questo toohello codice metodo Main:

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Distribuire il modello di hello

Distribuire il modello di hello e i parametri dall'account di archiviazione hello che è stato creato. 

modello di hello toodeploy, aggiungere questo toohello codice metodo Main:

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Eliminare le risorse di hello

Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari. Non è necessario toodelete ogni risorsa separatamente da un gruppo di risorse. Elimina il gruppo di risorse hello e tutte le relative risorse vengono eliminate automaticamente. 

risorsa hello toodelete gruppo, aggiungere questo toohello codice metodo Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Eseguire un'applicazione hello

Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish. 

1. un'applicazione console hello toorun, fare clic su **avviare**.

2. Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure. Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.

## <a name="next-steps"></a>Passaggi successivi
* Se si sono verificati problemi con la distribuzione di hello, un passaggio successivo consisterebbe toolook in [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
* Informazioni su come toodeploy una macchina virtuale e le risorse di supporto, è consigliabile consultare [distribuire un Azure macchina virtuale utilizzando c#](csharp.md).
