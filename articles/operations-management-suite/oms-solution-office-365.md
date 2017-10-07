---
title: soluzione aaaOffice 365 Operations Management Suite (OMS) | Documenti Microsoft
description: In questo articolo vengono fornite informazioni dettagliate sulla configurazione e utilizzo di soluzioni di Office 365 hello in OMS.  Include una descrizione dettagliata del record di hello Office 365 creati nel Log Analitica.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Soluzione Office 365 in Operations Management Suite (OMS)

![Logo di Office 365](media/oms-solution-office-365/icon.png)

soluzioni di Office 365 per Operations Management Suite (OMS) Hello consente toomonitor ambiente Office 365 in Log Analitica.  

- Monitorare le attività utente in schemi di utilizzo tooanalyze account Office 365, nonché identificare le tendenze di comportamento. Ad esempio, è possibile estrarre scenari di utilizzo specifici, ad esempio i file condivisi all'esterno di un'organizzazione o i siti di SharePoint più diffusi hello.
- Monitorare le modifiche di configurazione tootrack le attività di amministratore o le operazioni con privilegi elevati.
- Rilevamento e analisi del comportamento utente indesiderato, che può essere personalizzato per esigenze organizzative.
- Dimostrazione di conformità e controllo. Ad esempio, è possibile monitorare le operazioni di accesso file nel file di informazioni riservate, che consentono il processo di controllo e conformità hello.
- Risoluzione dei problemi operativi usando la ricerca di OMS per i dati di attività di Office 365 dell'organizzazione.

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello è soluzione obbligatorio toothis precedenti viene installato e configurato.

