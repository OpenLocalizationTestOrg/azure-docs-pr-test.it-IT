---
title: aaaHow tooConfigure v1 un ambiente del servizio App
description: Configurazione, gestione e monitoraggio di hello v1 ambiente del servizio App
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Configurazione di un ambiente del servizio app v1

> [!NOTE]
> Questo articolo è sull'ambiente del servizio App v1 hello.  È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Panoramica
A livello generale, un ambiente del servizio app di Azure è costituito da vari componenti principali:

* Risorse di calcolo che sono in esecuzione nell'ambiente del servizio App hello servizio ospitato
* Archiviazione
* Un database
* Una rete virtuale di Azure classica (V1) o di Resource Manager (V2) 
* Una subnet con il servizio di ambiente del servizio App ospitata hello in esecuzione

### <a name="compute-resources"></a>Risorse di calcolo
Utilizzare le risorse di calcolo hello per il pool di quattro risorse.  Ogni ambiente del servizio app contiene un set di front-end e tre pool di lavoro possibili. Non è necessario di tutti i pool di lavoro tre - toouse se si desidera, è possibile utilizzare solo uno o due.

gli host di Hello nei pool di risorse hello (front-end e lavoratori) non sono direttamente accessibili tootenants. Impossibile utilizzare toothem tooconnect Remote Desktop Protocol (RDP), modificare il provisioning o agire come un amministratore su di essi.

È possibile impostare la quantità e le dimensioni dei pool di risorse. In un ambiente del servizio app sono disponibili quattro opzioni di dimensioni, denominate da P1 a P4. Per informazioni dettagliate sulle dimensioni e sui relativi prezzi, vedere la sezione "Prezzi" in [Informazioni sul servizio app di Azure](../app-service/app-service-value-prop-what-is.md).
Modifica quantità hello o dimensioni, si tratta di un'operazione di scala.  È possibile eseguire una sola operazione di ridimensionamento alla volta.

**Front-end**: front-end hello sono gli endpoint HTTP/HTTPS hello per le app che vengono mantenuti nel ASE. Non vengono eseguiti i carichi di lavoro in hello front-end.

* Un ambiente del servizio app include inizialmente due P2, sufficienti per carichi di lavoro di sviluppo e test e carichi di lavoro di produzione di basso livello. È consigliabile P3s per tooheavy moderata i carichi di lavoro.
* Per i carichi di lavoro di produzione tooheavy con gravità moderata, si consiglia di disporre di almeno quattro tooensure P3s esistono sufficienti front-end in esecuzione quando si verifica di manutenzione pianificata. Nelle attività di manutenzione pianificata, verrà arrestato un front-end per volta e la capacità complessiva disponibile di front-end risulterà così ridotta.
* Front-end può richiedere tooan ora tooprovision. 
* Per ottimizzare ulteriormente la scala, è necessario monitorare la percentuale di CPU hello, percentuale di memoria e le metriche di richieste attive per il pool di server front-end hello. Se durante l'esecuzione di P3s. le percentuali di CPU o memoria hello sono superiore al 70%, aggiungere ulteriori server front-end. Se il valore di richieste attive hello calcola Media too15, too20 000 000 richieste per ogni front-end, è necessario aggiungere ulteriori server front-end. Hello obiettivo complessivo è tookeep CPU e delle percentuali di memoria inferiore a 70% e di richieste attive Media out toobelow 15.000 richieste al front-end, quando si esegue P3s.  

**Thread di lavoro**: lavoratori hello sono in cui vengono eseguiti effettivamente le app. Quando si aumenta il del servizio App piani, che utilizza i lavoratori in hello associati pool di lavoro.

* Non è possibile aggiungere immediatamente ruoli di lavoro. Che occupino tooan ora tooprovision.
* Hello dimensioni di una risorsa di calcolo per qualsiasi pool richiederà < 1 ora per ogni dominio di aggiornamento. Sono disponibili 20 domini di aggiornamento in un ambiente del servizio app. Se in scala di dimensioni di calcolo hello di un pool di lavoro con le istanze di 10, potrebbero richiedere too10 ore toocomplete.
* Se si modifica la dimensione hello hello delle risorse di calcolo che vengono utilizzati in un pool di lavoro, si verificherà l'avvio a freddo di hello App che sono in esecuzione in tale pool di lavoro.

