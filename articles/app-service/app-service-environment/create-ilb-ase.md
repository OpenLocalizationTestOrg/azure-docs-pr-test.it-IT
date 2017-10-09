---
title: aaaCreate e utilizzare un servizio di bilanciamento del carico interno con un ambiente del servizio App di Azure
description: Informazioni dettagliate su come toocreate e utilizzare un ambiente di servizio App di Azure isolata internet
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Creare e usare un servizio di bilanciamento del carico interno con un ambiente del servizio app #

 L'ambiente del servizio app di Azure è una distribuzione di Servizio app di Azure in una subnet in una rete virtuale di Azure. Esistono due modi toodeploy un ambiente del servizio App (ASE): 

- Con un indirizzo VIP su un indirizzo IP esterno, spesso denominato ambiente del servizio app esterno.
- Con un indirizzo VIP all'indirizzo IP interno, spesso chiamato ASE un bilanciamento del carico interno perché l'endpoint interno hello è un servizio di bilanciamento del carico interno (ILB). 

In questo articolo illustra come toocreate ASE un bilanciamento del carico interno. Per una panoramica su hello ASE, vedere [gli ambienti del servizio tooApp Introduzione][Intro]. toolearn toocreate un ASE esterni, vedere [creare un ASE esterno][MakeExternalASE].

## <a name="overview"></a>Panoramica ##

È possibile distribuire un Ambiente del servizio app con un endpoint accessibile da Internet o con un indirizzo IP nella rete virtuale. tooset l'indirizzo IP di hello tooa indirizzo di rete virtuale, hello ASE deve essere distribuito con un bilanciamento del carico interno. Per la distribuzione dell'ambiente del servizio app con un bilanciamento del carico interno, è necessario fornire:

-   Il proprio dominio usato durante la creazione delle app.
-   certificato Hello usato per HTTPS.
-   La gestione del DNS per il dominio.

È possibile eseguire operazioni come:

-   Ospitare applicazioni intranet in modo protetto nel cloud hello, che si accede tramite un sito a sito o VPN di Azure ExpressRoute.
-   App di host nel cloud hello che non sono elencate nel server DNS pubblici.
-   la creazione di applicazioni back-end isolate da Internet con cui le app front-end possono integrarsi in modo sicuro.

### <a name="disabled-functionality"></a>Funzionalità disabilitata ###

Quando si usa un ambiente del servizio app con bilanciamento del carico interno, non è possibile eseguire alcune operazioni.

-   Uso di IPSSL
-   Assegnare indirizzi IP toospecific app.
-   Acquistare e usare un certificato a un'app tramite hello portale di Azure. È possibile ottenere i certificati direttamente da un'autorità di certificazione e usarli con le app. Non è possibile ottenerle tramite hello portale di Azure.

## <a name="create-an-ilb-ase"></a>Creare un ambiente del servizio app con bilanciamento del carico interno ##

toocreate ASE un bilanciamento del carico interno:

1. Nel portale di Azure hello, selezionare **New** > **Web e dispositivi mobili** > **ambiente del servizio App**.

2. Selezionare la propria sottoscrizione.

3. Selezionare o creare un gruppo di risorse.

4. Selezionare o creare una rete virtuale.

5. Se si seleziona una rete virtuale di esistente, è necessario un hello toohold subnet ASE toocreate. Assicurarsi che tooset una subnet dimensioni sufficientemente grande tooaccommodate crescita futura del ASE. La dimensione consigliata è `/25`, contenente 128 indirizzi, in grado di gestire un ambiente del servizio app con dimensione massima. è possibile selezionare la dimensione minima Hello è un `/28`. Dopo che l'infrastruttura deve, questa dimensione può essere scalato tooa massimo di istanze di 11.

    * Andare oltre 100 istanze massimo predefinito hello nei piani di servizio App.

    * Usare una scalabilità intorno a 100, ma con ridimensionamento front-end più rapido.

6. Selezionare **Rete virtuale/Località** > **Configurazione rete virtuale**. Set hello **tipo VIP** troppo**interno**.

7. Immettere un nome di dominio Questo dominio è hello quello utilizzato per le app create con questa base. Si applicano alcune restrizioni. Non usare:

    * net   

    * azurewebsites.net

    * p.azurewebsites.net

    * &lt;asename&gt;.p.azurewebsites.net

   nome di dominio personalizzato Hello usato per le App e il nome di dominio hello utilizzato per il tipo di base non può sovrapporsi. Per un ASE di bilanciamento del carico interno con il nome di dominio hello _contoso.com_, è possibile utilizzare nomi di dominio personalizzato per l'App come:

    * www.contoso.com

    * abcd.def.contoso.com

    * abcd.contoso.com

   Se si conoscono i nomi di dominio personalizzati hello per le app, scegliere un dominio per hello ASE di bilanciamento del carico interno che non sia in conflitto con i nomi di dominio personalizzato. In questo esempio, è possibile utilizzare un risultato simile *contoso internal.com* per dominio hello del ASE perché che non entrino in conflitto con i nomi di dominio personalizzato che terminano in *. contoso.com*.