- Sottoscrizione a Office 365 dell'organizzazione.
- Credenziali per un account utente che rappresenta un Amministratore globale.
- dati di controllo tooreceive, è necessario [configurare il controllo](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) nella sottoscrizione di Office 365.  Si noti che [controllo delle cassette postali](https://technet.microsoft.com/library/dn879651.aspx) viene configurato separatamente.  È comunque possibile installare la soluzione hello e raccogliere altri dati se il controllo non è configurato.
 


## <a name="management-packs"></a>Management Pack
Questa soluzione non installa alcun Management Pack nei gruppi di gestione connessi.
  

## <a name="configuration"></a>Configurazione
Dopo aver [Aggiungi sottoscrizione di Office 365 hello soluzione tooyour](../log-analytics/log-analytics-add-solutions.md), si dispone di tooconnect è tooyour abbonamento a Office 365.

1. Aggiungere tooyour soluzione di gestione degli avvisi hello all'area di lavoro OMS tramite il processo di hello [aggiungere soluzioni](../log-analytics/log-analytics-add-solutions.md).
2. Andare troppo**impostazioni** nel portale OMS hello.
3. In **Origini connesse**selezionare **Office 365**.
4. Fare clic su **Connetti Office 365**.<br>![Connetti Office 365](media/oms-solution-office-365/configure.png)
5. Accedi tooOffice 365 con un account che sia un amministratore globale per la sottoscrizione. 
6. sottoscrizione Hello verrà elencati con carichi di lavoro hello soluzione hello eseguirà il monitoraggio.<br>![Connettere Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Raccolta dei dati
### <a name="supported-agents"></a>Agenti supportati
Hello soluzioni di Office 365 non recuperare i dati da qualsiasi hello [gli agenti OMS](../log-analytics/log-analytics-data-sources.md).  Recupera dati direttamente da Office 365.

### <a name="collection-frequency"></a>Frequenza della raccolta
Office 365 invia un [webhook notifica](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) con dati dettagliati tooLog Analitica ogni volta che viene creato un record.

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello
Quando si aggiunge l'area di lavoro OMS tooyour soluzione hello Office 365, hello **Office 365** riquadro verrà aggiunto il dashboard OMS tooyour. Questo riquadro Visualizza un numero e la rappresentazione grafica del numero di hello del computer nel proprio ambiente e la conformità di aggiornamento.<br><br>
![Riquadro di riepilogo di Office 365](media/oms-solution-office-365/tile.png)  

Fare clic su hello **Office 365** riquadro tooopen hello **Office 365** dashboard.

![Dashboard di Office 365](media/oms-solution-office-365/dashboard.png)  

dashboard Hello sono incluse colonne hello hello nella tabella seguente. Ogni colonna sono elencati hello primi dieci avvisi associando conteggio che i criteri della colonna per hello specificato intervallo di ambito e tempo. È possibile eseguire una ricerca di log che fornisce l'intero elenco hello facendo vedere tutte nella parte inferiore di hello della colonna hello o facendo clic sull'intestazione di colonna hello.

| Colonna | Descrizione |
|:--|:--|
| Operazioni | Fornisce informazioni su hello utenti attivi da monitorate tutte le sottoscrizioni Office 365. Sarà anche il numero hello toosee in grado di attività che si verificano nel corso del tempo.
| Exchange | Mostra dettagli hello delle attività di Exchange Server, ad esempio Add-Mailbox autorizzazione o Set-Mailbox. |
| SharePoint | Mostra le attività principali hello che gli utenti di eseguire nei documenti di SharePoint. Quando si visualizzano i dettagli da questo riquadro, pagina di ricerca hello Mostra i dettagli di hello di queste attività, ad esempio il documento di destinazione hello e il percorso di hello di questa attività. Ad esempio, per un evento di accesso al File, sarà documento hello toosee in grado di cui si accede, un nome account associato e un indirizzo IP. |
| Azure Active Directory | Include le attività degli utenti superiori, ad esempio i tentativi di accesso e di reimpostazione password utente. Quando drill-down, sarà dettagli hello toosee in grado di queste attività, ad esempio hello stato del risultato. Questa funzionalità è particolarmente utile se si desidera che le attività sospette toomonitor in Azure Active Directory. |




## <a name="log-analytics-records"></a>Record di Log Analytics

Contiene tutti i record creato nell'area di lavoro Log Analitica hello dalla soluzione Office 365 hello un **tipo** di **OfficeActivity**.  Hello **OfficeWorkload** proprietà determina quali record hello del servizio Office 365 fa riferimento troppo Exchange, AzureActiveDirectory, SharePoint o OneDrive.  Hello **RecordType** proprietà specifica il tipo di hello dell'operazione.  proprietà Hello variano per ogni tipo di operazione e vengono mostrate hello seguito nelle tabelle.

### <a name="common-properties"></a>Proprietà comuni
Hello le proprietà seguenti è comuni record tooall Office 365.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo | *OfficeActivity* |
| ClientIP | indirizzo IP di Hello del dispositivo hello utilizzato durante l'attività hello è stata registrata. indirizzo IP Hello viene visualizzato in formato di indirizzo IPv4 o IPv6. |
| OfficeWorkload | Servizio di Office 365 che si riferisce hello record.<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| Operazione | nome di Hello dell'attività utente o amministratore di hello.  |
| OrganizationId | Hello GUID per il tenant di Office 365 dell'organizzazione. Questo valore sarà sempre essere hello stesso per l'organizzazione, indipendentemente dal servizio di Office 365 hello in cui si verifica. |
| RecordType | Tipo di operazione eseguita. |
| ResultStatus | Indica se l'azione di hello (Buongiorno specificato nella proprietà Operation) è riuscita o meno. I possibili valori sono Succeeded, PartiallySucceded o Failed. Per l'attività di amministrazione di Exchange, il valore di hello è True o False. |
| UserId | Hello UPN (User Principal Name) dell'utente di hello che ha eseguito l'azione di hello che ha generato il record di hello in corso la registrazione; ad esempio, my_name@my_domain_name. Si noti che sono inclusi anche i record per l'attività eseguita dall'account di sistema (ad esempio SHAREPOINT\system o NTAUTHORITY\SYSTEM). | 
| UserKey | Un ID alternativo per l'utente hello individuato hello proprietà UserId.  Ad esempio, questa proprietà viene popolata con l'ID univoco di hello passport (PUID) per gli eventi eseguiti dagli utenti in SharePoint, OneDrive for Business e di Exchange. Questa proprietà può inoltre specificare hello stesso valore di hello proprietà UserID per eventi che si verificano in altri servizi e gli eventi eseguiti dall'account di sistema|
| UserType | tipo di Hello dell'utente che ha eseguito l'operazione di hello.<br><br>Admin<br>Applicazione<br>DcAdmin<br>Regolare <br>Riservato<br>ServicePrincipal<br>Sistema |


### <a name="azure-active-directory-base"></a>Base di Azure Active Directory
Hello le proprietà seguenti è record di Azure Active Directory tooall comuni.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | tipo di Hello di eventi di Azure AD. |
| ExtendedProperties | Hello le proprietà estese degli eventi hello Azure AD. |


### <a name="azure-active-directory-account-logon"></a>Accesso all'account di Azure Active Directory
Questi record vengono creati quando un utente di Active Directory tenta toolog su.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| Applicazione | applicazione Hello che attiva l'evento di accesso account hello, ad esempio Office 15. |
| Client | Dettagli sui client hello dispositivo, sistema operativo del dispositivo e browser del dispositivo che è stato utilizzato per hello dell'evento di accesso account hello. |
| LoginStatus | Questa proprietà deriva direttamente da OrgIdLogon.LoginStatus. mapping di Hello vari interessanti errori di accesso potrebbe essere eseguito da algoritmi di avviso. |
| UserDomain | Hello informazioni di identità Tenant (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Questi record vengono creati quando si modifica o aggiunte modifiche tooAzure oggetti di Active Directory.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | utente Hello è stata eseguita l'azione hello (identificato dalla proprietà operazione hello). |
| Attore | utente Hello o entità servizio che ha eseguito hello azione. |
| ActorContextId | GUID dell'organizzazione hello che hello attore Hello a cui appartiene. |
| ActorIpAddress | Hello indirizzo IP dell'attore in formato di indirizzo IPV4 o IPV6. |
| InterSystemsId | GUID che tengono traccia delle azioni hello tra componenti all'interno del servizio di Office 365 hello Hello. |
| IntraSystemId |   Hello GUID generato da azione hello tootrack di Azure Active Directory. |
| SupportTicketId | cliente Hello supporta ID ticket per l'azione di hello in situazioni "act-on-behalf-of". |
| TargetContextId | Hello GUID dell'organizzazione hello che hello utente di destinazione a cui appartiene. |


### <a name="data-center-security"></a>Sicurezza del centro dati
Questi record vengono creati dai dati di controllo della sicurezza del centro dati.  

| Proprietà | Descrizione |
|:--- |:--- |
| EffectiveOrganization | nome Hello del tenant hello che hello elevazione/cmdlet è destinato. |
| ElevationApprovedTime | timestamp di Hello per quando è stato approvato l'elevazione dei privilegi hello. |
| ElevationApprover | nome Hello di una gestione di Microsoft. |
| ElevationDuration | durata Hello per cui hello elevazione era attivo. |
| ElevationRequestId |  Un identificatore univoco per la richiesta di elevazione hello. |
| ElevationRole | è stata richiesta l'elevazione dei privilegi di Hello ruolo hello. |
| ElevationTime | Hello ora di inizio dell'elevazione di hello. |
| Start_Time | Hello ora di inizio dell'esecuzione dei cmdlet hello. |


### <a name="exchange-admin"></a>Amministratore di Exchange
Questi record vengono creati quando le modifiche vengono apportate tooExchange configurazione.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  Specifica se è stato eseguito il cmdlet hello da un utente nell'organizzazione, dal personale del data center Microsoft o un account di servizio di Data Center o da un amministratore delegato. il valore di Hello False indica che cmdlet hello è stato eseguito da un utente nell'organizzazione. il valore di Hello True indica che cmdlet hello è stato eseguito da Data Center personale, un account del servizio Data Center o un amministratore delegato. |
| ModifiedObjectResolvedName |  Si tratta di hello nome descrittivo dell'oggetto hello che è stato modificato da hello cmdlet. Viene registrata solo se hello cmdlet modifica l'oggetto hello. |
| OrganizationName | nome Hello del tenant hello. |
| OriginatingServer | nome Hello del server di hello dalla quale hello cmdlet è stato eseguito. |
| parameters | nome Hello e il valore per tutti i parametri utilizzati con i cmdlet di hello identificato nella proprietà Operations hello. |


### <a name="exchange-mailbox"></a>Cassetta postale di Exchange
Questi record vengono creati quando le modifiche sono state definite le cassette postali tooExchange.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | Informazioni sul client di posta elettronica hello che è stato utilizzato tooperform hello operazione, ad esempio una versione del browser, Outlook e informazioni sul dispositivo mobile. |
| Client_IPAddress | indirizzo IP di Hello del dispositivo hello utilizzato durante l'operazione di hello è stato registrato. indirizzo IP Hello viene visualizzato in formato di indirizzo IPv4 o IPv6. |
| ClientMachineName | nome del computer Hello che ospita il client di Outlook hello. |
| ClientProcessName | Hello client di posta elettronica è stato cassetta postale hello tooaccess utilizzato. |
| ClientVersion | versione di Hello del client di posta elettronica hello. |
| InternalLogonType | Riservato per uso interno. |
| Logon_Type | Indica il tipo di hello dell'utente che ha accesso cassetta postale hello e operazione hello è stato registrato. |
| LogonUserDisplayName |    nome descrittivo di Hello dell'utente di hello che ha eseguito l'operazione di hello. |
| LogonUserSid | SID dell'utente hello che ha eseguito l'operazione di hello Hello. |
| MailboxGuid | Hello Exchange GUID di cassetta postale hello che ha effettuato l'accesso. |
| MailboxOwnerMasterAccountSid | ID di sicurezza dell'account proprietario della cassetta postale. |
| MailboxOwnerSid | SID del proprietario della cassetta postale hello Hello. |
| MailboxOwnerUPN | indirizzo di posta elettronica Hello di hello proprietario della cassetta postale hello che ha effettuato l'accesso. |


### <a name="exchange-mailbox-audit"></a>Controllo della cassetta postale di Exchange
Questi record vengono creati quando viene creata una voce di controllo delle cassette postali.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| Elemento | Rappresenta l'elemento hello sulle quali hello è stata eseguita l'operazione | 
| SendAsUserMailboxGuid | Hello Exchange GUID di cassetta postale hello che è stato accedere alla posta elettronica toosend come. |
| SendAsUserSmtp | Indirizzo SMTP dell'utente hello che viene rappresentato. |
| SendonBehalfOfUserMailboxGuid | Hello Exchange GUID di cassetta postale hello che è stato accedere alla posta elettronica toosend per conto di. |
| SendOnBehalfOfUserSmtp | Indirizzo SMTP dell'utente hello sul conto hello posta elettronica viene inviato. |


### <a name="exchange-mailbox-audit-group"></a>Gruppo di controllo della cassetta postale di Exchange
Questi record vengono creati quando le modifiche sono state definite gruppi tooExchange.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Informazioni su ogni elemento nel gruppo di hello. |
| CrossMailboxOperations | Indica se l'operazione di hello coinvolto più di una cassetta postale. |
| DestMailboxId | Impostare solo se il parametro CrossMailboxOperations hello è True. Specifica hello destinazione GUID di cassetta postale. |
| DestMailboxOwnerMasterAccountSid | Impostare solo se il parametro CrossMailboxOperations hello è True. Specifica hello SID di account principale hello SID del proprietario della cassetta postale di destinazione hello. |
| DestMailboxOwnerSid | Impostare solo se il parametro CrossMailboxOperations hello è True. Specifica hello SID della cassetta postale di destinazione hello. |
| DestMailboxOwnerUPN | Impostare solo se il parametro CrossMailboxOperations hello è True. Specifica nome UPN del proprietario di hello della cassetta postale di destinazione hello hello. |
| DestFolder | cartella di destinazione Hello, per operazioni quali Move. |
| Cartella | cartella Hello in cui si trova un gruppo di elementi. |
| Cartelle |     Informazioni sulle cartelle del codice sorgente hello coinvolte in un'operazione; ad esempio, se le cartelle vengono selezionate e quindi eliminate. |


### <a name="sharepoint-base"></a>Base SharePoint
Queste proprietà sono comuni tooall SharePoint record.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Identifica un evento che si è verificato in SharePoint. I valori possibili sono ObjectModel o SharePoint. |
| ItemType | tipo di Hello dell'oggetto accessibile o modificata. Vedere tabella ItemType hello per informazioni dettagliate sui tipi di hello di oggetti. |
| MachineDomainInfo | Informazioni sulle operazioni di sincronizzazione dei dispositivi. Questa informazione viene segnalata solo se è presente nella richiesta di hello. |
| MachineId |   Informazioni sulle operazioni di sincronizzazione dei dispositivi. Questa informazione viene segnalata solo se è presente nella richiesta di hello. |
| Site_ | GUID del sito hello in cui si trova il file di hello o una cartella accessibile hello utente Hello. |
| Source_Name | entità Hello che ha attivato hello controllata l'operazione. I valori possibili sono ObjectModel o SharePoint. |
| UserAgent | Informazioni dell'utente hello client o browser. Queste informazioni vengono fornite da hello client o browser. |


### <a name="sharepoint-schema"></a>Schema di SharePoint
Questi record vengono creati quando vengono apportate tooSharePoint di modifiche di configurazione.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Stringa facoltativa per gli eventi personalizzati. |
| Event_Data |  Payload facoltativo per gli eventi personalizzati. |
| ModifiedProperties | proprietà Hello è inclusa per gli eventi amministrativi, ad esempio l'aggiunta di un utente come membro di un sito o un gruppo di Amministrazione raccolta siti. proprietà Hello include nome hello della proprietà di hello che è stata modificata (ad esempio, il gruppo di amministrazione del sito hello), nuovo valore di hello modificato proprietà (tale utente hello che è stato aggiunto come amministratore del sito), e hello precedente il valore di hello oggetto hello. |


### <a name="sharepoint-file-operations"></a>Operazioni sui file di SharePoint
Questi record vengono creati in operazioni toofile risposta in SharePoint.

| Proprietà | Descrizione |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | estensione di file Hello di un file che viene copiato o spostato. Questa proprietà viene visualizzata solo per gli eventi FileCopied e FileMoved. |
| DestinationFileName | nome di Hello del file hello che viene copiato o spostato. Questa proprietà viene visualizzata solo per gli eventi FileCopied e FileMoved. |
| DestinationRelativeUrl | Hello l'URL della cartella di destinazione hello in un file viene copiato o spostato. combinazione di Hello di hello valori per parametri SiteURL, DestinationRelativeURL e DestinationFileName è hello corrisponde al valore di hello per proprietà di ObjectID hello, ovvero nome e percorso completo del file hello che è stato copiato hello. Questa proprietà viene visualizzata solo per gli eventi FileCopied e FileMoved. |
| SharingType | tipo di Hello autorizzazioni che sono state assegnate toohello utente condiviso con risorse hello di condivisione. Questo utente viene identificato dal parametro UserSharedWith hello. |
| Site_Url | Hello l'URL del sito di hello in cui si trova il file di hello o una cartella accessibile hello utente. |
| SourceFileExtension | estensione del file hello che ha effettuato l'accesso utente hello file Hello. Questa proprietà è vuota se l'oggetto hello che ha effettuato l'accesso è una cartella. |
| SourceFileName |  nome Hello del file hello o della cartella utente hello effettuato l'accesso. |
| SourceRelativeUrl | Hello l'URL della cartella di hello che contiene file hello hello utente effettuato l'accesso. combinazione di Hello di hello valori per i parametri SiteURL SourceRelativeURL e SourceFileName hello è hello corrisponde al valore di hello per proprietà di ObjectID hello, ovvero nome e percorso completo del file hello hello utente accede a hello. |
| UserSharedWith |  utente Hello condiviso con una risorsa. |




## <a name="sample-log-searches"></a>Ricerche di log di esempio
Hello nella tabella seguente fornisce le ricerche log di esempio per aggiornare i record raccolti da questa soluzione.

| Query | Descrizione |
| --- | --- |
|Conteggio di tutte le operazioni di hello nella sottoscrizione di Office 365 |`Type=OfficeActivity | measure count() by Operation` |
|Uso di siti di SharePoint|`Type=OfficeActivity OfficeWorkload=sharepoint | measure count() as Count by SiteUrl | ordinamento Count asc`|
|Operazioni di accesso ai file per tipo di utente|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|Ricerca con una parola chiave specifica|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Azioni esterne di monitoraggio di Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Risoluzione dei problemi

Se la soluzione Office 365 non raccoglie i dati come previsto, controllare lo stato nel portale OMS hello in **impostazioni** -> **Connected Sources** -> **Office 365** . Hello nella tabella seguente viene descritto ogni stato.

| Stato | Descrizione |
|:--|:--|
| Attivo | Hello abbonamento a Office 365 è attivo e carico di lavoro di hello è l'area di lavoro OMS tooyour connesso correttamente. |
| In sospeso | Hello abbonamento a Office 365 è attivo, ma il carico di lavoro di hello non è ancora connesso correttamente tooyour area di lavoro OMS. Hello prima connessione di sottoscrizione di Office 365 hello, tutti i carichi di lavoro hello saranno in questo stato fino a quando non sono connessi correttamente. Attendere 24 ore affinché tutti hello carichi di lavoro tooswitch tooActive. |
| Inactive | Hello abbonamento a Office 365 è in uno stato inattivo. Controllare la pagina di amministrazione di Office 365 per i dettagli. Dopo aver attivato la sottoscrizione a Office 365, scollegarla dall'area di lavoro OMS e ricollegarlo toostart la ricezione di dati. |



## <a name="next-steps"></a>Passaggi successivi
* Usare le ricerche Log in [Log Analitica](../log-analytics/log-analytics-log-searches.md) tooview in dettaglio i dati di aggiornamento.
* [Creare dashboard personalizzati](../log-analytics/log-analytics-dashboards.md) toodisplay le query di ricerca di Office 365 preferite.
* [Creare avvisi](../log-analytics/log-analytics-alerts.md) toobe in modo proattivo una notifica delle attività di Office 365 importanti.  
