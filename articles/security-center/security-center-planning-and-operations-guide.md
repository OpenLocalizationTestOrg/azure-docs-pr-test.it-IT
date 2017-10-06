---
title: Center aaaSecurity Guida alla pianificazione e le operazioni | Documenti Microsoft
description: Questo documento consente di tooplan prima di adottare Centro sicurezza di Azure e prendere in considerazione le operazioni quotidiane.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f984e4a2-ac97-40bf-b281-2f7f473494c4
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: b0a0a6f5fd56fbd46f7736928c99e3bcd0b1e140
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-planning-and-operations-guide"></a>Guida alla pianificazione e alla gestione del Centro sicurezza di Azure
Questa guida è per i professionisti IT (IT), architetti IT, gli analisti della sicurezza di informazioni e gli amministratori cloud il cui organizzazioni prevede toouse Centro sicurezza di Azure.

>[!NOTE] 
>A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>

## <a name="planning-guide"></a>Guida alla pianificazione
Questa guida illustra una serie di passaggi e attività che è possibile seguire toooptimize che l'utilizzo del Centro sicurezza basata sul modello di gestione di cloud e i requisiti di sicurezza dell'organizzazione. tootake sfruttare Centro sicurezza PC, è importante toounderstand come i diversi utenti o i team nell'organizzazione Usa sviluppo sicuro toomeet hello e operazioni, monitoraggio, governance e necessita di risposta agli eventi imprevisti. Hello aree principali tooconsider quando si pianifica il Centro sicurezza PC toouse sono:

* Ruoli di sicurezza e controlli di accesso
* Criteri di sicurezza e raccomandazioni
* Raccolta dati e archiviazione
* Monitoraggio continuo della sicurezza
* Risposta agli eventi imprevisti

Nella sezione successiva hello, si apprenderà come tooplan per ognuno di tali aree e applicare le indicazioni in base alle esigenze.

> [!NOTE]
> Lettura [Centro sicurezza di Azure domande frequenti (FAQ)](security-center-faq.md) per un elenco di domande comuni che può essere utile anche durante la progettazione e pianificazione della fase di hello.
> 

## <a name="security-roles-and-access-controls"></a>Ruoli di sicurezza e controlli di accesso
A seconda delle dimensioni di hello e la struttura dell'organizzazione, più utenti e i team possono utilizzare attività Centro sicurezza PC tooperform diverse relative alla sicurezza. Nel seguente diagramma hello sono un esempio di utenti fittizi e i rispettivi ruoli e le responsabilità di sicurezza:

![Ruoli](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig01-new.png)

Centro sicurezza PC consente toomeet queste persone questi ruoli diversi. ad esempio:

**Jeff (proprietario del carico di lavoro cloud)**

* Gestisce un carico di lavoro cloud e le risorse correlate.
* È responsabile delle attività di implementazione e gestione della protezione secondo i criteri di sicurezza aziendale.

**Ellen (CISO/CIO)**

* Responsabile per tutti gli aspetti della sicurezza per società hello
* Richiede di condizioni di sicurezza della società toounderstand hello in carichi di lavoro di cloud
* È necessario toobe informati dei rischi e attacchi principali

**David (sicurezza IT)**

* Set di protezioni di tooensure hello appropriati siano soddisfatti i criteri di sicurezza della società
* Monitora la conformità ai criteri.
* Genera report per la direzione o i revisori.

**Judy (attività di sicurezza)**

* Consente di monitorare e risponde toosecurity avvisi 24/7
* Inoltra tooCloud proprietario del carico di lavoro o un analista di sicurezza IT

**Sam (analista della sicurezza)**

* Analizza gli attacchi
* Lavorare con monitoraggio e aggiornamento tooapply proprietario del carico di lavoro di Cloud 

Centro sicurezza PC utilizza [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md), che fornisce [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) che può essere assegnato toousers, gruppi e i servizi in Azure. Quando un utente apre il Centro sicurezza PC, vedono solo informazioni correlate tooresources hanno accesso. Ovvero utente hello viene assegnato il ruolo di hello proprietario, collaboratore o lettore toohello sottoscrizione o la risorsa del gruppo di una risorsa a cui appartiene. Nei ruoli toothese aggiunta, sono disponibili due ruoli specifici del Centro sicurezza:

