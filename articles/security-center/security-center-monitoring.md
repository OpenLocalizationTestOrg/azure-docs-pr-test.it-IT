---
title: monitoraggio aaaSecurity nel Centro protezione di Azure | Documenti Microsoft
description: "In questo articolo vengono tooget presentato di monitoraggio delle funzionalità in Centro sicurezza di Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure
In questo articolo consente di utilizzare funzionalità di monitoraggio in conformità toomonitor Centro sicurezza di Azure con i criteri di hello.

## <a name="what-is-security-health-monitoring"></a>Che cos'è il monitoraggio dello stato di sicurezza?
È spesso considerato come il controllo e in attesa di un evento toooccur in modo che è possibile rispondere toohello situazione di monitoraggio. Monitoraggio di sicurezza, si riferisce toohaving una strategia proattiva che controlla i sistemi tooidentify risorse che non soddisfano gli standard aziendali o le procedure consigliate.

## <a name="monitoring-security-health"></a>Monitoraggio dello stato di sicurezza
Dopo aver abilitato [criteri di sicurezza](security-center-policies.md) per le risorse di una sottoscrizione, il Centro sicurezza PC analizza le risorse tooidentify potenziali vulnerabilità della sicurezza hello. Le informazioni sulla configurazione di rete sono disponibili immediatamente. Potrebbe richiedere un'ora o ulteriori informazioni sulla configurazione della macchina virtuale, ad esempio la protezione aggiornare lo stato e configurazione del sistema operativo, toobecome disponibile. È possibile visualizzare lo stato di sicurezza hello delle risorse e i problemi in hello **prevenzione** sezione. È inoltre possibile visualizzare un elenco di tali problemi nel hello **indicazioni** riquadro.

Per ulteriori informazioni su come indicazioni tooapply, leggere [implementazione delle indicazioni di sicurezza nel Centro protezione Azure](security-center-recommendations.md).

In hello **prevenzione** sezione, è possibile monitorare lo stato di sicurezza hello delle risorse. Nell'esempio seguente di hello, è possibile visualizzare nel riquadro di ogni risorsa (calcolo, rete, archiviazione & data e dell'applicazione) con numero totale di hello dei problemi identificati.

