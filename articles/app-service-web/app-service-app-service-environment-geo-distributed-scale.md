---
title: aaaGeo scala distribuite con gli ambienti del servizio App
description: Informazioni su come toohorizontally ridimensionare le app usando geo-distribuzione con gestione traffico e gli ambienti del servizio App.
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Scalabilità distribuita a livello geografico con ambienti del servizio app
## <a name="overview"></a>Panoramica
Scenari di applicazioni che richiedono scalabilità molto elevato possono superare hello calcolo risorse capacità disponibile tooa singola distribuzione di un'app.  Applicazioni di voto, eventi sportivi ed eventi di intrattenimento televisivi sono tutti esempi di scenari che richiedono una scalabilità estremamente elevata. Requisiti su larga scala possono essere soddisfatti tramite la scalabilità orizzontale di App, con più distribuzioni di app eseguite in una singola regione, nonché in aree geografiche, requisiti di carico particolarmente intenso toohandle.

Gli ambienti del servizio app sono una piattaforma ideale per la scalabilità orizzontale.  Dopo aver selezionata una configurazione dell'ambiente del servizio App che può supportare una velocità di richiesta, gli sviluppatori possono distribuire gli ambienti del servizio App aggiuntive in "utensile cookie" modo tooattain una capacità di carico di picco desiderato.

Si supponga ad esempio un'app in esecuzione in una configurazione dell'ambiente del servizio App è stata testata toohandle 20K richieste al secondo (RPS).  Se il carico di picco desiderato hello capacità è 100K RPS, è possibile creare ambienti di servizio App cinque (5) e un'applicazione hello tooensure configurato gestibili carico previsto massimo hello.

Poiché i clienti in genere App scritte in un dominio personalizzato (o personale), gli sviluppatori devono accedere a un'app toodistribute modo richiede tutte le istanze di ambiente del servizio App hello.  Tooaccomplish un ottimo modo tratta tooresolve hello dominio personalizzato utilizzando un [profilo di Traffic Manager di Azure][AzureTrafficManagerProfile].  Hello Traffic Manager profilo può essere configurato toopoint tutti hello singoli gli ambienti del servizio App.  Gestione traffico consente di gestire automaticamente la distribuzione ai clienti in tutti gli ambienti del servizio App in base alle impostazioni nel profilo di Traffic Manager hello di bilanciamento carico di hello hello.  Questo approccio funziona indipendentemente dal fatto se tutti gli ambienti del servizio App hello sono distribuiti in una singola regione di Azure o distribuiti in tutto il mondo in più aree di Azure.

Inoltre, poiché i clienti di accedere alle App tramite il dominio di reindirizzamento a microsito hello, i clienti non sono consapevoli del numero di hello di esecuzione di un'applicazione gli ambienti del servizio App.  Di conseguenza, gli sviluppatori possono aggiungere e rimuovere in modo rapido e facile ambienti del servizio app in base al carico di traffico osservato.

diagramma concettuale Hello riportato di seguito viene illustrata un'applicazione con scalata orizzontale in tre ambienti di servizio App all'interno di una singola area.

![Architettura concettuale][ConceptualArchitecture] 

resto Hello di questo argomento vengono illustrati hello passaggi coinvolti con l'impostazione di una topologia distribuita per app di esempio di hello con più ambienti di servizio App.

## <a name="planning-hello-topology"></a>Pianificazione della topologia hello
Prima di compilare un footprint di applicazione distribuita, è utile toohave alcune informazioni parti anticipatamente.

