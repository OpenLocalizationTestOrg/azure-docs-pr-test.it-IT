---
title: aaaMigrate da servizi mobili tooan App Mobile di servizio App
description: Informazioni su come tooeasily esegue la migrazione del tooan di applicazione di servizi mobili App del servizio Mobile App
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Eseguire la migrazione del tooAzure servizio Mobile di Azure esistente di servizio App
Con hello [disponibilità generale di servizio App di Azure], servizi mobili di Azure siti possono essere facilmente eseguita la migrazione sul posto tootake sfruttare tutte le funzionalità di hello servizio App di Azure.  Questo documento illustra quali tooexpect durante la migrazione del sito da servizi mobili di Azure tooAzure servizio App.

## <a name="what-does-migration-do"></a>Come la migrazione vengono tooyour sito
Migrazione del servizio Mobile di Azure attiva il servizio Mobile in un [Azure App Service] app senza influire sul codice hello.  Gli hub di notifica, la connessione dati SQL, le impostazioni di autenticazione, i processi pianificati e il nome di dominio rimangono invariati.  Client mobili utilizzando il servizio Mobile di Azure continua a funzionare normalmente toooperate.  Migrazione riavvia il servizio una volta trasferiti tooAzure servizio App.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Perché eseguire la migrazione del sito
È consigliabile eseguire la migrazione del servizio Mobile di Azure tootake sfruttare hello funzionalità di servizio App di Azure, tra cui:

* Nuove funzionalità host, come [Processi Web] e [nomi di dominio personalizzati].
* Connettività tooyour risorse locali utilizzando [VNet] inoltre troppo[connessioni ibride].
* Monitoraggio e risoluzione dei problemi con New Relic o [Application Insights].
* Strumenti DevOps incorporati, tra cui [gli slot di gestione temporanea], rollback e test nell'ambiente di produzione.
* [Scalabilità automatica], bilanciamento del carico e [monitoraggio delle prestazioni].

Per ulteriori informazioni sui vantaggi di hello di servizio App di Azure, vedere hello [vs servizi mobili. e il servizio app].

## <a name="before-you-begin"></a>Prima di iniziare
Prima di iniziare qualsiasi attività importante nel sito, è consigliabile eseguire un backup degli script e del database SQL del servizio mobile.

## <a name="migrating-site"></a>Migrazione dei siti
il processo di migrazione Hello esegue la migrazione di tutti i siti in una singola regione di Azure.

toomigrate del sito:

1. Accedi toohello [portale di Azure classico].
2. Selezionare un servizio Mobile nell'area di hello desiderato toomigrate.
3. Fare clic su hello **eseguire la migrazione del servizio tooApp** pulsante.

   ![Hello pulsante Esegui migrazione][0]
4. Finestra di dialogo hello migrazione tooApp servizio di lettura.
5. Immettere il nome di hello del servizio Mobile nell'apposita casella hello.  Ad esempio, se il nome di dominio è contoso.azure mobile.net, quindi immettere *contoso* nell'apposita casella hello.
6. Fare clic su pulsante segni di graduazione hello.

