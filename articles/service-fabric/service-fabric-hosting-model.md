---
title: Modello di Hosting di servizi dell'infrastruttura aaaAzure | Documenti Microsoft
description: Questo articolo descrive la relazione tra le repliche (o istanze) di un servizio Servic Fabric distribuito e il processo host del servizio.
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Modello di hosting di Service Fabric
Questo articolo viene fornita una panoramica dei modelli forniti dall'infrastruttura del servizio di hosting e vengono descritte le differenze di hello tra hello **processo condiviso** e **processo esclusivo** modelli. Viene illustrato l'aspetto di un'applicazione distribuita in un nodo di Service Fabric e una relazione tra le repliche o istanze di servizio hello e processo host del servizio hello.

Prima di procedere, verificare di avere acquisito familiarità con il [modello applicativo di Service Fabric][a1] e di aver compreso i diversi concetti e le relazioni esistenti tra di essi. 

> [!NOTE]
> In questo articolo, per semplicità, a meno che non indicato in modo esplicito:
>
> - Tutte le occorrenze della parola *replica* fa riferimento a una replica di un servizio con stato o un'istanza di un servizio statless tooboth.
> - *CodePackage* è troppo equivalente trattati*ServiceHost* processo che si registra un *ServiceType* e le repliche di host dei servizi di tale *ServiceType*.
>

toounderstand hello modello di hosting, segnalare il problema esaminato un esempio. Si supponga di avere un *ApplicationType* 'MyAppType' con un *ServiceType* 'MyServiceType' fornito dal *ServicePackage* 'MyServicePackage' che ha un *CodePackage* 'MyCodePackage' che registra *ServiceType* 'MyServiceType' quando viene eseguito.

Si supponga inoltre di avere un cluster a 3 nodi e di creare un'*applicazione* **fabric:/App1** di tipo 'MyAppType'. All'interno di questa *applicazione* **fabric:/App1** viene creato un servizio **fabric:/App1/ServiceA** di tipo 'MyServiceType' con 2 partizioni, **P1** & **P2**, e 3 repliche per partizione. Hello diagramma seguente mostra vista hello di questa applicazione come finisce distribuito in un nodo.

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-one]
</center>

Service Fabric attivato 'MyServicePackage' avviato 'MyCodePackage', che ospita le repliche da entrambe le partizioni hello ovvero **P1** & **P2**. Si noti che tutti i nodi nel cluster hello hello avrà stessa vista perché è stato scelto di numero di repliche per ogni partizione toonumber pari di nodi nel cluster hello. Viene ora creato un altro servizio **fabric:/App1/ServiceB** nell'applicazione **fabric:/App1** con una partizione, **P3**, e 3 repliche per partizione. Diagramma seguente illustra una nuova vista di hello nel nodo hello:

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-two]
</center>

Come possiamo vedere Service Fabric inserito nuova replica per la partizione di hello **P3** del servizio **fabric: / App1/ServiceB** attivazione esistente di hello di 'MyServicePackage'. Viene ora creata un'altra *applicazione* **fabric:/App2** di tipo 'MyAppType'. All'interno di **fabric:/App2** viene creato il servizio **fabric:/App2/ServiceA** con due partizioni, **P4** & **P5**, e 3 repliche per partizione. Diagrammi di seguito mostra hello nuovo nodo:

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-three]
</center>

Questa volta Service Fabric ha attivato una nuova copia di 'MyServicePackage', che a sua volta avvia una nuova copia di 'MyCodePackage'. Repliche di entrambe le partizioni del servizio **fabric:/App2/ServiceA**, ovvero **P4** & **P5**, vengono posizionate in questa nuova copia 'MyCodePackage'.

## <a name="shared-process-model"></a>Modello Processo condiviso
Cosa è stato illustrato sopra è predefinita hello modello fornito dall'infrastruttura del servizio di hosting ed è denominato tooas **processo condiviso** modello. In questo modello, per un determinato *applicazione*un solo una copia un specificato *ServicePackage* viene attivato in base un *nodo* (che avvia hello tutti *CodePackages* in esso contenuti) e tutti hello repliche di tutti i servizi di un determinato *ServiceType* vengono inseriti in hello *CodePackage* che registra *ServiceType*. In altre parole, tutti hello repliche di tutti i servizi di un determinato *ServiceType* condividere hello stesso processo.

## <a name="exclusive-process-model"></a>Modello Exclusive Process (Processo esclusivo)
Hello altri modello host fornito da Service Fabric è **processo esclusivo** modello. In questo modello, in un determinato *nodo*, per la distribuzione di ogni replica, Service Fabric è attiva una nuova copia del *ServicePackage* (che avvia hello tutti *CodePackages* in esso contenuti ) e replica si trova nell'hello *CodePackage* tale hello registrato *ServiceType* di hello servizio toowhich replica appartiene. In altri termini, ogni replica si trova nel proprio processo dedicato. 

