---
title: aaaManage le applicazioni in Visual Studio | Documenti Microsoft
description: Utilizzare toocreate di Visual Studio, sviluppare, pacchetto, distribuzione e debug di applicazioni di Service Fabric e ai servizi.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Utilizzare Visual Studio toosimplify scrittura e la gestione delle applicazioni di Service Fabric
È possibile gestire le applicazioni e i servizi di Service Fabric di Azure tramite Visual Studio. Dopo aver [configurare l'ambiente di sviluppo](service-fabric-get-started.md), è possibile utilizzare applicazioni di Service Fabric toocreate Visual Studio, aggiungere registro servizi o di pacchetto e distribuire le applicazioni del cluster di sviluppo locale.

## <a name="deploy-your-service-fabric-application"></a>Distribuire l'applicazione di Service Fabric
Per impostazione predefinita, la distribuzione di un'applicazione combina hello in una semplice operazione come segue:

1. Creazione pacchetto di applicazione hello
2. Archivio di immagini di caricamento hello applicazione pacchetto toohello
3. Registrazione del tipo di applicazione hello
4. Rimozione delle eventuali istanze dell'applicazione in esecuzione
5. Creazione di un'istanza dell'applicazione

In Visual Studio, premere **F5** distribuisce l'applicazione e collegare le istanze dell'applicazione hello debugger tooall. È possibile utilizzare **Ctrl + F5** toodeploy un'applicazione senza debug oppure è possibile pubblicare tooa locale o remota del cluster tramite hello profilo di pubblicazione. Per ulteriori informazioni, vedere [pubblicare un cluster remoto tooa delle applicazioni con Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Modalità di debug applicazione
Visual Studio forniscono una proprietà denominata **modalità di Debug dell'applicazione**, che controlla la modalità di distribuzione di applicazioni di Visual studi toohandle come parte di debug.

#### <a name="tooset-hello-application-debug-mode-property"></a>hello tooset proprietà modalità di Debug dell'applicazione
1. In hello Service Fabric del progetto dell'applicazione (*. sfproj) dal menu di scelta rapida scegliere **proprietà** (o premere hello **F4** chiave).
2. In hello **proprietà** finestra, hello set **modalità di Debug dell'applicazione** proprietà.

![Impostare la proprietà Modalità di debug applicazione][debugmodeproperty]

#### <a name="application-debug-modes"></a>Modalità di debug dell'applicazione

1. **Aggiornare applicazione** questa modalità consente modifiche tooquickly ed eseguire il debug del codice e supporta la modifica di file web statici durante il debug. Questa modalità funziona solo se il cluster di sviluppo locale è in [modalità a 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Rimuovere l'applicazione** cause hello toobe applicazione rimossi quando termina la sessione di debug hello.
3. **L'aggiornamento automatico** applicazione hello continua toorun quando termina la sessione di debug hello. Hello successiva sessione di debug verrà considerato distribuzione hello un aggiornamento. processo di aggiornamento Hello mantiene tutti i dati immessi in una sessione di debug precedente.
4. **Applicazione di mantenere** mantiene applicazione hello in esecuzione in cluster hello quando hello debug sessione termina. Hello inizio hello successiva sessione di debug, un'applicazione hello verrà rimossi.

Per **l'aggiornamento automatico** i dati vengono conservati applicando la funzionalità di aggiornamento dell'applicazione hello di Service Fabric. Per altre informazioni sull'aggiornamento delle applicazioni e su come è possibile eseguire un aggiornamento in un ambiente reale, vedere [Aggiornamento di un'applicazione di Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Aggiungere un tooyour servizio applicazione di Service Fabric
È possibile aggiungere nuovi servizi tooyour applicazione tooextend relativa funzionalità.  tooensure servizio hello viene incluso nel pacchetto dell'applicazione, aggiungere il servizio di hello tramite hello **nuovo Service Fabric...**  voce di menu.

![Aggiungere un nuovo servizio di Service Fabric][newservice]

Selezionare un'applicazione di Service Fabric progetto tipo tooadd tooyour e specificare un nome per il servizio di hello.  Vedere [scelta di un framework per il servizio](service-fabric-choose-framework.md) toohelp si decide quale servizio digitare toouse.

![Selezionare un'applicazione tooyour tooadd tipo di Service Fabric servizio progetto][addserviceproject]

nuovo servizio Hello viene aggiunto tooyour soluzione e il pacchetto di applicazione esistente. riferimenti al servizio Hello e un'istanza del servizio predefinito sarà manifesto dell'applicazione toohello aggiunto, causando hello servizio toobe creata e avviata hello successivo che si distribuisce un'applicazione hello.

![nuovo servizio Hello viene aggiunto il manifesto di applicazione tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Creazione del pacchetto per l'applicazione di Service Fabric
un'applicazione hello toodeploy e il cluster tooa services, è necessario toocreate un pacchetto di applicazione.  Consente di organizzare i pacchetti Hello manifesto dell'applicazione hello, i manifesti del servizio e altri file necessari in un layout specifico.  Visual Studio configura e gestisce i pacchetti hello nella cartella del progetto dell'applicazione hello, nella directory 'pkg' hello.  Fare clic su **pacchetto** da hello **applicazione** Crea menu di scelta rapida o aggiornamenti hello pacchetto dell'applicazione.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Rimuovere applicazioni e tipi di applicazione con Cloud Explorer
È possibile eseguire le operazioni di Gestione cluster di base dall'interno Visual Studio Cloud Explorer, che è possibile avviare da hello usando **vista** menu. È ad esempio possibile eliminare applicazioni e annullare il provisioning di tipi di applicazione in cluster locali o remoti.

![Rimuovere un'applicazione][removeapplication]

> [!TIP]
> Per funzionalità di gestione dei cluster più avanzate, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
* [Modello di applicazione di Service Fabric](service-fabric-application-model.md)
* [Distribuzione di un'applicazione di Service Fabric](service-fabric-deploy-remove-applications.md)
* [Gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md)
* [Debug dell'applicazione di Service Fabric](service-fabric-debugging-your-application.md)
* [Visualizzazione del cluster con l’explorer di Service Fabric](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png