Hello più rapido toochange hello calcolare la dimensione di risorsa di un pool di lavoro che non è in esecuzione di qualsiasi App consiste nel:

* Scalare verso il basso quantità hello di too2 processi di lavoro.  Scala minima del Hello verso il basso della dimensione nel portale di hello è 2. Può richiedere alcuni minuti toodeallocate le istanze. 
* Selezionare nuove dimensioni di calcolo hello e numero di istanze. A questo punto, occuperà too2 ore toocomplete.

Se le app richiedono una dimensione di risorse di calcolo più grande, si può usufruire di informazioni aggiuntive precedenti hello. Anziché modificare dimensioni hello del pool di lavoro hello che ospita queste App, è possibile popolare un altro pool di lavoro con processi di lavoro di dimensioni desiderato hello e sposta le app su toothat pool.

* Creare istanze aggiuntive di hello di hello necessario calcolare le dimensioni in un altro pool di lavoro. Questa operazione richiederà di tooan ora toocomplete.
* Riassegnare i piani di servizio App che ospitano applicazioni hello che richiedono un pool di lavoro di maggiori dimensioni toohello appena configurato. Si tratta di un'operazione di rapida esecuzione che dovrà essere minore di un minuto toocomplete.  
* Ridurre il pool di lavoro prima hello se non è necessario più di tali istanze inutilizzate. Questa operazione richiede pochi minuti toocomplete.

**La scalabilità automatica**: uno degli strumenti hello che consentono di toomanage il consumo di risorse di calcolo è la scalabilità automatica. che può essere usato per pool di lavoro o front-end. È possibile eseguire operazioni, ad esempio aumentare le istanze di qualsiasi tipo di pool mattino hello e ridurlo sera hello. O forse è possibile aggiungere istanze quando il numero di hello di processi di lavoro che sono disponibili in un pool di lavoro scende sotto una determinata soglia.

È necessario se si desidera che le regole di scalabilità automatica tooset intorno metriche pool risorse di calcolo, mantenere nel tempo hello tenga presente che il provisioning. Per altre informazioni sugli ambienti di servizio App per la scalabilità automatica, vedere [come tooconfigure scalabilità automatica in un ambiente del servizio App][ASEAutoscale].

### <a name="storage"></a>Archiviazione
Ogni ambiente del servizio app è configurato con 500 GB di spazio di archiviazione. Questo spazio viene utilizzato in tutte le app hello in hello ASE. Questo spazio di archiviazione è una parte di hello ASE e attualmente non può essere disattivati toouse lo spazio di archiviazione. Se si apportano modifiche tooyour rete virtuale routing o la sicurezza, è necessario toostill consentire accesso tooAzure archiviazione - o hello ASE non può funzionare.

### <a name="database"></a>Database
database Hello contiene informazioni di hello che definisce l'ambiente hello, nonché informazioni dettagliate di hello sulle applicazioni hello che sono in esecuzione all'interno di esso. Questa è troppo una parte di hello sottoscrizione contenuti di Azure. Non è un elemento che si dispone di un toomanipulate possibilità diretto. Se si apportano modifiche tooyour rete virtuale routing o la sicurezza, è necessario toostill consentire accesso tooSQL Azure - o hello ASE non può funzionare.

### <a name="network"></a>Rete
rete virtuale che viene utilizzato con il ASE Hello può essere uno apportate durante la creazione di hello ASE o eseguito in anticipo. Quando si creano subnet hello durante la creazione di base, viene forzato toobe hello ASE in hello rete virtuale hello stesso gruppo di risorse. Se è necessario il gruppo di risorse hello utilizzato il toobe ASE diverso da quello di una rete virtuale, è necessario toocreate il ASE utilizzando un modello di gestione risorse.