Questo modello è supportato a partire dalla versione 5.6 di Service Fabric. **Processo esclusivo** modello può essere scelte in fase di creazione servizio hello di hello (utilizzando [PowerShell][p1], [REST] [ r1]o [FabricClient][c1]) specificando **ServicePackageActivationMode** come 'ExclusiveProcess'.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Se nel manifesto dell'applicazione è presente un servizio predefinito, è possibile scegliere il modello **Exclusive Process** (Processo esclusivo) specificando l'attributo **ServicePackageActivationMode**, come mostrato di seguito:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Continuare con l'esempio precedente, consente di creare un altro servizio **fabric: / App1/ServiceC** nell'applicazione **fabric: / App1** che dispone di 2 partizioni si possono (ad esempio **P6**  &  **P7**) e 3 repliche per ogni partizione con **ServicePackageActivationMode** impostare too'ExclusiveProcess'. Diagramma seguente illustra una nuova vista nel nodo hello:

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-four]
</center>

Come è possibile notare, Service Fabric ha attivato due nuove copie di 'MyServicePackage', una per ciascuna replica dalle partizioni **P6** & **P7**, e ha posizionato ciascuna replica nella relativa copia dedicata di *CodePackage*. Un'altra operazione, toonote qui è, quando **processo esclusivo** modello viene utilizzato, per un determinato *applicazione*, più copie di un specificato *ServicePackage* può essere attivo su un  *Nodo*. Nell'esempio precedente è possibile notare che le tre copie di 'MyServicePackage' sono attive per **fabric:/App1**. A ciascuna di queste copie di 'MyServicePackage' è associato un **ServicePackageAtivationId** che identifica la copia all'interno dell'*applicazione* **fabric:/App1**.

Quando per un'*applicazione*, ad esempio **fabric:/App2** nell'esempio precedente, viene usato soltanto il modello **Processo condiviso**, è presente una sola copia attiva di *ServicePackage* su un *Nodo* e il **ServicePackageAtivationId** per questa attivazione di *ServicePackage* è 'empty string'.

> [!NOTE]
>- **Processo condiviso** modello di hosting corrisponde troppo**ServicePackageAtivationMode** uguale **SharedProcess**. Questo è l'impostazione predefinita di hello modello di hosting e **ServicePackageAtivationMode** non deve essere specificato in fase di creazione servizio hello di hello.
>
>- **Processo esclusivo** modello di hosting corrisponde troppo**ServicePackageAtivationMode** uguale **ExclusiveProcess** ed è necessario toobe specificato in modo esplicito in fase di creazione di hello di hello servizio. 
>
>- Modello di hosting di un servizio può essere conosciuto eseguendo una query hello [descrizione del servizio] [ p2] ed esaminando valore **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Utilizzo del pacchetto del servizio distribuito
Una copia attiva di un *ServicePackage* su un nodo viene definita [pacchetto del servizio distribuito][p3]. Come già indicato in precedenza, quando **processo esclusivo** modello viene utilizzato per la creazione di servizi, per un determinato *applicazione*, potrebbe esserci servizio distribuito più pacchetti per hello stesso  *ServicePackage*. Durante l'esecuzione di operazioni come pacchetto del servizio specifico toodeployed [reporting integrità di un pacchetto del servizio distribuito] [ p4] o [il riavvio del pacchetto di codice di un pacchetto del servizio distribuito] [ p5] e così via, **ServicePackageActivationId** toobe esigenze fornito tooidentify un pacchetto specifico servizio distribuito.

 **ServicePackageActivationId** di un servizio distribuito pacchetto può essere ottenuto eseguendo una query di elenco hello di [servizio pacchetti distribuiti] [ p3] in un nodo. Quando si eseguono query [distribuito i tipi di servizio][p6], [distribuito repliche] [ p7] e [distribuiti i pacchetti di codice] [ p8] in un nodo, il risultato della query hello contiene anche hello **ServicePackageActivationId** del pacchetto del servizio padre distribuita.

