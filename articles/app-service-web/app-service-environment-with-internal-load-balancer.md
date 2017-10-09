---
title: aaaCreating e l'utilizzo di un bilanciamento del carico interno con un ambiente del servizio App | Documenti Microsoft
description: Creazione e uso di un ambiente del servizio app con bilanciamento del carico interno
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Uso di un servizio di bilanciamento del carico interno con un ambiente del servizio app

> [!NOTE] 
> Questo articolo è sull'ambiente del servizio App v1 hello. È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
>

funzionalità di ambiente del servizio App (ASE) Hello è un'opzione di servizio Premium di Azure App Service che offre una funzionalità avanzata di configurazione che non è disponibile in timbri di hello multi-tenant. funzionalità di ASE Hello distribuisce sostanzialmente hello Azure App Service nel Network(VNet) virtuale di Azure. toogain una maggiore conoscenza delle funzionalità di hello disponibili per gli ambienti del servizio App di leggere hello [che cos'è un ambiente del servizio App] [ WhatisASE] documentazione. Se non si conosce vantaggi hello di operativo in una rete virtuale leggere hello [domande frequenti sulla rete virtuale Azure][virtualnetwork]. 

## <a name="overview"></a>Panoramica
Un ambiente del servizio app può essere distribuito con un endpoint accessibile da Internet o con un indirizzo IP nella rete virtuale. In ordine tooset hello IP indirizzo tooa indirizzo di rete virtuale è necessario toodeploy il ASE con un Balancer(ILB) carico interno. Quando l'ambiente è configurato con un bilanciamento del carico interno, fornire:

* il proprio dominio o sottodominio. toomake è più facile, che questo documento presuppone sottodominio ma è possibile configurarla in entrambi i casi. 
* certificato Hello usato per HTTPS
* la gestione del DNS per il sottodominio. 

È possibile eseguire operazioni come:

* ospitare applicazioni intranet, ad esempio applicazioni line of business, in modo protetto nel hello cloud a cui si accede tramite un sito tooSite o ExpressRoute VPN
* applicazioni host nel cloud hello che non sono elencate nel server DNS pubblici
* creazione di applicazioni back-end isolate da Internet con cui le app front-end possono integrarsi in modo sicuro

#### <a name="disabled-functionality"></a>Funzionalità disabilitata
Non è possibile eseguire alcune operazioni quando si usa un ambiente del servizio app con bilanciamento del carico interno. Alcuni esempi sono:

* uso di IPSSL
* assegnazione di indirizzi IP toospecific App
* acquistare e utilizzare un certificato a un'app tramite il portale di hello. Naturalmente ancora, è possibile ottenere i certificati direttamente con un'autorità di certificazione e usarla con le applicazioni, ma non tramite hello portale di Azure.

## <a name="creating-an-ilb-ase"></a>Creazione di un ambiente del servizio app con bilanciamento del carico interno
La creazione di un ambiente del servizio app con bilanciamento del carico interno non è molto diversa dalla creazione di un ambiente del servizio app regolare. Per una discussione più approfondita sulla creazione di un ASE leggere [come un ambiente del servizio App tooCreate][HowtoCreateASE]. Hello processo toocreate ASE un bilanciamento del carico interno è hello uguali tra la creazione di una rete virtuale durante la creazione di base o la selezione di una rete virtuale esistente. toocreate ASE un bilanciamento del carico interno: 

1. In selezionare portale Azure hello **nuovo -> Web + Mobile -> ambiente del servizio App**
2. Selezionare la propria sottoscrizione
3. Selezionare o creare un gruppo di risorse
4. Selezionare o creare una rete virtuale
5. Creare una subnet se si seleziona una rete virtuale
6. Selezionare **/percorso di rete virtuale -> configurazione della rete virtuale** e set hello tooInternal tipo VIP
7. Specificare il nome di sottodominio (questo è il sottodominio hello utilizzato per le app create con questo ASE)
8. Selezionare OK, quindi Crea

![][1]

Nel Pannello di rete virtuale hello è disponibile un'opzione di configurazione della rete virtuale. È possibile scegliere tra un indirizzo VIP esterno o interno. valore predefinito di Hello è esterno. Se è stata impostata tooExternal il ASE utilizzerà un indirizzo VIP accessibile a internet. Se si seleziona l'opzione Interno, l'ambiente del servizio app verrà configurato con un bilanciamento del carico interno su un indirizzo IP all'interno della rete virtuale. 

