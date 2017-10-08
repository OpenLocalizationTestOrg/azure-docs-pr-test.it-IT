---
title: aaaDocument protezione dei dati personali con strumenti di report di Azure | Documenti Microsoft
description: toouse Azure toohelp reporting services e a tecnologie come proteggere la riservatezza dei dati personali.
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Documentare la protezione dei dati personali con gli strumenti di creazione di report di Azure

Questo articolo viene illustrato come toouse Azure reporting services e le tecnologie toohelp proteggere la privacy dei dati personali.

## <a name="scenario"></a>Scenario

Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico. toohelp queste attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito

la società Hello utilizza Microsoft Azure per l'elaborazione e archiviazione dei dati aziendali. Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale, Include inoltre informazioni sulle risorse umane di tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni. riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.

Rete con i dipendenti aziendali accesso hello da sedi remote e agenzie di viaggio hello aziendali presenti in ogni HelloWorld hanno accesso alle risorse aziendali toosome.

## <a name="problem-statement"></a>Presentazione del problema

società Hello necessario proteggere la privacy hello dei dipendenti e clienti dati personali tramite una strategia di protezione a più livelli che utilizza controlli strict tooimpose funzionalità di sicurezza sull'elaborazione tooand accesso dei dati personali e di gestione di Azure e deve essere toodemonstrate in grado di misure di relativa protezione toointernal e revisori esterni.

## <a name="company-goal"></a>Obiettivo dell'azienda

Come parte della strategia di sicurezza di difesa in profondità, è un tootrack obiettivo aziendale tutta l'elaborazione di tooand accesso dei dati personali e assicurarsi che la documentazione di protezione adeguato sulla privacy per i dati personali siano operative e funzionanti.

## <a name="solutions"></a>Soluzioni

Microsoft Azure fornisce la registrazione di monitoraggio, completa e toohelp strumenti di diagnostica di rilevare e registrare le attività e gli eventi associati con l'accesso e l'elaborazione dati personali, geografico flusso di dati e i dati di accesso di terze parti toopersonal. Poiché la sicurezza dei dati personali nel cloud hello è una responsabilità condivisa, Microsoft fornisce anche i clienti con:

- Informazioni dettagliate sull'elaborazione dei dati dei clienti da parte di Microsoft

- Misure di sicurezza gestite da Microsoft

- Informazioni sull'uso e la destinazione dei dati dei clienti

- Informazioni dettagliate sul processo di revisione della privacy di Microsoft

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) è un servizio Microsoft per la gestione delle identità e delle directory multi-tenant, basato sul cloud. Hello sign-del servizio e funzionalità di creazione di report di controllo di fornire accesso dettagliate e informazioni attività applicazione utilizzo toohelp monitorare e verificare che i dati personali toocustomers' accesso appropriato e dei dipendenti.

Esistono due tipi di report attività:

- Hello [report/log attività di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) in modo dettagliato l'attività o delle attività di sistema

- Hello [report/log attività accessi](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) mostra che ha eseguito ogni attività elencata nel report di verifica hello

Utilizza due hello insieme, è possibile tenere traccia della cronologia di hello di ogni attività eseguita e che ogni utente che ha eseguito. Entrambi i tipi di report sono personalizzabili e possono essere filtrati.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Come si accede a sicurezza e controllo hello log?

Hello registri di controllo e sicurezza è possibile accedere dal portale di Active Directory hello in tre modi diversi: tramite hello **attività** sezione (selezionare **log di controllo** o **accessi**), o da **utenti e gruppi** o **applicazioni aziendali** in **Gestisci** in Active Directory. I report sono inoltre possibile accedere tramite hello Azure Active Directory reporting API. 

1. Nel portale di Azure hello, selezionare **Azure Active Directory.**

2. In hello **attività** selezionare **log di controllo.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.

4.  Selezionare un elemento toosee di hello elenco Visualizza tutte le informazioni disponibili su di esso.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

