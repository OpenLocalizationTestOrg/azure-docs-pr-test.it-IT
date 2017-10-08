---
title: servizi di bilanciamento del carico aaaUsing in Azure | Documenti Microsoft
description: 'Questa esercitazione viene illustrato come toocreate uno scenario con hello portfolio di bilanciamento del carico Azure: gestione traffico Gateway applicazione e servizio di bilanciamento del carico.'
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Uso dei servizi di bilanciamento del carico in Azure

## <a name="introduction"></a>Introduzione

Microsoft Azure offre numerosi servizi che consentono di gestire la distribuzione del traffico e il bilanciamento del carico. È possibile utilizzare i servizi singolarmente o combinare i relativi metodi, a seconda delle esigenze, soluzione ottimale di toobuild hello.

In questa esercitazione, è innanzitutto definire un caso d'uso del cliente e visualizzare come è possibile renderla più affidabile e ad alte prestazioni tramite hello seguente portfolio di bilanciamento del carico Azure: gestione traffico Gateway applicazione e servizio di bilanciamento del carico. È quindi possibile fornire istruzioni dettagliate per la creazione di una distribuzione geograficamente ridondanti, distribuisce il traffico tooVMs, che consente di gestiscono diversi tipi di richieste.

A livello concettuale, ognuno di questi servizi svolge un ruolo distinto nella gerarchia di bilanciamento del carico hello.

* **Gestione traffico** offre il bilanciamento del carico DNS globale. Esegue la ricerca in richieste DNS in ingresso e risponde con un endpoint integro, in base alle hello routing cliente hello di criteri selezionato. Le opzioni per i metodi di routing sono le seguenti:
  * Prestazioni routing toosend hello richiedente toohello endpoint più vicino in termini di latenza.
  * Priorità routing toodirect tutti traffico tooan endpoint con altri endpoint come backup.
  * Ponderato round robin routing, che distribuisce il traffico in base hello peso assegnato tooeach endpoint.

  client di Hello si connette direttamente toothat endpoint. Gestione traffico di Azure rileva se un endpoint non è integro e quindi reindirizzamenti hello istanza integro tooanother di client. Fare riferimento troppo[documentazione di Azure Traffic Manager](traffic-manager-overview.md) toolearn ulteriori informazioni sul servizio hello.
* Il **gateway applicazione** offre un servizio di controller per la distribuzione di applicazioni con numerose funzionalità di bilanciamento del carico di livello 7. Consente ai clienti la produttività di toooptimize web farm tramite l'offload di gateway applicazione toohello di terminazione SSL con utilizzo intensivo della CPU. Altre funzionalità di routing di livello 7 includono la distribuzione round-robin del traffico in ingresso, l'affinità di sessione basato su cookie, il routing basato sul percorso URL e hello possibilità toohost più siti Web protetti da un gateway singola applicazione. Il gateway applicazione può essere configurato come gateway con connessione Internet, come gateway solo interno o come una combinazione di queste due opzioni. È completamente gestito in Azure e offre scalabilità e disponibilità elevata, oltre a un set completo di funzionalità di registrazione e diagnostica che ne migliorano la gestibilità.
* **Bilanciamento del carico** è parte integrante dello stack SDN Azure hello, che forniscono prestazioni elevate, bassa latenza livello 4 bilanciamento del carico servizi per i protocolli TCP e UDP di tutte. Gestisce le connessioni in ingresso e in uscita. È possibile configurare gli endpoint con bilanciamento del carico pubblici e interni e definire toomap regole connessioni in entrata le destinazioni di pool di connessioni tooback-end utilizzando HTTP e TCP probe di integrità opzioni toomanage la disponibilità del servizio.

## <a name="scenario"></a>Scenario

