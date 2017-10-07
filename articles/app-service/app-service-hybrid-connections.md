---
title: aaa "connessioni ibride di servizio App di Azure | Documenti di Microsoft"
description: Come toocreate e utilizzare le connessioni ibride tooaccess delle risorse in reti diverse
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Connessioni ibride del Servizio app di Azure #

## <a name="overview"></a>Panoramica ##

Le connessioni ibride è un servizio in Azure oltre a una funzionalità di hello servizio App di Azure.  Come un servizio dispone di utilizzo e funzionalità oltre a quelle che vengono utilizzati in hello Azure App Service.  altre informazioni sulle connessioni ibride e il relativo utilizzo di fuori di hello Azure App Service è possibile iniziare da qui, toolearn [le connessioni ibride di inoltro di Azure][HCService]

All'interno di hello servizio App di Azure, le connessioni ibride possono essere risorse dell'applicazione tooaccess utilizzati nelle altre reti. Fornisce accesso dall'endpoint di applicazione della tooan app.  Non consente un tooaccess alternativa dalla capacità dell'applicazione.  Utilizzato in hello servizio App, ogni connessione ibrida correla tooa singolo host e porta combinazione TCP.  Ciò significa che tale endpoint della connessione ibrida hello può essere in qualsiasi sistema operativo e qualsiasi applicazione fornito che si raggiunge una porta di attesa TCP. Connessioni ibride non conosce o si è interessati è il protocollo di applicazione hello o si accede.  in quanto si limita a fornire l'accesso alla rete.  


## <a name="how-it-works"></a>Funzionamento ##
funzionalità di connessioni ibride Hello è costituita da due chiamate in uscita tooService inoltro del Bus.  C'è una connessione da una libreria nell'host di hello in cui l'app è in esecuzione nel servizio app di hello e quindi sia disponibile una connessione di inoltro del Bus tooService hello Manager(HCM) connessione ibrida.  Hello HCM è un servizio di inoltro che si distribuisce in hosting rete hello 

Tramite hello due connessioni unita in join l'app abbia un tooa tunnel TCP predefinito combinazione host: porta su hello altro lato della hello HCM.  connessione Hello Usa TLS 1.2 per la sicurezza e le chiavi di firma di accesso condiviso per l'autenticazione/autorizzazione.    

![][1]

Quando l'app esegue una richiesta DNS che corrisponde a un endpoint della connessione ibrida configura, quindi il traffico TCP in uscita hello verrà reindirizzato verso il basso la connessione ibrida hello.  

> [!NOTE]
> Ciò significa che è consigliabile provare tooalways utilizzare un nome DNS per la connessione ibrida.  Alcuni software client non esegue una ricerca DNS se l'endpoint di hello utilizza invece di un indirizzo IP.
>
>

Esistono due tipi di connessioni ibride, le connessioni ibride di nuovo hello che vengono offerto come servizio in Azure inoltro e hello connessioni ibride di BizTalk precedenti.  Hello connessioni ibride di BizTalk precedenti sono cui tooas classico connessioni ibride nel portale di hello.  Per altre informazioni su queste connessioni, vedere più avanti in questo documento.

### <a name="app-service-hybrid-connection-benefits"></a>Vantaggi della funzionalità Connessioni ibride del Servizio app di Azure ###

Esistono una serie di vantaggi toohello ibrida connessioni funzionalità incluse

- Le app possono accedere in modo sicuro a servizi e sistemi locali
- funzionalità di Hello non richiede un endpoint accessibile da internet
- è veloce e semplice tooset backup  
- combinazione di host: porta singola tooa che rappresenta un aspetto eccellente sicurezza corrisponde a ogni connessione ibrida
- in genere non comporta problemi di firewall connessioni hello sono tutti in uscita sulle porte web standard
- Poiché la funzionalità hello è il livello di rete che significa anche che è toohello indipendenti dal linguaggio utilizzato per la tecnologia di app e hello utilizzata dall'endpoint hello
- è possibile usare accesso tooprovide in più reti da una singola app 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Operazioni che non è possibile eseguire con la funzionalità Connessioni ibride ###

Esistono alcune operazioni che non è possibile eseguire con le connessioni ibride tra cui:

- Montaggio di un'unità
- Utilizzo del protocollo UDP
- Accesso a servizi basati su TCP che usano porte dinamiche, ad esempio la modalità FTP passiva o la modalità passiva estesa
- Supporto LDAP, in quanto talvolta richiede il protocollo UDP
- Supporto di Active Directory.

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Aggiunta e creazione di una connessione ibrida nell'app ##

È possibile creare connessioni ibride tramite il portale di app hello o dal portale del servizio di hello connessione ibrida.  È consigliabile utilizzare hello toocreate portale tramite app hello connessioni ibride desiderato toouse con l'app.  una connessione ibrida toocreate passare toohello [portale di Azure] [ portal] , entra in hello dell'interfaccia utente per l'app.  Selezionare **Rete > Configurare gli endpoint della connessione ibrida**.  Da qui è possibile visualizzare le connessioni ibride hello configurati con l'app  

