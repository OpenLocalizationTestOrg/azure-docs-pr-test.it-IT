---
title: aaaOverview di Service Fabric e contenitori | Documenti Microsoft
description: "Una panoramica di Service Fabric e hello utilizzare contenitori toodeploy microservizio applicazioni. In questo articolo viene fornita una panoramica di come contenitori possono essere utilizzati e hello funzionalità disponibili in Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric e contenitori
> [!NOTE]
> Questa funzionalità è disponibile in anteprima per Linux.  Distribuzione di contenitori di cluster di Service Fabric tooa in Windows 10 non è supportata ma (presto disponibile). 
>   

## <a name="introduction"></a>Introduzione
Azure Service Fabric è un [agente di orchestrazione](service-fabric-cluster-resource-manager-introduction.md) dei servizi in un cluster di computer, con anni di uso e ottimizzazione alle spalle nei servizi Microsoft con scalabilità estremamente elevata. I servizi possono essere sviluppati in diversi modi, utilizzando hello [modelli di programmazione di Service Fabric](service-fabric-choose-framework.md) toodeploying [eseguibili guest](service-fabric-deploy-existing-app.md). Per impostazione predefinita, Service Fabric distribuisce e attiva i servizi come processi. Processi forniscono attivazione più veloce hello e utilizzo di densità più elevato di risorse hello in un cluster. Service Fabric può anche distribuire servizi in immagini contenitore. Inoltre, è possibile combinare i servizi nei processi e servizi in contenitori hello stessa applicazione. 

## <a name="containers-and-service-fabric-roadmap"></a>Guida di orientamento per contenitori e Service Fabric
Per le versioni future sono previsti molti miglioramenti all'orchestrazione dei contenitori con Service Fabric. I miglioramenti includono funzionalità di rete avanzate quali supporto delle reti virtuali in un'applicazione, funzionalità di protezione, diagnostica migliorata e supporto per gli strumenti. Service Fabric consente applicazioni toocreate combinato contenitori inclusi nel pacchetto con il codice esistente (ad esempio, applicazioni MVC IIS) con i servizi sviluppati utilizzando modelli di programmazione di Service Fabric hello.  È possibile eseguire diverse applicazioni di questo tipo in un singolo cluster. 

## <a name="what-are-containers"></a>Informazioni sui contenitori
I contenitori sono incapsulati, distribuibili separatamente componenti eseguiti come istanze di tipo isolate in hello stesso kernel tootake sfruttare la virtualizzazione che fornisce un sistema operativo. Pertanto, ogni applicazione e le relative librerie di runtime, le dipendenze e il sistema eseguire all'interno di un contenitore con visualizzazione di isolamento del contenitore toohello accesso completo e privati di costrutti di sistema operativo. Insieme a garantire la portabilità, questo livello di sicurezza e isolamento delle risorse è vantaggio principale di hello per l'utilizzo di contenitori con Service Fabric, che esegue i servizi in processi in caso contrario.

I contenitori sono una tecnologia di virtualizzazione che virtualizza il sistema operativo sottostante hello dalle applicazioni. I contenitori forniscono un ambiente non modificabile per applicazioni toorun con diversi livelli di isolamento. I contenitori sono eseguiti direttamente su kernel hello e dispongono di una visualizzazione isolata del file system di hello e altre risorse. Toovirtual confrontati macchine, contenitori hanno hello seguenti vantaggi:

* **Piccola**: contenitori utilizzano un singolo spazio e il livello versioni e aggiornamenti tooincrease efficienza di archiviazione.
* **Fast**: contenitori non dispongono della tooboot un intero sistema operativo, pertanto è possibile avviare più veloce, in genere in secondi.
* **Portabilità**: un'immagine dell'applicazione nei contenitori può essere stato eseguito il porting toorun nel cloud hello, in locale, all'interno delle macchine virtuali o direttamente in computer fisici.
* **Governance delle risorse**: un contenitore è possibile limitare le risorse fisiche hello utilizzabile sul relativo host.

## <a name="container-types"></a>Tipi di contenitori
Service Fabric supporta i contenitori di Linux e Windows e supporta anche la modalità di isolamento di Hyper-V in hello quest'ultimo. 