> [!NOTE]
>- In base al modello di hosting **Processo condiviso**, in un determinato *nodo* per un'*applicazione* specificata viene attivata una sola copia di un *ServicePackage*. Ha **ServicePackageActivationId** uguale troppo*una stringa vuota* e non è necessario specificare durante le operazioni di relative esecuzione pacchetto del servizio distribuito. 
>
> - In base al modello di hosting **Exclusive Process** (Processo esclusivo), in un determinato *nodo* per un'*applicazione* specificata possono essere attive una o più copie di un *ServicePackage*. Ogni attivazione ha un *non vuoto* **ServicePackageActivationId** ed è necessario toobe specificato anche se il pacchetto del servizio distribuito eseguire le operazioni correlate. 
>
> - Se **ServicePackageActivationId** è il valore predefinito è la stringa too'empty ommited'. Se un servizio distribuito crea un pacchetto che è stata attivata in **processo condiviso** modello sia presente, quindi viene eseguita su di esso, in caso contrario hello operazione avrà esito negativo.
>
> - Non è consigliabile tooquery una sola volta e cache **ServicePackageActivationId** perché viene generata dinamicamente e può cambiare per vari motivi. Prima di eseguire un'operazione che deve **ServicePackageActivationId**, è innanzitutto necessario eseguire una query elenco hello di [servizio pacchetti distribuiti] [ p3] su un nodo e quindi utilizzare  *ServicePackageActivationId** da query risultato tooperform hello originale per l'operazione.
>
>

## <a name="guest-executable-and-container-applications"></a>Applicazioni eseguibili guest e contenitore
Service Fabric tratta le applicazioni di tipo [eseguibile guest][a2] e [contenitore][a3] come servizi senza stato indipendenti. In altri termini, in *ServiceHost* non è presente alcun runtime di Service Fabric (processo o contenitore). Dal momento che si tratta di servizi indipendenti, il numero di repliche per *ServiceHost* non è applicabile. configurazione più comune utilizzata con questi servizi Hello è singola partizione con [InstanceCount] [ c2] uguale troppo-1 (ad esempio una copia hello del codice di servizio in esecuzione in ogni nodo del cluster). 

Hello predefinito **ServicePackageActivationMode** per questi servizi è **SharedProcess** nel qual caso Service Fabric attiva solo una copia di *ServicePackage* in un *Nodo* per un determinato *applicazione* ovvero solo una copia del codice del servizio verrà eseguito un *nodo*. Se si desiderino più copie di toorun di codice del servizio in un *nodo* quando si creano più servizi (*Service1* troppo*ServiceN*) di *ServiceType* (specificato in *manifesto del servizio*) o quando il servizio è partizionato più, è necessario specificare **ServicePackageActivationMode** come **ExclusiveProcess**in fase di creazione servizio hello di hello.