- **Lettore di sicurezza**: utente appartenente al ruolo toothis essere in grado di tooview diritti tooSecurity Center, che include consigli, avvisi, criteri e integrità, ma non sarà in grado di toomake modifiche.
- **Amministratore sicurezza**: stesso come lettore sicurezza ma può anche aggiornare i criteri di sicurezza hello, eliminare avvisi e indicazioni.

Centro sicurezza: ruoli Hello descritti in precedenza non dispone di accesso tooother servizio aree di Azure, ad esempio l'archiviazione, Web e dispositivi mobili o Internet delle cose.  

> [!NOTE]
> Un utente deve toobe almeno una sottoscrizione, proprietario del gruppo di risorse o collaboratore toobe in grado di toosee Centro sicurezza PC in Azure. 
> 
> 

Utilizzando gli utenti tipo hello illustrati nel diagramma precedente hello, hello sarebbero necessari in RBAC seguenti:

**Jeff (proprietario del carico di lavoro cloud)**

* Proprietario del gruppo di risorse/Collaboratore.

**David (sicurezza IT)**

* Proprietario della sottoscrizione/Collaboratore o Amministratore della protezione

**Judy (attività di sicurezza)**

* Lettore di sottoscrizione o gli avvisi di sicurezza Reader tooview
* Sottoscrizione proprietario o collaboratore o amministratore responsabile della sicurezza necessari toodismiss avvisi

**Sam (analista della sicurezza)**

* Sottoscrizione lettore tooview avvisi
* Proprietario o collaboratore di sottoscrizione necessario toodismiss avvisi
* Area di lavoro toohello accesso potrebbe essere necessario

Alcuni altri tooconsider informazioni importanti:

* Solto i ruoli Proprietario/Collaboratore della sottoscrizione e Amministratore della protezione possono modificare i criteri di sicurezza.
* Solo i ruoli Proprietario e Collaboratore della sottoscrizione e del gruppo di risorse possono applicare le raccomandazioni relative alla sicurezza per una risorsa.

Quando si pianifica il controllo di accesso tramite RBAC per Centro sicurezza PC, essere toounderstand assicurarsi che all'interno dell'organizzazione dovranno utilizzare il Centro sicurezza PC. Si dovrà sapere anche quali tipi di attività eseguiranno e configurare di conseguenza il Controllo degli accessi in base al ruolo.

> [!NOTE]
> È consigliabile assegnare hello restrittivo ruolo necessari per utenti toocomplete le proprie attività. Ad esempio, gli utenti che devono solo tooview informazioni sullo stato di sicurezza di hello delle risorse ma non eseguire l'azione, ad esempio l'applicazione delle indicazioni o la modifica di criteri, devono assegnati il ruolo di lettore hello.
> 
> 

## <a name="security-policies-and-recommendations"></a>Criteri di sicurezza e raccomandazioni
Un criterio di sicurezza definisce il set di hello dei controlli, sono consigliate per le risorse all'interno di hello specificato sottoscrizione. Centro sicurezza PC, definire i criteri in base della società tooyour requisiti di protezione e riservatezza dei dati hello o il tipo di hello delle applicazioni.

Criteri che sono abilitati automaticamente nel livello di sottoscrizione hello propagano tooall gruppi di risorse all'interno di sottoscrizione hello come illustrato nel seguente diagramma hello:

![Criteri di sicurezza](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig2-newUI.png)

