---
title: connettori Proxy di applicazione aaaUnderstand Azure AD | Documenti Microsoft
description: Nozioni fondamentali di hello include informazioni sui connettori Proxy di applicazione di Azure AD.
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
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 294cb26803ef7cf8be9f3af0678d6d2e64f6cc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-ad-application-proxy-connectors"></a>Comprendere i connettori del proxy applicazione Azure AD

I connettori sono ciò che rende possibile il proxy di applicazione di Azure AD. Sono semplici, facili toodeploy e mantenere e con privilegi avanzati potente. In questo articolo descrive quali connettori, il loro funzionamento e alcuni suggerimenti per la toooptimize la distribuzione. 

## <a name="what-is-an-application-proxy-connector"></a>Informazioni su un connettore proxy di applicazione

I connettori sono lightweight agenti che si trovano in locale e facilitano il servizio Proxy applicazione toohello di hello connessione in uscita. In un Server di Windows che dispone di accesso toohello back-end applicazione, è necessario installare i connettori. È possibile organizzare i connettori in gruppi di connettori, con ogni gruppo di gestione delle applicazioni toospecific traffico. Il bilanciamento del carico connettori automaticamente e consentono toooptimize la struttura di rete. 

## <a name="requirements-and-deployment"></a>Requisiti e distribuzione

Proxy dell'applicazione toodeploy correttamente, è necessario almeno un connettore, ma è consigliabile due o più per maggiore resilienza. Installare il connettore di hello in Windows Server 2012 R2 o computer 2016. connettore di Hello deve toocommunicate in grado di toobe con servizio Proxy applicazione hello, nonché applicazioni locali hello da pubblicare. 