## <a name="changing-hosting-model-of-an-existing-service"></a>Modifica del modello di hosting di un servizio esistente
Modifica modello di hosting di un servizio esistente da **processo condiviso** troppo**processo esclusivo** e viceversa tramite meccanismo di aggiornamento (aggiornamento o predefinita specifica nell'applicazione di servizio manifesto) non è attualmente supportato. Il supporto per questa funzionalità è previsto per una versione futura.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Scelta tra i modelli Processo condiviso ed Exclusive Process (Processo esclusivo)
Questi modelli di hosting hanno vantaggi e svantaggi sia utente deve tooevaluate quello più appropriato per i relativi requisiti. **Processo condiviso** modello consente un migliore uso delle risorse del sistema operativo in quanto un minor numero di processi vengono distribuiti, più repliche in hello stesso processo può condividere le porte e così via. Tuttavia, se una delle repliche hello riscontri un errore in cui è necessario toobring all'host del servizio hello, può rallentare tutte le altre repliche nello stesso processo.

 Il modello **Exclusive Process** (Processo esclusivo) offre un migliore isolamento con ciascuna replica in un proprio processo e un errore di una replica non avrà conseguenze sulle altre repliche. Si rivela utile nei casi in cui la condivisione delle porte non è supportata dal protocollo di comunicazione hello. Facilita hello possibilità tooapply la governance delle risorse a livello di replica. Hello d'altro canto, **processo esclusivo** utilizzerà più risorse del sistema operativo come genera un processo per ogni replica nel nodo hello.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Considerazioni sul modello Exclusive Process (Processo esclusivo) e sul modello dell'applicazione
Hello consigliato toomodel modo l'applicazione di Service Fabric è tookeep uno *ServiceType* per *ServicePackage* e questo modello funziona bene per la maggior parte delle applicazioni di hello. 

Tuttavia, tooenable particolari scenari in cui un *ServiceType* per *ServicePackage* potrebbe non essere appropriato, a livello funzionale Service Fabric consente toohave più di uno *ServiceType* per *ServicePackage* (e uno *CodePackage* possibile registrare più *ServiceType*). Di seguito sono alcuni degli scenari di hello in cui possono essere utile queste configurazioni:

- Si vuole toooptimize l'utilizzo delle risorse del sistema operativo, la generazione di un minor numero di processi e per avere maggiore densità di replica per ogni processo.
- Le repliche dalla ServiceTypes diversi necessario tooshare alcuni dati comuni che ha un elevato inizializzazione o l'utilizzo della memoria.
- Si dispone di un'offerta di servizio gratuito e si desidera tooput un limite all'utilizzo delle risorse mediante l'inserimento di tutte le repliche del servizio hello nello stesso processo.

Il modello di hosting **Exclusive Process** (Processo esclusivo) non è coerente con il modello dell'applicazione con più *ServiceType* per *ServicePackage*. Infatti, più *ServiceTypes* per *ServicePackage* è progettato tooachieve superiore condivisione delle risorse tra le repliche e consente una maggiore densità di replica per ogni processo. Si tratta di contrarie toowhat **processo esclusivo** modello è tooachieve progettato.

Si consideri il caso hello di più *ServiceTypes* per *ServicePackage* con diversi *CodePackage* registrazione ogni *ServiceType*. Si supponga di avere un *ServicePackage* 'MultiTypeServicePackge' con due *CodePackage*:

- 'MyCodePackageA', che registra il *ServiceType* 'MyServiceTypeA'.
- 'MyCodePackageB', che registra il *ServiceType* 'MyServiceTypeB'.

A questo punto viene creata un'*applicazione* **fabric:/SpecialApp**. All'interno di **fabric:/SpecialApp** vengono quindi creati i due servizi seguenti con il modello **Exclusive Process** (Processo esclusivo):

- Servizio **fabric:/SpecialApp/ServiceA** di tipo 'MyServiceTypeA' con due partizioni, **P1** e **P2**, e 3 repliche per partizione.
- Servizio **fabric:/SpecialApp/ServiceB** di tipo 'MyServiceTypeB' con due partizioni, **P3** e **P4**, e 3 repliche per partizione.

Su un determinato nodo, entrambi i servizi hello avrà due repliche. Poiché è stato usato **processo esclusivo** toocreate del modello di servizi hello, Service Fabric attiverà una nuova copia di 'MyServicePackge' per ogni replica. Ogni attivazione di 'MultiTypeServicePackge' avvierà una copia di 'MyCodePackageA' e 'MyCodePackageB'. Tuttavia, solo uno di 'MyCodePackageA' o 'MyCodePackageB' ospiterà replica hello per cui è stata attivata 'MultiTypeServicePackge'. Diagramma seguente mostra una visualizzazione del nodo hello:

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-five]
</center>

 Come possiamo vedere, attivazione hello di 'MultiTypeServicePackge' per la replica della partizione **P1** del servizio **fabric: / SpecialApp/Service**, ospita la replica hello 'MyCodePackageA' e ' MyCodePackageB' sia sufficiente in esecuzione. Analogamente, nell'attivazione di 'MultiTypeServicePackge' per la replica della partizione **P3** del servizio **fabric: / SpecialApp/ServiceB**, ospita la replica hello 'MyCodePackageB' e 'MyCodePackageA' è appena installato e in esecuzione e così via. Di conseguenza, più hello numero di *CodePackages* (registrazione diversi *ServiceTypes*) per ogni *ServicePackage*, maggiore sarà utilizzo delle risorse di archiviazione con ridondanza. 
 
 In hello invece se si creano servizi **dell'infrastruttura: SpecialApp/Service** e **fabric: / SpecialApp/ServiceB** con **processo condiviso** del modello, verrà Service Fabric attiva solo una copia di 'MultiTypeServicePackge' per *applicazione* **fabric: / SpecialApp** (come illustrato in precedenza). 'MyCodePackageA' ospiterà tutte le repliche per il servizio **fabric: / SpecialApp/Service** (o di qualsiasi servizio di tipo 'MyServiceTypeA' toobe più preciso) e 'MyCodePackageB' ospiterà tutte le repliche per il servizio **fabric: / SpecialApp/ServiceB** (o di qualsiasi servizio di tipo 'MyServiceTypeB' toobe più preciso). Diagramma seguente mostra una visualizzazione nodo hello in questa impostazione: 

<center>
![Visualizzazione del nodo dell'applicazione distribuita][node-view-six]
</center>

Hello esempio precedente, si potrebbe pensare se 'MyCodePackageA' Registra 'MyServiceTypeA' sia 'MyServiceTypeB' non è presente alcun MyCodePackageB' ', quindi verrà non ridondante *CodePackage* in esecuzione. Si tratta di una considerazione corretta, ma, come indicato in precedenza, questo modello di applicazione non è coerente con il modello di hosting **Exclusive Process** (Processo esclusivo). Se l'obiettivo è tooput ogni replica nel proprio dedicata processo quindi la registrazione di entrambi *ServiceTypes* stessa *CodePackage* non è necessario e inserire ogni *ServiceType* in il proprio *ServicePacakge* è una scelta più idonea.

## <a name="next-steps"></a>Passaggi successivi
[Pacchetto di un'applicazione] [ a4] ed toodeploy pronto.

[Distribuire e rimuovere le applicazioni] [ a5] viene descritto come le istanze dell'applicazione toomanage toouse PowerShell.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage