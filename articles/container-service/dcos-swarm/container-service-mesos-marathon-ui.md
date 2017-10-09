---
title: aaaManage controller di dominio o sistema operativo Azure cluster con interfaccia utente maratona | Documenti Microsoft
description: Distribuire i contenitori tooan Azure contenitore cluster del servizio tramite l'interfaccia utente web di maratona hello.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Contenitori, Micro-servizi, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Gestire un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo tramite web maratona hello dell'interfaccia utente
Controller di dominio/OS offre un ambiente per la distribuzione e scalabilità i carichi di lavoro cluster eliminando l'hardware sottostante hello. In DC/OS è disponibile anche un framework che gestisce la pianificazione e l'esecuzione dei carichi di lavoro di calcolo.

Mentre i Framework sono disponibili per molti carichi di lavoro comuni, questo documento descrive come tooget iniziare la distribuzione di contenitori con maratona. 


## <a name="prerequisites"></a>Prerequisiti
Prima di eseguire questi esempi, è necessario avere un cluster DC/OS configurato nel servizio contenitore di Azure. È inoltre necessario cluster toothis di toohave connettività remota. Per ulteriori informazioni su questi elementi, vedere hello seguenti articoli:

* [Distribuire un cluster del servizio contenitore di Azure](container-service-deployment.md)
* [Connettersi tooan cluster del servizio di contenitore di Azure](../container-service-connect.md)

> [!NOTE]
> In questo articolo si presuppone che sono di tunneling toohello cluster di controller di dominio o del sistema operativo tramite la porta locale 80.
>

## <a name="explore-hello-dcos-ui"></a>Esplorare hello dell'interfaccia utente di controller di dominio o del sistema operativo
Con un tunnel SSH (Secure Shell) [stabilita](../container-service-connect.md), Sfoglia toohttp://localhost/. Questo carica l'interfaccia utente web di controller di dominio/OS hello e Mostra le informazioni sui cluster di hello, ad esempio le risorse, gli agenti active e servizi in esecuzione.

![Interfaccia utente di DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Esplorare hello maratona UI
hello toosee maratona dell'interfaccia utente, toohttp://localhost/marathon Sfoglia. In questa schermata è possibile avviare un nuovo contenitore o un'altra applicazione nel cluster di hello Azure contenitore del servizio controller di dominio o del sistema operativo. È anche possibile visualizzare le informazioni sull'esecuzione di contenitori e applicazioni.  

![Interfaccia utente di Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Distribuire un contenitore Docker formattato
Fare clic su un nuovo contenitore usando maratona, toodeploy **Crea applicazione**e immettere le seguenti informazioni in schede modulo hello hello:

| Campo | Valore |
| --- | --- |
| ID |nginx |
| Memoria | 32 |
| Image |nginx |
| Network |Bridged |
| Host Port |80 |
| Protocol |TCP |

![Interfaccia utente New Application--General](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interfaccia utente New Application--Docker Container](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interfaccia utente New Application--Ports and Service Discovery](./media/container-service-mesos-marathon-ui/dcos6.png)

Se si desidera toostatically mappa hello contenitore tooa porte nell'agente hello, è necessario toouse modalità JSON. toodo passare in tal caso, creazione guidata nuova applicazione hello troppo**modalità JSON** utilizzando l'elemento toggle hello. Immettere quindi hello seguente impostazione hello `portMappings` sezione hello dalla definizione dell'applicazione. Questo esempio associa la porta 80 del contenitore di hello tooport 80 dell'agente di controller di dominio/OS hello. Dopo aver apportato questa modifica è possibile uscire dalla modalità JSON della procedura guidata.

```none
"hostPort": 80,
```

![Interfaccia utente New Application--esempio con porta 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Se si desidera tooenable controlli di integrità, è possibile impostare un percorso su hello **controlli di integrità** scheda.

![Nuova interfaccia utente dell'applicazione - Verifiche di integrità](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

cluster di controller di dominio/OS Hello viene distribuito con set di agenti privati e pubblici. Applications hello cluster toobe tooaccess in grado di hello Internet, è necessario agente pubblica tooa toodeploy hello applicazioni. toodo in tal caso, selezionare hello **facoltativo** scheda della creazione guidata nuova applicazione hello e immettere **slave_public** per hello **accettato ruoli risorsa**.

Fare clic su **Create Application** (Crea applicazione).

![Interfaccia utente New Application--impostazione dell'agente pubblico](./media/container-service-mesos-marathon-ui/dcos14.png)

Indietro nella pagina principale di maratona hello, è possibile visualizzare lo stato di distribuzione hello per contenitore hello. Inizialmente è visualizzato lo stato **Deploying** (Distribuzione). Dopo una corretta distribuzione, hello modifiche allo stato troppo**esecuzione**.

![Interfaccia utente della pagina principale di Marathon--stato di distribuzione contenitore](./media/container-service-mesos-marathon-ui/dcos7.png)

Quando si passa indietro toohello web di controller di dominio o del sistema operativo dell'interfaccia utente (http://localhost/), vedrai che un'attività (in questo caso, un contenitore Docker in formato) sia in esecuzione nel cluster di controller di dominio/OS hello.

![Controller di dominio o del sistema operativo interfaccia utente web - attività in esecuzione nel cluster hello](./media/container-service-mesos-marathon-ui/dcos8.png)

nodo del cluster hello toosee che hello attività è in esecuzione in, fare clic su hello **nodi** scheda.

![Interfaccia utente Web di DC/OS--nodo del cluster dell'attività](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Raggiungere hello contenitore

In questo esempio, un'applicazione hello è in esecuzione in un nodo agente pubblica. Si raggiunge un'applicazione hello da hello internet esplorando toohello agente FQDN del cluster hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, dove:

* **DNSPREFIX** è un prefisso DNS hello fornito al momento della distribuzione cluster hello.
* **AREA** hello area in cui si trova il gruppo di risorse.

    ![Nginx da Internet](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Passaggi successivi
* [Utilizzare i controller di dominio/OS e hello maratona API](container-service-mesos-marathon-rest.md)

* Informazioni approfondite su hello servizio contenitore di Azure con Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
