---
title: distribuzione di applicazioni di Service Fabric aaaAzure | Documenti Microsoft
description: Utilizzare hello FabricClient APIs toodeploy e rimuovere le applicazioni nell'infrastruttura del servizio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a>Distribuire e rimuovere applicazioni con il client Fabric
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [API client Fabric](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Dopo aver creato il [pacchetto di un tipo di applicazione][10], è possibile distribuirlo in un cluster di Azure Service Fabric. Distribuzione coinvolge hello tre passaggi:

1. Caricare l'archivio di immagini toohello pacchetto applicazione hello
2. Registrare il tipo di applicazione hello
3. Creare l'istanza dell'applicazione hello

Dopo che un'applicazione viene distribuita e cluster hello è in esecuzione un'istanza, è possibile eliminare l'istanza dell'applicazione hello e il relativo tipo di applicazione. Rimuovi toocompletely un'applicazione dal cluster hello prevede hello alla procedura seguente:

1. Rimuovere hello esegue l'istanza dell'applicazione (o eliminare)
2. Annullare la registrazione del tipo di applicazione hello se non è più necessario
3. Rimuovere il pacchetto di applicazione hello dall'archivio immagini hello

Se si utilizza [Visual Studio per la distribuzione e debug di applicazioni](service-fabric-publish-app-remote-cluster.md) nel cluster di sviluppo locale, tutti i passaggi precedenti di hello vengono gestite automaticamente tramite uno script di PowerShell.  Questo script è presente in hello *script* nella cartella del progetto di applicazione hello. In questo articolo vengono fornite informazioni su cosa fa lo script in modo che sia possibile eseguire hello stesse operazioni all'esterno di Visual Studio. 
 
## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello
Connettere il cluster di toohello creando un [FabricClient](/dotnet/api/system.fabric.fabricclient) istanza prima di eseguire una delle hello esempi di codice in questo articolo. Per esempi di cluster di sviluppo locale tooa connessione o un cluster remoto o un cluster protetto tramite Azure Active Directory, X509 certificati o Active Directory di Windows vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis). cluster di sviluppo locale di toohello di tooconnect, eseguire hello seguente:

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a>Caricare il pacchetto di applicazione hello
Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio. Per impostazione predefinita, nome del tipo applicazione hello elencati in ApplicationManifest.xml hello è "MyApplicationType".  Hello pacchetto di applicazione, che contiene un manifesto dell'applicazione hello, i manifesti del servizio e i pacchetti di configurazione/codice/dati, si trova *C:\Users\&lt; nome utente&gt;\Documents\Visual 2017\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.

Caricamento del pacchetto dell'applicazione hello lo inserisce in una posizione accessibile da componenti interni di Service Fabric hello. Service Fabric verifica il pacchetto di applicazione hello durante la registrazione di hello hello del pacchetto di applicazione. Tuttavia, se si desidera localmente pacchetto dell'applicazione hello tooverify (ad esempio, prima del caricamento), utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API Carica archivio di immagini cluster toohello pacchetto applicazione hello. 

Se il pacchetto di applicazione hello è di grandi dimensioni e/o dispone di molti file, è possibile [comprimerli](service-fabric-package-apps.md#compress-a-package) e copiarlo toohello archivio di immagini tramite PowerShell. la compressione di Hello riduce hello dimensioni e il numero di hello dei file.

Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.

## <a name="register-hello-application-package"></a>Registrare il pacchetto di applicazione hello
tipo di applicazione Hello e versione dichiarati nel manifesto dell'applicazione hello diventano disponibile per l'utilizzo quando il pacchetto di applicazione hello viene registrato. sistema Hello legge pacchetto hello caricato nel passaggio precedente hello, verifica i pacchetti hello, elabora i contenuti del pacchetto hello e Copia percorso di sistema interno tooan pacchetto hello elaborato.  

Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registri hello tipo di applicazione in cluster hello e renderlo disponibile per la distribuzione.

Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fornisce informazioni su tutti i tipi di applicazione registrato correttamente. È possibile utilizzare questo toodetermine API quando viene eseguita la registrazione di hello.

## <a name="create-an-application-instance"></a>Creare un'istanza dell'applicazione
È possibile creare un'istanza di un'applicazione da qualsiasi tipo di applicazione che è stato registrato correttamente tramite hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API. nome Hello di ogni applicazione deve iniziare con hello *"fabric:"* dello schema e deve essere univoco per ogni istanza dell'applicazione (all'interno di un cluster). Vengono creati anche i servizi predefiniti definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello.

Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione. Ogni istanza dell'applicazione viene eseguita in isolamento, con una propria directory di lavoro e un proprio set di processi.

toosee denominato applicazioni e servizi sono in esecuzione in cluster hello, eseguire hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API.

