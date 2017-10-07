---
title: aaaCloud considerazioni sulla Privacy e sulla sicurezza di individuazione di App | Documenti Microsoft
description: Questo argomento descrive la sicurezza hello e sulla privacy considerazioni correlate tooCloud App Discovery.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Considerazioni sulla sicurezza e sulla privacy in Cloud App Discovery
Microsoft è eseguito il commit tooprotecting la privacy degli utenti e proteggere i dati, offrendo al contempo software e servizi che consentono di gestire la sicurezza hello dell'organizzazione.  
È possibile riconoscere che, quando si affidano i dati tooothers, tale trust richiede investimenti finalizzati alla progettazione di sicurezza rigorose e competenze tooback è.
Microsoft aderisce linee guida di sicurezza e conformità toostrict dal software sicuro lo sviluppo del ciclo di vita consigliate toooperating un servizio.  
La sicurezza e la protezione dei dati sono altamente prioritarie per Microsoft.

Questo argomento descrive le modalità di raccolta, elaborazione e protezione dei dati in Azure Active Directory Cloud App Discovery.

## <a name="overview"></a>Panoramica
Cloud App Discovery è una funzionalità di Azure AD ed è ospitata in Microsoft Azure.  
agente di endpoint Cloud App Discovery Hello è toocollect utilizzati dati di individuazione dell'applicazione dai computer gestiti IT.  
Hello i dati raccolti vengono inviati in modo sicuro tramite un servizio di Azure AD Cloud App Discovery di toohello canale crittografato.  
Hello dati di Cloud App Discovery per un'organizzazione sono quindi visibile nel portale di Azure hello. 