La creazione di report di Azure Active Directory include anche due tipi di report di sicurezza, **Utenti contrassegnati per il rischio** e **Accessi a rischio**, che consentono di monitorare i rischi potenziali nell'ambiente di Azure.

Per ulteriori informazioni su hello reporting service, vedere [reporting di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Visitare [rapporti sull'attività di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) per maggiori informazioni sui report hello disponibili in Azure Active Directory. Questo sito sono inclusi ulteriori dettagli su come tooaccess e utilizzare [i report di attività di log di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) e [report attività di accesso](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) nel portale di hello. Include anche informazioni relative ai report sulla sicurezza [Utenti contrassegnati per il rischio](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) e [Accessi a rischio](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).

Visitare hello [il controllo di Azure Active Directory di riferimento all'API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) sito per ulteriori informazioni su come tooconnect tooAzure Directory a livello di programmazione di reporting.

### <a name="log-analytics"></a>Log Analytics

[Log Analitica](https://azure.microsoft.com/services/log-analytics/) possibile [raccogliere i dati da Azure monitoraggio](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate con altri dati e fornire un'ulteriore analisi. Monitoraggio di Azure raccoglie e analizza i dati di monitoraggio per l'ambiente di Azure. 

Gli strumenti di analisi in Log Analytics, come le ricerche nei log, le visualizzazioni e le soluzioni, vengono applicati a tutti i dati raccolti per offrire un'analisi centralizzata dell'intero ambiente. Log Analitica possibile aggregare e analizzare i registri eventi di Windows, i log di IIS e i registri di sistema, che consentono di rilevare potenziali violazioni della sicurezza dei dati personali in grado di esporre gli utenti toounauthorized dati personali.

#### <a name="how-do-i-use-log-analytics"></a>Uso di Log Analytics

È possibile accedere Analitica Log tramite il portale OMS hello o hello portale di Azure da qualsiasi web browser. Log Analitica include un recupero tooquickly linguaggio di query e consolida i dati nel repository di hello. È possibile creare e salvare le ricerche Log toodirectly analizzare i dati nel portale di hello.

un'area di lavoro Log Analitica nel portale di Azure hello toocreate hello seguenti:

1. Selezionare **Log Analitica** dall'elenco di hello dei servizi in hello Marketplace.

2. Selezionare **Create,** quindi specificare il nome di hello dell'area di lavoro OMS, selezionare la sottoscrizione, un gruppo di risorse, un percorso e livello di prezzo.

3. Fare clic su **OK** toodisplay un elenco delle aree di lavoro.

4. Selezionare i dettagli di un toosee dell'area di lavoro.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Visitare hello [documentazione Analitica Log](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn ulteriori informazioni sul servizio hello.

Visitare hello [Introduzione a un'area di lavoro Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) esercitazione toocreate un'area di lavoro di valutazione e nozioni di base hello di modalità toouse hello del servizio.

Visitare hello seguenti pagine web per ulteriori informazioni sul funzionamento dei registri tooconnect toouse Log Analitica con hello descritto in precedenza:

[Origini dei dati del registro eventi di Windows in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Log di IIS in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Origini dati Syslog in Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Monitoraggio di Azure/Log attività di Azure 

Attualmente [Monitoraggio di Azure](https://azure.microsoft.com/services/monitor/) offre log e metrica dell'infrastruttura di livello base per la maggior parte dei servizi in Microsoft Azure.
Il monitoraggio consente di toogain approfondite relative alle applicazioni Azure. Monitoraggio di Azure si basa su al estensione di diagnostica di Azure di hello (Windows o Linux) per raccogliere la maggior parte dei registri e le metriche a livello di applicazione. [Log attività Azure Hello](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) è una delle risorse di hello è possibile visualizzare con il monitoraggio di Azure. Tiene traccia di ogni chiamata API e fornisce numerose informazioni sulle attività eseguite in [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
È possibile cercare hello Log attività (precedentemente denominato Operational o i log di controllo) per informazioni sulla risorsa stessa forma visualizzata hello dell'infrastruttura di Azure. 

Sebbene la maggior parte delle informazioni di hello registrate in hello attività log relativo tooperformance e il servizio integrità, è anche le informazioni correlate tooprotection dei dati. Hello registro attività, consentono di determinare hello "cosa, chi e quando" per le operazioni (PUT, POST, DELETE) eseguite su risorse hello nella sottoscrizione di Azure di scrittura.

Ad esempio, fornisce un record quando un amministratore elimina un gruppo di sicurezza di rete, che può compromettere la protezione dei dati personali hello. Le voci del log attività vengono archiviate in Monitoraggio di Azure per 90 giorni.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Utilizzo di dati hello raccolti dal Monitor di Azure

Esistono numerosi modi toouse hello dati di log attività hello e altre risorse di monitoraggio di Azure.

- È possibile trasmettere percorsi tooother hello dei dati nella riga reale.

- È possibile archiviare dati hello per periodi di tempo più lungo rispetto a valori predefiniti di hello, utilizzando un [account di archiviazione Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) e l'impostazione di criteri di conservazione.

- È possibile dati visual hello in grafici e grafici, utilizzando hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), o gli strumenti di visualizzazione di terze parti.

- È possibile eseguire query di dati di hello utilizzando l'API REST di Azure Monitor, i comandi CLI, hello [PowerShell](https://docs.microsoft.com/powershell/) cmdlet, o hello .NET SDK.

Introduzione a monitoraggio di Azure, tooget selezionare **più servizi** in hello portale di Azure.

1. Scorrere verso il basso troppo**monitoraggio** in hello **monitoraggio e la gestione** sezione.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Monitoraggio viene aperto in hello **Log attività** visualizzazione.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

È possibile creare e salvare le query per filtri comuni, quindi pin hello più importanti query tooa dashboard del portale in modo si saprà sempre se si sono verificati gli eventi che soddisfano i criteri specificati.

1. È possibile filtrare una vista hello dal gruppo di risorse, timespan e categoria di eventi.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. È quindi possibile aggiungere dashboard del portale tooa query facendo clic su hello **Pin** pulsante. Ciò consente di creare un'unica fonte di informazioni per i dati operativi nei servizi. nome della query Hello e numero di risultati verrà visualizzati nel dashboard di hello.

È inoltre utilizzare le misurazioni di hello monitoraggio tooview per tutte le risorse di Azure, configurare gli avvisi e le impostazioni di diagnostica e cercare nel registro eventi hello. Per ulteriori informazioni su come toouse hello Azure monitoraggio e il registro attività, vedere [un'introduzione a Azure monitoraggio](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Diagnostica Azure 

funzionalità di diagnostica Hello in Azure abilita la raccolta di dati da origini diverse. registri eventi di Windows Hello, che includono il Registro di sicurezza di hello, possono essere particolarmente utili di rilevamento e la documentazione di protezione dei dati personali. Registro protezione Hello tiene traccia eventi riusciti e non riusciti di accesso, nonché le modifiche alle autorizzazioni, il rilevamento dei modelli che indica di determinati tipi di attacchi, modifiche ai criteri di sicurezza, le modifiche l'appartenenza al gruppo di sicurezza e molto altro ancora.

Ad esempio, 4695 ID evento avvisa si toohello tentato unprotection dei dati protetti controllabili. Questa condizione si riferisce toohello Data Protection API (DPAPI), che consente di tooprotect dati, ad esempio le chiavi private, le credenziali archiviate e altre informazioni riservate.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Come abilitare l'estensione diagnostica hello per le macchine virtuali Windows

È possibile utilizzare l'estensione diagnostica hello tooenable PowerShell per una macchina virtuale di Windows, così come dati del log toocollect. passaggi di Hello per questa operazione variano in quale modello di distribuzione è utilizzare (classica o gestione delle risorse). estensione di diagnostica tooenable hello in una macchina virtuale esistente creata tramite il modello di distribuzione del hello Resource Manager, è possibile utilizzare hello [cmdlet di PowerShell Set-AzureRMVMDiagnosticsExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* hello percorso toohello file che contiene la configurazione di diagnostica hello in XML. Per ulteriori istruzioni sull'abilitazione di diagnostica di Azure in una macchina virtuale, vedere [tooenable PowerShell utilizzare diagnostica Azure in una macchina virtuale che esegue Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello estensione diagnostica di Azure può trasferire account di archiviazione di Azure hello raccolti dati tooan o inviarlo tooservices, ad esempio Application Insights. È quindi possibile utilizzare dati hello per il controllo.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Come archiviare e visualizzare dati di diagnostica

È importante tooremember che dati di diagnostica non vengono archiviati in modo permanente solo se vengono trasferiti toohello archiviazione emulatore o tooAzure archiviazione di Microsoft Azure. toostore e visualizzare dati di diagnostica in archiviazione di Azure, seguire questi passaggi:

1. Specificare un account di archiviazione nel file ServiceConfiguration. cscfg hello. Diagnostica di Azure è possibile utilizzare servizio Blob hello o del servizio tabelle hello, in base al tipo di hello di dati. I registri eventi di Windows vengono archiviati in formato tabella.

2. Trasferimento dati hello. È possibile richiedere i dati di diagnostica hello tootransfer tramite file di configurazione hello. Per SDK 2.4 e quella precedente, è possibile effettuare anche hello richiesta a livello di codice.

3. Visualizzare i dati di hello, utilizzando [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Esplora Server](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) in Visual Studio, o [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) in Management Studio di Azure.

Per ulteriori informazioni su come tooperform di questi passaggi, vedere [archiviare e visualizzare dati di diagnostica in archiviazione di Azure.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Analisi archiviazione di Azure 

Archiviazione Analitica registra informazioni dettagliate sul servizio di archiviazione tooa richieste riuscite e non riuscite. Queste informazioni possono essere utilizzati toomonitor singole richieste, che consentono di documentare toopersonal di accedere ai dati archiviati nel servizio hello. Tuttavia, la registrazione di Analisi archiviazione non è abilitata per impostazione predefinita per l'account di archiviazione. È possibile abilitarlo nel portale di Azure hello.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Come configurare il monitoraggio per un account di archiviazione

per un account di archiviazione di monitoraggio tooconfigure hello seguenti:

1. Selezionare **gli account di archiviazione** in hello portale di Azure, quindi selezionare il nome di hello di account di hello desiderato toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. In hello **monitoraggio** selezionare **diagnostica.**

3.  Seleziona hello **tipo** di dati di metrica desiderato toomonitor per ogni servizio (Blob, tabelle, File). log di diagnostica di toosave tooinstruct di archiviazione di Azure per la lettura, scrittura ed eliminazione delle richieste per hello blob, tabella e i servizi di coda, selezionare **i registri del Blob, tabella di log** e **coda log.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Utilizzando il dispositivo di scorrimento hello nella parte inferiore di hello, impostare hello **conservazione** criteri in giorni (valore di 1 – 365). Sette giorni è l'impostazione predefinita di hello.

5. Selezionare **salvare** tooapply le impostazioni di configurazione hello.

Le voci di log di registrazione archiviazione contengono le seguenti informazioni relative alle singole richieste hello:

- Informazioni sui tempi quali l'ora di inizio, la latenza end-to-end e la latenza del server.

- Dettagli dell'operazione di archiviazione hello, ad esempio il tipo di operazione hello, chiave di hello del client di hello archiviazione oggetto hello è l'accesso, success o failure e codice di stato HTTP hello client toohello restituito.

- Dettagli di autenticazione, ad esempio il tipo di hello del client di hello di autenticazione utilizzato.

- Informazioni sulla concorrenza, ad esempio il valore di ETag hello e l'ultimo timestamp modificato.

- dimensioni Hello dei messaggi di richiesta e risposta hello.

Per ulteriori istruzioni su come tooenable Analitica archiviazione registrazione, vedere [monitorare un account di archiviazione nel portale di Azure hello.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Centro sicurezza di Azure 

[Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/) monitoraggi hello lo stato di protezione delle risorse di Azure in ordine tooprevent e rilevare le minacce e fornire suggerimenti per la risposta. Documento di toohelp diversi modi fornisce le misure di sicurezza per proteggere la privacy hello dei dati personali.

Il monitoraggio dell'integrità della sicurezza consente di garantire la conformità ai criteri di sicurezza. Monitoraggio della protezione è una strategia proattiva che controlla i sistemi tooidentify risorse che non soddisfano gli standard aziendali o le procedure consigliate. È possibile monitorare lo stato di sicurezza hello di hello seguenti risorse:

- Calcolo: macchine virtuali e servizi cloud

- Rete: reti virtuali

- Archiviazione e dati: controllo di server e database, rilevamento delle minacce e Transparent Data Encryption

- Applicazioni: problemi di sicurezza potenziali

Problemi di sicurezza in qualsiasi di queste categorie può comportare l'informativa sulla privacy toohello minaccia dei dati personali.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Come è possibile visualizzare lo stato di sicurezza hello delle risorse Azure?

Centro sicurezza PC analizza periodicamente lo stato di sicurezza hello delle risorse di Azure. È possibile visualizzare le potenziali vulnerabilità di sicurezza che identifica in hello **prevenzione** sezione dashboard hello.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. In hello **prevenzione** sezione, seleziona hello **calcolo** riquadro. Potete vedere un **panoramica,** insieme hello **macchine virtuali** elenco di tutte le macchine virtuali e i relativi stati di sicurezza e hello **servizi Cloud** elenco di ruoli web e di lavoro monitorata tramite il Centro sicurezza PC.

2. In hello **Panoramica** scheda, secondo un tooview raccomandazione ulteriori informazioni.

3. In hello **macchine virtuali** , selezionare una VM tooview i dettagli aggiuntivi.

Quando la raccolta dei dati è abilitata nel Centro protezione di Azure, hello Microsoft Monitoring Agent è automaticamente disponibile in tutte esistenti e supportate nuove macchine virtuali distribuite. I dati raccolti dall'agente vengono archiviati in un'area di lavoro di [Log Analytics](https://azure.microsoft.com/services/log-analytics/) esistente associata alla sottoscrizione o in una nuova area di lavoro.

Il Centro sicurezza di Azure genera [report di intelligence sulle minacce](https://docs.microsoft.com/azure/security-center/security-center-threat-report). Questi contengono informazioni utili toohelp discernere identità dell'utente malintenzionato di hello, obiettivi, correnti e cronologici, campagne e tattiche, strumenti e procedure utilizzate. Includono anche informazioni sulla mitigazione dei rischi e la correzione.

scopo principale di Hello di questi report di minaccia è toohelp si toorespond in modo efficace toohello immediato di minacce e della Guida prende le misure in un secondo momento problema hello toomitigate. le informazioni di Hello nei report hello possono essere utile anche quando documento di risposta per i report e ai fini del controllo.

Hello Threat Intelligence report vengono presentati in. Il formato PDF, accesso tramite un collegamento in hello **report** campo hello **sospetta processo eseguito** pannello per ogni avviso di sicurezza nel Centro protezione di Azure.

Per ulteriori informazioni su come tooview e utilizzare hello Report sullo stato della minaccia, vedere [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Passaggi successivi:

[Introduzione a hello reporting API Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Che cos'è Log Analytics?](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Panoramica del monitoraggio in Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Introduzione toohello Log attività di Azure (video)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