### <a name="docker-containers-on-linux"></a>Contenitori Docker in Linux
Docker offre toocreate di alto livello API e gestire i contenitori nella parte superiore di contenitori kernel Linux. Hub docker è toostore un repository centrale e recuperare le immagini contenitore.
Per un'esercitazione, vedere [distribuire un tooService contenitore Docker dell'infrastruttura](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Contenitori Windows Server
Windows Server 2016 fornisce due diversi tipi di contenitori che si differenziano nel livello hello di isolamento specificato. Contenitori di Windows Server e i contenitori di Docker sono simili poiché dispongono di spazio dei nomi e i file di sistema isolamento ma condivisione hello kernel con host hello in che vengono eseguiti. In Linux questo isolamento viene tradizionalmente garantito con `cgroups` e `namespaces` e i contenitori Windows Server presentano un comportamento simile.

I contenitori di Hyper-V di Windows offrono maggiore isolamento e protezione perché ogni contenitore condividono kernel del sistema operativo hello con gli altri contenitori o con host hello. Con questo livello superiore di isolamento di sicurezza, i contenitori Hyper-V sono destinati a scenari multi-tenant ostili.
Per un'esercitazione, vedere [distribuire un tooService di contenitore di Windows Fabric](service-fabric-get-started-containers.md).

Hello nella figura seguente mostra hello diversi tipi di livelli di isolamento e virtualizzazione disponibili nel sistema operativo hello.
![Piattaforma Service Fabric][Image1]

## <a name="scenarios-for-using-containers"></a>Scenari per l'uso di contenitori
Ecco alcuni esempi tipici dei casi in cui un contenitore rappresenta una buona scelta:

* **IIS sollevare e spostare**: se si dispone [ASP.NET MVC](https://www.asp.net/mvc) App che si desidera toouse toocontinue, inserirli in un contenitore anziché eseguirne la migrazione tooASP.NET Core. Queste app ASP.NET MVC dipendono da IIS (Internet Information Services). È possibile comprimere queste applicazioni in immagini contenitore dall'immagine IIS creati in precedenza hello e distribuirle con Service Fabric. Vedere [immagini contenitore in Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) per informazioni su come immagini IIS toocreate.
* **Combinazione di contenitori e microservizi di Service Fabric**: usare un'immagine contenitore esistente per parte dell'applicazione. Ad esempio, è possibile utilizzare hello [contenitore NGINX](https://hub.docker.com/_/nginx/) per front-end web hello dell'applicazione e i servizi con stato per hello calcolo più intenso di back-end.
* **Ridurre l'impatto dei servizi "rumore router adiacenti"**: È possibile utilizzare possibilità di governance delle risorse hello delle risorse di hello toorestrict contenitori utilizzati da un servizio in un host. Se servizi potrebbero utilizzare molte risorse e influire sulle prestazioni di hello di altri utenti (ad esempio, un'operazione con esecuzione prolungata, simile a query), considerare l'inserimento di questi servizi in contenitori di governance delle risorse.

## <a name="service-fabric-support-for-containers"></a>Supporto di Service Fabric per i contenitori
Service Fabric attualmente supporta la distribuzione di contenitori Docker in Linux e di contenitori Windows Server in Windows Server 2016, nonché la modalità di isolamento di Hyper-V. 

In Service Fabric hello [modello applicativo](service-fabric-application-model.md), un contenitore rappresenta un'applicazione host nel quale servizio più repliche vengono inserite. Service Fabric è possibile eseguire tutti i contenitori e hello risulta simile toohello [scenario eseguibile guest](service-fabric-deploy-existing-app.md), in cui si crea il pacchetto di un'applicazione esistente all'interno di un contenitore. Questo scenario è hello-caso di utilizzo comune per i contenitori e gli esempi includono l'esecuzione di un'applicazione scritta utilizzando qualsiasi linguaggio o Framework, ma non utilizza hello incorporato Service Fabric modelli di programmazione.

È anche possibile eseguire i servizi Service Fabric all'interno dei contenitori. Supporto per i servizi di Service Fabric in esecuzione all'interno di contenitori è limitato al momento, ma toobe migliorato nelle versioni future.

* **I servizi senza stati affidabili all'interno di contenitori**: servizi Reliable senza stato tramite hello servizi affidabili in Linux sono supportati solo i modelli di programmazione. Il supporto per i servizi Reliable senza stato nei contenitori Windows è previsto per una versione futura.
* **Stato servizi all'interno di contenitori**: questi servizi utilizzano hello Reliable Actors o servizi affidabili modello di programmazione. Il supporto per l'esecuzione di servizi con stato nei contenitori verrà aggiunto in una versione futura.

Service Fabric offre diverse funzionalità relative ai contenitori che consentono di creare applicazioni costituite da microservizi inseriti in contenitori, Hello di Service Fabric offre funzionalità per i servizi nei contenitori seguenti:

* Distribuzione e attivazione di immagini contenitore
* Governance delle risorse.
* Autenticazione nel repository.
* Mapping delle porte toohost porta del contenitore.
* Individuazione e comunicazione da contenitore a contenitore.
* Tooconfigure possibilità e impostare le variabili di ambiente.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo sono stati illustrati i contenitori, la funzione di agente di orchestrazione dei contenitori svolta da Service Fabric e le funzionalità offerte da Service Fabric per supportare i contenitori. Come passaggio successivo, verranno esaminate negli esempi di ogni tooshow funzionalità hello è come toouse li.

[Distribuire un tooService di contenitore di Windows Fabric in Windows Server 2016](service-fabric-get-started-containers.md)

[Distribuire un tooService contenitore Docker dell'infrastruttura in Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
