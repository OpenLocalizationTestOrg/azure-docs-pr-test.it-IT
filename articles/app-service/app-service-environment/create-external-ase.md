---
title: aaaCreate un ambiente esterno del servizio App di Azure
description: Viene illustrato come toocreate un ambiente del servizio App quando si crea un'app o autonomo
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Creare un ambiente del servizio app esterno #

L'ambiente del servizio app di Azure è una distribuzione di Servizio app di Azure in una subnet in una rete virtuale di Azure. Esistono due modi toodeploy un ambiente del servizio App (ASE):

- Con un indirizzo VIP su un indirizzo IP esterno, spesso denominato ambiente del servizio app esterno.
- Con hello VIP all'indirizzo IP interno, spesso chiamato ASE un bilanciamento del carico interno perché l'endpoint interno hello è un servizio di bilanciamento del carico interno (ILB).

In questo articolo illustra come toocreate un ASE esterno. Per una panoramica di hello ASE, vedere [un ambiente del servizio App di toohello Introduzione][Intro]. Per informazioni su come toocreate un bilanciamento del carico interno ASE, vedere [creare e usare un ASE ILB][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Prima di creare l'ambiente del servizio app ##

Dopo aver creato il tipo di base, è possibile modificare l'esempio hello:

- Percorso
- Subscription
- Gruppo di risorse
- Rete virtuale usata
- Subnet usata
- Dimensioni della subnet

> [!NOTE]
> Quando si sceglie una rete virtuale e specificare una subnet, assicurarsi che sia abbastanza grande tooaccommodate conto della crescita futura. È consigliabile una dimensione pari a `/25` con 128 indirizzi.
>

## <a name="three-ways-toocreate-an-ase"></a>Tre modi toocreate un ASE ##

Esistono tre modi toocreate un ASE:

- **Durante la creazione di un piano di servizio app**. Questo metodo crea hello ASE e hello piano di servizio App in un unico passaggio.
- **Come azione autonoma**. Questo metodo crea un ambiente del servizio app autonomo, ovvero un ambiente del servizio app vuoto. Questo metodo è un toocreate di processo un ASE più avanzate. Viene usato un ASE toocreate con un bilanciamento del carico interno.
- **Da un modello di Azure Resource Manager**. Questo metodo è per gli utenti avanzati. Per altre informazioni, vedere [Creare un ambiente del servizio app da un modello][MakeASEfromTemplate].

Un ASE esterna ha un indirizzo VIP pubblico, il che significa che tutte le app toohello il traffico HTTP/HTTPS in hello ASE riscontri un indirizzo IP accessibile tramite internet. Un ASE con un bilanciamento del carico interno è un indirizzo IP dalla subnet hello utilizzato da hello ASE. Hello App ospitate in una base di bilanciamento del carico interno non sono esposte direttamente toohello internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Creare contemporaneamente un ambiente del servizio app e un piano di servizio app ##

piano di servizio App Hello è un contenitore di App. Quando si crea un'applicazione nel servizio app, scegliere o creare un piano di servizio app. gli ambienti di Hello contenitore modello contengono i piani di servizio App e le piani di servizio App contengono le app.

toocreate un ASE durante la creazione di un piano di servizio App:

1. In hello [portale di Azure](https://portal.azure.com/)selezionare **New** > **Web e dispositivi mobili** > **App Web**.

    ![Creazione dell'app Web][1]

2. Selezionare la propria sottoscrizione. app Hello e hello ASE vengono creati in hello stesso sottoscrizioni.

3. Selezionare o creare un gruppo di risorse. Con i gruppi di risorse è possibile gestire insieme le risorse di Azure correlate. I gruppi di risorse sono utili anche quando si stabiliscono le regole di controllo degli accessi in base al ruolo per le app. Per ulteriori informazioni, vedere hello [Panoramica di gestione risorse di Azure][ARMOverview].

4. Selezionare il piano di servizio App hello, quindi **Crea nuovo**.

    ![Nuovo piano di servizio app][2]

5. In hello **percorso** elenco a discesa, selezionare hello area in cui toocreate hello ASE. Se si seleziona un ambiente del servizio app esistente, non viene creato un nuovo ambiente del servizio app. piano di servizio App Hello viene creato in hello ASE selezionato. 

6. Selezionare **tariffario**e scegliere una delle hello **Isolated** prezzi SKU. Se si sceglie una scheda SKU **Isolato** e una località diversa da un ambiente del servizio app, un nuovo ambiente del servizio app viene creato in tale località. Selezionare toostart hello processo toocreate un ASE, **selezionare**. Hello **Isolated** SKU è disponibile solo in combinazione con un tipo di base. Non è inoltre possibile usare qualsiasi altro codice di riferimento del prodotto per i prezzi in un ambiente del servizio app diverso da **Isolato**.

    ![Selezione del piano tariffario][3]

7. Immettere il nome di hello per il tipo di base. Questo nome viene utilizzato nel nome indirizzabile di hello per le app. Se il nome di hello di hello ASE _appsvcenvdemo_, il nome di dominio hello *. appsvcenvdemo.p.azurewebsites.net*. Se è stata creata un'app denominata *mytestapp*, questa sarà disponibile all'indirizzo mytestapp.appsvcenvdemo.p.azurewebsites.net. Non è possibile utilizzare gli spazi vuoti nel nome hello. Se si usano caratteri maiuscoli, il nome di dominio di hello è totale versione minuscola di hello di tale nome.

    ![Nome del nuovo piano di servizio app][4]

8. Specificare i dettagli della rete virtuale Azure. Selezionare **Crea nuovo** o **Seleziona esistente**. Hello opzione tooselect una rete virtuale di esistente è disponibile solo se si dispone di una rete virtuale in un'area selezionata hello. Se si seleziona **Crea nuovo**, immettere un nome per hello rete virtuale. Viene creata una nuova rete virtuale con questo nome, Usa lo spazio degli indirizzi hello `192.168.250.0/23` in un'area selezionata hello. Se si sceglie **Seleziona esistente**, è necessario:

    a. Selezionare il blocco di indirizzi di rete virtuale hello, se si dispone di più di uno.

    b. Immettere un nuovo nome di subnet.

    c. Selezionare dimensione hello della subnet hello. *Tenere presente che una crescita futura tooaccommodate sufficientemente grande di dimensioni del ASE tooselect.* È consigliabile scegliere `/25`, che contiene 128 indirizzi e può gestire un ambiente del servizio app con dimensione massima. Non è consigliato, ad esempio, `/28`, perché sono disponibili solo 16 indirizzi. L'infrastruttura usa almeno cinque indirizzi. In una subnet `/28` il ridimensionamento massimo possibile è di 11 istanze.

    d. Selezionare intervallo IP di subnet hello.

9. Selezionare **crea** toocreate hello ASE. Questo processo crea anche il piano di servizio App hello e app hello. app Hello ASE e piano di servizio App sono tutte nella hello stessa sottoscrizione e anche in hello stesso gruppo di risorse. Se il ASE necessita di un gruppo di risorse separato o se è necessario un ASE ILB, seguire hello passaggi toocreate un ASE da se stesso.

## <a name="create-an-ase-by-itself"></a>Creare un ambiente del servizio app autonomo ##

Se si crea un ambiente del servizio app autonomo, risulterà vuoto. Un ASE vuoto comporta comunque addebiti mensili per infrastruttura hello. Seguire questi toocreate passaggi un ASE con un bilanciamento del carico interno o toocreate un ASE nel proprio gruppo di risorse. Dopo aver creato il tipo di base, è possibile creare applicazioni in essa contenuti utilizzando il normale processo di hello. Selezionare il nuovo ASE come percorso di hello.

1. Ricerca hello Azure Marketplace per **ambiente del servizio App**, oppure selezionare **New** > **Web Mobile** > **servizio App Ambiente**. 

2. Immettere il nome di hello del ASE. Questo nome viene utilizzato per le app hello create in hello ASE. Se il nome di hello *mynewdemoase*, il nome di sottodominio hello è *. mynewdemoase.p.azurewebsites.net*. Se è stata creata un'app denominata *mytestapp*, questa sarà disponibile all'indirizzo mytestapp.mynewdemoase.p.azurewebsites.net. Non è possibile utilizzare gli spazi vuoti nel nome hello. Se si usano caratteri maiuscoli, il nome di dominio di hello è totale versione minuscola di hello del nome hello. Se si usa un servizio di bilanciamento del carico interno, il nome dell'ambiente del servizio app non viene usato nel sottodominio, ma viene dichiarato in modo esplicito durante la creazione dell'ambiente.

    ![Denominazione dell'ambiente del servizio app][5]

3. Selezionare la propria sottoscrizione. Questa sottoscrizione è inoltre hello che tutte le App in hello ASE usare. Non è possibile inserire l'ambiente del servizio app in una rete virtuale che si trova in un'altra sottoscrizione.

4. Selezionare o specificare un nuovo gruppo di risorse. gruppo di risorse Hello utilizzato per la base deve essere identico a quello utilizzato per la rete virtuale hello. Se si seleziona una rete virtuale di esistente, selezione del gruppo risorse hello per le ASE è tooreflect aggiornato che di una rete virtuale. *È possibile creare un ASE con un gruppo di risorse che è diverso dal gruppo di risorse di rete virtuale hello se si utilizza un modello di gestione risorse.* toocreate un ASE da un modello, vedere [creare un ambiente del servizio App da un modello][MakeASEfromTemplate].

    ![Selezione del gruppo di risorse][6]

5. Selezionare la rete virtuale e la località. È possibile creare una nuova rete virtuale o selezionare una rete virtuale esistente: 

    * Se si seleziona una nuova rete virtuale, è possibile specificare un nome e una località. Hello nuova rete virtuale ha hello indirizzo intervallo 192.168.250.0/23 e una subnet denominato default. subnet Hello è definito come 192.168.250.0/24. È possibile selezionare solo una rete virtuale di Resource Manager. Hello **tipo VIP** selezione determina se il tipo di base è possibile accedere direttamente da hello internet (esterno) o se utilizza un bilanciamento del carico interno. toolearn informazioni su queste opzioni, vedere [creare e usare un servizio di bilanciamento del carico interno con un ambiente del servizio App][MakeILBASE]. 

      * Se si seleziona **esterno** per hello **tipo VIP**, è possibile selezionare il numero hello sistema gli indirizzi IP esterno viene creato con per scopi SSL basato su IP. 
    
      * Se si seleziona **interno** per hello **tipo VIP**, è necessario specificare il dominio hello che utilizza il tipo di base. È possibile distribuire un ambiente del servizio app in una rete virtuale che usa gli intervalli di indirizzi pubblici o privati. toouse una rete virtuale con un intervallo di indirizzi pubblico, è necessario toocreate hello rete virtuale anticipatamente. 
    
    * Se si seleziona una rete virtuale di esistente, una nuova subnet viene creata quando viene creato hello ASE. *Non è possibile utilizzare una subnet creata in precedenza nel portale di hello. È possibile creare un ambiente del servizio app con una subnet esistente se si usa un modello di Resource Manager.* toocreate un ASE da un modello, vedere [creare un ambiente del servizio App da un modello][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>Ambiente del servizio app 1 ##

È comunque possibile creare istanze della prima versione di hello di ambiente del servizio App (ASEv1). toostart che elaborano, hello ricerca Marketplace per **ambiente del servizio App v1**. Create ASE hello in hello allo stesso modo che crei ASE autonomo hello. Al termine, l'ambiente del servizio app 1 ha due front-end e due ruoli di lavoro. Con ASEv1, è necessario gestire processi di lavoro e front-end hello. Questi non vengono aggiunti automaticamente quando si creano i piani di servizio app. front-end Hello fungono da endpoint HTTP/HTTPS hello e nell'inviare traffico toohello worker. i lavoratori Hello sono ruoli di hello che ospitano le applicazioni. Dopo aver creato il tipo di base, è possibile modificare quantità hello di front-end e worker. 

vedere toolearn ulteriori informazioni su ASEv1, [toohello introduzione v1 ambiente del servizio App][ASEv1Intro]. Per ulteriori informazioni sulla scalabilità, gestione e monitoraggio ASEv1, vedere [come un ambiente del servizio App tooconfigure][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
