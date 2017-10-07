---
title: aaaHow tooCreate v1 un ambiente del servizio App
description: Descrizione del flusso di creazione di un ambiente del servizio app (versione 1)
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Come tooCreate v1 un ambiente del servizio App 

> [!NOTE]
> Questo articolo è sull'ambiente del servizio App v1 hello. È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Panoramica
Hello ambiente del servizio App (ASE) è un'opzione di servizio Premium di Azure App Service che offre una funzionalità avanzata di configurazione che non è disponibile in timbri di hello multi-tenant. funzionalità ASE Hello distribuisce sostanzialmente hello Azure App Service nella rete virtuale del cliente. toogain una maggiore conoscenza delle funzionalità di hello disponibili per gli ambienti del servizio App di leggere hello [che cos'è un ambiente del servizio App] [ WhatisASE] documentazione.

### <a name="before-you-create-your-ase"></a>Prima di creare l'ambiente del servizio app
È importante toobe compatibile con significati hello che non è possibile modificare. Dopo la creazione dell'ambiente del servizio app non è possibile modificare questi elementi:

* Percorso
* Sottoscrizione
* Gruppo di risorse
* Rete virtuale usata
* Subnet usata 
* Dimensioni della subnet

Quando il prelievo di una rete virtuale e specificare una subnet, assicurarsi che sia abbastanza grande tooaccomodate crescita futura. 

### <a name="creating-an-app-service-environment-v1"></a>Creazione di un ambiente del servizio app (versione 1)
toocreate v1 un ambiente del servizio App è necessario toosearch hello Azure Marketplace per ***ambiente del servizio App v1***, o in modo nuovo -> Web + Mobile -> ambiente del servizio App. toocreate un ASEv1:

1. Specificare il nome di hello del ASE. nome Hello specificato per hello ASE verrà utilizzato per le app hello create in hello ASE. Se il nome di hello ASE è appsvcenvdemo, il nome di sottodominio hello sarà. *appsvcenvdemo.p.azurewebsites.net*. Se è stata creata un'app denominata *mytestapp*, questa sarà disponibile all'indirizzo *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Non è possibile utilizzare gli spazi vuoti nel nome del ASE hello. Se si utilizzano caratteri maiuscoli nel nome hello, il nome di dominio hello sarà totale versione minuscola di hello di tale nome. Se si usa un servizio di bilanciamento del carico interno, il nome dell'ambiente del servizio app non viene usato nel sottodominio ma viene dichiarato in modo esplicito durante la creazione dell'ambiente.
   
    ![][1]
2. Selezionare la propria sottoscrizione. sottoscrizione Hello utilizzata per la base è anche hello uno che verranno create con tutte le App in tale ASE. Non è possibile posizionare l'ambiente del servizio app in una rete virtuale che si trova in un'altra sottoscrizione
3. Selezionare o specificare un nuovo gruppo di risorse. gruppo di risorse Hello utilizzato per il ASE deve hello uguale a quello utilizzato per la rete virtuale. Se si seleziona una rete virtuale esistente, quindi selezione gruppo di risorse hello per le ASE sarà aggiornata tooreflect che di una rete virtuale.
   
    ![][2]
4. Selezionare la rete virtuale e la località. È possibile scegliere toocreate una nuova rete virtuale o selezionare una rete virtuale esistente. Se si seleziona una nuova rete virtuale, è possibile specificare un nome e una località. Hello nuova rete virtuale avranno hello indirizzo intervallo 192.168.250.0/23 e una subnet denominata **predefinito** definito come 192.168.250.0/24. È anche possibile selezionare semplicemente una rete virtuale classica o di Resource Manager già esistente. selezione del tipo di indirizzo VIP Hello determina se il ASE direttamente accessibili da hello internet (esterno) o se utilizza un servizio di bilanciamento del carico interno (ILB). ulteriori informazioni sulla loro leggere toolearn [con un bilanciamento del carico interno di un ambiente del servizio App][ILBASE]. Se si seleziona un tipo di indirizzo VIP di esterna è possibile selezionare quanti hello sistema gli indirizzi IP esterno viene creato con scopi IPSSL. Se si seleziona interno è necessario il sottodominio hello toospecify che verrà utilizzato il tipo di base. Gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano *gli* intervalli di indirizzi pubblici *o gli* spazi di indirizzi RFC1918, ovvero gli indirizzi privati. In ordine toouse una rete virtuale con un intervallo di indirizzi pubblico, sarà necessario toocreate hello rete virtuale anticipatamente. Quando si seleziona una rete virtuale esistente durante la creazione di ASE sarà necessario toocreate una nuova subnet. **Non è possibile utilizzare una subnet creata in precedenza nel portale di hello. È possibile creare un ambiente del servizio app con una subnet già esistente se si crea l'ambiente del servizio app usando un modello di Resource Manager.** toocreate un ASE da un modello di utilizzare informazioni hello in questo caso, [creazione di un ambiente del servizio App da modello] [ ILBAseTemplate] e in questo caso, [creazione di un ambiente del servizio di bilanciamento del carico interno App da modello] [ASEfromTemplate].

### <a name="details"></a>Dettagli
Un ambiente del servizio app viene creato con due front-end e due ruoli di lavoro. Hello front-end fungono da endpoint HTTP/HTTPS hello e nell'inviare traffico lavoratori toohello che sono ruoli hello che ospitano le applicazioni. È possibile regolare la quantità hello dopo la creazione di ASE e può anche impostare le regole di scalabilità automatica su questi pool di risorse. Per ulteriori informazioni dettagliate sugli ridimensionamento manuale, gestione e monitoraggio di un ambiente del servizio App fare clic qui: [come tooconfigure un ambiente del servizio App][ASEConfig] 

Solo hello uno ASE può esistere nella subnet hello utilizzato da hello ASE. Hello subnet non può essere utilizzata per qualsiasi elemento diverso da hello ASE

### <a name="after-app-service-environment-v1-creation"></a>Dopo la creazione dell'ambiente del servizio app (versione 1)
Dopo la creazione dell'ambiente del servizio app è possibile modificare:

* Quantità di server front-end (minimo: 2)
* Quantità di processi di lavoro (minimo: 2)
* Quantità di indirizzi IP disponibili per IP SSL
* Calcolare le dimensioni delle risorse utilizzate da hello worker o front-end (la dimensione minima di Front-End è P2)

Sono disponibili ulteriori informazioni manuale scalabilità, gestione e monitoraggio di ambienti di servizio App qui: [come tooconfigure un ambiente del servizio App][ASEConfig] 

Per informazioni sulla scalabilità automatica è disponibile una guida qui: [come tooconfigure scalabilità automatica per un ambiente del servizio App][ASEAutoscale]

Esistono dipendenze aggiuntive che non sono disponibili per la personalizzazione, ad esempio database hello e l'archiviazione. Questi sono gestiti da Azure e vengono forniti con il sistema hello. supporta l'archiviazione del sistema Hello too500 GB per hello intero ambiente del servizio App e database hello è regolato da Azure in base alle esigenze scala hello del sistema hello.

## <a name="getting-started"></a>introduttiva
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

tooget avviato con l'ambiente del servizio App v1, vedere [toohello introduzione v1 ambiente del servizio App][WhatisASE]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