![Funzionamento di Cloud App Discovery](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Hello nelle sezioni seguenti illustrano flusso hello di informazioni e descrivono viene protetto durante lo spostamento dal servizio Cloud App Discovery toohello di organizzazione e infine il portale di Cloud App Discovery toohello.

## <a name="collecting-data-from-your-organization"></a>Raccolta di dati dall'organizzazione
In Cloud App discovery funzionalità tooget informazioni approfondite del ordine toouse Azure Active Directory relative hello applicazioni usate dai dipendenti dell'organizzazione, è necessario toofirst distribuire hello Azure AD Cloud App Discovery endpoint agent toomachines all'interno dell'organizzazione.

Gli amministratori di tenant di Azure Active Directory hello (o un loro delegato) possono scaricare pacchetto di installazione dell'agente di hello da hello portale di Azure. agente Hello può essere manualmente installato o installato in più computer nell'organizzazione di hello tramite SCCM o criteri di gruppo.

Per altre istruzioni sulle opzioni di distribuzione, vedere la [guida alla distribuzione di Criteri di gruppo in Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Dati raccolti dall'agente hello
Hello descritte nell'elenco di hello seguito raccolti dall'agente di hello quando una connessione viene effettuata tooa applicazione Web. Hello informazioni vengono raccolte solo per le applicazioni, tale messaggio per l'amministratore ha configurato per l'individuazione.  
È possibile modificare l'elenco di hello delle App cloud hello monitoraggi agente tramite Pannello di Cloud App Discovery hello in hello Microsoft [portale di Azure](https://portal.azure.com/)in **impostazioni**->**dati Raccolta**->**elenco raccolta di App**. Per informazioni dettagliate, vedere [Introduzione a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Categoria di informazioni**: informazioni utente  
**Descrizione**:  
nome utente di Windows Hello del processo di hello apportate a un'applicazione Web di destinazione toohello richiesta (ad esempio: dominio omeutente) nonché l'ID di sicurezza Windows (SID) dell'utente hello hello.

**Categoria delle informazioni**: informazioni sui processi  
**Descrizione**:  
nome Hello del processo di hello che ha effettuato l'applicazione Web di destinazione di hello richiesta toohello (ad esempio: "iexplore.exe")

**Categoria delle informazioni**: informazioni sui computer  
**Descrizione**:  
nome NetBIOS del Hello computer in cui hello è installato l'agente.

**Categoria delle informazioni**: informazioni sul traffico app  
**Descrizione**: 

Hello le seguenti informazioni di connessione:

* origine Hello (computer locale) e gli indirizzi IP di destinazione e i numeri di porta
* indirizzo IP pubblico Hello dell'organizzazione hello tramite cui hello richiesta si estende.
* Hello ora di hello richiesta
* volume Hello del traffico inviato e ricevuto
* versione di Hello IP (4 o 6)
* Per solo le connessioni TLS: nome host di destinazione hello dall'estensione di indicazione nome Server hello o certificato hello del server.

Hello informazioni HTTP seguenti:

* Metodo (GET, POST e così via)
* Protocollo (HTTP/1.1 e così via)
* Stringa agente utente
* Nome host
* URI di destinazione (esclusa la stringa di query)
* Informazioni sul tipo di contenuto
* Informazioni sull'URL di referrer (esclusa la stringa di query)

> [!NOTE]
> Hello informazioni HTTP precedenti verrà raccolti per tutte le connessioni non crittografate.
> Per le connessioni TLS, queste informazioni vengono acquisite solo quando è l'impostazione 'Ispezione approfondita' hello nel portale di hello. impostazione di Hello è impostata su 'ON' per impostazione predefinita.
> Per informazioni dettagliate, vedere di seguito e vedere [Introduzione a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Inoltre toohello dati che l'agente di hello raccoglie hello dell'attività di rete, inoltre raccoglie informazioni anonime sulla configurazione hardware e software hello segnalazioni degli errori e informazioni sull'utilizzo dell'agente di hello.


### <a name="how-hello-agent-works"></a>Funzionamento dell'agente di hello
installazione dell'agente Hello include due componenti:

* Un componente per la modalità utente
* Un componente per il driver della modalità kernel (driver della Piattaforma filtro Windows)

Alla prima installazione di agente hello archivia un certificato attendibile di specifiche del computer nel computer di hello cui si utilizza quindi tooestablish una connessione sicura con il servizio Cloud App Discovery hello.  
agente Hello recupera periodicamente la configurazione dei criteri da hello servizio Cloud App Discovery tramite questa connessione sicura.  
criteri di Hello includono informazioni quali toomonitor applicazioni cloud e indica se l'aggiornamento automatico deve essere abilitato, tra l'altro.

Come il traffico Web inviato e ricevuto nel computer di hello da Internet Explorer e Chrome, agente di Cloud App Discovery hello analizza il traffico hello ed estrae hello metadati rilevanti (vedere hello **dati raccolti dall'agente hello** sezione sopra).  
Ogni minuto, agente hello carica hello raccolti metadati toohello servizio Cloud App Discovery tramite un canale crittografato.

Hello driver componente intercetta il traffico crittografato hello e si inserisce nel flusso crittografato hello. Altre informazioni, vedere hello **intercettazione dei dati da connessioni crittografate (ispezione approfondita)** sezione riportata di seguito.

### <a name="respecting-user-privacy"></a>Rispetto della privacy degli utenti
L'obiettivo è tooprovide amministratori hello strumenti tooset hello equilibrio informazioni dettagliate nell'applicazione dell'utilizzo e privacy degli utenti come appropriato per l'organizzazione. fine toothat, forniamo hello manopole nella pagina Impostazioni hello hello portale seguente:

* **Raccolta dei dati**: gli amministratori possono scegliere toospecify quali applicazioni o categorie di applicazione si desiderano i dati di individuazione tooget in.
* **Ispezione approfondita**: se agente hello raccoglie il traffico HTTP per le connessioni SSL/TLS, gli amministratori possono scegliere toospecify (noto anche come **'Ispezione approfondita'**). Ulteriori informazioni su questo nella sezione successiva hello.
* **Opzioni di consenso**: gli amministratori possono utilizzare hello Cloud App Discovery portale toochoose se gli utenti toonotify hello di raccolta dei dati dall'agente di hello, e se l'utente toorequire acconsentire prima dell'avvio di agente di hello la raccolta dei dati utente.

agente di endpoint Cloud App Discovery Hello raccoglie le informazioni di hello descritte in hello **dati raccolti dall'agente hello** sezione precedente.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Intercettazione dei dati da connessioni crittografate (Ispezione approfondita)
Come menzionato in precedenza, gli amministratori possono configurare hello agente toomonitor dati connessioni crittografate ('ispezione approfondita'). TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) è uno dei hello un protocolli più comuni in uso nel hello Internet oggi. Per la crittografia delle comunicazioni con TLS, un client può stabilire un canale di comunicazione protetta e privata con un server web. TLS fornisce protezione essenziale per passare le credenziali di autenticazione ed evitare la diffusione di informazioni riservate hello.

Mentre hello end-to-end canale crittografato protetto fornita da TLS consente la protezione della privacy e sicurezza importanti, protocollo hello è spesso sfruttato per scopi dannosi o nefandi. Molto in tal caso, infatti, che TLS viene spesso definito tooas hello "universal firewall-bypass protocollo". radice Hello problema hello è che la maggior parte dei firewall sono la comunicazione TLS tooinspect non è possibile perché i dati a livello di applicazione hello sono crittografati con SSL. Pertanto, gli utenti malintenzionati spesso sfruttano certi che anche hello più intelligente a livello di applicazione i firewall sono completamente nascosta tooTLS e devono inoltrare semplicemente la comunicazione TLS tra host utente tooa payload dannoso toodeliver TLS. Gli utenti finali spesso sfruttare i controlli di accesso toobypass TLS imposti da server proxy, utilizzarlo tooconnect toopublic proxy e firewall aziendali e dei protocolli non TLS attraverso il firewall hello che in caso contrario potrebbero essere bloccati dai criteri di tunneling.

Ispezione approfondita consente tooact agente Cloud App Discovery di hello come un attendibile man-in-the-middle. Quando viene effettuata una richiesta client tooaccess HTTPS la risorsa protetta, il driver di agente di Endpoint hello intercetta connessione hello e stabilisce un nuovo tooretrieves di server di destinazione toohello connessione il proprio certificato SSL per conto del client hello. agente di Hello verifica quindi che il certificato di hello può essere considerati attendibili (il controllo non è stato revocato e l'esecuzione di altri controlli di certificato) e se questi passi, hello agente Endpoint hello informazioni vengono copiate dal certificato del server hello e crea il proprio certificato del server, noto come certificato intercettazione - utilizzo di tali informazioni. certificato di intercettazione Hello è firmato il volo dall'agente di endpoint hello con un certificato radice, che viene installato nell'archivio certificati attendibili di Windows hello. Questo certificato radice autofirmato è contrassegnato come non esportabile e ACL era tooadministrators. Si tratta di toonever previsto lasciare hello macchina in cui è stato creato. Quando l'applicazione client hello dell'utente finale riceve il certificato di intercettazione hello, correttamente è possibile convalidare la catena di certificati hello tutti hello modo toohello autorità di certificazione, verrà considerato attendibile. Questo processo è quasi completamente trasparente dal punto di vista dell'utente finale, ma occorre tenere presente alcuni aspetti, come descritto di seguito.

Abilitando l'opzione ispezione approfondita, hello Cloud App Discovery Endpoint Agent può decrittografare e controllare le comunicazioni TLS crittografato, consentendo il rumore di tooreduce servizio hello e forniscono informazioni dettagliate sull'utilizzo di hello delle applicazioni cloud crittografato hello.

#### <a name="a-word-of-caution"></a>Precisazione importante
Prima di abilitare l'opzione ispezione approfondita, si consiglia di comunicare le proprie intenzioni tooyour legali e reparti delle risorse Umane e ottenere il proprio consenso. Per ovvi motivi l'ispezione delle comunicazioni crittografate private di un utente finale può comportare problemi di tutela della privacy. Prima di una produzione roll-out di ispezione approfondita, verificare che la sicurezza azienda e sono stati aggiornati i criteri di utilizzo accettabile verrà esaminato tooindicate che comunicazioni crittografate. Notifica all'utente e esenzione di siti considerati sensibili (ad esempio bancari e medici) potrebbe inoltre essere necessari se si configura Cloud App Discovery toomonitor li. Come indicato in precedenza, gli amministratori possono utilizzare hello Cloud App Discovery portale toochoose se gli utenti toonotify hello di raccolta dei dati dall'agente di hello, e se l'utente toorequire acconsentire prima dell'avvio di agente di hello la raccolta dei dati utente.

### <a name="known-issues-and-drawbacks"></a>Problemi noti e svantaggi
Esistono alcuni casi in cui intercettazione TLS potrebbe compromettere l'esperienza dell'utente finale hello:

* I certificati di convalida estesa estesa sottoposti a rendering barra degli indirizzi hello di hello web browser verde tooact come un indizio visivo che visitato un sito attendibile. Ispezione TLS non è possibile duplicare EV nel certificato hello che emette toohello client, siti web che utilizzano i certificati di convalida estesa funzionerà normalmente ma sulla barra degli indirizzi di hello non visualizzerà verde.  
* Pubblica chiavi blocco (nota anche come aggiunta di certificati) sono progettati toohelp impedire gli attacchi man-in-the-middle e non autorizzati di autorità di certificazione. Quando il certificato radice hello per un sito aggiunto non corrisponde a uno di hello noto dell'autorità di certificazione valido, il browser hello Rifiuta connessione hello con un errore. Dal momento che l'intercettazione TLS è di fatto paragonabile a un attacco man-in-the-middle, queste connessioni non riusciranno.
* Se gli utenti fanno clic sull'icona di lucchetto hello hello browser barra browser tooinspect hello sito informazioni sull'indirizzo, non vedrà una catena che termina con l'autorità di certificazione hello utilizzato certificato del sito Web di hello toosign, ma invece una catena di certificati che termina con hello Windows archivio certificati attendibili.

le occorrenze di hello tooreduce di questi problemi, è tenere traccia dei servizi cloud e applicazioni client note toouse estese convalida o l'aggiunta di chiavi pubblica e indicano hello agente Endpoint tooavoid intercettano le connessioni interessate. Anche in questi casi, si riceverà comunque i report di usare hello di queste applicazioni cloud e hello del volume di dati trasferiti, tuttavia, poiché non sono complete controllato, non i dettagli sulla modalità di utilizzo delle App hello saranno disponibili.

## <a name="sending-data-toocloud-app-discovery"></a>L'invio di dati tooCloud App Discovery
Una volta che i metadati sono stati raccolti dall'agente di hello, viene memorizzato nel computer di hello per backup tooone minuto o fino a quando hello dati memorizzati nella cache raggiungono dimensioni pari a 5MB. Vengono quindi compressi e inviato a un servizio Cloud App Discovery di toohello connessione sicura.

Se l'agente di hello è Impossibile toocommunicate con hello servizio Cloud App Discovery per qualsiasi motivo, hello metadati raccolti vengono archiviati in una cache di file locale che è accessibile solo da utenti con privilegi nel computer di hello (ad esempio, gruppo di amministratori hello).  
agente Hello automaticamente tentativi tooresend hello metadati memorizzati nella cache fino a quando non è stato ricevuto correttamente dal servizio Cloud App Discovery hello.

## <a name="receiving-hello-data-at-hello-service-end"></a>Ricezione di dati alla fine di servizio hello hello
gli agenti di Hello autenticare toohello Cloud App Discovery servizio tramite certificato di autenticazione client specifico di hello computer indicato in precedenza e inoltra i dati tramite un canale crittografato.  
analitica del servizio Cloud App Discovery Hello della pipeline dei metadati di processi per ogni cliente separatamente, suddividendoli in modo logico in tutte le fasi della pipeline analitica hello.
Hello analizzati metadati unità hello vari report nel portale di hello.

Hello metadati non elaborati e metadati hello analizzato vengono archiviati per impostare i giorni too180. Inoltre, i clienti possono scegliere toocapture hello analizzato metadati in un account di archiviazione blob di Azure di loro scelta.
Ciò è utile per analizzare i metadati offline nonché più conservazione dei dati di hello.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Accesso ai dati di hello con hello portale di Azure
Nei metadati di hello tookeep impegno raccolti sicura, per impostazione predefinita solo gli amministratori globali del tenant hello hanno funzionalità Cloud App Discovery toohello di accesso nel portale di Azure hello.  
Tuttavia, gli amministratori possono scegliere toodelegate questo accesso tooother gli utenti o gruppi.

> [!NOTE]
> Per informazioni dettagliate, vedere [Introduzione a Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Qualsiasi utente l'accesso ai hello dati nel portale di hello devono avere una licenza con una licenza Azure AD Premium.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Come individuare app cloud non autorizzate usate nell'organizzazione](active-directory-cloudappdiscovery-whatis.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)