> [!NOTE]
> Se è necessario tooreview quali criteri sono stati modificati, è possibile utilizzare [registri di controllo Azure](https://blogs.msdn.microsoft.com/cloud_solution_architect/2015/03/10/audit-logs-for-azure-events/). Le modifiche ai criteri vengono sempre registrate nei log di controllo di Azure.
> 
> 

### <a name="security-recommendations"></a>Suggerimenti per la sicurezza
Prima di configurare i criteri di sicurezza, controllare ogni hello [consigli sulla sicurezza](security-center-recommendations.md)e determinare se questi criteri sono appropriati per le sottoscrizioni e i gruppi di risorse diversi. È inoltre importante toounderstand l'azione che deve essere eseguita tooaddress [consigli sulla sicurezza](https://docs.microsoft.com/en-us/azure/security-center/security-center-recommendations) e sugli utenti dell'organizzazione sarà responsabili del monitoraggio per nuove indicazioni e acquisire hello necessari passaggi.

Il Centro sicurezza visualizza una raccomandazione perché vengano specificati i dettagli dei contatti di sicurezza per la sottoscrizione di Azure. Queste informazioni verranno utilizzate da Microsoft toocontact se hello Microsoft Security Response Center (MSRC) rileva che i dati sui clienti eseguiti da una parte non autorizzata o illegale. Lettura [fornire dettagli di contatto di sicurezza nel Centro protezione Azure](security-center-provide-security-contact-details.md) per ulteriori informazioni su come tooenable questa raccomandazione.

## <a name="data-collection-and-storage"></a>Raccolta dati e archiviazione
Centro sicurezza di Azure Usa Microsoft Monitoring Agent hello: si tratta di hello stesso agente usato dal servizio di Log Analitica – toocollect i dati di protezione dalle macchine virtuali e di hello Operations Management Suite. I dati raccolti dall'agente verranno archiviati nelle aree di lavoro di Log Analytics.

### <a name="agent"></a>Agente

Dopo aver abilitata la raccolta dei dati nei criteri di sicurezza hello, hello Microsoft Monitoring Agent (per [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) o [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents)) è installato in tutte supportate macchine virtuali di Azure e quelli nuovi creati.  Se hello che VM dispone già di Microsoft Monitoring Agent installato, hello Centro sicurezza di Azure viene impiegata hello corrente installato l'agente. il processo dell'agente di Hello è progettato toobe non è invasivo e attiva impatto minimo sulle prestazioni della macchina virtuale.

Microsoft Monitoring Agent per Windows Hello è necessario utilizzare la porta TCP 443. Vedere hello [articolo Troubleshooting](security-center-troubleshooting-guide.md) per altri dettagli.

Se a un certo punto si desidera toodisable la raccolta dei dati, è possibile disattivare tale funzionalità in Criteri di sicurezza hello. Tuttavia, poiché hello Microsoft Monitoring Agent può essere utilizzato da altri management di Azure e monitoraggio dei servizi, agente hello non verrà disinstallato automaticamente quando si disattiva la raccolta dei dati del Centro sicurezza PC. Se necessario, è possibile disinstallare manualmente l'agente di hello.

> [!NOTE]
> un elenco di macchine virtuali supportate, leggere hello toofind [Centro sicurezza di Azure domande frequenti (FAQ)](security-center-faq.md).
> 

### <a name="workspace"></a>Area di lavoro

Dati raccolti da Microsoft Monitoring Agent (per conto di centro di sicurezza di Azure) verrà archiviato in entrambi un workspace Analitica di Log esistente hello associato alla sottoscrizione di Azure o un nuovo aree di lavoro, tenendo hello account geografica di hello VM. 

In hello portale di Azure, è possibile esplorare toosee un elenco delle aree di lavoro Log Analitica, inclusi quelli creati dal Centro sicurezza di Azure. Per le nuove aree di lavoro verrà creato un gruppo di risorse correlato. Entrambi seguiranno questa convenzione di denominazione: 

* Area di lavoro: *DefaultWorkspace-[subscription-ID]-[geo]*
* Gruppo di risorse: *DefaultResouceGroup-[geo]*

Per le aree di lavoro create dal Centro sicurezza di Azure, i dati vengono conservati per 30 giorni. Per disattivare le aree di lavoro, memorizzazione si basa sull'area di lavoro hello piano tariffario.

> [!NOTE]
> Microsoft rendere sicuro impegni tooprotect hello privacy e protezione dei dati. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio. Per altre informazioni sulla privacy e sulla gestione dei dati, leggere [Sicurezza dei dati nel Centro sicurezza di Azure](security-center-data-security.md).
> 

## <a name="ongoing-security-monitoring"></a>Monitoraggio continuo della sicurezza
Dopo la configurazione iniziale e dell'applicazione delle indicazioni di Centro sicurezza PC, passaggio successivo hello si sta occupando di processi operativi Centro sicurezza PC.

tooaccess Centro sicurezza PC dal portale di Azure è possibile fare clic su hello **Sfoglia** e tipo **Centro sicurezza PC** in hello **filtro** campo. viste Hello che hello utente ottiene sono in base a filtri toothese applicato, esempio hello riportato di seguito viene illustrato un ambiente con molti toobe problemi risolti:

![dashboard](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig6.png)

> [!NOTE]
> Centro sicurezza PC non interferisce con le normali procedure operative, saranno passivamente monitorare le distribuzioni e fornire indicazioni in base ai criteri di sicurezza hello che è abilitata.

Se si sceglie innanzitutto in toouse centro di sicurezza per l'ambiente di Azure corrente, verificare che tutte le indicazioni, che possono essere eseguite in hello **indicazioni** riquadro o per ogni risorsa (**calcolo** **Rete**, **archiviazione & dati**, **applicazione**).

Quando si indirizza tutte le indicazioni, hello **prevenzione** sezione deve essere verde per tutte le risorse che sono stati risolti. Monitoraggio continuo a questo punto diventa più semplice poiché avranno solo in base alle modifiche hello risorse sicurezza integrità e le indicazioni riquadri azioni.

Hello **rilevamento** sezione è più reattiva, questi sono gli avvisi relativi ai problemi che sono entrambi in atto a questo punto, o si è verificato in hello precedente e sono stati rilevati dai controlli di Centro sicurezza PC e i sistemi di terze parti 3rd. riquadro avvisi di sicurezza Hello verrà visualizzati i grafici a barre che rappresentano il numero di hello di avvisi di rilevamento minacce che sono stati trovati in ogni giorno e la relativa distribuzione tra le categorie di gravità diverso hello (basso, medio, alto). Per ulteriori informazioni sugli avvisi di sicurezza, vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> È anche possibile sfruttare toovisualize Microsoft Power BI i dati del Centro sicurezza PC. Vedere [Ottenere informazioni dettagliate sui dati del Centro sicurezza di Azure con Power BI](security-center-powerbi.md).
> 
> 

### <a name="monitoring-for-new-or-changed-resources"></a>Monitoraggio di risorse nuove o modificate
Gli ambienti Azure sono per la maggior parte dinamici, con nuove risorse che vengono attivate e disattivate a intervalli regolari, nuove configurazioni, modifiche e così via. Centro sicurezza PC consente di assicurarsi di avere visibilità dello stato di sicurezza hello di queste nuove risorse.

Quando si aggiungono nuove risorse (macchine virtuali, database SQL) tooyour ambiente Azure, il Centro sicurezza PC automaticamente individuare queste risorse e iniziare toomonitor il livello di protezione. Ciò include anche i ruoli di lavoro e i ruoli Web PaaS. Se la raccolta dei dati è abilitata in hello [criteri di sicurezza](security-center-policies.md), altre funzionalità di monitoraggio verrà abilitata automaticamente per le macchine virtuali.

![Aree principali](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig3-newUI.png)

1. Per le macchine virtuali, fare clic su **Calcolo** nella sezione **Prevenzione**. Problemi relativi all'abilitazione di dati o consigli correlati verranno rilevati in hello **Panoramica** scheda e **monitoraggio indicazioni** sezione.
2. Hello vista **indicazioni** toosee cosa, eventuali rischi di sicurezza sono stati identificati per le nuove risorse hello.
3. È molto comune che, quando l'ambiente tooyour aggiunta di nuove macchine virtuali, viene installato inizialmente solo sistema operativo hello. proprietario della risorsa Hello potrebbe essere necessario alcuni toodeploy ora altre App che verranno utilizzate da queste macchine virtuali.  Idealmente, è necessario sapere con finalità di hello finale di questo carico di lavoro. Stai toobe un Server applicazioni? In base alle quali questo nuovo carico di lavoro è toobe corso, è possibile abilitare hello appropriato **criteri di sicurezza**, ovvero hello terzo passaggio del flusso di lavoro.
4. Con l'aggiungono di nuove risorse tooyour ambiente Azure, è possibile che i nuovi avvisi vengono visualizzati in hello **degli avvisi di sicurezza** riquadro. Verificare se sono presenti nuovi avvisi in questo riquadro e intraprendere azioni in base a indicazioni Center tooSecurity sempre.

È anche possibile tooregularly hello lo stato di monitoraggio delle modifiche di configurazione esistente tooidentify risorse creati rischi di sicurezza, eventuale desincronizzazione da consigliato linee di base e degli avvisi di sicurezza. Inizia dal dashboard di hello Centro sicurezza PC. Da qui è tre aree principali tooreview in modo continuativo.

![Operazioni](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig4-newUI.png)

1. Hello **prevenzione** pannello sezione fornisce risorse chiave di accesso rapido tooyour. Utilizzare questo toomonitor opzione calcolo, rete, archiviazione e le applicazioni e i dati.
2. Hello **indicazioni** pannello consente tooreview indicazioni di centro di sicurezza. Durante il monitoraggio in corso è possibile che non è necessario raccomandazioni su base giornaliera, che può essere normale perché è stato indirizzato tutte le indicazioni durante l'installazione di centro di sicurezza iniziale hello. Per questo motivo, si potrebbe non essere nuove informazioni in questa sezione ogni giorno e sarà sufficiente tooaccess, in base alle esigenze.
3. Hello **rilevamento** sezione potrebbe cambiare in una base molto frequente o molto raramente. Esaminare sempre gli avvisi di sicurezza e intraprendere le azioni necessarie in base alle raccomandazioni del Centro sicurezza.

## <a name="incident-response"></a>Risposta agli eventi imprevisti
Centro sicurezza PC rileva e avvisa l'utente toothreats che si verificano. Le organizzazioni devono verificare la presenza di nuovi avvisi di sicurezza e agire come ulteriormente tooinvestigate necessari o correggere attacco hello. Per altre informazioni sul funzionamento del rilevamento delle minacce nel Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md).

Anche se in questo articolo non deve tooassist preventivo hello si crea il proprio piano di risposta di evento imprevisto, verrà toouse risposta di sicurezza di Microsoft Azure nel ciclo di vita di hello Cloud come foundation hello per le fasi di risposta agli eventi imprevisti. fasi Hello sono illustrate nel seguente diagramma hello:

![Attività sospetta](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-1.png)

> [!NOTE]
> Hello National Institute of Standards and Technology (NIST), è possibile utilizzare [Guida di gestione Computer sicurezza incidente](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf) come tooassist un riferimento per la creazione di propri.
> 

È possibile utilizzare gli avvisi del Centro sicurezza durante hello seguenti fasi:

* **Rilevamento**: identificazione di un'attività sospetta in una o più risorse. 
* **Valutare**: eseguire hello valutazione iniziale tooobtain ulteriori informazioni sulle attività sospette hello.
* **Diagnosticare**: utilizzare hello correzione passaggi tooconduct hello procedure tecniche tooaddress hello problema.

Ogni avviso di sicurezza vengono fornite informazioni che consentono di toobetter comprendere la natura hello di attacco hello e verranno suggerite le soluzioni possibili. Alcuni avvisi forniscono collegamenti tooeither anche altre fonti di informazioni o tooother di informazioni all'interno di Azure. È possibile utilizzare informazioni hello previste ulteriori ricerche e attenuazione toobegin ed è inoltre possibile cercare i dati relativi alla sicurezza che viene archiviati nell'area di lavoro.

Hello esempio seguente mostra un'attività sospetta di RDP in corso:

![Attività sospetta](./media/security-center-planning-and-operations-guide/security-center-planning-and-operations-guide-fig5-ga.png)

Come si può notare, questo pannello mostra i dettagli relativi alla fase di hello che attacco hello ha avuto luogo, hello nome host di origine, destinazione VM hello e inoltre vengono forniti passaggi di raccomandazione. In alcuni hello circostanze informazioni sull'origine dell'attacco hello può essere vuoti. Per altre informazioni su questo tipo di comportamento, vedere [Missing Source Information in Azure Security Center Alerts](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/25/missing-source-information-in-azure-security-center-alerts/) (Informazioni sull'origine mancanti negli avvisi del Centro sicurezza di Azure).

In hello [come tooLeverage hello Centro sicurezza di Azure & Microsoft Operations Management Suite per una risposta a eventi imprevisti](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703) video è possibile visualizzare alcune dimostrazioni che consentono di toounderstand utilizzo in ogni Centro sicurezza una di queste fasi.

> [!NOTE]
> Lettura [Leveraging Centro sicurezza di Azure per l'evento imprevisto risposta](security-center-incident-response.md) per ulteriori informazioni sulla modalità toouse Centro sicurezza PC funzionalità tooassist durante la risposta dell'evento imprevisto di elaborazione. 
> 
> 

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come tooplan per l'adozione di centro di sicurezza. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [La gestione e risponde avvisi toosecurity nel Centro protezione di Azure](security-center-managing-and-responding-alerts.md)
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure.
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.