Esistono alcune restrizioni relative alla rete virtuale hello utilizzato per un tipo di base:

* rete virtuale Hello deve essere una rete virtuale regionale.
* È necessaria una subnet con 8 o più indirizzi in cui è distribuito hello ASE toobe.
* Dopo una subnet è toohost usato un ASE, intervallo di indirizzi hello della subnet hello non può essere modificata. Per questo motivo, è consigliabile che la subnet hello contiene almeno 64 indirizzi tooaccommodate crescita futura ASE.
* Può essere presente esclusivamente nella subnet hello ma ASE hello.

A differenza dei servizi ospitato hello contenente ASE hello, hello [rete virtuale] [ virtualnetwork] e subnet sottoposti al controllo utente.  È possibile amministrare la rete virtuale tramite l'interfaccia utente di rete virtuale hello o PowerShell.  Un ambiente del servizio app può essere distribuito in una rete virtuale classica o di Resource Manager.  esperienze di API e portale Hello sono leggermente diverse tra classico e Gestione risorse VNets ma hello esperienza ASE è hello stesso.

rete virtuale che viene utilizzato toohost un ASE Hello è possibile utilizzare entrambi gli indirizzi IP RFC1918 privati o è possibile utilizzare gli indirizzi IP pubblici.  Se si desidera toouse un intervallo IP non è coperto da RFC1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) è necessario toocreate toobe la rete virtuale e subnet utilizzato per la base precedono creazione ASE.

Poiché questa funzionalità è posizionata hello Azure App Service nella rete virtuale, significa che le app che sono ospitate nel ASE possono ora accedere alle risorse vengono resi disponibili tramite ExpressRoute o reti private virtuali (VPN) da sito a sito direttamente. app di Hello nell'ambiente del servizio App non richiedono ulteriori rete funzionalità tooaccess risorse disponibili toohello rete virtuale che ospita l'ambiente del servizio App. Ciò significa che non è necessario toouse integrazione della rete virtuale o le connessioni ibride tooget tooresources in o rete virtuale connessa tooyour. È comunque possibile utilizzare entrambe queste funzionalità se le risorse tooaccess nelle reti che non sono connessi tooyour di rete virtuale.

Ad esempio, è possibile utilizzare toointegrate integrazione della rete virtuale con una rete virtuale nella sottoscrizione, ma non è connesso toohello la rete virtuale che è la base. È possibile utilizzare ancora anche le connessioni ibride tooaccess risorse in altre reti, analoga a quella normalmente.  

