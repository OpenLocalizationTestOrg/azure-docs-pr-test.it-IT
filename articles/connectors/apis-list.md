---
title: aaaConnectors per le app di logica di Azure | Documenti Microsoft
description: Scegliere tra tutti i toobuild connettori gestita da Microsoft disponibili hello e creare App per la logica
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Elenco dei connettori
> [!TIP]
> Hello [elenco completo A-Z](#az) (in questo argomento) Elenca tutti i connettori disponibili hello è possibile usare in App per la logica. [Dettagli connettore](/connectors/) Elenca tutti i trigger e azioni definite in swagger hello e sono inoltre elencati i limiti per ogni connettore.

I connettori sono una parte essenziale della creazione di app per la logica. Utilizzo di questi connettori, è effettivamente possibile espandere locale e cloud diverse toodo applicazioni con i dati che si creano e si dispone già di dati. i connettori di Hello sono disponibili in hello seguenti categorie: 

* **Connettori standard**: disponibili automaticamente e inclusi quando si usano le app per la logica, ad esempio bus di servizio, DropBox, Power BI, Oracle Database, OneDrive e altro ancora.

* **Connettori dell'account di integrazione**: disponibili quando si acquista un account di integrazione. Usando questi connettori, è possibile trasformare e convalidare il codice XML, elaborare messaggi business-to-business con AS2 / X12 / EDIFACT e codificare e decodificare file flat. Se si lavora con BizTalk Server, questi connettori sono che ideale tooexpand i flussi di lavoro di BizTalk in Azure.  

    BizTalk Server è anche un [scheda logica app](https://msdn.microsoft.com/library/mt787163.aspx) che include la ricezione da un'app di logica e l'invio di tooa logica app.

* **Connettori aziendali**: include MQ e SAP. Disponibili a un costo aggiuntivo. 

[Logica App prezzi](https://azure.microsoft.com/pricing/details/logic-apps/) e [modello prezzi](../logic-apps/logic-apps-pricing.md) forniscono ulteriori dettagli sui costi di hello. 

## <a name="popular-connectors"></a>Connettori più diffusi
Migliaia di applicazioni e milioni di esecuzioni elaborano correttamente dati e informazioni usando questi connettori. Hello nella tabella seguente sono elencati i più diffuso hello e alcuni preferiti con gli utenti:

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Archiviazione BLOB<br/>di Azure**][AzureBlobStoragedoc] | Se si desidera tooautomate tutte le attività con l'account di archiviazione, è necessario controllare a questo connettore. Supporta le operazioni CRUD (Create, Read, Update, Delete). | [![API Icon][Azure-Functionsicon]<br/>**Funzioni di Azure**][azure-functionsdoc] | Creare funzioni che eseguono frammenti di codice C# o node.js personalizzati e quindi usare queste funzioni nelle app per la logica.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Uno dei valori hello frequenti per i connettori. Include azioni e trigger toohelp automatizzare i flussi di lavoro con lead e molto altro. | [![API Icon][Event-Hubs-icon]<br/>**Hub eventi**][event-hubs-doc] | Utilizzare e pubblicare eventi in un hub eventi. Ad esempio, può ottenere l'output dall'app logica tramite hub di eventi e quindi inviare provider tooa analitica in tempo reale di output di hello. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | Se è accessibile dal server FTP hello internet, quindi è possibile automatizzare i flussi di lavoro toowork di file e cartelle. <br/><br/>SFTP è disponibile anche in connettore di hello SFTP. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Utilizzare la logica App toocommunicate con qualsiasi endpoint su HTTP. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Numero elevato di trigger e molte altre posta elettronica di Office 365 toouse azioni e gli eventi nei flussi di lavoro. <br/><br/>Questo connettore include un *posta elettronica di approvazione* note spese, le richieste di azione tooapprove ferie e così via. <br/><br/>Sono disponibili con il connettore di utenti di Office 365 hello anche agli utenti di Office 365.| [![API Icon][HTTP-Requesticon]<br/>**Richiesta/risposta**][HTTP-Requestdoc] | Questo connettore fornisce un URL HTTPS. Quando hello logica app riceve un URL della richiesta toothis, hello logica app viene avviata. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Accedere con facilità con la tooobjects di accesso tooget account Salesforce, ad esempio, i responsabili e altro ancora. |  [![API Icon][Service-Busicon]<br/>**Bus di servizio**][Service-Busdoc] | connettore più diffusi di Hello all'interno di App per la logica, include i trigger e messaggistica asincrona di azioni toodo e pubblicazione/sottoscrizione con argomenti, sottoscrizioni e le code. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Se si lavora con SharePoint e l'automazione potrebbe risultare utile, è consigliabile prendere in considerazione questo connettore. Può essere usato con SharePoint locale e SharePoint Online. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Una delle hello utilizzati più connettori, è possibile connettersi tooan locale SQL Server e Database SQL di Azure. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Accedere con facilità con un account Twitter e quindi avviare un flusso di lavoro quando viene inserito un nuovo tweet. Quindi salvare questi database SQL tooa TWEET o un elenco di SharePoint. | | | 

## <a name="integration-account-connectors"></a>Connettori dell'account di integrazione 

Hello Strumentazione gestione Windows (EIP, Enterprise Integration Pack) include i connettori toohello noto della community di BizTalk Server. Quando si acquista un [account integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), è anche possibile ottenere hello segue connettori: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**Decodifica</br> AS2**][as2decode] | [![API Icon][as2icon]<br/>**Codifica</br> AS2**][as2encode] | [![API Icon][x12icon]<br/>**Decodifica</br> EDIFACT**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**Codifica</br> EDIFACT**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Codifica</br>file flat**][flatfiledoc] | [![API Icon][flatfileicon]<br/>**Decodifica</br>file flat**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Integrazione<br/>account**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**Trasforma<br/>XML**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**Decodifica</br> X12**][x12decode] | [![API Icon][x12icon]<br/>**Codifica</br> X12**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**Convalida <br/>XML**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Connettori aziendali

Connettere le applicazioni enterprise tooyour all'interno di App per la logica.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Elenco completo dalla A alla Z

[Dettagli connettore](/connectors/) elenco trigger e azioni definite in swagger hello e sono inoltre elencati i limiti per ogni connettore.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 Appointment Scheduling<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Gestione API di Azure<br/>Servizi app di Azure<br/>Applicazione di Azure<br/>Automazione di Azure<br/>[Archiviazione BLOB di Azure][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Funzioni di Azure][azure-functionsdoc]<br/>[App per la logica di Azure][nested-logic-appdoc]<br/>AzureML<br/>Code di Azure<br/>Gestione risorse di Azure<br/>[Database SQL di Azure][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Benchmark Email<br/>Ricerca Bing<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>API Visione artificiale di Servizi cognitivi<br/>API Viso di Servizi cognitivi<br/>LUIS di Servizi cognitivi<br/>Analisi del testo di Servizi cognitivi<br/>Common Data Service<br/>Conversione del contenuto<br/>Control-Terminate<br/>[API/app Web personalizzate][api/web-appdoc]<br/><br/><a name="d"></a>Operazioni dati<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Hub eventi][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[File System][filesystemdoc]<br/>[File flat][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>FreshService<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Google Calendar<br/>Google Contacts<br/>Google Drive<br/>Google Sheets<br/>Google Tasks<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[Webhook HTTP][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Account di integrazione<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Media<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Meteo<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Utenti di Office 365<br/>Office 365 Video<br/>OneDrive<br/>OneDrive for Business<br/>OneNote (Business)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook Customer Manager<br/>Attività di Outlook<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Richiesta/Risposta][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[Server applicazioni SAP][sapconnector]<br/>[Server messaggi SAP][sapconnector]<br/>[Pianificare][recurrencedoc]<br/>Scope<br/>SendGrid<br/>Inviare i messaggi toobatch<br/>[Bus di servizio][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Trasformare XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variabili<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[Convalida XML][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget iniziare con le app di logica di Azure prima di iscriversi a un account Azure, andare troppo[provare logica app](https://tryappservice.azure.com/?appservice=logic). È possibile creare immediatamente un'app per la logica di base temporanea. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.

## <a name="connectors-as-triggers-and-actions"></a>Connettori come trigger e azioni

Un **trigger** avvia o esegue un'istanza dell'app per la logica. Alcuni connettori forniscono trigger che possono inviare notifiche all'app quando si verifica un evento specifico. Ad esempio, il connettore hello FTP ha hello `OnUpdatedFile` trigger che avvia l'app logica quando si aggiorna un file. 

Logica App includono i seguenti tipi di trigger hello:  

* *Eseguire il polling trigger*: I trigger di eseguire il polling del servizio in un toocheck frequenza specificata per i nuovi dati. 

    Quando sono disponibili nuovi dati, una nuova istanza dell'app logica viene eseguita con dati hello come input. 

* *Push trigger*: ascolto di questi trigger per i dati in un endpoint o per un evento toohappen, successivamente, viene attivata una nuova istanza della logica app.

* *Trigger di ricorrenza*: questo trigger crea istanze di un'app per la logica in base a una pianificazione predefinita.

I connettori forniscono anche **azioni** che è possibile usare nel flusso di lavoro dell'applicazione. L'app per la logica ad esempio può cercare dati e quindi usarli in seguito nell'app per la logica. In particolare, è possibile cercare i dati dei clienti da un database SQL e quindi utilizzare il flusso di lavoro questo toobuild di dati del cliente. 

> [!TIP]
> Per altri dettagli su trigger e azioni, vedere [Panoramica dei connettori](connectors-overview.md). 


## <a name="message-manipulation-actions"></a>Azioni di modifica dei messaggi

Le app per la logica includono azioni predefinite che consentono di modificare i dati del payload. Hello incorporato **operazioni sui dati** connettore include hello seguenti azioni: 

| | |
|---|---|
| **Componi** | Compilare o generare toouse oggetti o valori in un secondo momento oppure quando si compila il flusso di lavoro. Ad esempio, possibile creare un oggetto JSON con i valori da più passaggi o calcolare una costante tooreference più avanti in un'app di logica di esecuzione. |
| **Crea tabella CSV**<br/>**Crea tabella HTML** | È possibile trasformare un set di risultati di matrice in una tabella CSV o HTML. Ad esempio, aggiungere l'azione di "Record" hello CRM e aggiungere un filtro per i record aggiunti oggi. Quindi, è possibile inviare i risultati di hello come una tabella HTML in un messaggio di posta elettronica. |
| **Filtra matrice** (query) | Filtrare un voci toohello set dei risultati desiderati. Ad esempio, cercare tutti i tweet con `#Azure`, e quindi hello "filtro" restituiti TWEET tooonly restituiscono risultati che sono `Tweeted_by_followers > 50`. |
| **Join** | È possibile unire una matrice mediante un delimitatore. Ad esempio, hello operazione rilevare frasi chiave restituisce una matrice di frasi chiave. È possibile "unirle" con `,` o un approccio simile. Invece di `["Some", "Phrase"]` si ottiene `"Some, Phrase"`. |
| **Analizza JSON** | Analizzare e accedere ai valori da un oggetto JSON nella finestra di progettazione hello. Ad esempio, se la funzione di Azure restituisce un payload JSON, quindi è possibile analizzare la proprietà JSON tooaccess hello in seguito in un altro passaggio. azione di Hello inoltre convalida che hello JSON corrispondenze hello schema specificato in fase di esecuzione. | 
| **Select** | Selezionare alcune proprietà di una matrice per un'elaborazione aggiuntiva. Se si elencano record da SQL e vengono restituite 15 colonne, selezionare solo alcune colonne per un'elaborazione aggiuntiva. output di Hello è una matrice che contiene solo le proprietà di hello selezionate. |

## <a name="custom-connectors-and-azure-certification"></a>Connettori personalizzati e certificazione per Azure 

toocall nelle API che eseguono codice personalizzato o che non sono disponibili come connettori, è possibile estendere piattaforma di App per la logica di hello da [creazione basata su REST App per le API come connettori personalizzati](../logic-apps/logic-apps-create-api-app.md). 

Se si desidera toomake il personalizzato toouse pubblici e disponibile di App per le API di in Azure, quindi inviare il toohello le candidature [programma Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Ottenere aiuto

in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande passare toohello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito di commenti e suggerimenti dell'utente di App per la logica](http://aka.ms/logicapps-wish).

Se manca un argomento sui connettori o qualche dettaglio che si ritiene sia importante, In caso affermativo, quindi Aiutaci aggiungendo argomenti esistenti tooour o scriverne uno proprio. La documentazione è open source e ospitata su GitHub. Introduzione al [repository GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Passaggi successivi
* [Creare la prima app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Creare API personalizzate per app per la logica](../logic-apps/logic-apps-create-api-app.md)
* [Monitorare le app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integrare le app per la logica con le app per le API del servizio app"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Gestire i file in un contenitore BLOB con il connettore di archiviazione BLOB di Azure"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Integrate logic apps with Azure Functions" (Integrazione delle app per la logica con Funzioni di Azure)
[db2doc]: ./connectors-create-api-db2.md "Connettersi tooIBM DB2 in locale o cloud hello. Aggiornare una riga, recuperare una tabella e altro ancora"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Connettono tooDynamics CRM Online in questo modo è possibile utilizzare i dati CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Connettersi tooAzure hub di eventi. Ricevere e inviare eventi tra app per la logica e hub eventi"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "La connessione di sistema di file locale tooan"
[ftpdoc]: ./connectors-create-api-ftp.md "La connessione FTP tooan / server FTPS per attività FTP, come per il caricamento, il recupero, l'eliminazione di file e altro ancora"
[httpdoc]: ./connectors-native-http.md "Effettuare chiamate HTTP con connettore HTTP hello"
[http-requestdoc]: ./connectors-native-reqres.md "Aggiungere azioni per HTTP richieste e risposte tooyour logica App"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Effettuare chiamate HTTP con il connettore HTTP e Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Connettersi tooInformix in locale o cloud hello. Leggere una riga, elencare le tabelle di hello e altro ancora"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Integrare le app per la logica con flussi di lavoro annidati"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Connettere Office 365 tooyour account. Inviare e ricevere messaggi di posta elettronica, gestire il calendario e i contatti e altro ancora"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Connettersi tooan Oracle database tooadd, insert, delete righe e altro ancora"
[mqdoc]: ./connectors-create-api-mq.md "Connettere tooMQ locale o Azure e di inviare e ricevere messaggi"
[recurrencedoc]:  ./connectors-native-recurrence.md "Attivare azioni ricorrenti per le app per la logica"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Connettere l'account di Salesforce tooyour. Gestire account, lead, opportunità e altro ancora"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Connettersi a sistema SAP locale di tooan"
[service-busdoc]: ./connectors-create-api-servicebus.md "Inviare messaggi da code e argomenti del bus di servizio e ricevere messaggi da code e sottoscrizioni del bus di servizio"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Connettersi tooSharePoint Online. Gestire documenti, elementi elenco e altro ancora"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Connettersi tooSharePoint nel server locale. Gestire documenti, elementi elenco e altro ancora"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Connettere tooAzure Database SQL o SQL server. Creare, aggiornare, recuperare ed eliminare voci in una tabella del database SQL"
[twitterdoc]: ./connectors-create-api-twitter.md "Connettersi tooTwitter. Ottenere cronologie, pubblicare tweet e altro ancora"
[webhookdoc]: ./connectors-native-webhook.md "Aggiungere Webhook azioni e trigger tooyour logica App"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Learn about enterprise integration AS2" (Informazioni su Enterprise Integration: AS2)
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Learn about enterprise integration X12" (Informazioni su Enterprise Integration: X12)
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file" (Informazioni su Enterprise Integration: Flat File)
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file" (Informazioni su Enterprise Integration: Flat File)
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Learn about enterprise integration XML validation" (Informazioni su Enterprise Integration: convalida XML)
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about enterprise integration transforms" (Informazioni su Enterprise Integration: trasformazioni)
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Learn about enterprise integration AS2 decode" (Informazioni su Enterprise Integration: decodifica AS2)
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Learn about enterprise integration AS2 encode" (Informazioni su Enterprise Integration: codifica AS2)
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Learn about enterprise integration X12 decode" (Informazioni su Enterprise Integration: decodifica X12)
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Learn about enterprise integration X12 encode" (Informazioni su Enterprise Integration: codifica X12)
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Learn about enterprise integration EDIFACT decode" (Informazioni su Enterprise Integration: decodifica EDIFACT)
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Learn about enterprise integration EDIFACT encode" (Informazioni su Enterprise Integration: codifica EDIFACT)
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Cercare schemi, mappe, partner e altro ancora nell'account di integrazione"


[boxDoc]: ./connectors-create-api-box.md "Connettersi tooBox. Caricare, recuperare, eliminare ed elencare i file e altro ancora"
[delaydoc]: ./connectors-native-delay.md "Eseguire azioni di ritardo"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Connettersi tooDropbox. Caricare, recuperare, eliminare ed elencare i file e altro ancora"
[facebookdoc]: ./connectors-create-api-facebook.md "Connettersi tooFacebook. Dopo la sequenza temporale tooa, ottenere una pagina di avanzamento e altro ancora"
[githubdoc]: ./connectors-create-api-github.md "Connettersi tooGitHub e tenere traccia dei problemi"
[google-drivedoc]: ./connectors-create-api-googledrive.md "È possibile utilizzare i dati si connette tooGoogleDrive"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Connettersi tooGoogle fogli in modo possibile modificare i fogli"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Si connette tooGoogle attività, è possibile gestire le attività"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Si connette tooGoogle calendario e può gestire calendario."
[http-responsedoc]: ./connectors-native-reqres.md "Aggiungere azioni per HTTP richieste e risposte tooyour logica App"
[instagramdoc]: ./connectors-create-api-instagram.md "Connettersi tooInstagram. Attivare eventi o agire su di essi"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Connettere tooyour MailChimp account. Gestire e automatizzare i messaggi di posta elettronica"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Connettersi tooMandrill per la comunicazione"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Connettersi tooMicrosoft convertitore. Tradurre testo, rilevare le lingue e altro ancora" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Ottenere informazioni sui video, canali, elenchi dei video e URL di riproduzione per i video di Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Connettersi tooyour personale Microsoft OneDrive. Caricare, eliminare ed elencare i file e altro ancora"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Connettersi tooyour business Microsoft OneDrive. Caricare, eliminare ed elencare i file e altro ancora"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Connettere tooyour cassetta postale di Outlook. Gestire posta elettronica, calendari, contatti e altro ancora"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Connettersi tooMicrosoft Project Online. Gestire progetti, attività, risorse a altro ancora"
[querydoc]: ./connectors-native-query.md "Selezionare e filtrare le matrici con l'azione di Query hello"
[rssdoc]: ./connectors-create-api-rss.md "Pubblicare e recuperare elementi feed, attivare operazioni quando un nuovo elemento viene pubblicato tooan RSS feed."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Connettersi tooSendGrid. Inviare messaggi di posta elettronica e gestire elenchi di destinatari"
[sftpdoc]: ./connectors-create-api-sftp.md "Connettere tooyour SFTP account. Caricare, recuperare ed eliminare file e altro ancora"
[slackdoc]: ./connectors-create-api-slack.md "Connettersi tooSlack e inviare messaggi tooSlack canali"
[smtpdoc]: ./connectors-create-api-smtp.md "Connessione server SMTP tooa e inviare posta elettronica con allegati"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Si connette tooSparkPost per la comunicazione"
[trellodoc]: ./connectors-create-api-trello.md "Connettersi tooTrello. Gestire i progetti e organizzare qualsiasi cosa con chiunque"
[twiliodoc]: ./connectors-create-api-twilio.md "Connettersi tooTwilio. Inviare e ricevere messaggi, ottenere i numeri disponibili, gestire i numeri di telefono in arrivo e altro ancora"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Connettersi tooWunderlist. Gestire attività ed elenchi di attività, sincronizzare la propria vita e altro ancora"
[yammerdoc]: ./connectors-create-api-yammer.md "Connettersi tooYammer. Pubblicare messaggi, ottenerne di nuovi e altro ancora"
[youtubedoc]: ./connectors-create-api-youtube.md "Connettersi tooYouTube. Gestire video e canali"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