Dopo aver selezionato l'interno, hello tooadd possibilità più indirizzi IP tooyour che ase viene rimosso ed è invece necessario sottodominio hello tooprovide di hello ASE. In un ASE con hello un indirizzo VIP esterno nome di ASE hello viene utilizzato il sottodominio hello per le app create con tale ASE. Se è stato chiamato il ASE ***contosotest*** e l'applicazione in quel ASE è stato chiamato ***mytest*** sottodominio hello sarà del formato hello ***contosotest.p.azurewebsites.net*** e Hello URL per l'app sarebbe ***mytest.contosotest.p.azurewebsites.net***. Se si imposta il tipo di indirizzo VIP tooInternal hello, il nome di base non viene utilizzato nella sottodominio hello per hello ASE. Specificare il sottodominio hello in modo esplicito. Se il sottodominio ***contoso.corp.net*** ed eseguito in un'app in ASE denominato ***timereporting*** quindi hello URL per tale app sarebbe ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>App in un ambiente del servizio app con bilanciamento del carico interno
Creazione di un'app in un bilanciamento del carico interno ASE hello come creare un'app in un ASE normalmente. 

1. In selezionare portale Azure hello **nuovo -> Web + Mobile -> Web** o **Mobile** o **App per le API**
2. Immettere il nome dell'app
3. Selezionare la sottoscrizione
4. Selezionare o creare un gruppo di risorse
5. Selezionare o creare un piano di servizio app (ASP). Se la creazione di un nuovo ASP quindi selezionare il ASE come percorso hello e pool di lavoro selezionare hello si desidera che il toobe ASP creato in. Quando si crea hello ASP selezionare il ASE come percorso di hello e pool di lavoro hello. Quando si specifica il nome di hello dell'app hello in che verrà visualizzato tale sottodominio hello nome dell'app viene sostituito dal sottodominio hello per le ASE. 
6. Selezionare Crea. È consigliabile selezionare hello **toodashboard Pin** casella di controllo se si desidera hello app tooshow nel dashboard. 

![][2]

In app hello al nome di sottodominio hello Ottiene sottodominio hello tooreflect aggiornato del ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Convalida dopo la creazione dell'ambiente del servizio app con bilanciamento del carico interno
ASE un bilanciamento del carico interno è leggermente diverso rispetto a hello non - ILB ASE. Come già indicato è necessario toomanage proprio DNS e aver inoltre tooprovide il proprio certificato per le connessioni HTTPS. 

Dopo aver creato il ASE si noterà che sottodominio hello Mostra sottodominio hello è specificato e non esiste un nuovo elemento in hello **impostazione** denominata **ILB certificato**. Hello ASE viene creato con un certificato autofirmato che rende più semplice tootest HTTPS. Hello portale indicherà che è necessario tooprovide il proprio certificato per HTTPS, ma si tratta di toodrive si toohave un certificato con il sottodominio. 

![][3]

Se si sta semplicemente operazioni e sapere come toocreate un certificato, è possibile utilizzare hello MMC IIS toocreate di applicazione console un self-certificato di firma. Dopo averla creata è possibile esportarlo come file PFX e caricarla in hello interfaccia utente di certificati di bilanciamento del carico interno. L'accesso di un sito protetto con un certificato autofirmato, il browser verrà visualizzato un avviso che si accede al sito di hello quando non è sicuro scadenza certificato hello toovalidate impossibilità di toohello. Se si desidera tooavoid tale avviso, che è necessario un certificato firmato correttamente che corrisponde il sottodominio e dispone di una catena di certificati che sono stato riconosciuto dal browser.

![][6]

Se si desidera tootry hello flusso con i propri certificati e test ASE tooyour di accesso HTTP e HTTPS:

1. Passare tooASE dell'interfaccia utente dopo la creazione di ASE **ASE -> Impostazioni -> certificati di bilanciamento del carico interno**
2. Impostare il certificato ILB selezionando il file PFX e fornire la password. Questo passaggio richiede un po' durante tooprocess e verrà visualizzato il messaggio hello che è in corso un'operazione di ridimensionamento.
3. Ottenere l'indirizzo di bilanciamento del carico interno hello per le ASE (**ASE -> Proprietà -> indirizzi IP virtuali**)
4. Creare un'app Web nell'ambiente del servizio app dopo la creazione 
5. Creare una macchina virtuale se non si dispone di uno in tale rete virtuale (hello non nella stessa subnet hello ASE o interruzione di operazioni)
6. Impostare il DNS per il sottodominio. È possibile utilizzare un carattere jolly con il sottodominio nel DNS o se si desidera toodo alcuni semplici test, modificare il file hosts hello in VM tooset web app nome tooVIP indirizzo IP. Se il ASE ha il nome di sottodominio hello. ilbase.com e apportate hello mytestapp app web in modo che potrebbe essere risolto a mytestapp.ilbase.com quindi set che nel file hosts. (In Windows hello file degli host è in C:\Windows\System32\drivers\etc\)
7. Utilizzare un browser su tale macchina virtuale e passare toohttp://mytestapp.ilbase.com (o qualsiasi nome dell'app web è il sottodominio)
8. Utilizzare un browser su tale macchina virtuale e passare toohttps://mytestapp.ilbase.com è la mancanza di hello tooaccept di sicurezza se si utilizza un certificato autofirmato. 

