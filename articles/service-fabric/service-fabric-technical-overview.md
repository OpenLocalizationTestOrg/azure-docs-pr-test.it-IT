---
title: terminologia di Azure Service Fabric aaaLearn | Documenti Microsoft
description: Panoramica della terminologia di Service Fabric. Vengono illustrati terminologia concetti e termini utilizzati nel resto di hello della documentazione di hello.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Panoramica della terminologia di Service Fabric
Service Fabric è una piattaforma di sistemi distribuiti che rende facile toopackage, distribuire e gestire microservizi scalabili e affidabili. Questo argomento dettagli hello la terminologia utilizzata da Service Fabric toounderstand hello termini utilizzati nella documentazione di hello.

Hello concetti elencati in questa sezione vengono descritte anche nel hello seguente video Microsoft Virtual Academy: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">concetti fondamentali</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">concetti in fase di progettazione</a>, e <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">iconcettidiRun-time</a>.

## <a name="infrastructure-concepts"></a>Concetti relativi all'infrastruttura
**Cluster**: un set di computer fisici o macchine virtuali connesse tramite rete in cui vengono distribuiti e gestiti i microservizi.  I cluster possono essere ridimensionati toothousands macchine.

**Nodo**: un computer o una macchina virtuale che fa parte di un cluster viene chiamato nodo. A ogni nodo viene assegnato un nome (stringa). I nodi presentano delle caratteristiche, ad esempio le proprietà di posizionamento. In ogni computer o macchina virtuale è disponibile un servizio di avvio automatico di Windows, `FabricHost.exe`, che viene eseguito all'avvio e che a sua volta avvia due eseguibili: `Fabric.exe` e `FabricGateway.exe`. Questi due eseguibili costituiscono dal nodo hello. Negli scenari di test è possibile ospitare più nodi in un singolo PC o una singola macchina virtuale eseguendo più istanze di `Fabric.exe` e `FabricGateway.exe`.

## <a name="application-concepts"></a>Concetti relativi alle applicazioni
**Tipo di applicazione**: hello Nome/versione assegnata tooa raccolta dei tipi di servizio. Definito in un `ApplicationManifest.xml` file, incorporati in una directory del pacchetto di applicazione, che viene quindi copiato archivio di immagini del cluster di Service Fabric toohello. È quindi possibile creare un'applicazione denominata da questo tipo di applicazione all'interno di cluster hello.

Hello lettura [modello applicativo](service-fabric-application-model.md) per ulteriori informazioni.

**Pacchetto di applicazione**: una directory del disco contenente del tipo di applicazione hello `ApplicationManifest.xml` file. Riferimenti hello pacchetti del servizio per ogni tipo di servizio che costituisce il tipo di applicazione hello. file Hello nella directory del pacchetto di applicazione hello sono archivio di immagini del cluster di infrastruttura tooService copiato. Ad esempio, un pacchetto di applicazione per un tipo di applicazione di posta elettronica potrebbe contenere riferimenti tooa coda servizio pacchetto, un pacchetto del servizio front-end e un pacchetto del servizio di database.

**Nome applicazione**: un pacchetto di applicazione, dopo aver copiato toohello archivio di immagini, creerai un'istanza di un'applicazione hello all'interno di cluster hello specificando il tipo di applicazione del pacchetto di applicazione hello (mediante il relativo nome/versione). A ogni istanza del tipo di applicazione viene assegnato un nome URI simile al seguente: `"fabric:/MyNamedApp"`. All'interno di un cluster è possibile creare più applicazioni denominate da un singolo tipo di applicazione. È anche possibile creare applicazioni denominate da tipi di applicazione diversi. L'amministrazione e il controllo delle versioni sono gestiti in modo indipendente per ogni applicazione.      

**Tipo di servizio**: hello. nome/versione assegnato pacchetti di codice, i pacchetti di dati e pacchetti di configurazione del servizio tooa. Definito in un `ServiceManifest.xml` file, incorporato in una directory del pacchetto del servizio e una directory del pacchetto del servizio hello viene quindi fatto riferimento da un pacchetto di applicazione `ApplicationManifest.xml` file. All'interno di cluster hello, dopo la creazione di un'applicazione denominata, è possibile creare un servizio denominato da una delle hello tipi di servizio del tipo di applicazione. tipo di servizio Hello `ServiceManifest.xml` file descrive servizio hello.

Hello lettura [modello applicativo](service-fabric-application-model.md) per ulteriori informazioni.

Sono disponibili due tipi di servizi:

* **Stateless:** utilizzare un servizio senza stato, quando uno stato persistente del servizio hello viene archiviato in un servizio di archiviazione esterna, ad esempio l'archiviazione di Azure, Database SQL di Azure o Azure Cosmos DB. Utilizzare un servizio senza stato quando il servizio di hello non dispone di alcun archivio permanente affatto. Ad esempio, un servizio Calcolatrice in cui i valori vengono passati toohello servizio, viene eseguito un calcolo utilizzando questi valori e viene restituito un risultato.
* **Con stato:** utilizzare un servizio con stato quando si desidera che lo stato del servizio tramite il relativo raccolte affidabile o Reliable Actors modelli di programmazione toomanage Service Fabric. Specificare il numero di partizioni desiderate toospread lo stato su (per la scalabilità) quando si crea un servizio denominato. Specificare anche il numero di volte tooreplicate lo stato tra i nodi (per l'affidabilità). Ogni servizio denominato ha un'unica replica primaria e più repliche secondarie. Modificare lo stato del servizio denominata scrivendo toohello replica primaria. Quindi, Service Fabric replica questo stato tooall hello repliche secondarie mantenere sincronizzati i dati. Service Fabric rileva automaticamente una replica primaria ha esito negativo e Alza di livello una replica primaria tooa replica secondaria esistente. Crea quindi una nuova replica secondaria.  

**Pacchetto del servizio**: una directory del disco contenente del tipo di servizio hello `ServiceManifest.xml` file. Questo file fa riferimento a codice hello, dati statici e i pacchetti di configurazione per il tipo di servizio hello. i file nella directory del pacchetto del servizio hello Hello fanno riferimento del tipo di applicazione hello `ApplicationManifest.xml` file. Ad esempio, un pacchetto del servizio potrebbe fare riferimento a codice toohello, i dati statici e i pacchetti di configurazione che costituiscono un servizio di database.

**Nome servizio**: dopo la creazione di un'applicazione denominata, è possibile creare un'istanza di uno dei relativi tipi di servizio all'interno di cluster hello specificando il tipo di servizio hello (mediante il relativo nome/versione). A ogni istanza del tipo di servizio viene assegnato un nome URI con un ambito definito dall'URI della relativa applicazione denominata. Ad esempio, se si crea un servizio all'interno di un'applicazione denominata "MyNamedApp" denominato "MyDatabase", URI hello aspetto: `"fabric:/MyNamedApp/MyDatabase"`. All'interno di un'applicazione denominata è possibile creare vari servizi denominati. Ogni servizio denominato può avere uno schema di partizione e numeri di istanze/repliche specifici.

**Pacchetto di codice**: una directory su disco che contiene file eseguibili del tipo di servizio hello (in genere il file EXE o DLL). i file nella directory del pacchetto di codice hello Hello fanno riferimento del tipo di servizio hello `ServiceManifest.xml` file. Quando viene creato un servizio in questione, il pacchetto di codice hello è nodo toohello copiato o hello toorun selezionati nodi denominato "service". Codice hello quindi avvia l'esecuzione. Esistono due tipi di eseguibili di pacchetto di codice:

* **File eseguibili guest**: file eseguibili che vengono eseguiti come-il sistema operativo host hello (Windows o Linux). Vale a dire, questi file eseguibili non non riferimento al collegamento tooor eventuali file di runtime di Service Fabric e pertanto non utilizzano tutti modelli di programmazione di Service Fabric. Questi file eseguibili sono di tipo non è possibile toouse che alcune funzionalità di Service Fabric, ad esempio hello dei nomi di servizio per l'individuazione di endpoint. File eseguibili guest non è in grado di indicare carico metriche tooeach specifica istanza del servizio.
* **File eseguibili del servizio Host**: file eseguibili che utilizzano modelli di programmazione tramite il collegamento a file di runtime dell'infrastruttura tooService, Service Fabric attivazione di funzionalità di Service Fabric. Un'istanza di servizio denominato può ad esempio registrare gli endpoint con il servizio Naming di Service Fabric e anche segnalare le metriche di carico.      

**Pacchetto di dati**: una directory del disco contenente file di dati di sola lettura, statici del tipo di servizio hello (in genere, foto, file audio e video). i file nella directory del pacchetto di dati hello Hello fanno riferimento del tipo di servizio hello `ServiceManifest.xml` file. Quando viene creato un servizio in questione, il pacchetto di dati di hello è nodo toohello copiato o hello toorun selezionati nodi denominato "service".  codice Hello viene avviata l'esecuzione e può accedere ai file di dati hello.

**Pacchetto di configurazione**: file di configurazione di sola lettura di una directory del disco contenente statico del tipo di servizio hello, (in genere i file di testo). i file nella directory del pacchetto di configurazione hello Hello fanno riferimento del tipo di servizio hello `ServiceManifest.xml` file. Quando viene creato un servizio in questione, file di hello nel pacchetto di configurazione hello sono toohello copiato uno o più hello toorun selezionato di nodi denominato "service". Quindi codice hello viene avviata l'esecuzione e può accedere ai file di configurazione hello.

**Contenitori**: per impostazione predefinita, Service Fabric distribuisce e attiva i servizi come processi. Service Fabric può anche distribuire servizi in immagini contenitore. I contenitori sono una tecnologia di virtualizzazione che virtualizza il sistema operativo sottostante hello dalle applicazioni. Un'applicazione e le relative librerie di runtime, le dipendenze e il sistema vengono eseguite in un contenitore con visualizzazione di isolamento del contenitore toohello accesso completo e privati di costrutti di sistema operativo. Service Fabric supporta contenitori Docker in Linux e contenitori Windows Server.  Per altre informazioni, vedere [Service Fabric e contenitori](service-fabric-containers-overview.md).

**Schema di partizione**: quando si crea un servizio denominato, è necessario specificare uno schema di partizione. I servizi con grandi quantità di stato divisione dei dati hello tra partizioni, che viene distribuita stato hello nei nodi del cluster hello. In questo modo tooscale lo stato del servizio denominata. All'interno di una partizione, per i servizi denominati senza stato sono presenti istanze mentre per i servizi denominati con stato sono presenti repliche. In genere i servizi denominati senza stato avranno sempre una sola partizione, dal momento che non hanno uno stato interno. le istanze di partizione Hello forniscono disponibilità; Se un'istanza non riesce, le altre istanze toooperate continuano a funzionare normalmente e quindi Service Fabric creerà una nuova istanza. Con stato denominato services mantenimento dello stato all'interno di repliche e ogni partizione dispone di propri repliche con tutti gli stati di hello mantenuti sincronizzati. Una replica avrà esito negativo, Service Fabric crea una nuova replica da repliche esistenti hello.

Hello lettura [servizi affidabili partizione Service Fabric](service-fabric-concepts-partitioning.md) per ulteriori informazioni.

## <a name="system-services"></a>Servizi di sistema
Sono disponibili servizi di sistema vengono creati in ogni cluster che forniscono funzionalità della piattaforma hello di Service Fabric.

**Servizio di denominazione**: dell'infrastruttura del servizio di ogni cluster dispone di un servizio di denominazione, che risolve percorso tooa i nomi del servizio cluster hello. Gestire i nomi dei servizi di hello e proprietà, simile tooan internet del servizio DNS (Domain Name) per il cluster hello. I client comunicano in modo sicuro con qualsiasi nodo cluster hello hello Naming Service tooresolve utilizzando un nome di servizio e il relativo percorso.  Applicazioni spostarsi all'interno del cluster di hello, ad esempio a causa di toofailures bilanciamento delle risorse o hello il ridimensionamento del cluster di hello. È possibile sviluppare servizi e client di cui risolvere il percorso di rete corrente hello. I client ottenere l'indirizzo IP di computer effettivo hello e la porta in cui è attualmente in esecuzione.

Lettura [per comunicare con servizi](service-fabric-connect-and-communicate-with-services.md) per ulteriori informazioni su hello servizio di comunicazione tra client e le API che utilizzano il servizio di denominazione hello.

**Servizio Image Store**: ogni cluster di Service Fabric ha un servizio Image Store in cui vengono conservati i pacchetti dell'applicazione distribuiti e con controllo delle versioni. Copiare un toohello pacchetto di applicazione Image Store e quindi registrare il tipo di applicazione hello contenuto all'interno di tale pacchetto di applicazione. Dopo il provisioning, il tipo di applicazione hello è creare un'applicazione denominata da esso. È possibile annullare la registrazione di un tipo di applicazione da hello servizio Image Store dopo aver eliminate tutte le applicazioni denominate.

Lettura [comprendere impostazione ImageStoreConnectionString hello](service-fabric-image-store-connection-string.md) per ulteriori informazioni su hello servizio Image Store.

Hello lettura [distribuire un'applicazione](service-fabric-deploy-remove-applications.md) per ulteriori informazioni sulla distribuzione del servizio di archiviazione di applicazioni toohello immagine.

## <a name="built-in-programming-models"></a>Modelli di programmazione predefiniti
Modelli di programmazione di .NET Framework sono disponibili servizi di Service Fabric toobuild:

**Servizi affidabili**: un'API toobuild servizi senza stato. I servizi con stato archiviano il proprio stato in Reliable Collections, ad esempio un dizionario o una coda. Anche possibile ottenere tooplug in vari stack di comunicazione, ad esempio API Web e Windows Communication Foundation (WCF).

**Reliable Actors**: oggetti un'API toobuild e senza stati tramite hello virtuale attore modello di programmazione. Questo modello può risultare utile in presenza di molte unità indipendenti di calcolo/stato. Poiché questo modello viene utilizzato un modello di threading attiva, è migliore tooavoid il codice che chiama tooother attori o servizi poiché un attore singoli non possa elaborare altre richieste in ingresso fino al completamento di tutte le richieste in uscita.

Hello lettura [scegliere un modello di programmazione per il servizio](service-fabric-choose-framework.md) per ulteriori informazioni.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
informazioni su Service Fabric toolearn:

* [Panoramica di Service Fabric](service-fabric-overview.md)
* [Motivo per cui un microservizi approccio toobuilding applicazioni?](service-fabric-overview-microservices.md)
* [Scenari applicativi](service-fabric-application-scenarios.md)

