---
title: aaaScalability dei servizi di Service Fabric | Documenti Microsoft
description: Viene descritto come i servizi di Service Fabric tooscale
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Scalabilità in Service Fabric
Azure Service Fabric rende applicazioni scalabili toobuild facile gestendo hello servizi, partizioni e repliche in nodi hello di un cluster. In molti carichi di lavoro hello stesso hardware consente di massimo utilizzo, ma offre anche flessibilità in termini di modalità tooscale i carichi di lavoro. 

Esistono vari modi per impostare la scalabilità in Service Fabric:

1. Implementazione della scalabilità tramite creazione o rimozione di istanze del servizio senza stato
2. Implementazione della scalabilità tramite creazione o rimozione di nuovi servizi denominati
3. Implementazione della scalabilità tramite creazione o rimozione di nuove istanze dell'applicazione denominate
4. Implementazione della scalabilità tramite utilizzo di servizi partizionati
5. Scalabilità tramite l'aggiunta e rimozione di nodi dal cluster hello 
6. Implementazione della scalabilità tramite metriche di Gestione risorse cluster

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Implementazione della scalabilità tramite creazione o rimozione di istanze del servizio senza stato
Uno dei tooscale modi più semplici di hello all'interno di Service Fabric funziona con i servizi senza stati. Quando si crea un servizio senza stato, è un toodefine possibilità di ottenere un `InstanceCount`. `InstanceCount`definisce il numero di copie in esecuzione di codice del servizio viene creato all'avvio del servizio hello. Si supponga, ad esempio, sono presenti 100 nodi nel cluster hello. Si supponga anche che venga creato un servizio con un oggetto `InstanceCount` impostato su 10. Durante la fase di esecuzione, le copie in esecuzione 10 del codice hello diventino troppo occupate tutti (o potrebbe non essere sufficientemente occupate). Un modo tooscale tale carico di lavoro è il numero hello toochange di istanze. Ad esempio, alcuni frammenti di codice di monitoraggio o la gestione può cambiare numero di istanze too50 o too5 esistenti hello, a seconda della necessità di carico di lavoro hello tooscale in o out hello in base a caricare. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Utilizzo del numero delle istanze dinamico
In particolare per i servizi senza stati, Service Fabric offre un numero di istanze hello toochange modo automatico. In questo modo tooscale servizio hello in modo dinamico con il numero di hello di nodi disponibili. tooopt modo Hello in questo comportamento è il numero di istanze hello tooset = -1. InstanceCount = -1 è un tooService istruzione dell'infrastruttura che afferma "In ogni nodo, eseguire il servizio senza stato". Se viene modificato il numero di hello di nodi, Service Fabric modifica automaticamente hello istanza conteggio toomatch, assicurando che il servizio hello sia in esecuzione in tutti i nodi validi. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Implementazione della scalabilità tramite creazione o rimozione di nuovi servizi denominati
Un'istanza del servizio non è un'istanza specifica di un tipo di servizio (vedere [ciclo di vita dell'applicazione di Service Fabric](service-fabric-application-lifecycle.md)) all'interno di un'istanza di applicazione in cluster hello. 

È possibile creare o rimuovere nuove istanze del servizio denominate man mano che aumenta o diminuisce l'utilizzo dei servizi. In questo modo le richieste toobe distribuiti tra più istanze del servizio, consentendo in genere carico toodecrease services esistente. Quando si creano servizi, hello servizio di gestione delle risorse Cluster dell'infrastruttura, inserito servizi hello in cluster di hello in modalità distribuita. le decisioni esatta Hello dipendono dall'hello [metriche](service-fabric-cluster-resource-manager-metrics.md) in cluster hello e altre regole di selezione host. I servizi possono essere creati molti modi diversi, ma hello più comuni sono tramite azioni amministrative, ad esempio un utente chiama [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), oppure chiamando codice [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`può anche essere chiamato all'interno di altri servizi in esecuzione nel cluster hello.

La creazione dinamica dei servizi può essere usata in tutti i tipi di scenari ed è un criterio di uso comune. Si consideri ad esempio un servizio con stato che rappresenta uno specifico flusso di lavoro. Le chiamate che rappresentano lavoro stanno tooshow toothis servizio e il servizio è corso tooexecute hello passaggi toothat del flusso di lavoro e record di stato di avanzamento. 

Come è necessario apportare questa scala specifica del servizio? Hello servizio potrebbe essere multi-tenant in una determinata forma e accettare le chiamate e avviano i passaggi per molte istanze diverse di hello stesso flusso di lavoro in una sola volta. Tuttavia, che può rendere hello codice più complesso, poiché ora tooworry su molte istanze diverse di hello stesso flusso di lavoro, tutti in fasi diverse e di clienti diversi. Inoltre, la gestione di più flussi di lavoro su hello contemporaneamente persiste hello problema di scala. Questo avviene perché a un certo punto, il servizio utilizzerà toofit un numero eccessivo di risorse in un computer specifico. Molti servizi non creati per questo modello in primo luogo hello anche difficoltà scadenza collo di bottiglia inerente toosome o scarse prestazioni riscontrati nel codice. Questi tipi di problemi che il servizio di hello non toowork anche quando si ottiene maggiore numero hello di flussi di lavoro simultanei che tiene traccia.  

È una soluzione toocreate un'istanza del servizio per ogni istanza del flusso di lavoro hello diversa desiderato tootrack. Si tratta di un modello ideale e funziona se il servizio di hello è senza stato o con stato. Per toowork questo modello, è in genere un altro servizio che si comporta come un "servizio di gestione del carico di lavoro". il processo di Hello di questo servizio è richieste tooreceive e tooroute tali servizi tooother richieste. gestione Hello possibile creare dinamicamente un'istanza del servizio di carico di lavoro hello quando viene ricevuto un messaggio hello e quindi passare servizi toothose richieste. servizio di gestione di Hello può anche ricevere i callback quando un servizio flusso di lavoro specificato viene completato il processo. Quando il gestore di hello riceve questi callback è Impossibile eliminare tale istanza del servizio del flusso di lavoro hello o lasciare il campo se si prevede che più chiamate. 

Versioni avanzate di questo tipo di gestione possono anche creare pool di servizi di hello che gestisce. pool di Hello contribuisce a garantire che quando una nuova richiesta non ha toowait per hello servizio toospin. Invece, manager hello può solo selezionare un servizio flusso di lavoro che non è attualmente occupato dal pool hello o indirizzare in modo casuale. Mantenere un pool di servizi disponibili rende nuove richieste di gestione più velocemente, perché è meno probabile che la richiesta di hello è toowait per un nuovo servizio di toobe riattivata. La creazione di nuovi servizi è rapida, ma non è libera o immediata. pool di Hello consente di ridurre al minimo hello quantità di tempo richiesta hello è toowait prima fase di manutenzione. Si noterà spesso questo modello di gestione e pool quando i tempi di risposta hello più importanti. Richiesta di Accodamento messaggi hello e di creazione servizio hello in background hello e _quindi_ passarlo è anche un modello di gestione comuni, come la creazione e l'eliminazione di servizi basati su un servizio di rilevamento della quantità di hello di lavoro che attualmente è in sospeso. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Implementazione della scalabilità tramite creazione o rimozione di nuove istanze dell'applicazione denominate
Creazione ed eliminazione di istanze dell'intera applicazione è simile a toohello di creazione e l'eliminazione dei servizi. Per questo motivo, è un servizio di gestione che effettua decisione hello in base alle richieste di hello che visualizzi e informazioni hello vengono ricevuti dal hello altri servizi all'interno di cluster hello. 

Quando è preferibile usare la creazione di una nuova istanza dell'applicazione denominata al posto della creazione di una nuova istanza del servizio denominata in un'applicazione già esistente? Esistono alcuni casi in cui questa soluzione è preferibile:

  * nuova istanza dell'applicazione Hello è per un cliente il cui codice deve toorun in alcune specifica identità o le impostazioni di sicurezza.
    * Service Fabric consente di definire codice diversi pacchetti toorun con identità specifica. In ordine toolaunch hello stesso pacchetto di codice con diverse identità attivazioni hello necessario toooccur in istanze diverse dell'applicazione. Si consideri il caso in cui sono presenti carichi di lavoro distribuiti di un cliente esistente. Questi può essere eseguito con una specifica identità che consente di monitorare e controllare le relative risorse tooother di accesso, ad esempio database remoti o altri sistemi. In questo caso, quando un nuovo cliente si iscrive, probabilmente non si desidera tooactivate codice in hello stesso contesto (spazio di processo). Mentre è possibile, questo rende più difficile per tooact di codice del servizio nel contesto di hello di una specifica identità. È necessario in genere disporre di ulteriore codice per la gestione della sicurezza, dell'isolamento e delle identità. Anziché utilizzare diversi servizio istanze nella stessa istanza dell'applicazione hello e pertanto hello stesso spazio di processo, è possibile utilizzare diverse istanze denominate di applicazione di Service Fabric. Questo rende più semplici contesti di identità diversi toodefine.
  * nuova istanza dell'applicazione Hello serve anche come strumento di configurazione
    * Per impostazione predefinita, tutti i servizi le istanze denominata di un tipo di servizio specifico all'interno di un'istanza dell'applicazione hello verrà eseguito in hello stessa procedura su un determinato nodo. Ciò significa che, sebbene sia possibile configurare ogni istanza del servizio in modo diverso, si tratta di un approccio complicato. Servizi devono disporre di alcuni token usano toolook i loro configurazione all'interno di un pacchetto di configurazione. In genere si tratta solo il nome del servizio hello. Questa procedura funziona correttamente, ma associa nomi di toohello configurazione hello hello singoli denominate istanze del servizio all'interno di tale istanza dell'applicazione. Ciò può generare confusione e toomanage disco poiché configurazione è in genere un elemento della fase di progettazione con valori specifici dell'istanza dell'applicazione. Creazione di più servizi sempre comporta più gli aggiornamenti dell'applicazione informazioni di hello toochange all'interno di pacchetti di configurazione hello o toodeploy nuovi in modo che i nuovi servizi hello è possono esaminare le proprie informazioni specifiche. È spesso più facile toocreate una nuova istanza dell'applicazione denominata. È quindi possibile utilizzare hello applicazione parametri tooset qualsiasi configurazione è necessaria per servizi hello. In questo modo tutti i servizi di hello che vengono creati all'interno che nome istanza dell'applicazione può ereditare le impostazioni di configurazione specifico. Ad esempio, anziché un singolo file di configurazione con le impostazioni di hello e personalizzazioni per ogni cliente, ad esempio segreti o per i limiti delle risorse cliente, invece è un'istanza dell'applicazione diverso per ogni cliente con queste impostazioni sottoposto a override. 
  * nuova applicazione Hello funge da limite di un aggiornamento
    * All'interno di Service Fabric le diverse istanze dell'applicazione denominate fungono da limiti per l'aggiornamento. Un aggiornamento di un'istanza di applicazione denominata non influirà sul codice hello in esecuzione un'altra istanza dell'applicazione denominata. Hello diverse applicazioni finirà eseguono versioni diverse dello stesso codice hello hello stessi nodi. Può trattarsi di un fattore quando è necessario toomake una decisione relativa alla scalabilità perché è possibile scegliere che se il nuovo codice hello deve seguire hello stesso Aggiorna come un altro servizio o non. Ad esempio, che arriva una chiamata al servizio di gestione di hello che è responsabile del ridimensionamento dei carichi di lavoro di un particolare cliente tramite la creazione e l'eliminazione dei servizi in modo dinamico. In questo caso, tuttavia, la chiamata hello è per un carico di lavoro associata a un _nuova_ cliente. La maggior parte dei clienti come comunque isolate una da altra non solo per motivi di sicurezza e la configurazione di hello elencate in precedenza, ma poiché fornisce maggiore flessibilità in termini di in esecuzione versioni specifiche del software hello e scegliendo quando essi per eseguire l'aggiornamento. È anche possibile creare una nuova istanza di applicazione e creare il servizio hello sono semplicemente toofurther partizione hello quantità dei servizi che qualsiasi uno aggiornamento verrà cancellati. L'uso di istanze dell'applicazione separate offre maggiore granularità quando si eseguono gli aggiornamenti dell'applicazione e consente di usare i test A/B e le distribuzioni Blue/Green. 
  * istanza dell'applicazione esistente Hello è pieno
    * In Service Fabric, [capacità applicazione](service-fabric-cluster-resource-manager-application-groups.md) è un concetto che è possibile utilizzare quantità hello toocontrol di risorse disponibili per le istanze dell'applicazione specifico. Ad esempio, si può decidere che un dato servizio è necessario toohave creata in ordine tooscale di un'altra istanza. Questa istanza dell'applicazione è tuttavia fuori dalla capacità di una determinata metrica. Se il cliente specifico o un carico di lavoro deve ancora essere concesso più risorse, quindi è possibile aumentare hello capacità esistente per l'applicazione o creare una nuova applicazione. 

## <a name="scaling-at-hello-partition-level"></a>Scalabilità a livello di partizione hello
Service Fabric supporta il partizionamento. Il partizionamento suddivide un servizio in più sezioni logiche e fisiche, ognuna delle quali opera in modo indipendente. Ciò è utile con i servizi con stati, poiché nessun altro set di repliche è toohandle tutte le chiamate hello e modificare stato hello in una sola volta. Hello [partizionamento Panoramica](service-fabric-concepts-partitioning.md) vengono fornite informazioni sui tipi di hello degli schemi di partizionamento che sono supportati. repliche di Hello di ogni partizione vengono distribuite tra i nodi di hello in un cluster, distribuzione del carico del servizio e verificare che nessuno dei due hello nel suo complesso o qualsiasi partizione dispone di un singolo punto di errore. 

Si consideri un servizio che usa lo schema di partizionamento con intervallo con una chiave inferiore uguale a 0, una chiave superiore uguale a 99 e quattro partizioni. In un cluster con tre nodi, potrebbe essere disposti servizio hello con quattro repliche che condividono le risorse di hello in ogni nodo, come illustrato di seguito:

<center>
![Layout delle partizioni con tre nodi](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Se si aumenta il numero di hello di nodi, Service Fabric alcune delle repliche esistenti hello sposterà non esiste. Si supponga, ad esempio, il numero di hello di nodi aumenta toofour e ottengano ridistribuite repliche hello. Ora servizio hello dispone ora di tre repliche sono in esecuzione in ogni nodo, ogni appartenenti toodifferent partizioni. In questo modo l'utilizzo ottimale delle risorse poiché non è nuovo nodo hello freddo. In genere, con conseguente miglioramento delle prestazioni come ogni servizio dispone di più tooit disponibili di risorse.

<center>
![Layout delle partizioni con quattro nodi](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Il ridimensionamento tramite hello gestione delle risorse Cluster dell'infrastruttura del servizio e metrica
[Metriche](service-fabric-cluster-resource-manager-metrics.md) sono come i servizi express loro tooService consumo di risorse dell'infrastruttura. Uso delle metriche offre hello gestione delle risorse Cluster tooreorganize un'opportunità e ottimizzare il layout di hello del cluster di hello. Ad esempio, potrebbe esserci una notevole quantità di risorse cluster hello, ma non vengono allocate toohello servizi che sono in esecuzione l'attività. Uso delle metriche consente hello tooreorganize di gestione delle risorse Cluster hello cluster tooensure che i servizi hanno accesso alle risorse disponibili toohello. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Scalabilità tramite l'aggiunta e rimozione di nodi dal cluster hello 
Un'altra opzione per la scalabilità con Service Fabric è pari a hello toochange cluster hello. Modifica delle dimensioni di hello del cluster hello significa che l'aggiunta o rimozione di nodi per uno o più dei tipi di nodo hello in cluster hello. Ad esempio, si consideri il caso in cui tutti i nodi di hello cluster hello sono attivi. Ciò significa che le risorse del cluster hello vengono utilizzati quasi tutti. In questo caso, aggiungere ulteriori nodi toohello è tooscale modo migliore hello in cluster. Dopo l'aggiunta di nuovi nodi hello hello cluster hello gestione delle risorse Cluster di Service Fabric Sposta toothem servizi, risultante in totale meno carico sui nodi esistenti hello. Per i servizi senza stato con numero di istanze = -1, vengono create automaticamente più istanze del servizio. In questo modo alcuni toomove chiamate da hello esistente nodi toohello nuovi nodi. 

Aggiunta e rimozione di nodi toohello cluster può essere eseguito tramite il modulo di PowerShell di gestione risorse di Service Fabric Azure hello.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Riassumendo
Prendiamo tutte le idee di hello che è stato illustrato qui e comunicare attraverso un esempio. Prendere in considerazione hello seguente servizio: si sta tentando di un servizio che funge da una rubrica, toobuild su toonames e informazioni di contatto. 

Destra inizio si dispone di una serie di domande correlate tooscale: il numero di utenti è corso toohave? Quanti contatti archivierà ogni singolo utente? Ritentare il toofigure tutte le risorse quando sono permanente del servizio per hello prima volta che è difficile. Si supponga che si prevede di toogo con un singolo servizio statico con un numero di partizione specifica. conseguenze Hello di prelievo hello errato il numero di partizioni può causare problemi di scala toohave in un secondo momento. Analogamente, anche se si sceglie di conteggio di destra hello che potrebbe non essere tutte le informazioni di hello è necessario. Ad esempio, si hanno anche toodecide hello dimensione del cluster hello in anticipo, sia in termini di numero hello di nodi e le relative dimensioni. È in genere rigido toopredict quante risorse di un servizio in corso tooconsume nel corso della durata. Può anche essere tooknow rigido rispetto al modello di traffico hello ora servizio hello effettivamente visualizzato. Ad esempio persone maybe aggiungere e rimuovere i contatti solo in primo luogo mattino hello, o forse viene distribuito in modo uniforme nel corso hello del giorno hello. In base a questa che potrebbe essere necessario tooscale e in modo dinamico. Forse è possibile acquisire toopredict quando sarà tooneed tooscale e, ma in entrambi i casi è probabilmente il consumo di risorse tooneed tooreact toochanging dal servizio. Può comportare la modifica di dimensioni hello cluster hello in ordine tooprovide altre risorse durante la riorganizzazione di utilizzo delle risorse esistenti non è sufficiente. 

Ma perché tenta nemmeno toopick uno schema di partizione singola out per tutti gli utenti? Perché limitarsi tooone servizio e un cluster statico? situazione reale Hello è in genere più dinamiche. 

Quando si compila per scalabilità, prendere in considerazione hello modello dinamico. Potrebbe essere necessario tooadapt è tooyour situazione:

1. Anziché tentare toopick uno schema di partizionamento per tutti gli utenti in anticipo, compilare un servizio"manager".
2. il processo di Hello del servizio di gestione di hello è toolook informazioni cliente quando si iscriveranno al servizio. A seconda delle informazioni del servizio di gestione di hello creare un'istanza del _effettivo_ servizio di archiviazione di contatto _solo per quel cliente_. Se richiedono una particolare configurazione, l'isolamento o gli aggiornamenti, è anche possibile toospin di un'istanza di applicazione per il cliente. 

Questo modello di creazione dinamico offre molti vantaggi:

  - Si sta non tooguess hello partizione corretta conteggio per tutti gli utenti di o Compila un unico servizio che sia scalabile all'infinito tutto sul proprio. 
  - Gli utenti diversi non devono hello toohave stessa partizione numero, numero di repliche, vincoli di posizionamento, metriche, carica predefinito, i nomi dei servizi, le impostazioni dns oppure uno dei hello altre proprietà specificate nel servizio hello o livello di applicazione. 
  - Si ottiene una segmentazione dei dati aggiuntiva. Ogni cliente ha la propria copia del servizio hello
    - Ogni servizio del cliente può essere configurato in maniera diversa, con più o meno risorse, partizioni o repliche in base alle necessità e alla scalabilità prevista.
      - Ad esempio cliente hello pagato hello "Gold" a livelli: è stato possibile ottenere più repliche o il numero di partizioni maggiore e potenzialmente risorse dedicate servizi tootheir tramite capacità metriche e applicazione.
      - O, ad esempio vengono fornite informazioni che indica il numero di hello dei contatti sono necessari sono "Small": otterrebbe solo poche partizioni o può anche essere inserite in un pool di servizi condivisi con altri clienti.
  - Non si esegue una serie di istanze di servizi o le repliche durante l'attesa per i clienti tooshow backup
  - Se un cliente dovesse sfuggire, quindi rimuovendo le relative informazioni dal servizio è semplice come se avessero manager hello eliminare il servizio o applicazione che ha creato.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sui concetti di Service Fabric, vedere hello seguenti articoli:

* [Disponibilità dei servizi di Service Fabric](service-fabric-availability-services.md)
* [Partizionamento dei servizi di Service Fabric](service-fabric-concepts-partitioning.md)
