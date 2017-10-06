---
title: aaaWork con esistente locale server proxy e Azure AD | Documenti Microsoft
description: Descrive come toowork con esistente proxy server locali.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Usare server proxy locali esistenti

Questo articolo viene illustrato come toowork di connettori Proxy di applicazione di Azure Active Directory (Azure AD) tooconfigure con i server proxy in uscita. È rivolto ai clienti con ambienti di rete che dispongono di proxy esistenti.

Iniziamo esaminando questi scenari di distribuzione principali:
* Configurare i connettori toobypass i proxy in uscita in locale.
* Configurare i connettori toouse un Proxy di applicazione AD Azure di tooaccess proxy in uscita.

Per ulteriori informazioni sui connettori, vedere [Informazioni sui connettori proxy di applicazione di Azure AD](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Configurare il proxy in uscita hello

Se si dispone di un proxy in uscita nell'ambiente in uso, è possibile utilizzare un account proxy in uscita hello tooconfigure di autorizzazioni appropriate. Poiché il programma di installazione hello viene eseguito nel contesto di hello dell'utente hello che sta eseguendo l'installazione di hello, è possibile controllare configurazione hello utilizzando Microsoft Edge o un altro browser Internet.

impostazioni del proxy tooconfigure hello in Microsoft Edge:

1. Andare troppo**impostazioni** > **impostazioni avanzate di visualizzazione** > **aprire le impostazioni del Proxy** > **l'installazione manuale del Proxy** .
2. Impostare **utilizza un server proxy** troppo**su**selezionare hello **non utilizzare un server proxy hello per indirizzi locali (intranet)** casella di controllo, quindi scegliere Modifica hello indirizzo e porta tooreflect il server proxy locale.
3. Specificare le impostazioni del proxy necessarie hello.

   ![Finestra di dialogo per le impostazioni proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Ignorare i proxy in uscita

I connettori sono componenti del sistema operativo sottostanti che creano le richieste in uscita. Questi componenti tentano automaticamente di un server proxy nella rete hello toolocate. Utilizzano il rilevamento automatico WPAD (Web Proxy), se è abilitata nell'ambiente di hello.

componenti del sistema operativo Hello tentano toolocate un server proxy eseguendo una ricerca DNS per wpad.domainsuffix. Se viene risolto in DNS, IP toohello viene quindi eseguita una richiesta HTTP indirizzo per WPAD. La richiesta diventa script di configurazione proxy hello nell'ambiente in uso. connettore di Hello Usa questo tooselect di script, un server proxy in uscita. Tuttavia, connettore traffico potrà comunque non passa attraverso, a causa delle impostazioni di configurazione aggiuntive necessarie sul proxy hello.

È possibile configurare hello connettore toobypass toohello connettività Azure di indirizzare il tooensure proxy locale che utilizza i servizi. Questo approccio è consigliato (se i criteri di rete consentono), in quanto significa che si dispone di una minore toomaintain di configurazione.

utilizzo di proxy in uscita toodisable per connettore hello, modificare il file di C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config hello e hello *system.net* sezione illustrata in questo esempio di codice :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure che il servizio di aggiornamento del connettore hello ignora inoltre proxy hello, creare un file di ApplicationProxyConnectorUpdaterService.exe.config toohello modifica simile all'aggiornamento del connettore Proxy C:\Program Files\Microsoft AAD App.

Essere certi toomake copie dei file originali hello, nel caso in cui è necessario toorevert toohello file con estensione config predefinito.

## <a name="use-hello-outbound-proxy-server"></a>Utilizza un server proxy in uscita hello

In alcuni ambienti richiedono tutti toogo il traffico in uscita tramite un proxy in uscita, senza eccezione. Di conseguenza, ignorando il proxy di hello non è un'opzione.

È possibile configurare hello connettore traffico toogo tramite proxy in uscita hello, come illustrato nel seguente diagramma hello:

 ![Configurazione connettore traffico toogo tramite un tooAzure proxy in uscita AD Proxy dell'applicazione](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Di conseguenza di ottenere solo il traffico in uscita, non è tooconfigure è necessario l'accesso attraverso i firewall in ingresso.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Passaggio 1: Configurare il connettore di hello e relativi servizi toogo tramite proxy in uscita hello

Come illustrato in precedenza, se WPAD è abilitata nell'ambiente di hello e configurata in modo appropriato, connettore hello rileverà automaticamente i server e tentativo toouse di proxy in uscita di hello è. Tuttavia, è possibile configurare in modo esplicito hello connettore toogo tramite un proxy in uscita.

toodo in tal caso, modificare il file di C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config hello e aggiungere hello *system.net* sezione illustrata in questo esempio di codice. Modifica *proxyserver:8080* tooreflect il nome del server proxy locale o un indirizzo IP e hello porta che è in ascolto.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Successivamente, configurare proxy hello toouse del servizio di aggiornamento del connettore hello apportando una modifica toohello di file analoghi si trova in C:\Program Files\Microsoft AAD App Proxy connettore Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Passaggio 2: Configurare il traffico di hello proxy tooallow dal connettore hello e i servizi correlati tooflow tramite

Esistono quattro aspetti tooconsider proxy in uscita hello:
* Regole in uscita del proxy
* Autenticazione proxy
* Porte proxy
* Ispezione SSL

#### <a name="proxy-outbound-rules"></a>Regole in uscita del proxy
Consenti accesso toohello seguendo gli endpoint per l'accesso al servizio connettore:

* *.msappproxy.net
* *.servicebus.windows.net

Per la registrazione iniziale, Consenti accesso toohello seguenti endpoint:

* login.windows.net
* login.microsoftonline.com

Se non è possibile consentire la connettività di dominio completo e intervalli IP toospecify invece è necessario, è possibile utilizzare queste opzioni:

* Consentire l'accesso in uscita di hello connettore tooall destinazioni.
* Consentire l'accesso in uscita al connettore hello troppo[intervalli IP Data Center di Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). sfida di Hello con elenco hello intervalli IP di Data Center di Azure consiste nel fatto che viene aggiornato ogni settimana. È necessario tooput un processo in tooensure sul posto che le regole di accesso vengono aggiornate di conseguenza.

#### <a name="proxy-authentication"></a>Autenticazione proxy

L'autenticazione proxy non è attualmente supportata. Il Consiglio corrente è destinazioni di Internet toohello tooallow hello connettore l'accesso anonimo.

#### <a name="proxy-ports"></a>Porte proxy

connettore Hello consente le connessioni in uscita basata su SSL utilizzando il metodo CONNECT hello. Questo metodo imposta essenzialmente un tunnel tramite proxy in uscita hello. Configurare hello proxy server tooallow tunneling tooports 443 e 80.

>[!NOTE]
>Quando il bus di servizio viene eseguito su HTTPS, usa la porta 443. Tuttavia, per impostazione predefinita, Bus di servizio vengono tentate connessioni TCP dirette e ritorna tooHTTPS solo se si verifica un errore di connettività diretta.

tooensure hello Bus di servizio, il traffico viene inviato tramite server proxy in uscita hello, verificare che tale connettore hello non può connettersi direttamente toohello servizi di Azure per le porte 9350, 9352 e 5671.

#### <a name="ssl-inspection"></a>Ispezione SSL
Non utilizzare ispezione SSL per il traffico di connettore hello, perché causa problemi per il traffico connettore hello.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Risolvere i problemi relativi al connettore proxy e alla connettività del servizio
A questo punto dovrebbe essere tutto il traffico che passano attraverso il proxy di hello. Se si verificano problemi, dovrebbe consentire di hello le seguenti informazioni sulla risoluzione dei problemi.

Hello tooidentify modo migliore e risolvere i problemi di connettività del connettore problemi è una rete di acquisizione nel servizio del connettore hello durante l'avvio del servizio del connettore hello tootake. Questa può essere un'attività molto complessa, quindi vediamo alcuni semplici suggerimenti sull'acquisizione e il filtraggio delle tracce di rete.

È possibile utilizzare hello monitoraggio dello strumento di propria scelta. Ai fini di hello di questo articolo, abbiamo utilizzato Microsoft Network Monitor 3.4. È possibile [scaricarlo da Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

esempi di Hello e i filtri utilizzati in hello le sezioni seguenti sono specifici tooNetwork monitoraggio, ma i principi di hello possono essere applicato tooany lo strumento di analisi.

### <a name="take-a-capture-by-using-network-monitor"></a>Eseguire un'acquisizione con Network Monitor

toostart un'acquisizione:

1. Aprire Network Monitor e fare clic su **New Capture** (Nuova acquisizione).
2. Fare clic su hello **avviare** pulsante.

   ![Finestra di Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Dopo aver completato un'acquisizione, fare clic su hello **arrestare** tooend pulsante è.

### <a name="take-a-capture-of-connector-traffic"></a>Eseguire un'acquisizione del traffico del connettore

Per risolvere il problema iniziale, eseguire hello alla procedura seguente:

1. Da services.msc, arrestare il servizio di Azure Active Directory Application Proxy Connector hello.
2. Avviare l'acquisizione di rete hello.
3. Avviare il servizio di Azure Active Directory Application Proxy Connector hello.
4. Arrestare l'acquisizione di rete hello.

   ![Servizio connettore proxy applicazione di Azure AD in services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Esaminare le richieste di hello dal server proxy di hello connettore toohello

Ora che hai un'acquisizione di rete, si è pronti toofilter è. Hello toolooking chiave traccia hello è comprendere in che modo toofilter hello acquisire.

Un filtro è il seguente (dove 8080 è porta del servizio proxy hello):

**(http.Request or http.Response) and tcp.port==8080**

Se si immette questo filtro in hello **filtro di visualizzazione** window e selezionare **applica**, vengono applicati i filtri traffico hello acquisito in base al filtro hello.

Hello filtro precedente viene semplicemente hello richieste e risposte HTTP da e verso la porta proxy hello. Per l'avvio di un connettore in connettore di hello è toouse configurato un server proxy, il filtro hello mostrerebbe simile al seguente:

 ![Elenco di esempio di richieste e risposte HTTP filtrate](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Ora in modo specifico cercano le richieste di connessione che mostrano la comunicazione con i server proxy hello hello. Al completamento dell'operazione si ottiene una risposta HTTP affermativa (200).

Se viene visualizzato altri codici di risposta, ad esempio 407 o 502 proxy hello è che richiede l'autenticazione o non consenta il traffico di hello per altri motivi. A questo punto ci si rivolge al team di supporto del server proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Identificare tentativi di connessione TCP non riusciti

Hello altro scenario comune che potrebbe essere interessati è quando hello connettore tenta tooconnect direttamente, ma non è riuscito.

Un altro filtro di monitoraggio della rete che consente di identificare il problema si tooeasily è:

**property.TCPSynRetransmit**

Un pacchetto SYN è primo pacchetto hello inviati tooestablish una connessione TCP. Se il pacchetto non restituisce una risposta, è contrassegnandola hello SYN. Utilizzare qualsiasi SYNs ritrasmessi hello toosee filtro precedente. Controllare quindi se questi SYNs corrispondono tooany relativi al connettore traffico.

Hello esempio seguente viene illustrato un tentativo di connessione non riuscita porta Bus tooService 9352:

 ![Risposta di esempio per un tentativo di connessione non riuscito](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Se visualizzato qualcosa di simile hello prima risposta, connettore hello sta tentando di toocommunicate direttamente con hello Azure Service Bus di servizio. Se si prevede di hello connettore toomake connessioni dirette toohello Azure services, questa risposta è una chiara indicazione che si verifica un problema di rete o un firewall.

>[!NOTE]
>Se si toouse configurato un server proxy, la risposta potrebbe indicare che il Bus di servizio tenta una connessione diretta TCP prima del passaggio tooattempting una connessione tramite HTTPS.
>

L'analisi delle tracce di rete non è per tutti. Ma può essere un strumento prezioso tooget rapidamente le informazioni su cosa accade in rete.

Se si continua toostruggle con problemi di connettività di connettore, è possibile creare un ticket con il team di supporto. il team di Hello consente di semplificare la risoluzione del problema.

Per informazioni sulla risoluzione degli errori con il connettore del proxy applicazione, vedere [Risolvere i problemi del proxy applicazione](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Passaggi successivi

[Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md)<br>
[Come toosilently installa hello connettore del Proxy dell'applicazione AD Azure](active-directory-application-proxy-silent-installation.md)