* **Dominio personalizzato per l'applicazione hello:** qual è il nome di dominio personalizzato hello che i clienti utilizzerà tooaccess hello app?  Per il dominio personalizzato hello app esempio hello è nome *www.scalableasedemo.com*
* **Dominio di Traffic Manager:** un nome di dominio deve toobe scelto durante la creazione di un [profilo di Traffic Manager di Azure][AzureTrafficManagerProfile].  Questo nome verrà combinato con hello *trafficmanager.net* suffisso tooregister una voce di dominio che è gestita da Gestione traffico.  Per app di esempio hello, si è scelto di nome hello *scalabile di ase demo*.  Di conseguenza hello nome completo del dominio che è gestito da Gestione traffico è *scalabile di ase demo.trafficmanager.net*.
* **Strategia per la scalabilità footprint app hello:** verranno distribuiti tra più ambienti di servizio App in una singola area footprint dell'applicazione hello?  in più aree geografiche  o con una combinazione di entrambi gli approcci.  Hello decisione deve basarsi sulle aspettative di in cui avranno origine traffico dei clienti, nonché come rest hello e di un'applicazione che supporta l'infrastruttura di back-end possono essere ridimensionati.  Ad esempio, un'applicazione al 100% senza stato può essere considerevolmente ridimensionata usando una combinazione di più ambienti del servizio app per ogni area di Azure, moltiplicati per gli ambienti del servizio app distribuiti tra più aree di Azure.  Con almeno 15 pubblica aree di Azure toochoose disponibile da, gli utenti possono creare effettivamente un footprint di applicazione con tutto il mondo.  Per app di esempio hello utilizzato per l'articolo, tre gli ambienti del servizio App sono stati creati in una singola regione di Azure (centro-meridionali).
* **Convenzione di denominazione per gli ambienti del servizio App hello:** ogni ambiente del servizio App richiede un nome univoco.  Oltre a uno o due ambienti di servizio App è utile toohave una convenzione di denominazione toohelp identificare ogni ambiente del servizio App.  Per app di esempio hello è stata utilizzata una convenzione di denominazione semplice.  Hello nomi di hello e tre gli ambienti del servizio App sono *fe1ase*, *fe2ase*, e *fe3ase*.
* **Convenzione di denominazione per le app hello:** perché più istanze di hello app verranno distribuite, è necessario un nome per ogni istanza dell'applicazione hello distribuito.  Una funzionalità di poco noti ma molto pratico degli ambienti del servizio App è tale hello stesso nome di app può essere utilizzato in diversi ambienti di servizio App.  Poiché ogni ambiente del servizio App ha un suffisso di dominio univoci, gli sviluppatori possono scegliere toore utilizzare hello esatto nome di un'app in ogni ambiente.  Ad esempio, uno sviluppatore può avere app denominate come segue: *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net* e così via.  Per app di esempio hello anche se ogni istanza di applicazione ha anche un nome univoco.  Hello app istanza nomi utilizzati sono *webfrontend1*, *webfrontend2*, e *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Impostazione di hello profilo di gestione traffico
Una volta distribuite più istanze di un'applicazione in più ambienti di servizio App, è possibile che istanze singole app hello possono essere registrate con gestione traffico.  Per app di esempio hello una gestione traffico profilo è necessaria per *scalabile di ase demo.trafficmanager.net* che può indirizzare i clienti tooany di hello seguente distribuito app istanze:

* **webfrontend1.fe1ase.p.azurewebsites.NET:** un'istanza distribuita in app di esempio hello hello prima dell'ambiente del servizio App.
* **webfrontend2.fe2ase.p.azurewebsites.NET:** un'istanza distribuita in app di esempio hello hello secondo ambiente del servizio App.
* **webfrontend3.fe3ase.p.azurewebsites.NET:** un'istanza distribuita in app di esempio hello hello terzo ambiente del servizio App.

Hello tooregister modo più semplice di più endpoint di servizio App di Azure, tutti in esecuzione in hello **stesso** area di Azure, è con Powershell hello [il supporto di gestione traffico di Azure Resource Manager] [ ARMTrafficManager].  

primo passaggio Hello è toocreate un profilo di Traffic Manager di Azure.  codice Hello riportato di seguito viene illustrato come profilo hello è stato creato per app di esempio hello:

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Si noti come hello *RelativeDnsName* parametro è stato impostato troppo*scalabile di ase demo*.  Questo è hello come nome di dominio *scalabile di ase demo.trafficmanager.net* viene creato e associato a un profilo di Traffic Manager.

Hello *TrafficRoutingMethod* parametro definisce criteri di gestione traffico verrà utilizzato come il carico tra tutti gli endpoint disponibili hello cliente toospread toodetermine di bilanciamento del carico di hello.  In questo hello esempio *Weighted* è stato scelto il metodo.  Questo comporterà essere disseminate in tutti gli endpoint di applicazione hello registrato basati sui relativi pesi hello associati a ogni endpoint le richieste dei clienti. 