indirizzo IP Hello per il bilanciamento del carico interno è elencato nelle proprietà come indirizzo IP virtuale hello

![][4]

## <a name="using-an-ilb-ase"></a>Uso di un ambiente del servizio app con bilanciamento del carico interno
#### <a name="network-security-groups"></a>Gruppi di sicurezza di rete
Un isolamento di rete consente di ASE ILB per le app come App hello non sono accessibili o anche note da hello internet. Questa condizione è ideale per ospitare i siti intranet, ad esempio le applicazioni line of business. Quando è necessario anche accesso toorestrict ulteriormente è possibile comunque utilizzare accesso toocontrol Groups(NSGs) di sicurezza di rete a livello di rete hello. 

Se si desidera limitare l'accesso toouse NSGs toofurther quindi è necessario che non si interrompe la comunicazione hello toomake tale ASE hello deve in ordine toooperate. Anche se l'accesso HTTP/HTTPS hello solo tramite hello bilanciamento del carico interno utilizzato da hello hello ASE che ase ancora dipende dalla risorsa all'esterno di hello rete virtuale. toosee quali accesso di rete è ancora necessario esaminare le informazioni di hello nel documento hello in [tooan il traffico in ingresso di controllo dell'ambiente del servizio App] [ ControlInbound] e documento hello in [rete Dettagli di configurazione per gli ambienti del servizio App con ExpressRoute][ExpressRoute]. 

tooconfigure il NSGs occorre tooknow hello IP indirizzo che è utilizzato da Azure toomanage il ASE. L'indirizzo IP è anche hello in uscita indirizzo IP del ASE se effettua le richieste internet. indirizzo IP in uscita di Hello per le ASE rimane statico per ciclo di vita di hello del ASE. Se si elimina e si ricrea l'ambiente del servizio app, si ottiene un nuovo indirizzo IP. Questo indirizzo IP andare troppo toofind**Impostazioni -> proprietà** e trovare hello **indirizzo IP in uscita**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Gestione generale dell'ambiente del servizio app con bilanciamento del carico interno
La gestione di ASE un bilanciamento del carico interno è in gran parte hello come la gestione di un ASE normalmente. È necessario tooscale backup il toohost di pool di lavoro più istanze ASP e la scalabilità verticale gli importi toohandle aumentato di server front-End del traffico HTTP/HTTPS. Per informazioni generali sulla gestione della configurazione di un ASE hello, leggere il documento di hello in [la configurazione di un ambiente del servizio App][ASEConfig]. 

gli elementi di gestione aggiuntivo Hello sono la gestione dei certificati e la gestione di DNS. È necessario tooobtain e caricare il certificato di hello usato per HTTPS dopo la creazione di bilanciamento del carico interno ASE e sostituirlo prima della scadenza. Poiché Azure proprietaria di dominio base hello offriamo i certificati per ASEs con un indirizzo VIP esterno. Poiché il sottodominio hello utilizzato da un ASE di bilanciamento del carico interno può essere qualsiasi elemento, è necessario tooprovide il proprio certificato per HTTPS. 

#### <a name="dns-configuration"></a>Configurazione del DNS
Quando si utilizza un hello VIP esterno che DNS è gestito da Azure. Qualsiasi applicazione creata nel ASE viene aggiunto automaticamente tooAzure DNS che è un DNS pubblico. In una base di bilanciamento del carico interno è necessario toomanage il proprio servizio DNS. Per un sottodominio specifico, ad esempio contoso.corp.net occorre toocreate A DNS registra tale indirizzo ILB tooyour punto:

    * 
    *.scm ftp publish 


## <a name="getting-started"></a>introduttiva
Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione gli ambienti del servizio][WhatisASE]

Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