Se è la rete virtuale configurata con una VPN ExpressRoute, è necessario tenere conto delle esigenze di routing hello che dispone di un tipo di base. Alcune configurazioni di route definite dall'utente sono incompatibili con un ambiente del servizio app. Per altri dettagli sull'esecuzione di un ambiente del servizio app in una rete virtuale con ExpressRoute, vedere [Esecuzione di un ambiente del servizio app in una rete virtuale con ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Protezione del traffico in ingresso
Esistono due metodi principali toocontrol in ingresso ASE tooyour traffico.  È possibile utilizzare toocontrol Groups(NSGs) di sicurezza di rete quali IP indirizzi possono accedere i ASE come descritto qui [come toocontrol in ingresso il traffico in un ambiente del servizio App](app-service-app-service-environment-control-inbound-traffic.md) ed è anche possibile configurare il ASE con un carico interno Balancer(ILB).  Queste funzionalità possono inoltre essere utilizzate insieme se si desidera accedere toorestrict utilizzando NSGs tooyour ASE di bilanciamento del carico interno.

Quando si crea un ambiente del servizio app, verrà creato un indirizzo VIP nella rete virtuale.  Esistono due tipi di indirizzo VIP: esterno e interno.  Quando si crea un ambiente del servizio app con un indirizzo VIP esterno, le app nell'ambiente saranno accessibili tramite un indirizzo IP instradabile su Internet. Quando si seleziona un indirizzo VIP interno, l'ambiente del servizio app verrà configurato con un servizio di bilanciamento del carico interno e non sarà accessibile direttamente da Internet.  In un ambiente del servizio app con servizio di bilanciamento del carico interno è comunque necessario un indirizzo VIP esterno, ma viene usato solo per l'accesso a scopo di gestione e di manutenzione di Azure.  

Durante la creazione di bilanciamento del carico interno ASE Fornisci sottodominio hello utilizzato da hello ASE di bilanciamento del carico interno e sarà necessario toomanage DNS per il sottodominio hello specificate.  Poiché si imposta il nome di sottodominio hello è inoltre necessario il certificato di hello toomanage utilizzato per l'accesso tramite HTTPS.  Dopo avere ASE creazione che si è richiesto il certificato di hello tooprovide.  lettura toolearn ulteriori informazioni su creazione e l'uso di ASE un bilanciamento del carico interno [con un bilanciamento del carico interno di un ambiente del servizio App][ILBASE]. 

## <a name="portal"></a>di Microsoft Azure
È possibile gestire e monitorare l'ambiente del servizio App con hello dell'interfaccia utente nel portale di Azure hello. Se si dispone di un tipo di base, si è probabilmente toosee hello simbolo di servizio App l'intestazione laterale. Questo simbolo è toorepresent utilizzati gli ambienti del servizio App nel portale di Azure hello:

![Simbolo degli ambienti del servizio app][1]

tooopen hello dell'interfaccia utente che elenca tutti gli ambienti di servizio App, è possibile utilizzare freccia di espansione selezionare hello o di un'icona di hello (">" simbolo) nella parte inferiore di hello della barra laterale di hello tooselect gli ambienti del servizio App. Selezionando una delle ASEs hello elencati, aprire un'interfaccia utente utilizzati toomonitor hello e gestirlo.

![Interfaccia utente per il monitoraggio e la gestione di un ambiente del servizio app][2]

Il primo pannello mostra alcune proprietà dell'ambiente del servizio app e un grafico di metriche per ogni pool di risorse. Alcune proprietà che vengono visualizzati in hello hello **Essentials** blocco sono anche i collegamenti ipertestuali che verranno aperto il pannello hello che è associato. Ad esempio, è possibile selezionare hello **rete virtuale** tooopen nome backup hello dell'interfaccia utente associata con la rete virtuale hello in esecuzione il ASE in. I collegamenti **Piani di servizio app** e **App** consentono di aprire i pannelli contenenti gli elementi corrispondenti inclusi nell'ambiente del servizio app.  

### <a name="monitoring"></a>Monitoraggio
grafici di Hello consentono toosee un'ampia gamma di metriche delle prestazioni in ogni pool di risorse. Per il pool di hello front-end, è possibile monitorare hello utilizzo medio della CPU e memoria. Per il pool di lavoro, è possibile monitorare quantità hello utilizzato e quantità hello è disponibile.

Rendere i piani di servizio App di più l'utilizzo di lavori hello in un pool di lavoro. carico di lavoro Hello non viene distribuita in hello stesso modo come con i server front-end di hello, in modo non forniscono utilizzo della CPU e memoria hello perlopiù in modo hello di informazioni utili. Tootrack più importante è il numero di processi di lavoro che è stato usato e sono disponibili, in particolare se si gestisce questo sistema per altri toouse.  

È inoltre possibile utilizzare le metriche di hello che possono essere registrate in hello grafici tooset di avvisi. Impostazione di avvisi qui works hello stesso come in un' posizione nel servizio App. È possibile impostare un avviso da entrambi hello **avvisi** dell'interfaccia utente o parte di drill-down delle metriche dell'interfaccia utente e selezionando **Aggiungi avviso**.

![Interfaccia utente delle metriche][3]

le metriche di Hello appena descritti sono metriche di ambiente del servizio App hello. Sono inoltre disponibili le metriche disponibili nel livello di piano di servizio App hello. In questo caso, il monitoraggio di CPU e memoria risulta particolarmente utile.

In un ASE, tutti i piani di servizio App hello sono dedicati piani di servizio App. Che significa che hello solo le app che eseguono hello host allocate toothat piano di servizio App sono App hello in tale piano di servizio App. Dettagli toosee nel piano di servizio App, visualizzare il piano di servizio App da uno qualsiasi degli elenchi di hello hello dell'interfaccia utente di base o da **piani di servizio App di esplorare** (che elenca tutti gli elementi).   

### <a name="settings"></a>Impostazioni
Nel pannello hello ASE è un **impostazioni** sezione che contiene diverse funzionalità importanti:

**Impostazioni** > **proprietà**: hello **impostazioni** pannello verrà aperta automaticamente quando verrà distribuito il pannello ASE. Inizio hello è **proprietà**. Esistono un numero di elementi che sono toowhat ridondanti presenti in questa pagina **Essentials**, ma è molto utile **indirizzo IP virtuale**, così come **gli indirizzi IP in uscita**.

![Pannello Impostazioni e Proprietà][4]

**Impostazioni** > **Indirizzi IP**: quando si crea un'app IP SSL (Secure Sockets Layer) nell'ambiente del servizio app, è necessario un indirizzo IP SSL. Il ASE deve tooobtain ordine uno, gli indirizzi IP SSL di sua proprietà che possono essere allocati. Quando viene creato, l'ambiente del servizio app ha un indirizzo IP SSL a tale scopo, ma è possibile aggiungerne altri. È previsto un addebito per gli indirizzi di SSL IP aggiuntivo, come illustrato nel [servizio App prezzi] [ AppServicePricing] (nella sezione hello per le connessioni SSL). prezzo aggiuntive Hello è hello prezzo IP SSL.

**Impostazioni** > **Front-End Pool** / **pool di lavoro**: ognuno di questi pannelli di pool di risorse vengono fornite informazioni toosee possibilità hello solo in tale pool di risorse , inoltre tooproviding controlla la scala toofully tale pool di risorse.  

Pannello di base Hello per ogni pool di risorse fornisce un grafico con le metriche per il pool di risorse. Come con i grafici di hello dal pannello ASE hello, è possibile andare in grafico hello e impostare gli avvisi in base alle esigenze. Impostazione di un avviso dal pannello ASE hello per un pool di risorse specifico hello stessa operazione come farlo dal pool di risorse hello. Dal pool di lavoro hello **impostazioni** pannello sono hello tooall accesso App o i piani di servizio App che sono in esecuzione nel pool di lavoro.

![Interfaccia utente Impostazioni dei pool di lavoro][5]

### <a name="portal-scale-capabilities"></a>Funzionalità di ridimensionamento del portale
Le operazioni di ridimensionamento disponibili sono tre:

* Modifica il numero di hello di indirizzi IP in hello ASE disponibili per l'utilizzo di SSL IP.
* Modifica dimensioni hello hello di risorsa di calcolo utilizzato in un pool di risorse.
* Modifica il numero di hello delle risorse di calcolo che vengono utilizzati in un pool di risorse manualmente o tramite la scalabilità automatica.

Nel portale di hello, sono disponibili tre modi toocontrol il numero di server con il pool di risorse:

* Un'operazione di scala dal pannello ASE principale di hello nella parte superiore di hello. È possibile apportare scala più modifiche di configurazione toohello front-end e i pool di lavoro. Tutte le modifiche verranno applicate in un'unica operazione.
* Un'operazione di scala manuale dal pool di risorse singole hello **scala** pannello sotto **impostazioni**.
* Il ridimensionamento automatico, che devono essere impostate dal pool di risorse singole hello **scala** blade.

operazione di ridimensionamento hello toouse nel Pannello di ASE hello, trascinare quantity di toohello dispositivo di scorrimento di hello desiderato e salvare. Questa interfaccia supporta anche la modifica delle dimensioni di hello.  

![Interfaccia utente Piano][6]

funzionalità toouse hello manuale o scalabilità automatica in un pool di risorse specifiche, andare troppo**impostazioni** > **Front-End Pool** / **pool di lavoro** come appropriati. Aprire quindi pool hello che si desidera toochange. Andare troppo**impostazioni** > **orizzontale** o **impostazioni** > **scalabilità verticale**. Hello **orizzontale** pannello consente toocontrol quantità di istanza. **Scalabilità verticale** consente toocontrol dimensione di risorsa.  

![Interfaccia utente Impostazione Piano][7]

## <a name="fault-tolerance-considerations"></a>Considerazioni sulla tolleranza di errore
È possibile configurare un ambiente del servizio App di toouse delle risorse di calcolo totale too55. Tali 55 delle risorse di calcolo, solo 50 può essere utilizzato toohost i carichi di lavoro. motivo Hello è duplice. Esiste un minimo di 2 risorse di calcolo front-end.  Che lascia l'allocazione di too53 toosupport hello pool di lavoro. In ordine tooprovide la tolleranza d'errore, è necessario disporre di una risorsa di calcolo che viene allocata in base alle regole toohello toohave:

* Ogni pool di lavoro è necessario almeno 1 risorse di calcolo aggiuntive che non sono disponibile toobe assegnato a un carico di lavoro.
* Quando la quantità hello delle risorse di calcolo in un pool di lavoro passa di sopra di un determinato valore, quindi un'altra risorsa di calcolo è obbligatoria per la tolleranza di errore. Non è il caso di hello nel pool di server front-end hello.

All'interno di qualsiasi singolo lavoro, i requisiti di tolleranza di errore hello sono per un determinato valore di X risorse assegnate tooa pool di lavoro:

* Se X è compreso tra 2 e 20, quantità hello utilizzabile delle risorse di calcolo che è possibile utilizzare per i carichi di lavoro è x-1.
* Se X è compresa tra 21 e 40, quantità hello utilizzabile delle risorse di calcolo che è possibile utilizzare per i carichi di lavoro è X-2.
* Se X è compreso tra 41 e 53, quantità hello utilizzabile delle risorse di calcolo che è possibile utilizzare per i carichi di lavoro è X-3.

footprint minimo Hello 2 server front-end e 2 processi di lavoro.  Con hello sopra quindi le istruzioni, ecco alcuni esempi tooclarify:  

* Se si dispone di 30 processi di lavoro in un unico pool, 28 di essi può essere utilizzato toohost i carichi di lavoro.
* Se si dispone di 2 processi di lavoro in un unico pool, 1 può essere utilizzato toohost i carichi di lavoro.
* Se si dispone di 20 thread di lavoro in un unico pool, 19 può essere utilizzato toohost i carichi di lavoro.  
* Se si dispone di 21 lavori in un unico pool, ancora solo 19 possono essere utilizzati toohost i carichi di lavoro.  

aspetto della tolleranza di errore Hello è importante, ma è necessario tookeep la presenti durante la scalabilità di sopra di determinate soglie. Se si desidera tooadd più capacità da 20 istanze, quindi passare too22 o versione successiva perché 21 non aggiungere eventuali ulteriori capacità. Hello che è vero anche passare sopra 40, in numero successivo hello che consente di aggiungere capacità è 42.  

## <a name="deleting-an-app-service-environment"></a>Eliminazione di un ambiente del servizio app
Se si desidera toodelete un ambiente del servizio App, quindi utilizzare semplicemente hello **eliminare** azione nella parte superiore di hello del Pannello di ambiente del servizio App hello. Quando si esegue questa operazione, sarà tooconfirm l'ambiente del servizio App che si vuole toodo questo nome hello tooenter richiesta. Si noti che quando si elimina un ambiente del servizio App, è eliminare tutte hello contenuti all'interno di esso.  

![Interfaccia utente per l'eliminazione di un ambiente del servizio app][9]  

## <a name="getting-started"></a>introduttiva
tooget avviato con gli ambienti del servizio App, vedere [come un ambiente del servizio App toocreate](app-service-web-how-to-create-an-app-service-environment.md).

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