Profilo hello creato, ogni istanza di applicazione viene aggiunto toohello profilo come un endpoint di Azure nativo.  Recupera un'app web front-end di riferimento tooeach codice Hello seguente e quindi aggiunge ogni app come un endpoint di gestione traffico mediante hello *ID risorsa di destinazione* parametro.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Si noti come non esiste un'unica chiamata troppo*Aggiungi AzureTrafficManagerEndpointConfig* per ogni istanza di singole app.  Hello *ID risorsa di destinazione* parametro in ogni comando di Powershell fa riferimento a uno dei tre istanze di app distribuita hello.  profilo di gestione traffico Hello verrà esteso carico tra tutte e tre gli endpoint registrati nel profilo hello.

Tutti e tre gli endpoint utilizzano hello hello stesso valore (10) per hello *peso* parametro.  Gestione traffico distribuirà quindi le richieste dei clienti tra tutte e tre le istanze dell'app in modo relativamente uniforme. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Dominio dell'applicazione hello puntamento personalizzata hello dominio di Traffic Manager
passaggio finale Hello necessario è dominio personalizzato di hello toopoint dell'app hello al dominio di Traffic Manager hello.  Per app di esempio hello ciò significa che punta *www.scalableasedemo.com* in *scalabile di ase demo.trafficmanager.net*.  Questo passaggio è necessario toobe completato con il registrar hello che gestisce dominio personalizzato hello.  

Utilizzando gli strumenti di gestione del dominio del proprio registrar, un toobe esigenze di record CNAME che punti hello il dominio personalizzato creato nel dominio di Traffic Manager hello.  immagine di Hello riportata di seguito viene illustrato un esempio di questa configurazione di CNAME l'aspetto seguente:

![CNAME per il dominio personalizzato][CNAMEforCustomDomain] 

Anche se non trattate in questo argomento, tenere presente che ogni istanza di singole app deve dominio personalizzato hello toohave registrato anche con esso.  In caso contrario istanza app tooan rende una richiesta, se un'applicazione hello non dispone di hello di dominio personalizzato registrato con l'applicazione hello, hello richiesta avrà esito negativo.  

In questo hello esempio dominio personalizzato è *www.scalableasedemo.com*, e ogni istanza dell'applicazione dispone di dominio personalizzato di hello è associato.

![Dominio personalizzato][CustomDomain] 

Per un riepilogo della registrazione di un dominio personalizzato con le applicazioni di servizio App di Azure, vedere l'articolo seguente hello [registrazione domini personalizzati][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>Provare a hello topologia distribuita
Hello risultato finale della configurazione di DNS e di gestione traffico hello è che le richieste di *www.scalableasedemo.com* passeranno attraverso hello seguente sequenza:

1. Un browser o un dispositivo esegue una ricerca DNS di *www.scalableasedemo.com*
2. Hello voce CNAME presso il registrar di dominio hello causa hello DNS ricerca toobe reindirizzato tooAzure Traffic Manager.
3. Viene effettuata una ricerca DNS per *scalabile di ase demo.trafficmanager.net* su uno dei server DNS di Traffic Manager di Azure di hello.
4. In base al criterio di bilanciamento del carico di hello (hello *TrafficRoutingMethod* parametro utilizzato in precedenza, quando si crea il profilo di Traffic Manager hello), gestione traffico verrà selezionare una delle hello configurato gli endpoint e restituire hello FQDN di tale endpoint toohello browser o nel dispositivo.
5. Poiché hello FQDN dell'endpoint hello hello Url di un'istanza di applicazione in esecuzione in un ambiente del servizio App, hello browser o nel dispositivo verrà richiesto un server DNS di Microsoft Azure hello tooresolve l'indirizzo IP tooan FQDN. 
6. dispositivo o browser Hello invierà l'indirizzo IP hello HTTP/S richiesta toohello.  
7. richiesta di Hello arriverà a una delle istanze di hello app in esecuzione in uno di hello gli ambienti del servizio App.

Hello immagine console seguente viene illustrata una ricerca DNS per dominio personalizzato correttamente risoluzione tooan app istanza dell'app di esempio hello in esecuzione in uno di: esempio hello e tre gli ambienti del servizio App (in questo caso hello secondo di hello e tre gli ambienti del servizio App):

![Ricerca DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Informazioni e collegamenti aggiuntivi
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

Documentazione su hello Powershell [il supporto di gestione traffico di Azure Resource Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