Per ulteriori informazioni sui requisiti di rete di hello per hello connettore server, vedere [iniziare con Proxy dell'applicazione e installare un connettore](active-directory-application-proxy-enable.md).

## <a name="maintenance"></a>Manutenzione 
Hello connettori e servizio hello assicurarti di tutte le attività hello la disponibilità elevata. Possono essere aggiunti o rimossi in modo dinamico. Ogni volta che arriva una nuova richiesta è indirizzato tooone dei connettori hello che è attualmente disponibile. Se un connettore è temporaneamente non disponibile, non risponde toothis traffico.

connettori Hello sono senza stati e senza dati di configurazione nel computer di hello. Hello solo i dati che archiviano sono hello impostazioni per la connessione al servizio hello e il relativo certificato di autenticazione. Quando si connessione toohello servizio, essi pull di tutti i dati di configurazione necessarie hello e aggiornarlo ogni due minuti.

Connettori, è possibile eseguire anche il polling hello server toofind se è disponibile una versione più recente del connettore hello. Se viene trovata, i connettori di hello aggiornano.

È possibile monitorare i connettori dalla macchina di hello che sono in esecuzione, mediante il registro eventi di hello e i contatori delle prestazioni. In alternativa, è possibile visualizzare lo stato dalla pagina di Proxy dell'applicazione hello di hello portale di Azure:

 ![Connettori del proxy applicazione AzureAD](./media/application-proxy-understand-connectors/app-proxy-connectors.png)

Non è necessario toomanually eliminare connettori inutilizzate. Quando è in esecuzione un connettore, rimane attivo della connessione del servizio toohello. I connettori inutilizzati vengono contrassegnati come _inattivi_ e vengono rimossi dopo 10 giorni di inattività. Se si desidera toouninstall un connettore, disinstallare, tuttavia, il servizio connettore hello sia il servizio di aggiornamento hello dal server hello. Riavviare il servizio di hello remove toofully computer.

## <a name="automatic-updates"></a>Aggiornamenti automatici

Azure AD fornisce aggiornamenti automatici per tutti i connettori di hello da distribuire. Fino a quando il servizio di aggiornamento del connettore Proxy dell'applicazione hello è in esecuzione, i connettori di aggiornano automaticamente. Se non viene visualizzato hello servizio di aggiornamento del connettore sul server, è necessario troppo[reinstallare il connettore](active-directory-application-proxy-enable.md) tooget eventuali aggiornamenti. 

Se non si desidera toowait per un connettore tooyour toocome di aggiornamento automatico, è possibile eseguire un aggiornamento manuale. Passare toohello [pagina di download del connettore](https://download.msappproxy.net/subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/connector/download) sul server di hello in cui il connettore si trova e selezionare **scaricare**. Questo processo avvia un aggiornamento per il connettore locale hello. 

Per un tenant con più connettori, aggiornamenti automatici hello riferimento un connettore alla volta in ogni gruppo tooprevent dei tempi di inattività dell'ambiente. 

Potrebbero verificarsi tempi di inattività quando viene aggiornato il connettore se:  
- Si ha un solo connettore. tooavoid questo periodo di inattività e migliorare la disponibilità elevata, si consiglia di installare un altro connettore e [creare un gruppo di connettori](active-directory-application-proxy-connectors-azure-portal.md).  
- Un connettore è stato centro hello di una transazione all'inizio aggiornamento hello. Anche se la transazione iniziale hello viene persa, il browser deve automaticamente riprovare hello o è possibile aggiornare la pagina. Quando viene nuovamente inviata la richiesta di hello, traffico hello è indirizzato tooa connettore di backup.

## <a name="creating-connector-groups"></a>Creazione di gruppi di connettori

Gruppi di connettori consentono di applicazioni specifiche di tooassign connettori specifici tooserve. È possibile raggruppare una serie di connettori e quindi assegnare ogni gruppo di applicazioni tooa. 

Gruppi di connettori rendono più semplice toomanage grandi distribuzioni. Sono anche migliorare latenza per i tenant che hanno le applicazioni ospitate in aree diverse, in quanto è possibile creare gruppi di connettori basati sulla posizione tooserve locale solo applicazioni. 

toolearn ulteriori informazioni sui gruppi di connettori, vedere [pubblicare le applicazioni su reti separate e percorsi con gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md).

## <a name="security-and-networking"></a>Sicurezza e rete

I connettori possono essere installati in un punto qualsiasi rete hello che consenta toosend richieste toohello Proxy dell'applicazione servizio. L'aspetto importante è che hello nel computer che esegue il connettore hello anche è accesso tooyour app. È possibile installare i connettori all'interno della rete aziendale o in una macchina virtuale che viene eseguito nel cloud hello. I connettori possono essere eseguiti in una zona demilitarizzata (DMZ), ma non è necessario poiché tutto il traffico è in uscita, in modo che la rete è protetta.

I connettori inviano le richieste soltanto in uscita. il traffico in uscita Hello viene inviato al servizio Proxy applicazione toohello e toohello applicazioni pubblicate. Non è necessario tooopen porte in ingresso perché il traffico passa in entrambe le direzioni, una volta stabilita una sessione. Non hanno tooset di bilanciamento del carico tra i connettori di hello o configurare l'accesso in entrata attraverso i firewall. 

Per maggiori informazioni sulla configurazione delle regole del firewall in uscita, vedere [Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md).

Hello utilizzare [Azure AD applicazione Proxy porte Test strumento connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify che il connettore può raggiungere il servizio di Proxy applicazione hello. Come minimo, assicurarsi che area Stati Uniti centro hello e hello area più vicina tooyou hanno tutti i segni di spunta verde. La presenza di più segni di spunta verdi indica una maggiore resilienza. 

## <a name="performance-and-scalability"></a>Prestazioni e scalabilità

Scala per il servizio Proxy di applicazione hello è trasparente, ma la scala è un fattore per i connettori. È necessario toohave di traffico sufficiente connettori toohandle punta. Tuttavia, non è necessario tooconfigure il bilanciamento del carico perché tutti i connettori all'interno di un gruppo di connettori automaticamente il bilanciamento del carico.

Poiché i connettori sono senza stati, non sono influenzati dal numero di hello di utenti o le sessioni. In alternativa, rispondono toohello numero di richieste e le dimensioni del payload. In un traffico Web standard, un computer medio può gestire circa duemila richieste al secondo. capacità specifica Hello dipende dalle caratteristiche computer esatto hello. 

prestazioni dei connettori Hello sono associata della CPU e rete. Le prestazioni della CPU sono necessaria per la crittografia SSL e la decrittografia, mentre la rete è importante tooget connettività veloce toohello ad applicazioni del servizio online hello in Azure.

La memoria, al contrario, ha meno importanza per i connettori. servizio online Hello si occupa della maggior parte dell'elaborazione hello e tutto il traffico non autenticato. Tutti gli elementi che possono essere eseguiti nel cloud hello avviene nel cloud hello. 

Un altro fattore che influisce sulle prestazioni è qualità hello delle reti hello tra connettori hello, tra cui: 

* **servizio online Hello**: toohello rallentamento o ad alta latenza delle connessioni del servizio Proxy di applicazione delle prestazioni di connettore di Azure influenza hello. Per prestazioni ottimali hello, connettere tooAzure l'organizzazione con Express Route. Dispone in caso contrario, il team di rete assicurarsi che tooAzure le connessioni vengono gestite nel modo più efficiente possibile. 
* **applicazioni back-end di Hello**: In alcuni casi, esistono altri proxy tra il connettore di hello e applicazioni back-end hello che possono rallentare o impedire le connessioni. tootroubleshoot questo scenario, aprire un browser dal server connettore hello e provare a un'applicazione hello tooaccess. Se si esegue connettori hello in Azure, ma applicazioni hello sono locali, l'esperienza di hello potrebbe non essere ciò che gli utenti si aspettano.
* **i controller di dominio di Hello**: se i connettori di hello eseguono SSO mediante la delega vincolata Kerberos, contattano controller di dominio hello prima dell'invio di back-end di hello richiesta toohello. connettori Hello hanno una cache del ticket Kerberos, ma in un ambiente occupato i tempi di risposta hello hello dei controller di dominio può influire sulle prestazioni. Questa situazione è più comune per i connettori eseguiti in Azure, ma che comunicano con i controller di dominio locali. 

Per maggiori informazioni sull'ottimizzazione della rete, vedere [Considerazioni relative alla topologia di rete quando si usa il proxy di applicazione di Azure Active Directory](application-proxy-network-topology-considerations.md).

## <a name="domain-joining"></a>Aggiunta al dominio

I connettori possono essere eseguiti in un computer che non fa parte del dominio. Tuttavia, se si desidera single sign-on (SSO) tooapplications che utilizzano l'autenticazione integrata di Windows (IWA), è necessario un computer aggiunto al dominio. In questo caso, è necessario tooa aggiunti a un dominio che è possibile eseguire macchine connettore hello [Kerberos](https://web.mit.edu/kerberos) la delega vincolata per conto degli utenti hello per hello applicazioni pubblicate.

Connettori possono anche essere unite in join toodomains o insiemi di strutture che hanno una relazione di trust parziale o controller di dominio solo tooread.

## <a name="connector-deployments-on-hardened-environments"></a>Distribuzione dei connettori in ambienti protetti

Nella maggior parte dei casi la distribuzione dei connettori è molto semplice e non richiede una configurazione speciale. Esistono tuttavia alcune condizioni specifiche che devono essere considerate:

* Le organizzazioni che consentono di limitare il traffico in uscita hello devono [aprire le porte richieste](active-directory-application-proxy-enable.md#open-your-ports).
* Macchine conformi a FIPS potrebbero essere necessario toochange tooallow loro configurazione connettore processi toogenerate hello e archiviare un certificato.
* Le organizzazioni che blocca l'ambiente in base a processi hello hello tale problema le richieste di rete possono toomake assicurarsi che entrambi i servizi del connettore sono porte abilitato tooaccess tutte le necessarie e gli indirizzi IP.
* In alcuni casi, il proxy di inoltro in uscita potrebbe interrompere l'autenticazione del certificato bidirezionale hello e causare hello toofail di comunicazione.

## <a name="connector-authentication"></a>Autenticazione del connettore

servizio hello è tooauthenticate verso il connettore hello tooprovide un servizio protetto, i connettori sono tooauthenticate verso il servizio di hello. Questa autenticazione viene eseguita utilizzando i certificati client e server quando i connettori di hello avviano connessione hello. Nome utente e password dell'amministratore di hello in questo modo non vengono archiviate nel computer di connettore hello.

certificati Hello utilizzati sono toohello specifico del servizio Proxy di applicazione. Sono creati durante la registrazione iniziale hello e automaticamente rinnovato dai connettori hello ogni due mesi. 

Se non è connesso un connettore servizio toohello da diversi mesi, i certificati potrebbe non essere aggiornato. In questo caso, disinstallare e reinstallare registrazione tootrigger del connettore hello. È possibile eseguire i seguenti comandi PowerShell hello:

```
Import-module AppProxyPSModule
Register-AppProxyConnector
```

## <a name="under-hello-hood"></a>Quinte hello

I connettori sono basati su Proxy applicazione Web di Windows Server, pertanto hanno la maggior parte delle hello stessi strumenti di gestione, inclusi i registri eventi di Windows

 ![Gestire i registri eventi con hello Visualizzatore eventi](./media/application-proxy-understand-connectors/event-view-window.png)

e con i contatori delle prestazioni di Windows. 

 ![Aggiungere contatori toohello connettore con hello Performance Monitor](./media/application-proxy-understand-connectors/performance-monitor.png)

connettori Hello dispongono di amministrazione sia sessione di log. registri amministrativi Hello includono gli eventi principali e gli errori. registri di sessione Hello includono tutte le transazioni hello e i relativi dettagli di elaborazione. 

log hello toosee, passare toohello Visualizzatore eventi, aprire hello **vista** menu e abilitare **Mostra analitica e registri di debug**. Quindi, abilitarli toostart la raccolta di eventi. Questi log non appaiono nel Proxy applicazione Web in Windows Server 2012 R2, i connettori di hello sono basati su una versione più recente.

È possibile esaminare lo stato di hello del servizio hello nella finestra Servizi hello. connettore Hello è costituito da due servizi di Windows: connettore hello e aggiornamento hello. Entrambi gli elementi devono eseguire tutto il tempo hello.

 ![Servizi Azure AD locali](./media/application-proxy-understand-connectors/aad-connector-services.png)

## <a name="next-steps"></a>Passaggi successivi


* [Pubblicare applicazioni in reti e posizioni separate tramite i gruppi di connettori](active-directory-application-proxy-connectors-azure-portal.md)
* [Usare server proxy locali esistenti](application-proxy-working-with-proxy-servers.md)
* [Risolvere i problemi di errore del proxy di applicazione e del connettore](active-directory-application-proxy-troubleshoot.md)
* [Come toosilently installa hello connettore del Proxy dell'applicazione AD Azure](active-directory-application-proxy-silent-installation.md)