In questo scenario di esempio viene usato un semplice sito Web che gestisce due tipi di contenuto: immagini e pagine Web con rendering dinamico. sito Web di Hello devono essere geograficamente ridondanti e deve essere utilizzati per gli utenti da hello più vicino (latenza più bassa) toothem percorso. Hello sviluppatore di applicazioni ha deciso che tutti gli URL che corrispondono a hello modello/immagini / * vengono gestite da un pool dedicato di macchine virtuali che sono diverse da rest hello di web farm di hello.

Inoltre, i pool di macchine Virtuali predefinito hello del contenuto dinamico hello deve database back-end di tooa tootalk che è ospitato in un cluster a disponibilità elevata. intera distribuzione di Hello è viene configurata tramite Gestione risorse di Azure.

L'utilizzo di gestione traffico Gateway applicazione e servizio di bilanciamento del carico consente tooachieve questo sito Web questi obiettivi di progettazione:

* **Ridondanza geografica più**: se si arresta un'area, gestione traffico instrada il traffico facilmente toohello area più vicina senza l'intervento dal proprietario dell'applicazione hello.
* **Una latenza ridotta**: perché Gestione traffico indirizza automaticamente regione più vicina di hello cliente toohello, hello si verifica una latenza più bassa per la richiesta di contenuto di hello pagina Web.
* **La scalabilità indipendente**: perché il carico di lavoro dell'applicazione web hello è separato dal tipo di contenuto, proprietario dell'applicazione hello adattabile hello richiesta i carichi di lavoro indipendenti tra loro. Gateway applicazione assicura che il traffico hello sia indirizzato toohello pool di destra in base hello specificato regole e l'integrità di hello di un'applicazione hello.
* **Bilanciamento del carico interno**: bilanciamento del carico perché è davanti cluster a disponibilità elevata, hello solo endpoint attivi e integro hello, per un database è esposto toohello applicazione. Inoltre, un amministratore di database possibile ottimizzare il carico di lavoro di hello distribuendo attive e passive repliche tra cluster hello indipendente di un'applicazione front-end hello. Servizio di bilanciamento del carico offre un cluster a disponibilità elevata toohello connessioni e assicura che solo i database integro ricevano richieste di connessione.

Hello diagramma seguente mostra hello architettura di questo scenario:

![Diagramma dell'architettura di bilanciamento del carico](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> Questo esempio è solo uno dei numerosi possibili configurazioni di servizi di bilanciamento del carico hello che offre Azure. Gestione traffico Gateway applicazione e servizio di bilanciamento del carico possono essere combinate e toobest corrispondente in base alle esigenze di bilanciamento del carico. Se, ad esempio, l'offload SSL o l'elaborazione di livello 7 non sono necessari, è possibile usare Load Balancer al posto del gateway applicazione.

## <a name="setting-up-hello-load-balancing-stack"></a>Impostazione dello stack di bilanciamento del carico hello

### <a name="step-1-create-a-traffic-manager-profile"></a>Passaggio 1: creare un profilo di Gestione traffico

1. Nel portale di Azure hello, fare clic su **New**e quindi ricerca hello marketplace "Profilo di gestione traffico."
2. In hello **profilo di Traffic Manager creare** pannello, immettere le seguenti informazioni di base hello:

  * **Nome**: assegnare al profilo di Gestione traffico un nome del prefisso DNS.
  * **Metodo di routing**: selezionare hello criteri metodo di routing del traffico. Per ulteriori informazioni sui metodi di hello, vedere [i metodi di routing del traffico su gestione traffico](traffic-manager-routing-methods.md).
  * **Sottoscrizione**: selezionare hello sottoscrizione che contiene il profilo di hello.
  * **Gruppo di risorse**: gruppo di risorse hello Select che contiene il profilo di hello. Può trattarsi di un gruppo di risorse nuovo o esistente.
  * **Percorso del gruppo di risorse**: servizio di gestione traffico è percorso tooa globale e non è associato. Tuttavia, è necessario specificare un'area per il gruppo di hello in cui si trovano hello metadati associati al profilo di gestione traffico hello. Questo percorso non ha alcun impatto sulla disponibilità di runtime hello del profilo di hello.

3. Fare clic su **crea** toogenerate hello profilo di gestione traffico.

  ![Pannello "Crea profilo di Gestione traffico"](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Passaggio 2: Creare hello gateway applicazione

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su **New** > **rete** > **Gateway applicazione**.
2. Immettere le seguenti informazioni di base sul gateway applicazione hello hello:

  * **Nome**: nome hello del gateway applicazione hello.
  * **Dimensioni di SKU**: hello dimensioni del gateway applicazione hello, disponibile come Small, Medium o Large.
  * **Numero di istanza**: hello numero di istanze, un valore da 2 a 10.
  * **Gruppo di risorse**: gruppo di risorse hello che contiene i gateway applicazione hello. Può trattarsi di un gruppo di risorse nuovo o esistente.
  * **Percorso**: area hello per il gateway applicazione hello, che è hello stesso percorso del gruppo di risorse hello. percorso Hello è importante, perché la rete virtuale hello e indirizzo IP pubblico devono trovarsi in hello gateway hello stesso percorso.
3. Fare clic su **OK**.
4. Definire la rete virtuale hello, subnet, IP front-end e configurazioni del listener per il gateway applicazione hello. In questo scenario, è l'indirizzo IP front-end hello **pubblica**, che consente toobe aggiunto come un profilo di gestione traffico di toohello endpoint in un secondo momento.
5. Configurare il listener hello con una delle seguenti opzioni hello:
    * Se si Usa HTTP, non è necessario tooconfigure. Fare clic su **OK**.
    * Se si usa HTTPS sono necessarie operazioni di configurazione aggiuntive. Fare riferimento troppo[creare un gateway applicazione](../application-gateway/application-gateway-create-gateway-portal.md), iniziando dal passaggio 9. Dopo aver completato la configurazione hello, fare clic su **OK**.

#### <a name="configure-url-routing-for-application-gateways"></a>Configurare il routing degli URL per i gateway applicazione

Quando si sceglie un pool back-end, un gateway di applicazione che viene configurato con una regola di percorso ha un modello del percorso dell'URL di richiesta hello nella distribuzione round-robin tooround aggiunta. In questo scenario, si aggiungono toodirect una regola di percorso basato su un qualsiasi URL con "/images/\*" pool di server toohello immagine. Per ulteriori informazioni sulla configurazione di URL di routing basato sul percorso per un gateway di applicazione, fare riferimento troppo[creare una regola basata sul percorso per un gateway applicazione](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagramma di livello Web del gateway applicazione](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. Il gruppo di risorse, passare toohello istanza del gateway applicazione hello creato nella precedente sezione hello.
2. In **impostazioni**selezionare **pool back-end**, quindi selezionare **Aggiungi** tooadd hello macchine virtuali che si desidera tooassociate con pool back-end web a livello di hello.
3. In hello **aggiungere pool back-end** pannello, immettere il nome di hello del pool back-end hello e tutti gli indirizzi IP hello macchine hello che risiedono nel pool di hello. In questo scenario vengono connessi due pool back-end di server di macchine virtuali.

  ![Pannello "Aggiungi pool back-end" del gateway applicazione](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. In **impostazioni** di gateway applicazione hello, selezionare **regole**e quindi fare clic su hello **percorso basato su** tooadd pulsante una regola.

  ![Pulsante "Basata sul percorso", regole del gateway applicazione](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. In hello **Aggiungi regola di percorso basato su** pannello, configurare la regola hello fornendo hello le seguenti informazioni.

   Impostazioni di base:

   + **Nome**: nome descrittivo di hello della regola hello è accessibile nel portale di hello.
   + **Listener**: listener hello utilizzato per la regola di hello.
   + **Predefinito pool back-end**: hello toobe pool back-end utilizzato con la regola predefinita di hello.
   + **Impostazioni HTTP predefinite**: toobe impostazioni hello HTTP utilizzato con la regola predefinita di hello.

   Regole basate sul percorso:

   + **Nome**: nome descrittivo di hello della regola di percorso basato su hello.
   + **Percorsi**: regola di percorso hello utilizzata per inoltrare il traffico.
   + **Pool back-end**: hello toobe pool back-end utilizzato con questa regola.
   + **Le impostazioni HTTP**: toobe impostazioni hello HTTP utilizzato con questa regola.

   > [!IMPORTANT]
   > Percorsi: i percorsi validi devono iniziare con "/". carattere jolly Hello "\*" è consentita solo alla fine di hello. Alcuni esempi validi: /xyz, /xyz\* o /xyz/\*.

   ![Pannello "Aggiungi regola basata sul percorso" del gateway applicazione](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Passaggio 3: Aggiungere endpoint di gestione traffico toohello gateway applicazione

In questo scenario, gestione traffico è gateway tooapplication connesso (come configurato in hello passaggi precedenti) che si trovano in aree diverse. Ora che sono configurati i gateway applicazione hello, hello sarà tooconnect li tooyour profilo di gestione traffico.

1. Aprire il profilo di Gestione traffico. toodo Cerca in tal caso, nel gruppo di risorse o ricerca per nome hello del profilo di Traffic Manager hello da **tutte le risorse**.
2. Nel riquadro sinistro hello selezionare **endpoint**, quindi fare clic su **Aggiungi** tooadd un endpoint.

  ![Pulsante "Aggiungi" per gli endpoint di Gestione traffico](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. In hello **aggiungere endpoint** pannello, creare un endpoint tramite l'immissione di hello le seguenti informazioni:

  * **Tipo**: selezionare il tipo di hello di endpoint tooload bilanciamento. In questo scenario, selezionare **endpoint Azure** perché ci si sono connettendo le istanze di gateway applicazione toohello che sono state configurate in precedenza.
  * **Nome**: immettere il nome di hello dell'endpoint di hello.
  * **Tipo di risorsa di destinazione**: selezionare **indirizzo IP pubblico** e quindi in **risorsa di destinazione**, selezionare hello indirizzo IP pubblico del gateway applicazione hello configurata in precedenza.

   ![Pannello "Aggiungi endpoint" di Gestione traffico](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Ora è possibile verificare l'impostazione accedendovi con hello DNS del profilo di Traffic Manager (in questo esempio: TrafficManagerScenario.trafficmanager.net). È possibile inviare di nuovo le richieste, visualizzata o arrestare le macchine virtuali e i server web che sono stati creati in aree diverse e modificare l'impostazione dei tootest impostazioni profilo Traffic Manager di hello.

### <a name="step-4-create-a-load-balancer"></a>Passaggio 4: creare un servizio di bilanciamento del carico

In questo scenario, bilanciamento del carico distribuisce le connessioni da database toohello a livello web hello all'interno di un cluster a disponibilità elevata.

Se il cluster a disponibilità elevata database utilizza SQL Server AlwaysOn, fare riferimento troppo[configurare uno o più sempre sul listener](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) per istruzioni dettagliate.

Per ulteriori informazioni sulla configurazione di un servizio di bilanciamento del carico interno, vedere [creare un servizio di bilanciamento del carico interno nel portale di Azure hello](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. Nel portale di Azure, nel riquadro di sinistra hello, hello fare clic su **New** > **rete** > **bilanciamento del carico**.
2. In hello **Crea servizio di bilanciamento del carico** pannello, scegliere un nome per il bilanciamento del carico.
3. Set hello **tipo** troppo**interno**e scegliere la rete virtuale appropriata di hello e subnet per tooreside del servizio di bilanciamento carico di hello in.
4. In **Assegnazione indirizzo IP** selezionare **Dinamico** o **Statico**.
5. In **gruppo di risorse**, scegliere il gruppo di risorse hello di bilanciamento del carico hello.
6. In **percorso**, scegliere hello area appropriata per servizio di bilanciamento del carico hello.
7. Fare clic su **crea** toogenerate bilanciamento del carico di hello.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Connettersi a un bilanciamento del carico toohello di livello database back-end

1. Dal gruppo di risorse, trovare il servizio di bilanciamento del carico hello creato nei passaggi precedenti hello.
2. In **impostazioni**, fare clic su **pool back-end**, quindi fare clic su **Aggiungi** tooadd un pool back-end.

  ![Pannello "Aggiungi pool back-end" di Load Balancer](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. In hello **aggiungere pool back-end** pannello, immettere il nome di hello del pool back-end hello.
4. Aggiungere singoli computer o un pool di back-end toohello set di disponibilità.

#### <a name="configure-a-probe"></a>Configurare un probe

1. Nel servizio di bilanciamento del carico, in **impostazioni**selezionare **probe**, quindi fare clic su **Aggiungi** tooadd un probe.

 ![Pannello "Aggiungi probe" di Load Balancer](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. In hello **Aggiungi probe** pannello, immettere nome hello hello probe.
3. Seleziona hello **protocollo** per il probe hello. Per un database, può essere preferibile un probe TCP anziché un probe HTTP. toolearn ulteriori informazioni su probe di bilanciamento del carico, fare riferimento troppo[probe di bilanciamento del carico comprendere](../load-balancer/load-balancer-custom-probe-overview.md).
4. Immettere hello **porta** di toobe il database utilizzato per l'accesso a probe hello.
5. In **intervallo**, specificare la frequenza con cui tooprobe hello dell'applicazione.
6. In **soglia non integra**, specificare il numero di hello di errori di probe continua che deve verificarsi per hello back-end VM toobe considerato non integro.
7. Fare clic su **OK** probe hello toocreate.

#### <a name="configure-hello-load-balancing-rules"></a>Configurare le regole di bilanciamento del carico hello

1. In **impostazioni** del servizio di bilanciamento del carico, selezionare **regole di bilanciamento del carico**, quindi fare clic su **Aggiungi** toocreate una regola.
2. In hello **regola di bilanciamento del carico di Aggiungi** pannello immettere hello **nome** per la regola di bilanciamento del carico hello.
3. Scegliere hello **indirizzo IP di front-end** di hello bilanciamento del carico, **protocollo**, e **porta**.
4. In **porta back-end**, specificare hello porta toobe utilizzati nel pool back-end hello.
5. Seleziona hello **pool back-end** hello e **Probe** che sono stati creati in hello precedenti passaggi tooapply hello regola.
6. In **persistenza della sessione**, scegliere la modalità di hello sessioni toopersist.
7. In **i timeout di inattività**, specificare il numero di hello di minuti prima di un timeout di inattività.
8. Per **Indirizzo IP mobile** selezionare **Disabilitato** o **Abilitato**.
9. Fare clic su **OK** regola hello toocreate.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Passaggio 5: Bilanciamento del carico toohello di livello web le macchine virtuali di connettersi

Ora è stato possibile configurare porte di front-end di hello IP indirizzo e bilanciamento del carico in applicazioni hello che eseguono le macchine virtuali di livello web per tutte le connessioni di database. Questa configurazione è toohello specifiche applicazioni eseguite su queste macchine virtuali. indirizzo IP di destinazione tooconfigure hello e la porta, consultare la documentazione dell'applicazione toohello. indirizzo IP di hello toofind del front-end hello, nel portale di Azure hello andare pool IP front-end toohello hello **impostazioni del servizio di bilanciamento carico** blade.

![Riquadro "Pool di indirizzi IP front-end" di Load Balancer](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Passaggi successivi

* [Gestione traffico di Azure](traffic-manager-overview.md)
* [Panoramica del gateway applicazione](../application-gateway/application-gateway-introduction.md)
* [Panoramica di Azure Load Balancer](../load-balancer/load-balancer-overview.md)