Monitorare lo stato di hello migrazione hello in Monitoraggio attività di hello. Il sito è elencato come *migrazione* in hello portale classico di Azure.

  ![Monitoraggio dell'attività di migrazione][1]

Ogni migrazione può richiedere 3 minuti too15 per ogni servizio mobile viene eseguita la migrazione.  Il sito rimane disponibile durante la migrazione di hello.
Il sito viene riavviato alla fine di hello del processo di migrazione hello.  Hello sito non è disponibile durante il processo di riavvio hello, che hanno un paio di secondi di durata.

## <a name="finalizing-migration"></a>Finalizzazione hello migrazione
Pianificare tootest il sito da un client mobile alla conclusione hello del processo di migrazione hello.  Verificare che è possibile eseguire tutte le azioni client comuni senza modifiche toohello client mobili.  

### <a name="update-app-service-tier"></a>Selezionare un piano tariffario appropriato per il servizio app
Si dispone di maggiore flessibilità di prezzo dopo la migrazione tooAzure servizio App.

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **piano di servizio App** nel menu Impostazioni hello.
5. Fare clic su hello **tariffario** riquadro.
6. Fare clic su requisiti di hello riquadro tooyour appropriata, quindi fare clic su **selezionare**.  Potrebbe essere necessario tooClick **visualizzare tutti** hello toosee disponibile livelli di prezzo.

Come punto di partenza, è consigliabile hello livelli seguenti:

| Piano tariffario del servizio mobile | Piano tariffario del servizio app |
|:--- |:--- |
| Free |F1 Gratuito |
| Basic |B1 Basic |
| Standard |S1 Standard |

È una notevole flessibilità nella scelta hello destra piano tariffario per l'applicazione.  Fare riferimento troppo[prezzi del servizio App] ulteriori dettagli sui prezzi di hello del nuovo servizio App.

> [!TIP]
> livello Standard di servizio App Hello contiene funzioni di accesso toomany se si desidera toouse, tra cui [gli slot di gestione temporanea], i backup automatici e il ridimensionamento automatico.  Mentre si è presente un'occhiata nuove funzionalità di hello.
>
>

### <a name="review-migration-scheduler-jobs"></a>Esaminare i processi dell'utilità di pianificazione di eseguire la migrazione di hello
I processi dell'utilità di pianificazione non saranno visibili fino a circa 30 minuti dopo la migrazione.  I processi pianificati continuano toorun in background hello.
tooview i processi pianificati vengono nuovamente visibile:

1. Accedi toohello [portale di Azure].
2. Selezionare **Sfoglia >**, immettere **pianificazione** in hello *filtro* casella, quindi selezionare **raccolte dell'utilità di pianificazione**.

Dopo la migrazione è disponibile un numero limitato di processi dell'utilità di pianificazione gratuiti.  Esaminare le informazioni sull'utilizzo e hello [piani dell'utilità di pianificazione di Azure].

### <a name="configure-cors"></a>Configurare la condivisione CORS se necessario
Cross-origin resource Sharing, condivisione è tooallow una tecnica tooaccess un sito Web un'API Web in un dominio diverso.  Se si usano servizi mobili di Azure con un sito Web associato, è necessario tooconfigure CORS come parte della migrazione hello.  Se si accede a servizi mobili di Azure in modo esclusivo da dispositivi mobili, quindi CORS non è necessario configurarla solo in rari casi toobe.

Le impostazioni CORS migrate sono disponibili come hello **MS_CrossDomainWhitelist** impostazione dell'App.  toomigrate il toohello sito funzionalità CORS del servizio App:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **CORS** nel menu hello API.
5. Immettere tutte le origini consentite nella casella hello fornita, premendo INVIO dopo ciascun.
6. Quando l'elenco di origini consentite è corretta, fare clic su pulsante Salva hello.

> [!TIP]
> Uno dei vantaggi di hello dell'utilizzo di un servizio App di Azure è possibile eseguire il sito web e il servizio mobile in hello nello stesso sito.  Per ulteriori informazioni, vedere hello [passaggi successivi](#next-steps) sezione.
>
>

### <a name="download-publish-profile"></a>Scaricare un nuovo profilo di pubblicazione
profilo di pubblicazione Hello del sito viene modificato durante la migrazione del servizio App tooAzure.  Se si intende toopublish il sito da Visual Studio, è necessario un nuovo profilo di pubblicazione.  toodownload hello nuovo profilo di pubblicazione:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. Fare clic su **Recupera profilo di pubblicazione**.

file PublishSettings Hello è scaricato tooyour computer.  In genere è denominato *nomesito*.PublishSettings.  Hello Importa le impostazioni nel progetto esistente di pubblicazione:

1. Aprire Visual Studio e il progetto di Servizi mobili di Azure.
2. Pulsante destro del mouse sul progetto in hello **Esplora** e selezionare **pubblica...**
3. Fare clic su **Importa**.
4. Fare clic su **Sfoglia** e selezionare il file delle impostazioni di pubblicazione scaricato.  Fare clic su **OK**
5. Fare clic su **convalida connessione** tooensure hello lavoro di impostazioni di pubblicazione.
6. Fare clic su **pubblica** toopublish del sito.

## <a name="working-with-your-site"></a>Uso del sito dopo la migrazione
Iniziare a utilizzarla con il nuovo servizio App in hello [portale di Azure] post-migrazione.  di seguito Hello sono alcune note sulle operazioni specifiche di hello utilizzato tooperform [portale di Azure classico], insieme con i rispettivi equivalenti di servizio App.

### <a name="publishing-your-site"></a>Download e pubblicazione del sito di cui è stata eseguita la migrazione
Il sito è disponibile tramite Git o FTP e può essere pubblicato nuovamente con vari meccanismi, inclusi WebDeploy, TFS, Mercurial, GitHub e FTP.  le credenziali di distribuzione Hello vengono migrate con il resto di hello del sito.  Se le credenziali di distribuzione non sono state impostate o non sono disponibili, è possibile reimpostarle:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **le credenziali di distribuzione** in hello dal menu di pubblicazione.
5. Immettere le credenziali di distribuzione nuovo hello nelle caselle di hello fornite, quindi fare clic sul pulsante Salva hello.

È possibile utilizzare questi siti di hello tooclone credenziali con git o configurare distribuzioni automatiche da GitHub, TFS o Mercurial.  Per ulteriori informazioni, vedere hello [documentazione sulla distribuzione di servizio App di Azure].

### <a name="appsettings"></a>Impostazioni dell'applicazione
La maggior parte delle impostazioni di un servizio mobile di cui è stata eseguita la migrazione è disponibile in Impostazioni app.  È possibile ottenere un elenco di impostazioni applicazione hello da hello [portale di Azure].
tooview o modificare le impostazioni dell'app:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **le impostazioni dell'applicazione** nel menu Generale hello.
5. Scorrere sezione Impostazioni App toohello e individuare l'impostazione dell'app.
6. Fare clic su hello valore hello app impostazione tooedit hello.  Fare clic su **salvare** valore hello toosave.

È possibile aggiornare le impostazioni più app hello contemporaneamente.

> [!TIP]
> Sono disponibili due impostazioni applicazione con hello stesso valore.  Ad esempio, *ApplicationKey* e *MS\_ApplicationKey*.  Aggiornare entrambe le impostazioni dell'applicazione hello contemporaneamente.
>
>

### <a name="authentication"></a>Autenticazione
Tutte le impostazioni di autenticazione sono disponibili come impostazioni app nel sito di cui è stata eseguita la migrazione.  tooupdate le impostazioni di autenticazione, è necessario modificare le impostazioni di app appropriata.  Hello nella tabella seguente vengono mostrate hello app appropriata impostazioni per il provider di autenticazione:

| Provider | ID client | Client Secret | Altre impostazioni |
|:--- |:--- |:--- |:--- |
| Account Microsoft |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Nota: **MS\_AadTenants** viene archiviata come un elenco delimitato da virgole dei domini tenant (campi hello "Consentito tenant" nel portale di servizi mobili hello).

> [!WARNING]
> **Non utilizzare i meccanismi di autenticazione hello nel menu Impostazioni hello**
>
> Servizio App di Azure fornisce un "Nessun codice" autenticazione e autorizzazione sistema separato in hello *autenticazione / autorizzazione* menu impostazioni e hello (deprecato) *autenticazione Mobile* opzione nel menu Impostazioni hello.  Queste opzioni non sono compatibili con un servizio mobile di Azure di cui è stata eseguita la migrazione.  È possibile [aggiorna il sito](app-service-mobile-net-upgrading-from-mobile-services.md) tootake sfruttare l'autenticazione del servizio App di Azure hello.
>
>

### <a name="easytables"></a>Dati
Hello *dati* scheda nei servizi mobili è stata sostituita da *tabelle facile* all'interno di hello portale di Azure.  tooaccess tabelle semplice:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **tabelle facile** nel menu mobili hello.

È possibile aggiungere una tabella, fare clic su hello **Aggiungi** pulsante o accedere a una delle tabelle esistente, fare clic su un nome di tabella.  Da questo pannello è possibile eseguire una serie di operazioni, tra cui:

* Modifica delle autorizzazioni tabella
* La modifica di script operativi hello
* Gestione dello schema di tabella hello
* Eliminazione della tabella hello
* Cancellazione del contenuto di tabella hello
* Eliminazione di righe specifico della tabella hello

### <a name="easyapis"></a>API
Hello *API* scheda nei servizi mobili è stata sostituita da *API semplice* all'interno di hello portale di Azure.  tooaccess API semplice:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Fare clic su **API semplice** nel menu mobili hello.

Le API migrate sono già elencate nel pannello hello.  Dal pannello è anche possibile aggiungere un'API.  toomanage un'API specifica, fare clic su hello API.
Dal pannello nuova hello, è possibile modificare le autorizzazioni di hello e modificare script hello per hello API.

### <a name="on-demand-jobs"></a>Processi dell'Utilità di pianificazione
Tutti i processi dell'utilità di pianificazione sono disponibili tramite hello sezione raccolte processi dell'utilità di pianificazione.  tooaccess i processi dell'utilità di pianificazione:

1. Accedi toohello [portale di Azure].
2. Selezionare **Sfoglia >**, immettere **pianificazione** in hello *filtro* casella, quindi selezionare **raccolte dell'utilità di pianificazione**.
3. Selezionare hello raccolta processi per il sito.  È denominata *nomesito*-Processi.
4. Fare clic su **Impostazioni**.
5. Fare clic su **Processi dell'Utilità di pianificazione** in GESTISCI.

I processi pianificati vengono elencati con hello alla frequenza specificata prima della migrazione.  I processi su richiesta sono disabilitati.  toorun un processo su richiesta:

1. Selezionare il processo di hello desiderato toorun.
2. Se necessario, fare clic su **abilitare** processo hello tooenable.
3. Fare clic su **Impostazioni** e quindi su **Pianificazione**.
4. Selezionare la ricorrenza **Una sola volta** e quindi fare clic su **Salva**.

I processi su richiesta si trovano in `App_Data/config/scripts/scheduler post-migration`.  Si consiglia di convertire tutti i processi su richiesta troppo[Processi Web] o [funzioni].  Scrivere i nuovi processi dell'Utilità di pianificazione come [Processi Web] o [funzioni].

### <a name="notification-hubs"></a>Hub di notifica
Servizi mobili usa Hub di notifica per le notifiche push.  Hello seguendo le impostazioni dell'App viene utilizzati toolink hello tooyour Hub di notifica del servizio Mobile dopo la migrazione:

| Impostazione dell'applicazione | Descrizione |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Hello Namespace di Hub di notifica |
| **MS\_NotificationHubName** |Hello nome Hub di notifica |
| **MS\_NotificationHubConnectionString** |Stringa di connessione Hub di notifica Hello |
| **MS\_NamespaceName** |Alias per MS_PushEntityNamespace |

Hub di notifica viene gestita mediante hello [portale di Azure].  Si noti il nome dell'Hub di notifica hello (è possibile trovare questo usando le impostazioni dell'App hello):

1. Accedi toohello [portale di Azure].
2. Selezionare **Esplora>** e quindi **Hub di notifica**.
3. Fare clic su nome Hub di notifica hello associato al servizio mobile hello.

> [!NOTE]
> Se l'hub di notifica è di tipo "Misto", non è visibile.  Gli hub di notifica di tipo "Misto" utilizzano sia Hub di notifica che le funzionalità legacy del bus di servizio.  [Convertire gli spazi dei nomi di tipo Misto] prima di continuare.  Una volta completata la conversione di hello, l'hub di notifica viene visualizzata in hello [portale di Azure].
>
>

Per ulteriori informazioni, esaminare hello [gli hub di notifica] documentazione.

> [!TIP]
> Funzionalità di gestione degli hub di notifica di hello [portale di Azure] sono ancora in anteprima.  Hello [portale di Azure classico] rimane disponibile per la gestione di tutti gli hub di notifica.
>
>

### <a name="legacy-push"></a>Impostazioni push legacy
Se è stato configurato nel servizio mobile prima dell'introduzione di hello negli hub di notifica Push, si utilizza *push legacy*.  Se si usa il push e nella configurazione non è presente un hub di notifica, è probabile che si stia usando la funzione *push legacy*.  La migrazione di questa funzionalità viene eseguita insieme a tutte le altre.  Tuttavia, è consigliabile eseguire l'aggiornamento degli hub tooNotification subito dopo la migrazione di hello è stata completata.

In hello provvisorio, tutte le impostazioni di push legacy hello (con un'eccezione rilevante hello del certificato APN hello) sono disponibili nelle impostazioni dell'App.  Aggiornare il certificato APNS hello sostituendo hello file appropriato nel file System hello.

### <a name="app-settings"></a>Altre impostazioni app
Hello seguendo le impostazioni dell'app aggiuntive viene migrati dal servizio Mobile e sono disponibili in *impostazioni* > *impostazioni App*:

| Impostazione dell'applicazione | Descrizione |
|:--- |:--- |
| **MS\_MobileServiceName** |nome Hello dell'app |
| **MS\_MobileServiceDomainSuffix** |prefisso di dominio Hello. vale a dire azure-mobile.net |
| **MS\_ApplicationKey** |Chiave applicazione |
| **MS\_MasterKey** |Chiave master dell'app |

chiave applicazione Hello e la chiave master sono identica toohello le chiavi dell'applicazione dal servizio Mobile originale.  In particolare, hello chiave applicazione viene inviata da client mobili toovalidate l'uso di API portatili hello.

### <a name="cliequivalents"></a>Equivalenti della riga di comando
È possibile utilizzare più hello *azure mobile* comando toomanage il sito di servizi mobili di Azure.  Al contrario, molte funzioni sono state sostituite con hello *sito azure* comando.  Utilizzare hello equivalenti toofind tabella per i comandi comuni seguenti:

| Comando *azure mobile* | Comando *azure site* equivalente |
|:--- |:--- |
| mobile locations |site location list |
| mobile list |site list |
| mobile show *nome* |site show *nome* |
| mobile restart *nome* |site restart *nome* |
| mobile redeploy *nome* |site deployment redeploy *commitId* *nome* |
| mobile key set *nome* *tipo* *valore* |site appsetting delete *chiave* *nome* <br/> site appsetting add *chiave*=*valore* *nome* |
| mobile config list *nome* |site appsetting list *nome* |
| mobile config get *nome* *chiave* |site appsetting show *chiave* *nome* |
| mobile config set *nome* *chiave* |site appsetting delete *chiave* *nome* <br/> site appsetting add *chiave*=*valore* *nome* |
| mobile domain list *nome* |site domain list *nome* |
| mobile dominio add *nome* *dominio* |site domain add *dominio* *nome* |
| mobile domain delete *nome* |site domain delete *dominio* *nome* |
| mobile scale show *nome* |site show *nome* |
| mobile scale change *nome* |site scale mode *modalità* *nome* <br /> site scale instances *istanze* *nome* |
| mobile appsetting list *nome* |site appsetting list *nome* |
| mobile appsetting add *nome* *chiave* *valore* |site appsetting add *chiave*=*valore* *nome* |
| mobile appsetting delete *nome* *chiave* |site appsetting delete *chiave* *nome* |
| mobile appsetting show *nome* *chiave* |site appsetting delete *chiave* *nome* |

Aggiornare l'autenticazione o le notifiche push impostazioni aggiornando hello impostazione applicazione appropriata.
Modificare i file e pubblicare il sito tramite Git o FTP.

### <a name="diagnostics"></a>Diagnostica e registrazione
Nel servizio app di Azure la registrazione diagnostica è generalmente disabilitata.  registrazione diagnostica tooenable:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. pannello impostazioni Hello viene aperto per impostazione predefinita.
4. Selezionare **i log di diagnostica** nel menu funzionalità hello.
5. Fare clic su **ON** per hello seguenti registri: **registrazione delle applicazioni (file System)**, **messaggi di errore dettagliati**, e **traccia richieste non riuscita**
6. Fare clic su **File System** per la registrazione del server Web.
7. Fare clic su **Save**

tooview hello registri:

1. Accedi toohello [portale di Azure].
2. Selezionare **tutte le risorse** o **servizi App** quindi hello nome del servizio Mobile migrati.
3. Fare clic su hello **strumenti** pulsante
4. Selezionare **flusso del Log** nel menu NOTERÀ hello.

I log vengono visualizzati nella finestra di hello di generazione.  È anche possibile scaricare i log di hello per analisi successive utilizzando le credenziali di distribuzione. Per ulteriori informazioni, vedere hello [registrazione] documentazione.

## <a name="known-issues"></a>Problemi noti
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>L'eliminazione del clone di un'app per dispositivi mobili di cui è stata eseguita la migrazione provoca un'interruzione del sito
Se si clona il servizio mobile migrato utilizzando Azure PowerShell, quindi Elimina hello clone, hello voce DNS per il servizio di produzione viene rimosso.  Il sito è non essere accessibile da Internet hello.  

Risoluzione: Se si desidera che il sito tooclone, farlo tramite il portale di hello.

### <a name="changing-webconfig-does-not-work"></a>Le modifiche a Web.config non funzionano
Se si dispone di un sito ASP.NET, cambia toohello `Web.config` file non venga applicato.  Compila un adatto Hello Azure App Service `Web.config` file durante il runtime di servizi mobili di avvio toosupport hello.  È possibile eseguire l'override di alcune impostazioni, ad esempio le intestazioni personalizzate, tramite un file di trasformazione XML.  Creare un file denominato in `applicationHost.xdt` -questo file deve finire in hello `D:\home\site` directory hello servizio di Azure.  Caricare il file `applicationHost.xdt` tramite uno script di distribuzione personalizzato o direttamente tramite Kudu.  Hello seguito è riportato un documento di esempio:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Per ulteriori informazioni, vedere hello [XDT trasformare esempi] documentazione su GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Migrazione di servizi mobili non è possibile aggiungere tooTraffic Manager
Quando si crea un profilo di Traffic Manager, è possibile scegliere direttamente un profilo toohello migrati servizio mobile.  È necessario usare un "endpoint esterno".  L'endpoint esterno può essere aggiunto solo tramite PowerShell.  Per altre informazioni, vedere l'[esercitazione su Gestione traffico](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Passaggi successivi
Ora che l'applicazione è tooApp stata eseguita la migrazione del servizio, sono disponibili anche altre funzionalità, che è possibile usare:

* Distribuzione [gli slot di gestione temporanea] consentono di sito di tooyour toostage modifiche ed eseguire A / B test.
* [Processi Web] consente di sostituire i processi pianificati su richiesta.
* È possibile [continuamente distribuire] sito mediante il collegamento del sito tooGitHub, TFS o Mercurial.
* È possibile utilizzare [Application Insights] toomonitor del sito.
* Server del sito Web e un'API di dispositivi mobili da hello stesso codice.

### <a name="upgrading-your-site"></a>L'aggiornamento del tooAzure del sito di servizi mobili Mobile App SDK
* Per i progetti server basato su Node.js, hello nuovi [Mobile App Node.js SDK] fornisce numerose nuove funzionalità. Ad esempio, è possibile ora eseguire sviluppi e debug locali, utilizzare qualsiasi versione Node.js successiva alla 0.10 e personalizzare con qualsiasi middleware Express.js.
* Per. Progetti server basato su NET, hello nuovi [pacchetti NuGet SDK di App mobili](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) dispone di maggiore flessibilità sulle dipendenze di NuGet.  Questi pacchetti supportano l'autenticazione di servizio App nuovo hello e compongono un qualsiasi progetto ASP.NET. Per ulteriori informazioni sull'aggiornamento, vedere [aggiornare il tooApp .NET il servizio Mobile esistente servizio](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Prezzi del servizio app]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Scalabilità automatica]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[documentazione sulla distribuzione di servizio App di Azure]: ../app-service-web/web-sites-deploy.md
[portale di Azure classico]: https://manage.windowsazure.com
[portale di Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[piani dell'utilità di pianificazione di Azure]: ../scheduler/scheduler-plans-billing.md
[continuamente distribuire]: ../app-service-web/app-service-continuous-deployment.md
[Convertire gli spazi dei nomi di tipo Misto]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[nomi di dominio personalizzati]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[disponibilità generale di servizio App di Azure]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[connessioni ibride]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[registrazione]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Mobile App Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[vs servizi mobili. e il servizio app]: app-service-mobile-value-prop-migration-from-mobile-services.md
[gli hub di notifica]: ../notification-hubs/notification-hubs-push-notification-overview.md
[monitoraggio delle prestazioni]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[gli slot di gestione temporanea]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[Processi Web]: ../app-service-web/websites-webjobs-resources.md
[XDT trasformare esempi]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[funzioni]: ../azure-functions/functions-overview.md
