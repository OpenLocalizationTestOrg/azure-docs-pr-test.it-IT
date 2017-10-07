---
title: distribuzione di applicazioni di Service Fabric aaaAzure | Documenti Microsoft
description: Come toodeploy e rimuovere le applicazioni nell'infrastruttura del servizio tramite PowerShell.
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
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a>Distribuire e rimuovere applicazioni con PowerShell
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
Prima di eseguire qualsiasi comando di PowerShell in questo articolo, iniziano sempre con [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello cluster di Service Fabric. cluster di sviluppo locale di toohello di tooconnect, eseguire hello seguente:

```powershell
PS C:\>Connect-ServiceFabricCluster
```

Per esempi di connessione remota tooa del cluster o cluster protetti tramite Azure Active Directory, X509 certificati o Active Directory di Windows vedere [Connetti tooa sicura cluster](service-fabric-connect-to-secure-cluster.md).

## <a name="upload-hello-application-package"></a>Caricare il pacchetto di applicazione hello
Caricamento del pacchetto dell'applicazione hello lo inserisce in un percorso accessibile dai componenti interni di Service Fabric.
Se si desidera pacchetto dell'applicazione hello di tooverify localmente, utilizzare hello [Test ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.

Hello [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando caricamenti hello archivio di immagini cluster toohello pacchetto di applicazione.
Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.  modulo SDK di hello di tooimport, eseguire:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Si supponga di compilare e assemblare un'applicazione denominata *MyApplication* in Visual Studio 2015. Per impostazione predefinita, nome del tipo applicazione hello elencati in ApplicationManifest.xml hello è "MyApplicationType".  Hello pacchetto di applicazione, che contiene un manifesto dell'applicazione hello, i manifesti del servizio e i pacchetti di configurazione/codice/dati, si trova *C:\Users\<username\>\Documents\Visual 2015\Projects\ Studio MyApplication\MyApplication\pkg\Debug*. 

Hello comando riportato di seguito elenca hello contenuto del pacchetto di applicazione hello:

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

Se il pacchetto di applicazione hello è di grandi dimensioni e/o dispone di molti file, è possibile [comprimerli](service-fabric-package-apps.md#compress-a-package). la compressione di Hello riduce hello dimensioni e il numero di hello dei file.
effetto collaterale Hello è che la registrazione e annullamento della registrazione di hello tipo di applicazione sono più veloci. Tempo di caricamento può risultare più lenta attualmente, specialmente se si include pacchetto hello toocompress della fase di hello. 

un pacchetto, utilizzare toocompress hello stesso [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando. La compressione può essere eseguita separato dal caricamento con hello `SkipCopy` flag o insieme hello operazione di caricamento. L'applicazione della compressione a un pacchetto compresso è no-op.
un pacchetto compresso, utilizzare toouncompress hello stesso [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) con hello `UncompressPackage` passare.

Hello cmdlet seguente comprime i pacchetti hello senza copiarlo toohello archivio di immagini. pacchetto di Hello include ora i file ZIP per hello `Code` e `Config` pacchetti. Hello hello servizio manifesti dell'applicazione e non compressi, perché sono necessari per molte operazioni interne (ad esempio la condivisione, l'applicazione nome e la versione estrazione del tipo per alcune convalide di pacchetto). Compressione manifesti hello renderebbe queste operazioni inefficienti.

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

Per i pacchetti di applicazione di grandi dimensioni, la compressione di hello richiede tempo. Per ottenere risultati ottimali, usare un'unità SSD rapida. Hello la compressione e la dimensione di hello del pacchetto compresso hello anche variano in base al contenuto del pacchetto hello.
Ad esempio, ecco le statistiche della compressione per alcuni pacchetti, che mostrano iniziale hello e hello dimensione compressa del pacchetto, con il tempo di compressione hello.

|Dimensioni iniziali (MB)|Numero di file|Tempo di compressione|Dimensioni pacchetto compresso (MB)|
|----------------:|---------:|---------------:|---------------------------:|
|100|100|00:00:03.3547592|60|
|512|100|00:00:16.3850303|307|
|1024|500|00:00:32.5907950|615|
|2048|1000|00:01:04.3775554|1231|
|5012|100|00:02:45.2951288|3074|

Una volta che un pacchetto compresso, può essere caricato tooone o più Service Fabric cluster come necessario. il meccanismo di distribuzione Hello è lo stesso per i pacchetti compressi e non compressi. Se il pacchetto di hello è compresso, viene archiviata come tale nell'archivio di immagini cluster hello ed è non compressi in nodo hello prima di eseguita un'applicazione hello.


Hello esempio Carica archivio immagine toohello pacchetti hello in una cartella denominata "MyApplicationV1":

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

Hello **Get ImageStoreConnectionStringFromClusterManifest** cmdlet, che fa parte del modulo PowerShell di Service Fabric SDK hello, è immagine hello tooget utilizzati archiviare la stringa di connessione.  modulo SDK di hello di tooimport, eseguire:

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

Se non si specifica hello *- ApplicationPackagePathInImageStore* parametro, il pacchetto di applicazione hello viene copiato nella cartella "Debug" hello in archivio immagini hello.

Hello tempo tooupload un pacchetto diverso in base a più fattori. Alcuni di questi fattori sono il numero di hello di file nel pacchetto di hello, dimensione del pacchetto hello e delle dimensioni del file hello. velocità della rete tra il computer di origine hello e cluster di Service Fabric hello Hello influisce anche sull'ora di caricamento hello. Hello timeout predefinito per [copia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) è 30 minuti.
A seconda del hello fattori descritti, è possibile tooincrease hello timeout. Se la compressione di pacchetti hello in hello copia chiamata, è necessario tooalso prendere in considerazione il tempo di compressione hello.

Vedere [comprendere una stringa di connessione di archivio immagine hello](service-fabric-image-store-connection-string.md) informazioni supplementari sull'archivio di immagini hello e immagine archiviare una stringa di connessione.

## <a name="register-hello-application-package"></a>Registrare il pacchetto di applicazione hello
tipo di applicazione Hello e versione dichiarati nel manifesto dell'applicazione hello diventano disponibile per l'utilizzo quando il pacchetto di applicazione hello viene registrato. sistema Hello legge pacchetto hello caricato nel passaggio precedente hello, verifica i pacchetti hello, elabora i contenuti del pacchetto hello e Copia percorso di sistema interno tooan pacchetto hello elaborato.  

Eseguire hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister cmdlet hello tipo di applicazione in cluster hello e renderlo disponibile per la distribuzione:

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

"MyApplicationV1" è la cartella hello in archivio immagini hello in cui si trova il pacchetto di applicazione hello. tipo di applicazione Hello con nome "MyApplicationType" e la versione "1.0.0" (entrambi trovati nel manifesto dell'applicazione hello) è stato registrato nel cluster hello.

Hello [registro ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando restituisce solo dopo che il sistema di hello dispone di pacchetto dell'applicazione hello registrato correttamente. Registrazione accetta quanto tempo dipende dalla dimensione hello e il contenuto del pacchetto di applicazione hello. Se necessario, hello **- TimeoutSec** parametro può essere utilizzato toosupply un timeout più lungo (timeout di hello predefinito è 60 secondi).

Se si dispone di un'applicazione di grandi dimensioni del pacchetto o se si verificano i timeout, utilizzare hello **- Async** parametro. comando Hello restituisce quando cluster hello accetta comando register hello e l'elaborazione di hello continua in base alle esigenze.
Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione. È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a>Creare un'applicazione hello
È possibile creare un'istanza di un'applicazione da qualsiasi versione di tipo di applicazione che è stato registrato correttamente tramite hello [New ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet. nome Hello di ogni applicazione deve iniziare con hello *"fabric:"* dello schema e deve essere univoco per ogni istanza dell'applicazione. Vengono creati anche i servizi predefiniti definiti nel manifesto dell'applicazione hello del tipo di applicazione di destinazione hello.

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
Per qualsiasi versione di un tipo di applicazione registrato, è possibile creare più istanze dell'applicazione. Ogni istanza viene eseguita in isolamento, con un proprio processo e una propria directory di lavoro.

toosee denominato App e servizi sono in esecuzione in cluster hello, eseguire hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a>Rimuovere un'applicazione
Quando un'istanza di applicazione non è più necessario, è possibile rimuoverlo in modo permanente in base al nome utilizzando hello [Remove ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet. [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) rimuove automaticamente tutti i servizi che appartengono toohello applicazione nonché, in modo permanente la rimozione di tutti gli stati di servizio. 

> [!WARNING]
> Tale operazione non può essere annullata e lo stato dell'applicazione non può essere recuperato.

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a>Annullare la registrazione di un tipo di applicazione
Quando una particolare versione di un tipo di applicazione non è più necessario, si deve annullare la registrazione di tipo di applicazione hello utilizzando hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet. Annullamento della registrazione dell'applicazione non utilizzati tipi versioni spazio di archiviazione utilizzato dall'archivio immagini hello. È possibile annullare la registrazione di un tipo di applicazione solo se non sono state create istanze di applicazioni basate su di esso o non vi sono aggiornamenti di applicazioni in sospeso che vi fanno riferimento.

Eseguire [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) i tipi di applicazione hello toosee attualmente registrato nel cluster di hello:

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

Eseguire [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister un tipo specifico di applicazione:

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a>Rimuovere un pacchetto di applicazioni dall'archivio immagini hello
Quando un pacchetto di applicazione non è più necessario, è possibile eliminarlo dal hello immagine archivio toofree le risorse di sistema.

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

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
Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) raggiunge il timeout per un pacchetto dell'applicazione di grandi dimensioni (nell'ordine di GB).
Soluzione:
- Specificare un timeout maggiore per il comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps), con il parametro `TimeoutSec`. Per impostazione predefinita, il timeout di hello è 30 minuti.
- Controllare la connessione di rete hello tra il computer di origine e il cluster. Se hello connessione è lenta, considerare l'utilizzo di un computer con una connessione di rete migliorata.
Se hello client macchina si trova in un'altra area di cluster hello, considerare l'uso di un computer client in un'area più vicino o stesso come cluster hello.
- Controllare se si stiano raggiungendo le limitazioni esterne. Ad esempio, quando l'archivio immagini hello è configurato toouse azure storage, caricamento può essere limitato.

Problema: Il pacchetto è stato caricato completamente ma si è verificato un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). Soluzione:
- [Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini.
la compressione di Hello riduce le dimensioni di hello e hello diversi file, che a sua volta riduce hello quantità di traffico e di lavoro di Service Fabric devono eseguire. operazione di caricamento Hello potrebbe risultare più lenta (in particolare se si include il tempo di compressione hello), ma il tipo di applicazione hello registrare e annullare la registrazione sono più veloci.
- Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.
- Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando Hello restituisce quando cluster hello accetta comandi hello e registrazione di hello del tipo di applicazione hello continua in modo asincrono. Per questo motivo, non è toospecify è necessario un timeout superiore in questo caso. Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione. È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a>Distribuire un pacchetto di applicazione con numerosi file
Problema: Si verifica un timeout di [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) per un pacchetto di applicazione con molti file (nell'ordine di migliaia).
Soluzione:
- [Comprimere il pacchetto di hello](service-fabric-package-apps.md#compress-a-package) prima della copia toohello archivio di immagini. la compressione di Hello riduce il numero di hello di file.
- Specificare un timeout maggiore per il comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps), con il parametro `TimeoutSec`.
- Specificare lo switch `Async` per [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps). comando Hello restituisce quando cluster hello accetta comandi hello e registrazione di hello del tipo di applicazione hello continua in modo asincrono.
Per questo motivo, non è toospecify è necessario un timeout superiore in questo caso. Hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando Elenca tutte le versioni di tipo applicazione registrata correttamente e il relativo stato di registrazione. È possibile utilizzare questo comando toodetermine quando viene eseguita la registrazione di hello.

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a>Passaggi successivi
[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)

[Introduzione all'integrità di Service Fabric](service-fabric-health-introduction.md)

[Eseguire la diagnosi e la risoluzione dei problemi di un servizio di Service Fabric](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Modellare un'applicazione in Service Fabric](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