![Riquadro Integrità sicurezza delle risorse](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Monitorare le risorse di calcolo
Quando fa clic su **calcolo** riquadro, hello **calcolo** pannello visualizzato mostra tre schede:

- **Panoramica**: consigli sul monitoraggio e sulle macchine virtuali.
- **Macchine virtuali**: elenco di tutte le macchine virtuali e il rispettivo stato di sicurezza corrente.
- **Servizi cloud**: elenco di tutti i ruoli Web e di lavoro monitorati dal Centro sicurezza.

![Aggiornamento di sistema mancante per la macchina virtuale](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

In ogni scheda è possibile avere più sezioni e in ogni sezione, è possibile selezionare una singola opzione toosee ulteriori dettagli su hello consigliato passaggi tooaddress questo particolare problema. 

#### <a name="monitoring-recommendations"></a>Monitoraggio delle raccomandazioni
In questa sezione viene illustrato il numero totale di hello delle macchine virtuali che sono stati inizializzati per la raccolta dei dati e il relativo stato corrente. Dopo la raccolta dei dati inizializzata, tutte le macchine virtuali saranno pronti tooreceive criteri di sicurezza Centro sicurezza PC. Quando si fa clic su questa voce, hello **agente della macchina virtuale è mancante o non risponde** apre blade. 

![Aggiornamento di sistema mancante per la macchina virtuale](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Raccomandazioni per le macchine virtuali
Questa sezione include una serie di [raccomandazioni per ogni macchina virtuale](security-center-virtual-machine-recommendations.md) monitorata dal Centro sicurezza di Azure. prima colonna Hello Elenca raccomandazione hello. Hello seconda colonna Mostra numero totale di hello di macchine virtuali che sono interessati da tale indicazione. Hello terza colonna indica la gravità hello del problema hello come illustrato nella seguente schermata hello.

![Raccomandazioni per le macchine virtuali](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Vengono visualizzate solo le macchine virtuali che hanno almeno un endpoint pubblico in hello **rete integrità** pannello in hello **topologia di rete** elenco.
>
>

Ogni raccomandazione è inoltre associata a una serie di azioni che è possibile eseguire dopo aver fatto clic su di essa. Ad esempio, se si fa clic su **privi di aggiornamenti di sistema**, hello **privi di aggiornamenti di sistema** apre blade. Elenca le macchine virtuali hello che mancano le patch e hello gravità dell'aggiornamento mancante hello, come illustrato nell'esempio hello schermata.

![Aggiornamenti di sistema mancanti per le macchine virtuali](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Hello **privi di aggiornamenti di sistema** pannello è illustrata una tabella con hello le seguenti informazioni:

* **MACCHINA virtuale**: nome hello della macchina virtuale hello cui mancano aggiornamenti.
* **Gli aggiornamenti del sistema**: hello numero di aggiornamenti di sistema mancanti.
* **ORA dell'ultima analisi**: tempo hello che Centro sicurezza PC ultima scansione hello di macchina virtuale per gli aggiornamenti.
* **STATO**: hello stato corrente della raccomandazione hello:
  * **Aprire**: indicazione hello non è stata ancora risolta.
  * **In corso**: indicazione hello è attualmente in fase di risorse applicata toothose e senza alcun intervento da parte dell'utente.
  * **Risolto**: indicazione hello già terminata. (Quando è stato risolto il problema di hello, voce hello è visualizzata in grigio).
* **GRAVITÀ**: descrive gravità hello di raccomandazione particolare:
  * **Elevata**: esiste una vulnerabilità associata a una risorsa significativa, ad esempio applicazione, macchina virtuale, gruppo di sicurezza di rete, che richiede attenzione.
  * **Media**: Non critici o altri passaggi sono necessari toocomplete un processo o eliminare una vulnerabilità.
  * **Bassa**: vulnerabilità che è opportuno risolvere, ma non richiede attenzione immediata. (Per impostazione predefinita, non vengono presentati i consigli basse, ma è possibile filtrare indicazioni basse se si desidera tooview li.)

dettagli sulle raccomandazioni hello tooview, fare clic su nome hello della macchina virtuale hello. Un nuovo pannello per tale macchina virtuale viene aperto con elenco hello degli aggiornamenti, come illustrato nella seguente schermata hello.

![Aggiornamenti di sistema mancanti per una macchina virtuale specifica](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Hello qui consigli sulla sicurezza sono hello uguali a quelli presenti hello **indicazioni** blade. Vedere hello [implementazione delle indicazioni di sicurezza nel Centro protezione Azure](security-center-recommendations.md) per ulteriori informazioni su come tooresolve indicazioni. Questa opzione è disponibile, non solo per le macchine virtuali ma anche per tutte le risorse disponibili in hello **integrità delle risorse** riquadro.
>
>

#### <a name="virtual-machines-section"></a>Sezione Macchine virtuali
sezione di macchine virtuali Hello fornisce una panoramica di tutte le macchine virtuali e indicazioni. Ogni colonna rappresenta una serie di suggerimenti, come illustrato nella seguente schermata hello:

![Panoramica di tutte le macchine virtuali e delle raccomandazioni](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

icona Hello che viene visualizzata sotto ogni consente di raccomandazione è tooquickly identificare le macchine virtuali hello che richiedono attenzione e tipo di indicazione hello.

Nell'esempio precedente hello, una macchina virtuale è un'indicazione critica relativi endpoint protection. tooget ulteriori informazioni sulla macchina virtuale hello, selezionarla. Un nuovo pannello visualizzato rappresenta la macchina virtuale, come illustrato nella seguente schermata hello.

![Dettagli della sicurezza delle macchine virtuali](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Questo pannello contiene dettagli relativi alla protezione per la macchina virtuale hello hello. Nella parte inferiore di hello di questo pannello, è possibile visualizzare l'azione e gravità hello ogni problema di hello consigliati.

#### <a name="cloud-services-section"></a>Sezione Servizi cloud
Per i servizi cloud, una raccomandazione viene creata quando viene aggiornata come illustrato nella seguente schermata hello versione del sistema operativo hello:

![Stato di integrità per i servizi cloud](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

In uno scenario in cui è consigliabile (che non è il caso hello per hello esempio precedente), è necessario passaggi hello toofollow nella versione di hello raccomandazione tooupdate hello del sistema operativo. Quando è disponibile un aggiornamento, è necessario avere un avviso (rosso o arancione - dipende gravità hello del problema hello). Quando si fa clic su questo avviso nelle righe hello WebRole1 (che esegue Windows Server con il tooIIS distribuiti automaticamente app web) o WorkerRole1 (che esegue Windows Server con il tooIIS distribuiti automaticamente app web), consente di aprire un nuovo pannello con altre informazioni indicazione, come illustrato nella seguente schermata hello:

![Dettagli del servizio cloud](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

Fare clic su una spiegazione più ricchi di indicazioni, questa indicazione toosee **versione del sistema operativo aggiornamento** in hello **descrizione** colonna. Hello **versione del sistema operativo di aggiornamento (anteprima)** pannello apre con maggiori dettagli.

![Raccomandazioni sui servizi cloud](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Monitorare le reti virtuali
Quando fa clic su **rete** riquadro, hello **rete** pannello apre con maggiori dettagli, come illustrato nella seguente schermata hello:

![Pannello Rete](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Raccomandazioni di rete
Ad esempio hello informazioni sull'integrità di risorse della macchina virtuale, questo pannello fornisce un elenco riepilogativo di problemi nella parte superiore di hello del pannello hello e un elenco di reti monitorate nella parte inferiore di hello.

Hello sezione di riepilogo dello stato di rete sono elencati i problemi di sicurezza potenziali e offre [indicazioni](security-center-network-recommendations.md). I possibili problemi possono includere:

* Firewall di nuova generazione non installato
* Gruppi di sicurezza di rete nelle subnet non abilitati
* Gruppi di sicurezza di rete nelle macchine virtuali non abilitati
* Limitare l'accesso esterno tramite endpoint esterni pubblici
* Endpoint con connessione Internet integri

Quando si fa clic su una raccomandazione, apre un nuovo pannello con ulteriori informazioni sull'indicazione hello come illustrato nell'esempio seguente hello.

![Dettagli per una raccomandazione nel Pannello di rete hello](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

In questo esempio hello **configurare mancante rete gruppi di sicurezza per le subnet** blade dispone di un elenco di subnet e protezione di gruppo di sicurezza di rete di macchine virtuali che non sono presenti. Se si sceglie di hello subnet toowhich desiderato gruppo di sicurezza di rete hello tooapply, verrà visualizzata la finestra di un altro pannello.

In hello **scegliere gruppo di sicurezza di rete** pannello, è possibile selezionare hello più rete gruppo di sicurezza appropriato per la subnet hello, oppure è possibile creare un nuovo gruppo di sicurezza di rete.

#### <a name="internet-facing-endpoints-section"></a>Sezione Endpoint con connessione Internet
In hello **endpoint per Internet** sezione, è possibile visualizzare le macchine virtuali hello è attualmente configurate con un endpoint e lo stato corrente è connessa a Internet.

![Macchine virtuali configurate con stato ed endpoint con connessione Internet](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Questa tabella con nome endpoint hello che rappresenta hello macchina virtuale, hello indirizzo IP, è connessa a Internet e stato corrente di gravità del gruppo di sicurezza di rete hello hello e hello NGFW. tabella di Hello è ordinata in base alla gravità:

* Rosso (in alto): priorità elevata e da risolvere immediatamente
* Arancione: priorità media e da risolvere appena possibile
* Verde (ultimo): stato di integrità

#### <a name="networking-topology-section"></a>Sezione Topologia di rete
Hello **topologia della rete** sezione ha una visualizzazione gerarchica di risorse hello come mostrato nella seguente schermata hello:

![Visualizzazione gerarchica di risorse nella sezione Topologia di rete](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Questa tabella è ordinata (macchine virtuali e subnet) in base alla gravità:

* Rosso (in alto): priorità elevata e da risolvere immediatamente
* Arancione: priorità media e da risolvere appena possibile
* Verde (ultimo): stato di integrità

In questa vista della topologia, dispone di primo livello hello [reti virtuali](../virtual-network/virtual-networks-overview.md), [gateway di rete virtuale](/vpn-gateway/vpn-gateway-site-to-site-create.md), e [reti virtuali (classico)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). terzo livello hello è hello le macchine virtuali che appartengono a subnet toothose secondo livello Hello dispone di subnet. colonna di destra Hello lo stato hello corrente del gruppo di sicurezza di rete hello per le risorse, come illustrato nell'esempio seguente hello:

![Stato del gruppo di sicurezza di rete hello nella sezione della topologia di rete](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

nella parte inferiore della finestra di questo pannello Hello presenti hello indicazioni per la macchina virtuale, che è simile toowhat è descritto in precedenza. È possibile fare clic su una raccomandazione toolearn ulteriori o applicare il controllo di sicurezza necessita hello o configurazione.

### <a name="monitor-storage--data"></a>Monitoraggio di archiviazione e dati

Quando fa clic su **archiviazione & dati** in hello **prevenzione** sezione hello **risorse dati** pannello apre con consigli per l'archiviazione e SQL. Include inoltre [indicazioni](security-center-sql-service-recommendations.md) hello generale stato di integrità del database hello. Per altre informazioni sulla crittografia per l'archiviazione, vedere [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md) (Abilitare la crittografia per l'account di archiviazione di Azure nel Centro sicurezza di Azure).

![Risorse dati](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

In **indicazioni SQL**, è possibile scegliere le raccomandazioni e ottenere ulteriori informazioni sulle ulteriori azioni tooresolve un problema. Hello riportato di seguito espansione hello di hello **rilevamento minacce & di controllo del Database nel database SQL** raccomandazione.

![Informazioni dettagliate su una raccomandazione SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Hello **Attiva controllo & minaccia rilevamento nel database SQL** pannello è hello le seguenti informazioni:

* Elenco di database SQL.
* server Hello in cui si trovano
* Informazioni su se questa impostazione è stata ereditata dal server hello o se è univoco nel database
* stato corrente di Hello
* gravità Hello del problema hello

Quando si fa clic hello database tooaddress questa indicazione, hello **rilevamento controllo & minaccia** pannello viene visualizzato come mostrato nella seguente schermata hello.

![Pannello Controllo e rilevamento minacce](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

controllo tooenable, selezionare **ON** in hello **controllo** opzione.

### <a name="monitor-applications"></a>Monitorare le applicazioni

Se il carico di lavoro di Azure dispone di applicazioni che si trovano [macchine virtuali (create tramite Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) con porte web esposti (porte TCP 80 e 443), il Centro sicurezza PC è possibile monitorare tali tooidentify potenziali problemi di sicurezza e consigliano i passaggi di monitoraggio e aggiornamento. Quando si fa clic su hello **applicazioni** riquadro, hello **applicazioni** pannello viene aperto con una serie di raccomandazioni in hello **indicazioni applicazione** sezione. Dettagli dell'applicazione hello per ogni indirizzo IP virtuali o host viene inoltre illustrato come illustrato nella seguente schermata hello.

![Integrità sicurezza delle applicazioni](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Esattamente come si con hello altri suggerimenti, è possibile fare clic su una raccomandazione toosee ulteriori dettagli sul problema hello e come tooremediate. esempio Hello illustrato nella seguente illustrazione hello è un'applicazione che è stata identificata come un'applicazione web non sicuro. Quando si seleziona un'applicazione hello che non è stata considerata sicura, un altro pannello apre con hello opzione disponibile di seguito:

![Informazioni dettagliate su un'app non sicura](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Questo pannello visualizza un elenco di tutte le raccomandazioni per l'applicazione. Quando si fa clic su hello **aggiunge un firewall applicazione web** raccomandazione, hello **aggiungere una Web Application Firewall** pannello viene aperto con le opzioni per tooinstall è un firewall applicazione web (WAF) da un partner come hello illustrato nella seguente schermata.

![Finestra di dialogo Aggiungi un web application firewall](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Vedere anche
In questo articolo, si è appreso toouse capacità nel Centro protezione di Azure di monitoraggio. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md): informazioni su come le impostazioni di sicurezza tooconfigure nel Centro protezione di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md): informazioni su come avvisi toosecurity toomanage e rispondere.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md): informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md): domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.