## <a name="create-a-service-instance"></a>Creare un'istanza del servizio
È possibile creare un'istanza di un servizio da un tipo di servizio utilizzando hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.  Se il servizio di hello è dichiarato come un servizio predefinito nel manifesto dell'applicazione hello, viene creata un'istanza servizio hello quando viene creata un'istanza di un'applicazione hello.  Chiamare il metodo hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API per un servizio che viene creata un'istanza già restituirà un'eccezione di tipo FabricException contenente un codice di errore con un valore di FabricErrorCode.ServiceAlreadyExists.

## <a name="remove-a-service-instance"></a>Rimuovere un'istanza del servizio
Quando un'istanza del servizio non è più necessario, è possibile rimuoverlo dal hello eseguendo l'istanza dell'applicazione chiamante hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.  

> [!WARNING]
> Tale operazione non può essere annullata e lo stato del servizio non può essere recuperato.

## <a name="remove-an-application-instance"></a>Rimuovere un'istanza dell'applicazione
Quando un'istanza di applicazione non è più necessario, è possibile rimuoverlo in modo permanente in base al nome utilizzando hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API. [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) rimuove automaticamente tutti i servizi che appartengono toohello applicazione nonché, in modo permanente la rimozione di tutti gli stati di servizio.

> [!WARNING]
> Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.

## <a name="unregister-an-application-type"></a>Annullare la registrazione di un tipo di applicazione
Quando una particolare versione di un tipo di applicazione non è più necessario, si deve annullare la registrazione di quella versione specifica del tipo di applicazione hello utilizzando hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API. Annullamento della registrazione le versioni di spazio di archiviazione delle versioni di applicazione tipi utilizzato dall'archivio immagini hello. Una versione di un tipo di applicazione è possibile annullare la registrazione fino a quando non esistono applicazioni vengono creata un'istanza con tale versione del tipo di applicazione hello e non gli aggiornamenti in sospeso dell'applicazione fa riferimento a tale versione del tipo di applicazione hello.

## <a name="remove-an-application-package-from-hello-image-store"></a>Rimuovere un pacchetto di applicazioni dall'archivio immagini hello
Quando un pacchetto di applicazione non è più necessario, è possibile eliminarlo dal hello immagine archivio toofree le risorse di sistema utilizzando hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a>Copy-ServiceFabricApplicationPackage chiede un parametro ImageStoreConnectionString
ambiente di Service Fabric SDK Hello dovrebbe già disporre hello corretto impostare valori predefiniti. Ma se necessario, hello ImageStoreConnectionString per tutti i comandi debba corrispondere valore hello tale hello dell'infrastruttura del servizio cluster utilizza. È possibile trovare hello ImageStoreConnectionString nel manifesto del cluster hello, recuperati tramite hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e i comandi Get-ImageStoreConnectionStringFromClusterManifest:

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.  modulo SDK di hello di tooimport, eseguire:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


Hello ImageStoreConnectionString viene trovato nel manifesto del cluster hello:

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.

### <a name="deploy-large-application-package"></a>Distribuire un pacchetto dell'applicazione di grandi dimensioni
Problema: l'API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).
Soluzione:
- Specificare un timeout maggiore per il metodo [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) con il parametro `timeout`. Per impostazione predefinita, il timeout di hello è 30 minuti.
- Controllare la connessione di rete hello tra il computer di origine e il cluster. Se hello connessione è lenta, considerare l'utilizzo di un computer con una connessione di rete migliorata.
Se hello client macchina si trova in un'altra area di cluster hello, considerare l'uso di un computer client in un'area più vicino o stesso come cluster hello.
- Controllare se si stiano raggiungendo le limitazioni esterne. Ad esempio, quando l'archivio immagini hello è configurato toouse azure storage, caricamento può essere limitato.

Problema: il pacchetto è stato caricato completamente, ma si è verificato il timeout dell'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync). Soluzione:
- [Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.
la compressione di Hello riduce le dimensioni di hello e hello diversi file, che a sua volta riduce hello quantità di traffico e di lavoro di Service Fabric devono eseguire. operazione di caricamento Hello potrebbe risultare più lenta (in particolare se si include il tempo di compressione hello), ma il tipo di applicazione hello registrare e annullare la registrazione sono più veloci.
- Specificare un timeout maggiore per l'API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.

### <a name="deploy-application-package-with-many-files"></a>Distribuire un pacchetto di applicazione con numerosi file
Problema: si verifica un timeout di [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).
Soluzione:
- [Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini. la compressione di Hello riduce il numero di hello di file.
- Specificare un timeout maggiore per il metodo [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) con il parametro `timeout`.

## <a name="code-example"></a>Esempio di codice
Hello esempio copia di un archivio di immagini toohello pacchetto di applicazione, il tipo di applicazione hello viene eseguito il provisioning, crea un'istanza di applicazione, crea un'istanza del servizio, istanza dell'applicazione hello rimuove, disposizioni di un tipo di applicazione hello, e Elimina il pacchetto di applicazione hello dall'archivio immagini hello.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a>Passaggi successivi
[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)

[Introduzione all'integrità di Service Fabric](service-fabric-health-introduction.md)

[Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modellare un'applicazione in Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