8. Selezionare **OK**, quindi **Crea**.

    ![Creazione dell'ambiente del servizio app][1]

In hello **rete virtuale** pannello è presente un **configurazione di rete virtuale** opzione. È possibile utilizzarlo tooselect un indirizzo VIP esterno o un indirizzo VIP interno. valore predefinito di Hello è **esterno**. Se si seleziona **Esterno**, l'ambiente del servizio app userà un indirizzo VIP accessibile da Internet. Se si seleziona l'opzione **Interno**, l'ambiente del servizio app verrà configurato con un bilanciamento del carico interno su un indirizzo IP all'interno della rete virtuale.

Dopo aver selezionato **interno**, hello possibilità tooadd più indirizzi IP tooyour ASE viene rimosso. In alternativa, è necessario dominio hello tooprovide di hello ASE. In un ASE con un indirizzo VIP esterno, hello nome di ASE hello viene utilizzato nel dominio hello per le app create con tale ASE.

Se si imposta **tipo VIP** troppo**interno**, il nome di base non viene utilizzato nel dominio hello per hello ASE. Specificare il dominio hello in modo esplicito. Se il dominio è *contoso.corp.net* e si crea un'app in ASE denominato *timereporting*, hello URL per tale app è timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Creare un'app in un ambiente del servizio app con bilanciamento del carico interno ##

Creare un'app in un bilanciamento del carico interno di ASE in hello allo stesso modo di creare un'app in un ASE normalmente.

1. Nel portale di Azure hello, selezionare **New** > **Web e dispositivi mobili** > **Web** o **Mobile** o  **App per le API**.

2. Immettere il nome di hello dell'applicazione hello.

3. Selezionare la sottoscrizione hello.

4. Selezionare o creare un gruppo di risorse.

5. Selezionare o creare un piano di servizio app. Se si desidera toocreate un nuovo piano di servizio App, selezionare il tipo di base come percorso di hello. Selezionare il pool di lavoro hello in cui si desidera il toobe piano di servizio App creato. Quando si crea il piano di servizio App hello, selezionare il tipo di base come hello percorso e il pool di lavoro hello. Quando si specifica il nome di hello dell'applicazione hello, dominio hello in nome dell'app viene sostituito dal dominio hello per le ASE.

6. Selezionare **Crea**. Se si desidera hello app tooappear nel dashboard, selezionare il **toodashboard Pin** casella di controllo.

    ![Creazione del piano di servizio app][2]

    In **nome App**, il nome di dominio di hello è dominio hello tooreflect aggiornato del ASE.

## <a name="post-ilb-ase-creation-validation"></a>Convalida dopo la creazione dell'ambiente del servizio app con bilanciamento del carico interno ##

ASE un bilanciamento del carico interno è leggermente diverso rispetto a hello non - ILB ASE. Come già indicato, è necessario toomanage il proprio servizio DNS. È inoltre possibile tooprovide il proprio certificato per le connessioni HTTPS.

Dopo aver creato il tipo di base, il nome di dominio hello Mostra dominio hello specificato. Viene visualizzato un nuovo elemento nel menu **Impostazione** denominato **Certificato ILB**. Hello ASE viene creato con un certificato che non specifica il dominio di bilanciamento del carico interno ASE hello. Se si utilizza hello ASE con tale certificato, il browser indica che non è valido. Questo certificato rende più semplice tootest HTTPS, ma è necessario tooupload il proprio certificato dominio ASE ILB tooyour collegati. Questo passaggio è necessario indipendentemente dal fatto che sia autofirmato o acquisito da un'autorità di certificazione (CA).

![Nome di dominio dell'ambiente del servizio app ILB][3]

L'ambiente del servizio app ILB richiede un certificato SSL valido. Usare autorità di certificazione interne, acquistare un certificato da un'autorità di certificazione esterna o usare un certificato autofirmato. Indipendentemente dall'origine hello del certificato SSL di hello, hello seguenti attributi di certificato necessario toobe configurato correttamente:

* **Oggetto**: questo attributo deve essere impostato too*.your-radice-dominio-qui.
* **Nome alternativo soggetto**: questo attributo deve includere sia *.your-root-domain-here* che **.scm.your-root-domain-here*. Toohello connessioni SSL sito SCM/Kudu associata a ciascuna applicazione usa un indirizzo del modulo hello *your-app-name.scm.your-root-domain-here*.

Converti/Salva certificato SSL hello come file con estensione pfx. file con estensione pfx Hello deve includere tutti intermedia e certificati radice. Proteggerlo con una password.

Se si desidera toocreate un certificato autofirmato, è possibile utilizzare i comandi di PowerShell hello qui. Essere toouse che il nome di dominio di bilanciamento del carico interno ASE anziché *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

certificato Hello che generano questi comandi di PowerShell viene contrassegnato tramite browser perché il certificato di hello non è stato creato da un'autorità di certificazione che fa parte della catena di attendibilità del browser. tooget un certificato considerato attendibile dal browser, e ottenere da un'autorità di certificazione commerciale nella catena del browser di trust. 

![Impostare il certificato ILB][4]

tooupload propri certificati e verificare l'accesso:

1. Dopo la creazione di hello ASE passare toohello dell'interfaccia utente di base. Selezionare **Ambiente del servizio app** > **Impostazioni** > **Certificato ILB**.

2. certificato di bilanciamento del carico interno tooset hello, selezionare file pfx del certificato hello e immettere la password di hello. Questo passaggio richiede alcuni tooprocess ora. Viene visualizzato un messaggio che informa che è in corso un'operazione di caricamento.

3. Ottenere l'indirizzo di bilanciamento del carico interno hello per il tipo di base. Selezionare **Ambiente del servizio app** > **Proprietà** > **Indirizzo IP virtuale**.

4. Creare un'app web nel ASE dopo la creazione di hello ASE.

5. Creare una macchina virtuale, se non ne è già presente una nella rete virtuale.

    > [!NOTE] 
    > Non provare a questa macchina virtuale in toocreate hello stessa subnet come hello ASE perché esito negativo o causare problemi.
    >
    >

6. Impostare hello DNS per il dominio di base. È possibile usare un carattere jolly con il dominio nel DNS. test di alcune semplici toodo, modificare il file hosts hello nel toohello nome relativo a VM tooset hello web app indirizzo VIP IP:

    a. Se il ASE ha il nome di dominio di hello _. ilbase.com_ e si crea app web hello denominata _mytestapp_, essa viene indirizzata al _mytestapp.ilbase.com_. Impostare quindi _mytestapp.ilbase.com_ indirizzo di bilanciamento del carico interno toohello tooresolve. (In Windows, file hosts hello trova _C:\Windows\System32\drivers\etc\_.)

    b. tootest web distribuzione pubblicazione o accesso toohello avanzate console, creare un record per _mytestapp.scm.ilbase.com_.

7. Usare un browser su tale macchina virtuale e passare a http://mytestapp.ilbase.com. (O passare toowhatever che è il nome dell'applicazione web con il dominio).

8. Usare un browser in questa macchina virtuale e passare a https://mytestapp.ilbase.com. Se si utilizza un certificato autofirmato, accettare la mancanza di hello di sicurezza.

    indirizzo IP Hello per il bilanciamento del carico interno è elencato in **gli indirizzi IP**. Questo elenco contiene anche gli indirizzi IP hello utilizzati dall'indirizzo VIP esterno hello e per il traffico di gestione in ingresso.

    ![Indirizzo IP del servizio ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web processi, funzioni e hello ASE di bilanciamento del carico interno

Sono supportati sia le funzioni e processi web su ASE un bilanciamento del carico interno, ma per hello toowork portale con essi, è necessario disporre del sito di rete accesso toohello Gestione controllo servizi.  Ciò significa che il browser deve essere in un host che non è in o toohello di rete virtuale connessa.  

Quando si utilizzano le funzioni di Azure su ASE un bilanciamento del carico interno, è possibile che venga visualizzato un messaggio di errore che segnala "attualmente non sono in grado di tooretrieve delle funzioni attualmente. Riprovare più tardi". Questo errore si verifica perché hello funzioni UI sfrutta sito SCM hello tramite HTTPS e certificato radice hello non è presente nella catena di browser hello di trust. I processi Web presentano un problema simile. tooavoid questo problema è possibile eseguire una delle seguenti hello:

- Aggiungere l'archivio di certificati attendibili tooyour certificato hello. Questa operazione sblocca Microsoft Edge e Internet Explorer.
- Usare Chrome e andare prima sito SCM toohello, accettare certificati non attendibili hello e quindi passare toohello portale.
- Usare un certificato commerciale incluso nella catena di certificati del browser.  Questa è la soluzione migliore di hello.  

## <a name="dns-configuration"></a>Configurazione del DNS ##

Quando si utilizza un indirizzo VIP esterno, hello DNS è gestito da Azure. Qualsiasi applicazione creata nel ASE viene automaticamente aggiunto tooAzure DNS, ovvero un DNS pubblico. In un ambiente del servizio app ILB, è necessario gestire il proprio DNS. Per un dominio specifico, ad esempio _contoso.net_, è necessario toocreate A DNS registra nel DNS l'indirizzo di bilanciamento del carico interno punto tooyour per:

- *.contoso.net
- *.scm.contoso.net

Se il dominio di base di bilanciamento del carico interno viene utilizzato per più operazioni all'esterno di questo ASE, potrebbe essere necessario toomanage DNS in base al nome dell'app. Questo metodo è difficile perché è necessario tooadd ogni nuovo nome di applicazione in server DNS durante la creazione. Per questo motivo, è consigliabile usare un dominio dedicato.

## <a name="publish-with-an-ilb-ase"></a>Pubblicare con un ambiente del servizio app ILB ##

Per ogni app creata sono disponibili due endpoint. In un ambiente del servizio app ILB sono presenti *&lt;nome app>.&lt;Dominio ambiente del servizio app ILB>* e *&lt;nome app>.scm.&lt;Dominio ambiente del servizio app ILB>*. 

nome del sito di Gestione controllo servizi Hello accetta console Kudu toohello chiamato hello **portale avanzate**nell'hello portale di Azure. console Kudu Hello consente di visualizzare le variabili di ambiente, Esplora hello disco, utilizzare una console e molto altro ancora. Per informazioni, vedere [Kudu console for Azure App Service][Kudu] (Console Kudu per il servizio app di Azure). 

Multitenant hello servizio App e un ASE esterno è single sign-on tra hello portale di Azure e console Kudu hello. Per hello ASE ILB, tuttavia, è necessario toouse la pubblicazione toosign credenziali nella console Kudu hello.

L'endpoint di pubblicazione hello non è accessibile a internet, sistemi CI basato su Internet, ad esempio GitHub e Visual Studio Team Services, non funzionano con ASE un bilanciamento del carico interno. In alternativa, è necessario toouse un sistema di elemento di configurazione che utilizza un modello di pull, ad esempio Dropbox.

pubblicazione di endpoint Hello per le App in un bilanciamento del carico interno di ASE utilizzare dominio hello che hello che ase di bilanciamento del carico interno è stato creato con. Questo dominio viene visualizzato nel profilo di pubblicazione dell'applicazione hello e nel pannello del portale dell'applicazione hello (**Panoramica** > **Essentials** nonché **proprietà**). Se si dispone di un bilanciamento del carico interno di ASE con sottodominio hello *contoso.net* e un'app denominata *mytest*, utilizzare *mytest.contoso.net* per FTP e *mytest.scm.contoso.net*  per la distribuzione web.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Accoppiare un ambiente del servizio app ILB con un dispositivo WAF ##

Servizio App di Azure fornisce molte misure di sicurezza per proteggere il sistema hello. Consentono inoltre toodetermine se un'app è stata attaccata. la migliore protezione Hello per un'applicazione web è toocouple una piattaforma di hosting, ad esempio di servizio App di Azure, con un firewall applicazione web (WAF). Poiché hello ASE di bilanciamento del carico interno è un endpoint dell'applicazione di isolamento rete, è appropriato per tale tipo di utilizzo.

ulteriori informazioni sulla modalità tooconfigure ASE il bilanciamento del carico interno con un dispositivo WAF, vedere toolearn [configurare un firewall applicazione web con l'ambiente del servizio App][ASEWAF]. Questo articolo viene illustrato come toouse appliance virtuale Barracuda con il tipo di base. Un'altra opzione è toouse Gateway applicazione Azure. Gateway applicazione usa hello OWASP core regole toosecure tutte le applicazioni è posizionate dietro. Per ulteriori informazioni sul Gateway di applicazione, vedere [firewall applicazione web di Azure di introduzione toohello][AppGW].

## <a name="get-started"></a>Attività iniziali ##

Sono disponibili in tutti gli articoli e come-tooinstructions per ASEs il [file Leggimi per gli ambienti del servizio App][ASEReadme].

* vedere tooget introduttiva ASEs, [gli ambienti del servizio tooApp Introduzione][Intro].
* Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
