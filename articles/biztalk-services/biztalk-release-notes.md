---
title: aaaRelease note per i servizi BizTalk di Azure | Documenti Microsoft
description: Elenca i problemi noti per i servizi BizTalk di Azure hello
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Note sulla versione per Servizi BizTalk di Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

note sulla versione di Hello hello Microsoft servizi BizTalk di Azure contengono problemi noti di questa versione di hello.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Novità nell'aggiornamento di novembre di hello dei servizi BizTalk
* Crittografia può essere abilitata nel portale dei servizi BizTalk di hello. Vedere [Abilitare Crittografia dati inattivi nel portale di Servizi BizTalk](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Cronologia aggiornamenti
### <a name="october-update"></a>Aggiornamento di ottobre
* Supporto per gli account aziendali:  
  * **Scenario**: si è registrata una distribuzione del servizio BizTalk usando un account Microsoft (ad esempio, user@live.com). In questo scenario, gli utenti possono gestire solo Account di Microsoft hello BizTalk Service tramite il portale di servizi BizTalk di hello. Non è possibile usare un account aziendale.  
  * **Scenario**: si è registrata una distribuzione del servizio BizTalk usando un account aziendale in un'istanza di Azure Active Directory (ad esempio, user@fabrikam.com o user@contoso.com). In questo scenario, solo gli utenti di Azure Active Directory della stessa organizzazione può gestire hello hello BizTalk Service tramite il portale di servizi BizTalk di hello. Non è possibile usare un account Microsoft.  
* Quando si crea un BizTalk Service nel portale di Azure classico hello, vengono registrati automaticamente in hello portale dei servizi BizTalk.
  * **Scenario**: si accede a hello portale di Azure classico, creare un BizTalk Service e quindi selezionare **Gestisci** per hello prima volta. Quando si apre il portale di servizi BizTalk di hello, hello BizTalk Service viene registrato automaticamente ed è pronto per le distribuzioni.  
    Vedere [registrazione e aggiornamento di una distribuzione del servizio BizTalk nel portale dei servizi BizTalk di hello](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Aggiornamento del 14 agosto
* Accordo e bridge disaccoppiamento: commerciali accordi tra partner e i Bridge sono ora disaccoppiati nel portale dei servizi BizTalk di hello. Ora creare separatamente accordi e Bridge e in fase di esecuzione Bridge risolvere tooan contratto in base ai valori hello messaggio EDI. Vedere [Creare accordi in Servizi BizTalk di Azure](https://msdn.microsoft.com/library/azure/hh689908.aspx), [Creare un bridge EDI con il portale di Servizi BizTalk](https://msdn.microsoft.com/library/azure/dn793986.aspx), [Creare un bridge AS2 con il portale di Servizi BizTalk](https://msdn.microsoft.com/library/azure/dn793993.aspx) e [Come i bridge si risolvono in accordi in fase di esecuzione](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* modelli di toocreate Hello opzione per gli accordi è stata sospesa.  
* Per contratto lato invio hello, è ora possibile specificare il set di delimitatori diversi per ogni schema. Questa configurazione è specificata nelle impostazioni del protocollo per l'accordo sul lato trasmissione. Per altre informazioni, vedere [Creare un accordo X12 in Servizi BizTalk](https://msdn.microsoft.com/library/azure/hh689847.aspx) e [Creare un accordo EDIFACT in Servizi BizTalk](https://msdn.microsoft.com/library/azure/dn606267.aspx). Due nuove entità vengono aggiunti anche toohello API TPM OM per hello allo stesso scopo. Vedere [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) ed [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* I costrutti XSD standard, inclusi i tipi derivati, sono ora supportati. Vedere [Usare costrutti XSD standard nelle mappe](https://msdn.microsoft.com/library/azure/dn793987.aspx) e [Usare tipi derivati in scenari ed esempi di mapping](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 supporta nuovi algoritmi MIC per la firma dei messaggi e nuovi algoritmi di crittografia. Vedere [Creare un contratto AS2 nei servizi BizTalk di Azure](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Problemi noti

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Problemi di connettività dopo l'aggiornamento del portale di Servizi BizTalk
  Se si dispone di hello portale dei servizi BizTalk aprire durante l'aggiornamento dei servizi BizTalk tooroll in Cambia toohello servizio, si verificherebbero problemi di connettività con hello portale dei servizi BizTalk.  
  In alternativa, potrebbe riavviare il browser hello, eliminare la cache di hello browser o avviare il portale di hello in modalità privata.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Impossibile individuare l'elemento hello IDE di Visual Studio se si fa clic su un errore o un avviso in un progetto di servizi BizTalk
Installare problema di hello toofix hello Visual Studio 2012 Update 3 RC 1.  

### <a name="custom-binding-project-reference"></a>Riferimento al progetto di associazione personalizzata
Prendere in considerazione hello seguenti situazioni con un progetto di servizi BizTalk in una soluzione di Visual Studio:  

* Nella stessa soluzione di Visual Studio hello, non vi è un progetto di servizi BizTalk e un progetto di associazione personalizzata. progetto BizTalk Service Hello dispone di un file di progetto di riferimento toothis associazione personalizzata.
* Hello progetto BizTalk Service è un riferimento tooa personalizzato comportamento/associazione DLL.

È 'Compila' hello soluzione in Visual Studio completata. Successivamente, 'Rebuild' o 'Pulisci' soluzione di hello. Successivamente, quando si ricompila o pulito nuovamente, hello seguente errore:  
  File non è possibile toocopy <Path tooDLL> too"bin\Debug\FileName.dll". il processo di Hello non può accedere file hello 'bin\Debug\FileName.dll' perché è utilizzato da un altro processo.  

#### <a name="workaround"></a>Soluzione alternativa
* Se [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) è installato, si dispone di hello le due opzioni seguenti:
  
  * Riavviare Visual Studio
  * Riavviare la soluzione hello. Quindi, è possibile eseguire solo una compilazione su soluzione hello.  
* Se [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) non è installato, aprire Gestione attività, fare clic sulla scheda processi hello, fare clic su processo MSBuild.exe hello e quindi fare clic su pulsante Termina processo hello.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Routing tooBasicHttpRelay endpoint non è supportato dal bridge e portale dei servizi BizTalk se i caratteri non stampabili vengono alzate di livello come intestazioni HTTP
Se si utilizzano caratteri non stampabili come parte delle proprietà innalzate di livello per i messaggi, tali messaggi non possono essere indirizzato toorelay destinazioni che utilizzano l'associazione BasicHttpRelay hello. Inoltre, hello proprietà innalzate di livello che sono disponibili come parte del rilevamento sono senza codifica per le destinazioni e la codifica URL per i BLOB.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>Messaggio MDN viene inviato in modo asincrono anche se hello inviare opzione MDN asincrono è deselezionata
Si consideri lo scenario: se si seleziona hello **invio di MDN asincroni** casella di controllo e quindi specificare un asincrono di hello toosend URL MDN, quindi deselezionare hello **invio di MDN asincroni** casella di controllo nuovamente, hello MDN è ancora URL toohello inviato specificato anche se hello opzione toosend async MDN non è selezionata.  
In alternativa, è necessario deselezionare hello URL specificato prima di deselezionare hello **invio di MDN asincroni** casella di controllo e quindi distribuire il contratto AS2 hello.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Spazi vuoti che superano una causa di un interscambio valido toohello di toobe inviato un messaggio vuoto sospendere endpoint
Se sono presenti spazi vuoti che superano un segmento IEA, disassembler hello interpreta come la fine dell'interscambio corrente e viene visualizzata nel set successivo di hello di spazi vuoti come un messaggio successivo. Poiché non si tratta di un interscambio valido, è possibile osservare che un messaggio ha esito positivo viene inviato a destinazione route toohello e un messaggio vuoto viene inviato hello sospendere l'endpoint.  

### <a name="tracking-in-biztalk-services-portal"></a>Rilevamento nel portale di Servizi BizTalk
Gli eventi di rilevamento vengono acquisiti l'elaborazione del messaggio EDI toohello e correlazioni. Se un messaggio non riesce all'esterno di hello fase del protocollo, rilevamento verrà elaborato in modo corretto. In questo caso, fare riferimento sezione LOG toohello hello **dettagli** colonna **rilevamento** per i dettagli dell'errore.
Hello X12 di ricezione e le impostazioni di invio ([creare un X12 contratto di servizi BizTalk di Azure](https://msdn.microsoft.com/library/azure/hh689847.aspx)) forniscono informazioni su hello fase del protocollo.  

### <a name="update-agreement"></a>Accordo di aggiornamento
Portale dei servizi BizTalk di Hello consente toomodify hello qualificatore di un'identità quando viene configurato un contratto. Per effetto di questa operazione è possibile che vengano create proprietà incoerenti. È ad esempio, un contratto mediante zz: 1234567 e 7654321 hello qualificatore. In impostazioni del profilo di hello portale dei servizi BizTalk, si modifica 1234567 toobe 01:ChangedValue. Si apre il contratto di hello e viene visualizzato il 01:ChangedValue anziché 1234567.
hello toomodify qualificatore di un'identità, eliminare hello contratto, aggiornare **identità** hello profilo partner in e ricreare il contratto di hello.  

> AZURE.WARNING Questo comportamento influisce su X12 e AS2.  
> 
> 

### <a name="as2-attachments"></a>Allegati dei messaggi AS2
Gli allegati dei messaggi AS2 non sono supportati né in invio né in ricezione. In particolare, gli allegati vengono automaticamente ignorati e il corpo del messaggio hello viene elaborato come un normale messaggio AS2.  

### <a name="resources-remembering-path"></a>Risorse: memorizzazione del percorso
Quando si aggiungono **risorse**, finestra di dialogo hello potrebbe non ricordare hello percorso precedentemente usato tooadd una risorsa. percorso precedentemente usato hello tooremember, provare ad aggiungere sito web portale dei servizi BizTalk di hello troppo**siti attendibili** in Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Se si rinomina il nome di entità hello di un bridge e il progetto hello Chiudi senza salvare le modifiche, aprire di nuovo l'entità hello genera un errore
Si consideri uno scenario in hello seguente ordine:  

* Aggiungere un progetto BizTalk Service di tooa bridge (ad esempio un Bridge XML unidirezionale)  
* Rinominare il bridge hello specificando un valore per la proprietà nome entità hello. Viene rinominato il file con estensione bridgeconfig associato hello con nome hello specificato.  
* Senza salvare le modifiche di hello, chiudere il file con estensione BCS hello (chiudendo scheda hello in Visual Studio).  
* Aprire di nuovo file con estensione BCS hello da hello Esplora soluzioni.  
  Si noterà che mentre file hello. bridgeconfig associato ha hello nuovo nome, nome dell'entità nell'area di progettazione hello hello è ancora hello vecchio nome. Se si tenta di hello tooopen configurazione Bridge facendo doppio clic sul componente bridge hello, viene visualizzato hello errore seguente:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid in esecuzione in questo scenario, assicurarsi di salvare le modifiche dopo avere rinominato le entità hello in un progetto BizTalk Service.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>La compilazione di un progetto di Servizi BizTalk viene eseguita in modo corretto anche se un elemento è stato escluso da un progetto di Visual Studio
Si consideri uno scenario in cui aggiungere un progetto BizTalk Service di tooa elemento (ad esempio, un file XSD), include tale elemento nella configurazione del Bridge hello (ad esempio, specificandolo come un tipo di messaggio di richiesta) e quindi lo si esclude dal progetto di Visual Studio hello. In tal caso, la compilazione progetto hello non fornirà qualsiasi errore, purché sia disponibile sul disco hello hello artefatto hello eliminato dello stesso percorso da cui è stata inclusa nel progetto di Visual Studio hello.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hello progetto BizTalk Service non verifica la disponibilità dello schema durante la configurazione del bridge hello
In un progetto BizTalk Service, se uno schema che è stato aggiunto il progetto toohello Importa in un altro schema, hello progetto BizTalk Service non verifica se schema importato hello viene aggiunto il progetto toohello. Se si tenta di toobuild di un progetto, non si ottengono gli eventuali errori di compilazione.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>messaggio di risposta Hello un Bridge di richiesta / risposta XML è sempre del set di caratteri UTF-8
Per questa versione, set di caratteri di hello del messaggio di risposta hello da un Bridge di richiesta-risposta XML è sempre impostato tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Tipi di dati definiti dall'utente
tipi di dati definito dall'utente per operazioni degli adapter può utilizzare l'adapter BizTalk Adapter Pack Hello nella funzionalità servizio Adapter BizTalk hello.
Quando si utilizzano tipi di dati definito dall'utente, copiare i file (. dll) di hello toodrive:\Program Files\Microsoft BizTalk Adapter Service\BAServiceRuntime\bin\ o toohello Global Assembly Cache (GAC) nel server di hello hello servizio Adapter BizTalk servizio di hosting. In caso contrario, il seguente errore hello può verificarsi nel client hello:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> È consigliato toouse GACUtil.exe tooinstall un file in hello Global Assembly Cache. Documenti GACUtil.exe come toouse questo opzioni della riga di comando dello strumento e hello Visual Studio.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Il riavvio di hello sito Web del servizio Adapter BizTalk
L'installazione hello **Runtime del servizio Adapter BizTalk*** crea hello **servizio Adapter BizTalk** sito web in IIS che contiene hello **BAService** dell'applicazione. **BAService** applicazione utilizza internamente copertura di inoltro associazione tooextend hello del cloud di toohello endpoint servizio locale. Per un servizio ospitato in locale, endpoint di inoltro hello corrispondente verrà registrato in Bus di servizio hello solo quando hello locale il servizio viene avviato.  

Se si arresta e avvia un'applicazione, la configurazione hello dell'avvio automatico di un'applicazione non viene applicata. Quando **BAService** viene arrestato, è sempre necessario riavviare hello **servizio Adapter BizTalk** web invece del sito. Non avviare o arrestare hello **BAService** dell'applicazione.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Non usare caratteri speciali per i nomi degli indirizzi e delle entità dei componenti LOB
Evitare l'uso dei caratteri speciali per i nomi degli indirizzi e delle entità dei componenti LOB. Se si esegue questa operazione, si verificherà un errore durante la distribuzione del progetto BizTalk Service hello. Per alcuni caratteri, ad esempio '%', sito Web del servizio Adapter BizTalk hello potrebbe entra in uno stato interrotto e sarà necessario toomanually avviarlo.

### <a name="test-map-with-get-context-property"></a>Mappa di test con Get Context Property
Se una trasformazione contiene un'operazione di mappa **Get Context Property (Ottieni proprietà di contesto)**, l'operazione **Test mappa** non riuscirà. Come soluzione alternativa temporanea, sostituire hello **Get Context Property** dell'operazione di mapping con operazione mappa concatenare una stringa contenente dati fittizi. Verrà compilare lo schema di destinazione hello e sarà possibile testare altre funzionalità di trasformazione.

### <a name="test-map-property-does-not-display"></a>La proprietà Mappa di test non viene visualizzata
Hello **Test mappa** proprietà non è disponibile in Visual Studio. Ciò può verificarsi se hello **proprietà** finestra e hello **Esplora** finestra non vengono ancorate contemporaneamente. tooresolve hello, questo ancoraggio **proprietà** hello e **Esplora** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>L'elenco a discesa dell'operazione DateTime Reformat non è disponibile
Quando un'operazione di mapping DateTime Reformat viene aggiunta toohello progettare hello superficie di attacco e configurato, formato elenco a discesa potrebbe non essere disponibile. Questa situazione può verificarsi se il computer di hello visualizzato è impostato **medio – 125%** o **grande – 150%**. tooresolve, impostare la visualizzazione di hello troppo**piccolo – 100% (impostazione predefinita)** hello procedura riportata di seguito:  

1. Aprire hello **Pannello di controllo** e fare clic su **aspetto e personalizzazione**.
2. Fare clic su **Schermo**.
3. Fare clic su **Piccolo - 100% (impostazione predefinita)** e quindi su **Applica**.

Hello **formato** riepilogo ora dovrebbe funzionare come previsto.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Contratti duplicati nel portale dei servizi BizTalk di hello
Prendere in considerazione hello seguente scenario:

1. Creare un contratto tramite API di OM gestione Partner commerciali hello.
2. Aprire il contratto di hello in hello portale dei servizi BizTalk in due schede diverse.
3. Distribuire il contratto di hello da entrambe le schede hello.
4. Di conseguenza, entrambi gli accordi hello vengono distribuiti risultante voci duplicate nel portale dei servizi BizTalk di hello

**Soluzione alternativa**. Aprire uno dei contratti duplicati hello nel portale dei servizi BizTalk di hello e annullare la distribuzione.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>I bridge non usano i certificati aggiornati anche dopo l'aggiornamento di un certificato nell'archivio elementi hello
Prendere in considerazione hello seguenti scenari:  

**Scenario 1: Utilizzo di certificati basati sull'identificazione personale per proteggere il trasferimento di messaggi da un endpoint del servizio tooa bridge**  
Provare a usare certificati basati su identificazione personale nel progetto di Servizi BizTalk. Si aggiorna il certificato di hello nel portale dei servizi BizTalk di hello con hello stesso nome e un'altra identificazione personale, ma non vengono aggiornati di conseguenza hello progetto BizTalk Service. In tale scenario, il bridge hello potrebbe continuare messaggi hello tooprocess perché i dati del certificato precedenti hello potrebbero essere ancora in cache del canale hello. Quando questi dati non sono più presenti, l'elaborazione dei messaggi ha esito negativo.  

**Soluzione alternativa**: certificato hello nel progetto BizTalk Service hello e ridistribuire il progetto hello.  

**Scenario 2: Utilizzo di certificati tooidentify comportamenti basati sul nome per la protezione di trasferimento di messaggi da un endpoint del servizio tooa bridge**

Si consideri uno scenario in cui utilizzare certificati tooidentify comportamenti basati sul nome del progetto BizTalk Service. Aggiorna certificato hello nel portale dei servizi BizTalk di hello, ma non vengono aggiornati di conseguenza hello progetto BizTalk Service. In tale scenario, il bridge hello potrebbe continuare messaggi hello tooprocess perché i dati del certificato precedenti hello potrebbero essere ancora in cache del canale hello. Quando questi dati non sono più presenti, l'elaborazione dei messaggi ha esito negativo.  

**Soluzione alternativa**: certificato hello nel progetto BizTalk Service hello e ridistribuire il progetto hello.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>I bridge continuano tooprocess messaggi anche quando il database SQL hello è offline
Bridge di servizi BizTalk di Hello continuano tooprocess messaggi per un periodo di tempo, anche se Microsoft Database SQL di Azure (che archivia informazioni quali pipeline ed elementi distribuiti esecuzione hello) hello è offline. Questo avviene perché i servizi BizTalk utilizza gli elementi memorizzati nella cache di hello e la configurazione del bridge.
Se si desidera hello Bridge tooprocess tutti i messaggi quando hello SQL Database è offline, è possibile utilizzare toostop cmdlet PowerShell di servizi BizTalk di hello o sospendere hello BizTalk Service. Vedere [esempio di gestione del servizio BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=329019) per operazioni toomanage i cmdlet di Windows PowerShell hello.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Un messaggio XML lettura hello in componente del codice personalizzato di un bridge include un carattere BOM aggiuntivo
Si consideri uno scenario in cui si desidera tooread un messaggio XML all'interno di codice personalizzato di un bridge. Se si utilizza hello System.Text.Encoding.UTF8.GetString(bytes) API .NET è incluso un carattere BOM aggiuntivo nell'output di hello all'inizio di hello del messaggio hello. Pertanto, se non si desidera hello tooinclude output di hello carattere BOM aggiuntivo, è necessario utilizzare ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>L'invio di messaggi tooa bridge mediante WCF non è scalabile
I messaggi inviati tooa bridge mediante WCF non è scalabile. Se si vuole un client scalabile, è necessario usare HttpWebRequest.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>AGGIORNAMENTO: Errore del Provider di Token dopo l'aggiornamento da BizTalk Services anteprima tooGeneral Availability (GA)
Questa situazione si verifica quando è presente un accordo EDI o AS2 con batch attivi. Quando BizTalk Service hello viene aggiornato da Anteprima tooGA, può verificarsi seguente hello:

* Errore: provider di token hello è stato Impossibile tooprovide un token di sicurezza. Messaggio restituito dal provider di token: nome remoto hello non può essere risolto.
* Le attività batch vengono annullate.

**Soluzione alternativa**: hello BizTalk Service, dopo aver aggiornato tooGeneral Availability (GA), ridistribuire il contratto di hello.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>AGGIORNAMENTO: Casella degli strumenti Mostra hello icone bridge precedente dopo l'aggiornamento di hello BizTalk Services SDK
Dopo l'aggiornamento di una versione precedente di hello BizTalk Services SDK, che era precedente icone che rappresentano i bridge hello, casella degli strumenti hello continua icone di vecchio hello tooshow per i bridge hello. Tuttavia, se si aggiunge una bridge tooBizTalk servizio progetto area di progettazione, area hello Mostra icona nuova hello.  

**Soluzione alternativa**. È possibile risolvere questo problema eliminando il file TBD hello in <system drive>: \Users\<utente > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>AGGIORNAMENTO: Aggiornamento del portale BizTalk dalla tooGA anteprima potrebbe mostrare un errore che indica che la funzionalità EDI hello non è disponibile
Se si è connessi in hello portale dei servizi BizTalk, mentre i servizi BizTalk di hello viene aggiornato da tooGA di anteprima, si potrebbe ricevere l'errore seguente nel portale di hello hello:  

Questa funzionalità non è disponibile come parte di questa versione di Servizi BizTalk di Microsoft Azure. toouse edizione appropriata tooan di passare queste funzionalità.  

**Risoluzione**: disconnessione dal portale hello browser hello close e open e quindi accedere al portale hello.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>AGGIORNAMENTO: Nuovi dati di rilevamento non viene visualizzato al termine dei servizi BizTalk tooGA aggiornato
Si consideri uno scenario in cui un bridge XML è stato distribuito con la sottoscrizione della versione di anteprima di Servizi BizTalk. Si invia messaggi toohello bridge e dati di rilevamento corrispondenti hello sono disponibili nel portale dei servizi BizTalk di hello. Ora, se i componenti di runtime hello portale dei servizi BizTalk e i servizi BizTalk sono tooGA aggiornato e si invia un messaggio toohello stesso endpoint del bridge distribuito in precedenza, hello dati di rilevamento non vengono visualizzati per i messaggi inviati dopo l'aggiornamento.  

### <a name="pipelines-versus-bridges"></a>Pipeline e bridge
In questo documento, termini hello "pipeline" e "bridge" vengono utilizzati in modo intercambiabile. Entrambi significa essenzialmente hello stessa operazione, ovvero, un'unità di elaborazione messaggi distribuita nei servizi BizTalk.  

### <a name="concepts"></a>Concetti
[Servizi BizTalk](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

