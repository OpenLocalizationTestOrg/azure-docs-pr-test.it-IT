---
title: codici di errore API REST di Machine Learning aaaAzure | Documenti Microsoft
description: Questi codici errore possono essere restituiti da un'operazione in un servizio Web di Azure Machine Learning.
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Codici errore dell'API REST di Azure Machine Learning
 
Hello seguenti codici di errore potrebbero essere restituiti da un'operazione in un servizio web Azure Machine Learning.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (codice di stato HTTP 400)
 
È stato specificato un argomento non valido.
 
Questa classe di errori indica che un argomento specificato nel codice non è valido. Potrebbe trattarsi di una credenziale o il percorso del servizio web toohello passato toosomething di archiviazione di Azure. Controllare il campo "codice di errore" hello in toodiagnose di sezione "Dettagli" hello l'argomento specifico non è valido.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| BadParameterValue | valore di parametro Hello non soddisfa regola parametro hello sul parametro hello |
| BadSubscriptionId | sottoscrizione Hello Id tooscore utilizzato non è hello presente nella risorsa hello |
| BadVersionCall | È stato passato il parametro di versione non valida durante la chiamata API hello: {0}. Controllo hello API pagina per passare la versione corretta di hello della Guida e riprovare. |
| BatchJobInputsNotSpecified | uno o più input obbligatorio seguito Hello non sono stata specificata con richiesta di hello: {0}. Assicurarsi che tutti i dati di input siano specificati e riprovare. |
| BatchJobInputsTooManySpecified | specificare la richiesta di Hello più input quanto definito nel servizio hello. Elenco di input accettati: {0}. Assicurarsi che tutti i dati di input siano specificati correttamente e riprovare. |
| BlobNameTooLong | Il percorso dell'archivio BLOB di Azure specificato per l'output di diagnostica è troppo lungo: {0}. Abbreviare il percorso di hello e riprovare. |
| BlobNotFound | Non è possibile tooaccess hello fornito blob di Azure - {0}.  Messaggio di errore di Azure: {1}. |
| ContainerIsEmpty | Non sono stati specificati nomi di contenitori di archiviazione di Azure. Specificare un nome di contenitore valido e riprovare. |
| ContainerSegmentInvalid | Il nome del contenitore non è valido. Specificare un nome di contenitore valido e riprovare. |
| ContainerValidationFailed | La convalida del contenitore BLOB ha avuto esito negativo con questo errore: {0}. |
| DataTypeNotSupported | È stato specificato un tipo di dati non supportato. Specificare tipi di dati validi e riprovare. |
| DuplicateInputInBatchCall | richiesta batch Hello non è valido. Non è possibile specificare uno o più input di hello stesso tempo. Rimuovere uno di questi elementi dalla richiesta hello e riprovare. |
| ExpiryTimeInThePast | È ora di scadenza fornita in hello precedente: {0}. Specificare una scadenza futura in formato UTC e riprovare. toonever scadenza, impostare tooNULL ora di scadenza. |
| IncompleteSettings | Le impostazioni di diagnostica non sono complete. |
| InputBlobRelativeLocationInvalid | Non sono stati specificati nomi del BLOB di Archiviazione di Azure. Specificare un nome di BLOB valido e riprovare. |
| InvalidBlob | La specifica del BLOB non è valida per il BLOB: {0}. Verificare che la stringa di connessione o il percorso relativo oppure la specifica del token di firma di accesso condiviso sia corretta e riprovare. |
| InvalidBlobConnectionString | stringa di connessione specificata per un BLOB di input/output di hello non valido di Hello: {0}. Correggere e riprovare. |
| InvalidBlobExtension | riferimento blob Hello: {0} ha un'estensione di file mancanti o non valido. Le estensioni di file supportate per questo output sono: "{1}". |
| InvalidInputNames | Servizio non valido specificati nella richiesta di hello nomi di input: {0}. . Eseguire il mapping di input di hello dati di input toohello servizio corretto e riprovare. |
| InvalidOutputOverrideName | Il nome di override dell'output non è valido: {0}. servizio Hello non dispone di un nodo di output con questo nome. Passare un toooverride nome nodo di output corretto (si applica distinzione maiuscole/minuscole). |
| InvalidQueryParameter | Il parametro di query '{0}' non è valido. {1} |
| MissingInputBlobInformation | Le informazioni sul BLOB di Archiviazione di Azure non sono presenti. Specificare una stringa di connessione valida e il percorso relativo o l'URI e riprovare. |
| MissingJobId | Non è stato specificato alcun ID di processo. Un processo Id viene restituito quando un processo è stato inviato per hello prima volta. Verificare che tale processo hello Id sia corretto e riprovare. |
| MissingKeys | Non sono state specificate chiavi o non è presente una chiave primaria o secondaria. |
| MissingModelPackage | Non sono stati specificati ID di pacchetto o pacchetti di modelli. Specificare un ID di pacchetto di modelli o un pacchetto di modelli valido e riprovare. |
| MissingOutputOverrideSpecification | richiesta di Hello manca la specifica di blob hello per eseguire l'override di output {0}. . Specificare un percorso blob validi con richiesta di hello, o rimuovere hello specifica dell'output se nessun override della posizione desiderata. |
| MissingRequestInput | servizio web Hello prevede un input, ma è stato specificato alcun input. Verificare gli input validi sono forniti in base hello pubblicato nel modello hello porte di input e riprovare. |
| MissingRequiredGlobalParameters | Non sono stati specificati tutti i parametri obbligatori del servizio Web. Verificare i parametri di hello previsto per hello moduli siano corrette e riprovare. |
| MissingRequiredOutputOverrides | Quando si chiama un endpoint di servizio crittografata in che è obbligatorio toopass output le sostituzioni per gli output del servizio di hello tutti. Override attualmente mancanti per questi output: {0} |
| MissingWebServiceGroupId | Non sono stati specificati ID del gruppo di servizi. Specificare un ID di gruppo di servizi Web valido e riprovare. |
| MissingWebServiceId | Non sono stati specificati ID del servizio Web. Specificare un ID di servizio Web valido e riprovare. |
| MissingWebServicePackage | Non sono stati specificati pacchetti del servizio Web. Specificare un pacchetto del servizio Web valido e riprovare. |
| MissingWorkspaceId | Non sono stati specificati ID dell'area di lavoro. Specificare un ID dell'area di lavoro valido e riprovare. |
| ModelConfigurationInvalid | Configurazione del modello non valido nel pacchetto di modello hello. Verificare la configurazione di modello hello contiene definizione di endpoint di output, endpoint di errore standard, e std endpoint e riprovare. |
| ModelPackageIdInvalid | L'ID del pacchetto di modelli non è valido. Verificare che il pacchetto di modello hello Id sia corretto e riprovare. |
| RequestBodyInvalid | Alcun corpo della richiesta specificato o un errore nella deserializzazione del corpo della richiesta hello. |
| RequestIsEmpty | Non sono state specificate richieste. Specificare una richiesta valida e riprovare. |
| UnexpectedParameter | Sono stati specificati parametri imprevisti. Verificare che l'ortografia di tutti i nomi di parametro sia corretta e che vengano passati solo i parametri previsti, quindi riprovare. |
| UnknownError | Errore sconosciuto. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Non è possibile modificare i requisiti delle richieste simultanee per il servizio Web {0}. |
| WebServiceIdInvalid | L'ID del servizio Web specificato non è valido. L'ID del servizio Web deve essere un GUID valido. |
| WebServiceTooManyConcurrentRequestRequirement | Impossibile impostare toomore requisito di richieste simultanee di {0}. |
| WebServiceTypeInvalid | Il tipo del servizio Web specificato non è valido. Verificare che tipo di servizio web valido hello sia corretto e riprovare. Tipo di servizio Web validi: {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (codice di stato HTTP 400)
 
È stato specificato un argomento utente non valido.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| InputMismatchError | I dati di input non corrispondono allo schema di porte di input. |
| InputParseError | L'analisi dei vettori di input non è riuscita.  Verificare vettore input hello con numero di colonne e tipi di dati corretto hello.  Dettagli aggiuntivi: {0}. |
| MissingRequiredGlobalParameters | Non sono presenti parametri previsti dal servizio web hello. Verificare che tutti i parametri necessario hello previsti dal servizio web hello siano corretti e riprovare. |
| UnexpectedParameter | Verificare solo hello necessarie vengono passati parametri previsti dal servizio web hello e riprovare. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (codice di stato HTTP 400)
 
non è valido nel contesto corrente hello richiesta Hello.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| CannotStartJob | Impossibile avviare il processo di Hello perché è in stato {0}. |
| IncompatibleModel | non è compatibile con la versione richiesta hello modello Hello. versione richiesta Hello supporta solo i modelli di datatable singolo output. |
| MultipleInputsNotAllowed | modello di Hello non consente più input. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (codice di stato HTTP 400)
 
Si è verificato un errore di libreria interno durante l'esecuzione del modulo.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (codice di stato HTTP 400)
 
Si è verificato un errore durante l'esecuzione del modulo.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (codice di stato HTTP 400)
 
Il pacchetto del servizio Web non è valido. Verificare di pacchetto del servizio web hello fornito sia corretto e riprovare.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| FormatError | pacchetto del servizio web Hello non è valido. Dettagli: {0} |
| RuntimesError | grafico di pacchetto del servizio web Hello non è valido. Dettagli: {0} |
| ValidationError | grafico di pacchetto del servizio web Hello non è valido. Dettagli: {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Unauthorized (codice di stato HTTP 401)
 
Richiesta è una risorsa tooaccess non autorizzati.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| AdminRequestUnauthorized | Non autorizzata |
| ManagementRequestUnauthorized | Non autorizzata |
| ScoreRequestUnauthorized | Sono state specificate credenziali non valide. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (codice di stato HTTP 404)
 
La risorsa non è stata trovata.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| ModelPackageNotFound | Il pacchetto di modelli non è stato trovato. Verificare il pacchetto di modello hello Id sia corretto e riprovare. |
| WebServiceIdNotFoundInWorkspace | Il servizio Web in questa area di lavoro non è stato trovato. È presente una mancata corrispondenza tra webServiceId hello e Idareadilavoro hello. Verificare che il servizio web hello fornito fa parte dell'area di lavoro hello e riprovare. |
| WebServiceNotFound | Il servizio Web non è stato trovato. Verificare che il servizio web hello Id sia corretto e riprovare. |
| WorkspaceNotFound | L'area di lavoro non è stata trovata. Verificare l'area di lavoro hello Id sia corretto e riprovare. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (codice di stato HTTP 408)
 
non è stato possibile completare l'operazione di Hello all'interno di hello tempo consentito.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| RequestCanceled | Richiesta annullata dal client hello. |
| ScoreRequestTimeout | Si è verificato il timeout dell'esecuzione della richiesta. |
 
## <a name="conflict-http-status-code-409"></a>Conflict (codice di stato HTTP 409)
 
La risorsa esiste già.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Il nome del parametro di output non è valido. Provare a utilizzare le colonne toorename modulo di hello metadati editor e riprovare. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (codice di stato HTTP 413)
 
modello Hello ha superato la quota di memoria hello tooit assegnato.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| OutOfMemoryLimit | modello Hello utilizzata più memoria attualmente utilizzato con riferimento ad è stato appositamente. Numero massimo consentito di memoria per il modello di hello è {0} MB. Controllare il modello per individuare problemi. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (codice di stato HTTP 500)
 
Si è verificato un errore interno durante l'esecuzione.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | arresto anomalo del processo del contenitore Hello con errore di sistema |
| ContainerProcessTerminatedWithUnknownError | arresto anomalo del processo di Hello contenitore con un errore sconosciuto |
| ContainerValidationFailed | La convalida del contenitore BLOB ha avuto esito negativo con questo errore: {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Non sono stati specificati argomenti. Assicurarsi che vengano passati argomenti validi e riprovare. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | La porta con ID={0} ha un tipo di dati non supportato: {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | La generazione di Swagger non è riuscita. Dettagli: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Codice di stato del processo sconosciuto {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage. Dettagli: {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (codice di stato HTTP 500)
 
Si è verificato un errore interno durante l'esecuzione. La memoria del sistema è insufficiente. Riprova più tardi.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (codice di stato HTTP 500)
 
Il pacchetto di modelli non è valido. Verificare che il pacchetto di modello hello fornito sia corretto e riprovare.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (codice di stato HTTP 500)
 
Il pacchetto del servizio Web non è valido. Verificare che il pacchetto di web hello fornito sia corretto e riprovare.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| ModuleError | grafico di pacchetto del servizio web Hello non è valido. Dettagli: {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (codice di stato HTTP 503)
 
richiesta di Hello non è possibile eseguire come hello contenitori all'inizializzazione.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (codice di stato HTTP 503)
 
Il servizio è temporaneamente non disponibile.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| NoMoreResources | Non sono disponibili risorse per la richiesta. |
| RequestThrottled | La richiesta è stata limitata per l'endpoint {0}. concorrenza massima di Hello per endpoint hello è \\{1 \\}. |
| TooManyConcurrentRequests | Sono state inviate troppe richieste simultanee. |
| TooManyHostsBeingInitialized | Troppi host viene inizializzato in fase di hello stesso tempo. Prendere in considerazione la limitazione o la ripetizione dei tentativi. |
| TooManyHostsBeingInitializedPerModel | Troppi host viene inizializzato in fase di hello stesso tempo. Prendere in considerazione la limitazione o la ripetizione dei tentativi. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (codice di stato HTTP 504)
 
non è stato possibile completare l'operazione di Hello all'interno di hello tempo consentito.
 
| Codice di errore | Messaggio utente |
| ---------- |--------------|
| BackendInitializationTimeout | inizializzazione del servizio web di Hello hello consentito tempo potrebbe non essere completata. |
| BackendScoreTimeout | esecuzione della richiesta servizio web Hello hello consentito tempo potrebbe non essere completata. |
 
