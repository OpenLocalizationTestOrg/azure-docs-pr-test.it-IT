---
title: versione aaaCanary con Vamp nel cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
description: Come toouse Vamp toocanary servizi di rilascio e applicare smart traffico filtro in un cluster di Azure contenitore del servizio controller di dominio o del sistema operativo
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Microservizi della versione canary con Vamp in un cluster DC/OS del servizio contenitore di Azure

In questa procedura dettagliata viene configurato Vamp nel servizio contenitore di Azure con un cluster DC/OS. Abbiamo canary rilasciare servizio demo di hello Vamp "sava" e quindi risolvere un problema di incompatibilità del servizio hello con Firefox applicando filtri traffico smart. 

> [!TIP] 
> In questa procedura dettagliata Vamp viene eseguito in un cluster di controller di dominio o del sistema operativo, ma è anche possibile utilizzare Vamp con Kubernetes come orchestrator hello.
>

## <a name="about-canary-releases-and-vamp"></a>Informazioni sulle versioni canary e su Vamp


La [versione canary](https://martinfowler.com/bliki/CanaryRelease.html) è una strategia di distribuzione intelligente adottata da organizzazioni innovative come Netflix, Facebook e Spotify. È un buon approccio che consente di ridurre i problemi, introdurre reti di sicurezza e aumentare l'innovazione. Perché quindi non lo usato tutte le società? Estendere un tooinclude pipeline CI/CD strategie Canarie aggiunge complessità e richiede esperienza e le informazioni estese devops. È sufficiente tooblock piccole aziende e le aziende possono preliminari sono anche. 

[Vamp](http://vamp.io/) è tooease un sistema open source progettato questa transizione e portare canary rilascio funzionalità tooyour preferito contenitore dell'utilità di pianificazione. La funzionalità canary di Vamp va oltre le implementazioni basate su percentuale. Possibile filtrare il traffico e diviso in base a un'ampia gamma di condizioni, ad esempio tootarget utenti, gli intervalli IP o dispositivi specifici. Vamp tiene traccia e analizza le metriche delle prestazioni, consentendo l'automazione in base a dati reali. È possibile configurare il ripristino automatico dello stato precedente in caso di errori o aumentare le prestazioni delle varianti dei singoli servizi in base al carico o alla latenza.

## <a name="set-up-azure-container-service-with-dcos"></a>Configurare il servizio contenitore di Azure con DC/OS



1. [Distribuire un cluster DC/OS](container-service-deployment.md) con un master e due agenti di dimensioni predefinite. 

2. [Creare un tunnel SSH](../container-service-connect.md) cluster di tooconnect toohello controller di dominio o del sistema operativo. Questo articolo si presuppone che si tunnel cluster toohello porta locale 80.


## <a name="set-up-vamp"></a>Configurare Vamp

Dopo aver creato un cluster di controller di dominio o del sistema operativo in esecuzione, è possibile installare Vamp da hello controller di dominio o del sistema operativo dell'interfaccia utente (http://localhost:80). 

![Interfaccia utente di DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

L'installazione viene eseguita in due fasi:

1. **Distribuire Elasticsearch**.

2. Quindi **distribuire Vamp** installando pacchetto universo di hello controller di dominio di Vamp del sistema operativo.

### <a name="deploy-elasticsearch"></a>Distribuire Elasticsearch

Per la raccolta delle metriche e l'aggregazione Vamp richiede Elasticsearch. È possibile utilizzare hello [immagini Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy uno stack Vamp Elasticsearch compatibile.

1. Nell'interfaccia utente di controller di dominio/OS hello, andare troppo**servizi** e fare clic su **distribuzione servizio**.

2. Selezionare **modalità JSON** da hello **distribuire nuovo servizio** popup.

  ![Selezione della modalità JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Incollare in hello seguente JSON. Questa configurazione esegue contenitore hello con 1 GB di RAM e di controllo di integrità di base sulla porta Elasticsearch hello.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Fare clic su **Distribuisci**.

  Controller di dominio o sistema operativo distribuisce contenitore Elasticsearch hello. È possibile monitorare lo stato di avanzamento in hello **servizi** pagina.  

  ![distribuzione di Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Distribuire Vamp

Una volta che viene segnalato da Elasticsearch **in esecuzione**, è possibile aggiungere pacchetti di hello Vamp universo dei controller di dominio o del sistema operativo. 

1. Andare troppo**universo** e cercare **vamp**. 
  ![Vamp in Universe (Universo) DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Fare clic su **installare** toohello Avanti vamp pacchetto e scegliere **installazione avanzata**.

3. Scorrere verso il basso e immettere hello elasticsearch url seguente: `http://elasticsearch.marathon.mesos:9200`. 

  ![Immettere l'URL di Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Fare clic su **verifica e installa**, quindi fare clic su **installare** distribuzione hello toostart.  

  DC/OS distribuisce tutti i componenti necessari di Vamp. È possibile monitorare lo stato di avanzamento in hello **servizi** pagina.
  
  ![Distribuire Vamp come pacchetto universo](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Una volta completata la distribuzione, è possibile accedere hello Vamp dell'interfaccia utente:

  ![Servizio Vamp su DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Distribuire il primo servizio

Ora che Vamp è in esecuzione, è possibile distribuire un servizio da un progetto. 

Nella sua forma più semplice, un [Vamp progetto](http://vamp.io/documentation/using-vamp/blueprints/) descrive gli endpoint hello (gateway), i cluster e toodeploy di servizi. Vamp utilizza cluster toogroup diverse varianti di hello stesso servizio in gruppi logici per il rilascio canary o A / B test.  

Questo scenario usa un'applicazione monolitica di esempio denominata [**sava**](https://github.com/magneticio/sava), che è alla versione 1.0. monolito Hello viene compresso in un contenitore Docker, incluso nell'Hub Docker magneticio/sava:1.0.0. applicazione Hello viene normalmente eseguito sulla porta 8080, ma si desidera tooexpose nella porta 9050 in questo caso. Distribuire app hello tramite Vamp utilizzando un progetto semplice.

1. Andare troppo**distribuzioni**.

2. Fare clic su **Aggiungi**.

3. Incolla in seguito hello cianografia YAML. Questo progetto contiene un cluster con solo una variante di servizio, che verrà modificata in un passaggio successivo:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Fare clic su **Salva**. Vamp Avvia distribuzione hello.

distribuzione di Hello viene elencata in hello **distribuzioni** pagina. Fare clic su hello distribuzione toomonitor il relativo stato.

![Interfaccia utente Vamp: distribuzione sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![servizio sava nell'interfaccia utente di Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Vengono creati due gateway, che sono elencati nella hello **gateway** pagina:

* un hello tooaccess stabile endpoint servizio (porta 9050) 
* un gateway interno gestito da Vamp, altre informazioni su questo gateway verranno date in un secondo momento. 

![Interfaccia utente di Vamp: gateway sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

servizio sava Hello è ora distribuito, ma non è possibile accedervi esternamente perché hello bilanciamento del carico di Azure non riconosce tooforward traffico tooit ancora. servizio di hello tooaccess, hello aggiornamento configurazione di rete di Azure.


## <a name="update-hello-azure-network-configuration"></a>Aggiornare la configurazione di rete di Azure hello

Vamp servizio sava hello distribuito nei nodi di agente DC/OS hello, che espone un endpoint porta 9050 stabile. servizio hello tooaccess dal cluster di controller di dominio/OS hello esterno, apportare hello seguente configurazione di rete di Azure toohello modifiche nella distribuzione di cluster: 

1. **Configurare Bilanciamento carico di Azure hello** per gli agenti di hello (hello risorsa denominata **dcos-agente lb xxxx**) con un probe di integrità e il traffico sulla porta 9050 toohello sava a istanze tooforward una regola di. 

2. **Gruppo di sicurezza di rete hello aggiornamento** per gli agenti pubblica hello (hello risorsa denominata **XXXX-agent-public-gruppo-XXXX**) tooallow traffico sulla porta 9050.

Per i passaggi dettagliati toocomplete queste operazioni usando hello Azure portale, vedere [abilitare l'applicazione del servizio di contenitore di Azure tooan accesso pubblico](container-service-enable-public-access.md). Specificare la porta 9050 per tutte le impostazioni della porta.


Una volta tutto ciò che è stato creato, andare toohello **Panoramica** blade di bilanciamento del carico di hello DC/OS agente (hello risorsa denominata **dcos-agente lb xxxx**). Trovare hello **indirizzo IP pubblico**e utilizzare hello indirizzo tooaccess sava porta 9050.

![Portale di Azure: ottenere l'indirizzo IP pubblico](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Eseguire una versione canary

Si supponga di che avere una nuova versione dell'applicazione che si desidera toocanary versione nell'ambiente di produzione. È contenitore come magneticio/sava:1.1.0 e sono pronto toogo. Vamp consente di aggiungere facilmente nuovi toohello servizi in esecuzione la distribuzione. Questi servizi "merge" vengono distribuiti insieme ai servizi esistenti di hello cluster hello e assegnati un peso pari a 0%. Nessun traffico è tooa indirizzato appena unito servizio fino a quando non è regolare la distribuzione del traffico hello. dispositivo di scorrimento peso Hello in hello Vamp UI offre controllo completo sulla distribuzione di hello, consentendo di modifiche incrementali (versione canary) o un rollback immediato.

### <a name="merge-a-new-service-variant"></a>Unire una nuova variante di servizio

toomerge hello nuovo sava 1.1 servizio con hello in esecuzione la distribuzione:

1. In hello Vamp dell'interfaccia utente, fare clic su **disegni**.

2. Fare clic su **Aggiungi** e Incolla in seguito hello cianografia YAML: questo progetto viene descritto un nuovo toodeploy variant (sava: 1.1.0) di servizio all'interno di cluster esistente hello (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Fare clic su **Salva**. progetto iniziale di Hello viene archiviata ed elencato in hello **disegni** pagina.

4. Dal menu azione hello Apri progetto sava: 1.1 hello e fare clic su **di Merge per**.

  ![Interfaccia utente di Vamp: progetti](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Seleziona hello **sava** distribuzione e fare clic su **Merge**.

  ![Vamp dell'interfaccia utente - toodeployment progetto iniziale di tipo merge](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp distribuisce hello nuovo sava: 1.1.0 variante servizio descritto nel progetto hello insieme sava: 1.0.0 in hello **sava_cluster** di hello in esecuzione la distribuzione. 

![Interfaccia utente di Vamp: distribuzione sava aggiornato](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Hello **sava_cluster/sava/webport** gateway (endpoint cluster hello) viene anche aggiornato, aggiunta di una route toohello appena distribuito sava: 1.1.0. A questo punto, nessun traffico viene indirizzato qui (hello **peso** è set % too0).

![Interfaccia utente di Vamp: gateway del cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Versione canary

Entrambe le versioni di sava distribuito in hello stesso cluster, regolare hello distribuzione del traffico tra di essi spostando hello **peso** dispositivo di scorrimento.

1. Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avanti troppo**peso**.

2. Hello peso distribuzione too50%/50% e fare clic su **salvare**.

  ![Interfaccia utente di Vamp: dispositivo di scorrimento del peso del gateway](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Tornare indietro del browser tooyour e aggiornare pagina sava hello alcune altre volte. un'applicazione sava Hello ora si passa dalla pagina sava: 1.0 e una pagina sava: 1.1.

  ![alternanza dei servizi sava1.0 e sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > L'alternanza della pagina hello funziona meglio con hello "Incognito" o "Anonimo" modalità del browser a causa di risorse statiche la memorizzazione nella cache di hello.
  >

### <a name="filter-traffic"></a>Filtrare il traffico

Si supponga che in seguito alla distribuzione sia stato individuato un problema di incompatibilità in sava:1.1.0 che causa problemi di visualizzazione nel browser Firefox. È possibile impostare il traffico in entrata toofilter Vamp e indirizzare che tutti gli utenti di Firefox nuovamente toohello noto sava: 1.0.0 stabile. Questo filtro in modo istantaneo risolve hello interruzioni per gli utenti di Firefox, mentre qualsiasi altro utente continua hello vantaggi hello tooenjoy migliorate sava: 1.1.0.

Usa vamp **condizioni** toofilter il traffico tra le route in un gateway. Il traffico viene innanzitutto filtrato e indirizzati in base toohello condizioni applicate tooeach route. Tutto il traffico rimanente viene distribuito in base a impostazioni del peso toohello gateway.

È possibile creare una condizione toofilter tutti gli utenti di Firefox e invita toohello precedente sava: 1.0.0:

1. In hello sava/sava_cluster/webport **gateway** pagina, fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd un **condizione** toohello route sava/sava_cluster/sava:1.0.0/webport. 

2. Immettere una condizione di hello **agente utente = = Firefox** e fare clic su ![Vamp dell'interfaccia utente - Salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp aggiunge condizione hello con un livello di attendibilità predefinito pari a 0%. toostart filtrando il traffico, è necessario livello di condizione tooadjust hello.

3. Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **forza** toohello condizione applicata.
 
4. Set hello **forza** too100% e fare clic su ![Vamp dell'interfaccia utente - Salva](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp ora invia tutto il traffico corrispondente hello condizione (tutti gli utenti Firefox) toosava:1.0.0.

  ![Vamp dell'interfaccia utente - applicare toogateway condizione](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Infine, regolare hello gateway peso toosend tutti i rimanenti traffico (tutti gli utenti non Firefox) toohello nuova sava: 1.1.0. Fare clic su ![Vamp dell'interfaccia utente - modifica](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Avanti troppo**peso** e impostare distribuzione del peso hello in modo diretto toohello route sava/sava_cluster/sava:1.1.0/webport di è 100%.

  Tutto il traffico non filtrato condizione hello è diretto toohello nuova sava: 1.1.0.

6. filtro hello toosee in azione, aprire due diversi browser (uno Firefox e un altro browser) e accedere hello sava servizio da entrambi. Tutte le richieste di Firefox vengono inviate toosava:1.0.0, mentre tutti gli altri browser sono toosava:1.1.0 diretto.

  ![Interfaccia utente di Vamp: filtrare il traffico](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Riepilogo

Questo articolo è stato tooVamp una rapida introduzione in un cluster di controller di dominio o del sistema operativo. Per iniziare, ottenuto Vamp e in esecuzione in Azure contenitore del servizio controller di dominio o sistema operativo cluster, distribuito un servizio con un progetto iniziale Vamp e vi ha avuto accesso all'endpoint esposto hello (gateway).

È inoltre stata presa in considerazione alcune potenti funzionalità di Vamp: unione di un nuovo toohello variant di servizio in esecuzione la distribuzione e introducendo in modo incrementale, quindi filtrare il traffico tooresolve un'incompatibilità nota.


## <a name="next-steps"></a>Passaggi successivi

* Informazioni sulla gestione delle azioni Vamp tramite hello [Vamp API REST](http://vamp.io/documentation/api/api-reference/).

* Creazione di script di automazione Vamp in Node.js ed esecuzione degli stessi come [flussi di lavoro di Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Vedere altre [esercitazioni su Vamp](http://vamp.io/documentation/tutorials/overview/).