![][2]

tooadd una nuova connessione ibrida, fare clic su Aggiungi connessione ibrida.  Hello dell'interfaccia utente visualizzata vengono elencate le connessioni ibride hello che è già stato creato.  tooadd uno o più oggetti tooyour app, fare clic su hello quelli desiderati e hit **Add selected connessione ibrida**.  

![][3]

Se si desidera toocreate una nuova connessione ibrida, fare clic su **creare una nuova connessione ibrida**.  Qui occorre specificare gli elementi seguenti: 

- Nome dell'endpoint
- Nome host dell'endpoint
- Porta dell'endpoint
- spazio dei nomi Service bus desiderato toouse

![][4]

Ogni connessione ibrida tooa legati spazio dei nomi bus di servizio e ogni spazio dei nomi di service bus in un'area di Azure.  È importante tootry e utilizzare un servizio del bus di spazio dei nomi in hello così come latenza di rete provocato tooavoid stessa area dell'app.

Se si desidera tooremove la connessione ibrida dall'app, fare clic su di esso e selezionare **Disconnect**.  

Dopo aver aggiunto una connessione ibrida tooyour web app, è possibile visualizzare i dettagli su di esso, facendo semplicemente clic su di esso.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Connessioni ibride e piani di servizio app ##

Hello ibrida solo le connessioni a questo punto è possibile apportare in hello nuovo ibrido.  Sono disponibili solo per le SKU di prezzo Basic, Standard, Premium e per ambiente isolato.  Esistono limiti legati toohello prezzi piano.  

| Piano tariffario | Numero di connessioni ibride utilizzabile nel piano di hello |
|----|----|
| Basic | 5 |
| Standard | 25 |
| Premium | 200 |
| Isolato | 200 |

Poiché sono presenti restrizioni piano di servizio App è inoltre disponibile dell'interfaccia utente nel piano di servizio App in cui viene utilizzato il numero di connessioni ibride hello e per quali app.  

![][6]

Proprio come con visualizzazione app hello, è possibile vedere i dettagli per la connessione ibrida facendo clic su di esso.  Nelle proprietà hello qui è possibile visualizzare tutte le informazioni di hello in vista dell'applicazione hello è inoltre possibile visualizzare quanti altre App hello stesso il piano di servizio App utilizzano la connessione ibrida.

![][7]

Mentre è previsto un limite sul numero di hello di endpoint della connessione ibrida che può essere usato in un piano di servizio App, ogni connessione ibrida utilizzato può essere utilizzato in un numero qualsiasi di applicazioni in tale piano di servizio App.  Ovvero toosay se la connessione ibrida 1 utilizzati in applicazioni separate 5 il piano di servizio App, che è ancora 1 connessione ibrida.

È un connessioni toohybrid costi aggiuntivi oltre a essere solo utilizzabile in Basic, Standard, Premium o SKU di tipo isolato.  Per altre informazioni sui prezzi delle connessioni ibride, vedere [Prezzi di Bus di servizio][sbpricing].

## <a name="hybrid-connection-manager"></a>Gestione connessione ibrida ##

Affinché toowork connessioni ibride, è necessario un agente di inoltro nella rete hello che ospita l'endpoint della connessione ibrida.  Che l'agente di inoltro viene chiamato hello Hybrid Connection Manager (HCM).  Questo strumento può essere scaricato da hello **rete > configurare gli endpoint della connessione ibrida** dell'interfaccia utente disponibili dalla tua app in hello [portale di Azure][portal].  

Questo strumento viene eseguito in Windows Server 2008 R2 e versioni successive di Windows.  Una volta installato hello HCM viene eseguito come servizio.  Questo servizio si connette l'inoltro di Service bus tooAzure basata sugli endpoint hello configurato.  le connessioni Hello da hello HCM sono tooports in uscita 80 e 443.    

Hello HCM ha un tooconfigure dell'interfaccia utente è.  Dopo aver hello che HCM è installato è possibile visualizzare hello dell'interfaccia utente eseguendo hello HybridConnectionManagerUi.exe che si trova nella directory di installazione di hello Hybrid Connection Manager.  L'interfaccia può essere richiamata anche direttamente da Windows 10 digitando *interfaccia utente Gestione connessione ibrida* nella casella di ricerca.  

Quando viene avviato UI HCM, hello hello in primo luogo è vedere è una tabella che elenca tutte le connessioni ibride hello configurati con questa istanza di hello HCM.  Se si desiderano toomake tutte le modifiche, è necessario tooauthenticate con Azure. 

tooadd uno o più connessioni ibride tooyour HCM:

1. Avviare hello HCM UI
1. Fare clic su Configure another hybrid connection (Configura un'altra connessione ibrida)![][8].

1. Accedere con l'account Azure.
1. Scegliere una sottoscrizione.
1. Fare clic su connessioni ibride hello si desidera questo toorelay HCM![][9]

1. Fare clic su Salva.

A questo punto si noterà che le connessioni ibride hello che è stato aggiunto.  È anche possibile fare clic su una connessione ibrida hello configurato e visualizzare i dettagli relativi alla connessione hello.

![][10]

Per le HCM toobe toosupport in grado di hello ibrida connessioni che viene configurato con, è necessario:

- TooAzure accesso TCP sulla porta 80 e 443
- Endpoint della connessione ibrida toohello accesso TCP
- capacità toodo DNS aspetto ups sull'host di endpoint hello e dello spazio dei nomi di hello azure Service bus

Hello HCM supporta le nuove connessioni ibride nonché a connessioni ibride di BizTalk precedenti hello.

### <a name="redundancy"></a>Ridondanza ###

Ogni istanza di Gestione connessione ibrida può supportare più connessioni ibride.  Ogni connessione ibrida specificata può inoltre essere supportata da più istanze di Gestione connessione ibrida.  comportamento predefinito di Hello è traffico robin tooround tra hello configurato HCMs per qualsiasi endpoint specificato.  Se si intende usufruire della disponibilità elevata nelle connessioni ibride dalla rete, è sufficiente creare istanze di Gestione connessione ibrida in computer separati. 

### <a name="manually-adding-a-hybrid-connection"></a>Aggiunta manuale di una connessione ibrida ###

Se si desidera qualcuno all'esterno del toohost sottoscrizione istanza HCM per una connessione ibrida specificato, è possibile condividere con li hello stringa di connessione del gateway per la connessione ibrida hello.  È possibile vedere questo nelle proprietà hello per una connessione ibrida in hello [portale di Azure][portal]. toouse che stringa, fare clic su hello **configurare manualmente** pulsante hello HCM e incollare nella stringa di connessione del gateway hello.


## <a name="troubleshooting"></a>Risoluzione dei problemi ##

Quando la connessione ibrida è configurata con un'applicazione in esecuzione è presente almeno un HCM che dispone di tale connessione ibrida configurato, quindi viene indicato che stato hello **connesso** nel portale di hello.  Se non è selezionato **connesso** quindi significa che l'app è inattivo o non può connettersi la HCM out tooAzure sulle porte 80 o 443.  

principalmente Hello che i client non possono connettersi endpoint tootheir infatti endpoint hello è stato specificato utilizzando un indirizzo IP anziché un nome DNS.  Se l'app non è possibile raggiungere l'endpoint di hello desiderato e utilizzato un indirizzo IP, passare toousing un nome DNS valido nell'host di hello in hello HCM è in esecuzione.  Altri aspetti toocheck sono tale hello nome DNS venga risolto correttamente nell'host di hello in hello HCM è in esecuzione e che non vi è connettività da hello host in cui hello HCM è in esecuzione toohello endpoint della connessione ibrida.  

Si è uno strumento nel servizio App che può essere richiamato dalla console di hello denominato tcpping hello.  Questo strumento può indicare se si dispone di accesso tooa TCP endpoint ma non indica se si dispone di accesso tooa endpoint della connessione ibrida.  Quando utilizzato nella console di hello rispetto a un endpoint della connessione ibrida, un ping ha esito positivo solo indicherà che si dispone di una connessione ibrida configurata per l'applicazione che utilizza tale combinazione di host: porta.  

## <a name="biztalk-hybrid-connections"></a>Connessioni ibride BizTalk ##

funzionalità di connessioni ibride di BizTalk precedenti Hello è stato chiuso disattivare le operazioni di creazione di toofurther connessione ibrida BizTalk.  È possibile continuare a usare le connessioni ibride di BizTalk preesistente con le applicazioni, ma deve eseguire la migrazione toohello nuovo servizio.  Tra hello vantaggi nel servizio di nuovo hello rispetto alla versione di hello BizTalk sono:

- Non è richiesto alcun account BizTalk aggiuntivo
- La versione di TLS è 1.2 anziché 1.0 come in Connessioni ibride BizTalk
- La comunicazione è sulle porte 80 e 443 usando un tooreach di nome DNS Azure anziché agli indirizzi IP e un intervallo di ulteriori altre porte.  

tooadd app tooyour connessione ibrida BizTalk, app tooyour andare in hello [portale di Azure] [ portal] e fare clic su **rete > configurare gli endpoint della connessione ibrida**.  Nella tabella delle connessioni ibride hello classica fare clic su **aggiungere la connessione ibrida classico**.  Verrà visualizzato un elenco delle connessioni ibride BizTalk in uso.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

