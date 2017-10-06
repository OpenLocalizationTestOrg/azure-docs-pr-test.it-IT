---
title: Considerazioni relative alla topologia aaaNetwork quando si usa il Proxy di applicazione Azure Active Directory | Documenti Microsoft
description: Tratta alcune considerazioni relative alla topologia di rete quando si usa il proxy applicazione Azure AD.
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
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Considerazioni relative alla topologia di rete quando si usa il proxy applicazione di Azure Active Directory

Questo articolo presenta alcune considerazioni relative alla topologia di rete quando si usa il proxy applicazione di Azure Active Directory (Azure AD) per la pubblicazione delle applicazioni e il relativo accesso da remoto.

## <a name="traffic-flow"></a>Flusso del traffico

Quando un'applicazione viene pubblicata tramite Proxy di applicazione AD Azure, il traffico proveniente da applicazioni di hello utenti toohello passa attraverso tre connessioni:

1. utente di Hello si connette toohello endpoint pubblico del servizio Proxy di applicazione AD Azure in Azure
2. Hello servizio Proxy di applicazione si connette toohello connettore del Proxy di applicazione
3. connettore Proxy dell'applicazione Hello si connette l'applicazione di destinazione toohello

![Diagramma che illustra il flusso del traffico da applicazione tootarget utente](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Località del tenant e servizio proxy applicazione

Quando effettua l'iscrizione per un tenant di Azure AD, area hello del tenant è determinato dal paese hello specificate. Quando si abilita il Proxy di applicazione, le istanze del servizio Proxy di applicazione hello per il tenant sono scelte o create in hello stesso area come tenant di Azure AD o tooit area più vicina hello.

Ad esempio, se l'area del tenant di Azure AD hello dall'Unione europea (Europa), tutti i connettori Proxy di applicazione utilizzano le istanze del servizio nei Data Center di Azure in hello Europa. Quando agli utenti l'accesso pubblicazione delle applicazioni, il traffico passa attraverso le istanze del servizio Proxy di applicazione hello in questa posizione.

## <a name="considerations-for-reducing-latency"></a>Considerazioni per ridurre la latenza

Tutte le soluzioni proxy introducono latenza nella connessione di rete. Indipendentemente da quale proxy o una soluzione VPN si sceglie come soluzione di accesso remoto, include sempre un set di server di attivazione hello tooinside di connessione alla rete aziendale.

Le organizzazioni includono in genere endpoint server nella rete perimetrale. Con Proxy dell'applicazione AD Azure, tuttavia, il traffico passa attraverso il servizio proxy hello nel cloud hello mentre connettori hello si trovano nella rete aziendale. Non è richiesta alcuna rete perimetrale.

Nelle sezioni successive di Hello contengono toohelp suggerimenti aggiuntivi ridurre la latenza ulteriormente. 

### <a name="connector-placement"></a>Posizionamento dei connettori

Proxy dell'applicazione sceglie automaticamente il percorso di hello di istanze, in base alla località del tenant. Invece, si ottiene toodecide in connettore di hello tooinstall, offrendo hello caratteristiche di latenza power toodefine hello del traffico di rete.

Quando si configura il servizio Proxy di applicazione hello, chiedere hello seguenti domande:

* In cui si trova l'applicazione hello?
* La maggior parte degli utenti che accedono a hello app che si trova dove si trovano?
* In cui si trova l'istanza del Proxy di applicazione hello?
* Si dispone già un Data Center tooAzure connessione di rete dedicata configurato, Azure ExpressRoute o una simile VPN?

connettore Hello ha toocommunicate con Azure e le applicazioni (passaggi 2 e 3 nel diagramma di flusso del traffico hello), pertanto hello posizionamento della latenza di hello influisce sul connettore hello tali due connessioni. Quando si valuta la selezione di hello del connettore hello, tenere hello presente seguenti punti:

* Se si desidera toouse la delega vincolata Kerberos (KCD) per single sign-on, il connettore hello deve quindi un Data Center tooa di visibilità. Inoltre, server del connettore hello deve toobe di dominio.  
* In caso di dubbio, installare un'applicazione hello connettore più vicino toohello.

### <a name="general-approach-toominimize-latency"></a>Latenza toominimize approccio generale

È possibile ridurre la latenza di hello del traffico end-to-end hello ottimizzando ciascuna connessione di rete. Ogni connessione può essere ottimizzata eseguendo le operazioni seguenti:

* Riduzione della distanza hello tra due estremità di hello dell'hop hello.
* Scelta di hello tootraverse di rete più adatta. Ad esempio, attraversando una rete privata anziché hello Internet pubblico può risultare più veloce, a causa di collegamenti toodedicated.

Se si dispone di un collegamento VPN o ExpressRoute dedicato tra Azure e della rete aziendale, è opportuno toouse che.

## <a name="focus-your-optimization-strategy"></a>Individuare la migliore strategia di ottimizzazione

È minimo che è possibile eseguire connessione hello toocontrol tra utenti e servizio Proxy applicazione hello ci. poiché gli utenti possono accedere alle applicazioni da una rete domestica, un bar o un paese diverso. In alternativa, è possibile ottimizzare le connessioni hello da hello Proxy applicazione del servizio toohello Proxy dell'applicazione connettori toohello app. Si consideri l'inclusione di hello seguito modelli nell'ambiente in uso.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Modello 1: Inserire un'applicazione hello connettore toohello Chiudi

Sul posto hello connettore toohello chiusura dell'applicazione di destinazione rete cliente hello. Questa configurazione riduce il passaggio 3 nella diagramma topografia hello, perché connettore hello e applicazione sono simili. 

Se il connettore è un controller di dominio di visibilità toohello, questo modello è più vantaggioso. Molti clienti usano questo modello poiché è adatto alla maggior parte degli scenari. Questo modello può anche essere combinato con il traffico di toooptimize 2 modello tra servizio hello e connettore hello.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Modello 2: Sfruttare ExpressRoute con peering pubblico

Se si dispone di ExpressRoute di peering pubblico, è possibile utilizzare una connessione ExpressRoute più veloce hello per il traffico tra il Proxy di applicazione e connettore hello. connettore Hello è ancora connesso alla rete, Chiudi toohello app.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Modello 3: Sfruttare ExpressRoute con peering privato

Se tra Azure e la rete aziendale è configurato un collegamento VPN o ExpressRoute dedicato con peering privato, è disponibile un'altra opzione. In questa configurazione di rete virtuale di hello in Azure è in genere considerato un'estensione della rete aziendale hello. Pertanto è possibile installare il connettore di hello in hello Data Center di Azure e continua a soddisfare i requisiti di latenza bassa hello della connessione al connettore-app hello.

Poiché il traffico scorre attraverso una connessione dedicata, la latenza non è compromessa. È inoltre possibile ottenere migliorare latenza al connettore del servizio di Proxy dell'applicazione perché il connettore hello è installato in un tooyour Chiudi Data Center di Azure posizione del tenant Azure AD.

![Diagramma che illustra l'installazione del connettore in un data center di Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Altri approcci

Anche se lo stato attivo hello di questo articolo è la selezione di connettore, è inoltre possibile modificare la selezione di hello di hello tooget migliore latenza le caratteristiche dell'applicazione.

Le organizzazioni spostano sempre più spesso le loro reti in ambienti in hosting. In questo modo tooplace delle App in un ambiente host che fa anche parte della rete aziendale e ancora essere all'interno di dominio hello. In questo caso, i modelli di hello illustrati nelle sezioni precedenti hello possono essere applicato toohello nuovo percorso di applicazione. Se si sta considerando questa opzione, vedere [Azure AD Domain Services](../active-directory-domain-services/active-directory-ds-overview.md).

È inoltre consigliabile organizzare i connettori utilizzando [gruppi di connettori](active-directory-application-proxy-connectors.md) App tootarget presenti in diverse posizioni e reti. 

## <a name="common-use-cases"></a>Casi d'uso comuni

In questa sezione si esaminano alcuni scenari comuni. Si supponga che hello tenant di Azure AD (e pertanto proxy servizio endpoint) si trova in hello United States (Stati Uniti). Hello come illustrato in questi casi di utilizzo si applicano anche aree tooother mondo hello.

In questi scenari ogni connessione viene chiamata "hop" e viene numerata per semplificare la discussione:

- **Hop 1**: toohello utente servizio Proxy di applicazione
- **Hop 2**: connettore Proxy dell'applicazione toohello di Proxy applicazione del servizio
- **Hop 3**: applicazione di destinazione toohello connettore Proxy dell'applicazione 

### <a name="use-case-1"></a>Caso d'uso 1

**Scenario:** hello app è in una rete aziendale in hello, con gli utenti di hello stessa area. Nessun ExpressRoute o VPN esiste tra hello Data Center di Azure e la rete aziendale hello.

**Consiglio:** seguire pattern 1, illustrato nella sezione precedente hello. Per migliorare la latenza, valutare la possibilità di usare ExpressRoute, se necessario.

Si tratta di un modello semplice. È ottimizzare hop 3 inserendo connettore hello quasi app hello. In questo modo anche una scelta naturale, connettore hello è installato in genere operazioni di visibilità toohello app e toohello datacenter tooperform la delega vincolata Kerberos.

![Diagramma che mostra che gli utenti, proxy, connector e app sono tutti in hello](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Caso d'uso 2

**Scenario:** hello app è in una rete aziendale in hello noi, con utenti distribuiti a livello globale. Nessun ExpressRoute o VPN esiste tra hello Data Center di Azure e la rete aziendale hello.

**Consiglio:** seguire pattern 1, illustrato nella sezione precedente hello. 

Nuovo modello comune di hello toooptimize hop è 3, dove si posiziona il connettore hello quasi app hello. Passaggio 3 non è in genere dispendiosa, se è hello tutto nella stessa area. Tuttavia, hop 1 può essere più costosa, a seconda della posizione utente hello, perché gli utenti tra HelloWorld devono accedere l'istanza del Proxy di applicazione hello in hello Stati Uniti. È opportuno notare che qualsiasi soluzione proxy presenta caratteristiche simili in relazione a utenti distribuiti in tutto il mondo.

![Diagramma che mostra che gli utenti vengono distribuiti a livello globale, ma app e connettore proxy hello sono in hello](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Caso d'uso 3

**Scenario:** hello app si trova nella rete dell'organizzazione in hello ci. ExpressRoute con peering pubblico esiste tra Azure e hello rete aziendale.

**Consiglio:** seguire pattern 1 e 2, illustrato nella sezione precedente hello.

In primo luogo, connettore hello più vicino possibile toohello app. Quindi, il sistema hello utilizza automaticamente ExpressRoute per hop 2. 

Se il collegamento ExpressRoute hello utilizza peering pubblico, il traffico di hello tra proxy hello e connettore hello passa su tale collegamento. L'hop 2 ha una latenza ottimizzata.

![Diagramma che illustra ExpressRoute tra connettore e proxy hello](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Caso d'uso 4

**Scenario:** hello app si trova nella rete dell'organizzazione in hello ci. ExpressRoute con peering privato esiste tra Azure e hello rete aziendale.

**Consiglio:** seguire pattern, 3, illustrato nella sezione precedente hello.

Inserire il connettore hello hello Data Center toohello connesso alla rete aziendale tramite ExpressRoute di peering privato di Azure. 

connettore Hello può essere inserita in hello Data Center di Azure. Poiché connettore hello dispone ancora di un Data Center hello tramite rete privata hello e un'applicazione di toohello di visibilità, hop 3 rimane ottimizzato. Viene anche ulteriormente ottimizzato l'hop 2.

![Diagramma che mostra un connettore di hello in un Data Center di Azure ed ExpressRoute tra app e connettore hello](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Caso d'uso 5

**Scenario:** hello app si trova nella rete dell'organizzazione in hello Europa, con l'istanza del Proxy di applicazione hello e la maggior parte degli utenti in hello US.

**Consiglio:** connettore hello sul posto quasi app hello. Poiché gli utenti di Stati Uniti accedono a un'istanza di Proxy dell'applicazione che si verifica in hello toobe stessa area, hop 1 non è troppo costosa. L'hop 3 è ottimizzato. È possibile utilizzare ExpressRoute toooptimize hop 2. 

![Diagramma con utenti e i proxy hello US, con connettore hello e dell'applicazione hello Europa](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

In questa situazione è anche possibile prendere in considerazione l'uso di un'altra variante. Se la maggior parte degli utenti hello organizzazione hello US, probabilità sono che la rete si estende toohello ci anche. Inserire il connettore hello in hello Stati Uniti e utilizzare un'applicazione hello dedicato rete aziendale interna riga toohello in hello Europa. In questo modo, gli hop 2 e 3 vengono ottimizzati.

![Diagramma con gli utenti, il proxy e connettore hello Stati Uniti, in Europa hello app](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Passaggi successivi

- [Abilitare il proxy dell'applicazione](active-directory-application-proxy-enable.md)
- [Abilitare l'accesso Single Sign-On](active-directory-application-proxy-sso-using-kcd.md)
- [Abilitare l'accesso condizionale](active-directory-application-proxy-conditional-access.md)
- [Risolvere i problemi che si verificano con il proxy di applicazione](active-directory-application-proxy-troubleshoot.md)
