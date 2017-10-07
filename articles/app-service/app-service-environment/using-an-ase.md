---
title: aaaUse un ambiente del servizio App di Azure
description: Come toocreate, pubblicare e ridimensionare l'App in un ambiente di servizio App di Azure
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Usare un ambiente del servizio app #

## <a name="overview"></a>Panoramica ##

Ambiente del servizio app di Azure è una distribuzione di Servizio app di Azure in una subnet nella rete virtuale di Azure. È costituita da:

- **Front-end**: front-end hello sono in HTTP/HTTPS termina in un ambiente del servizio App (ASE).
- **Thread di lavoro**: lavoratori hello sono risorse hello che ospitano le applicazioni.
- **Database**: database hello contiene informazioni che definiscono l'ambiente hello.
- **Archiviazione**: hello trovi toohost utilizzati hello pubblicati cliente app.

> [!NOTE]
> Esistono due versioni dell'ambiente del servizio app: ASEv1 e ASEv2. In ASEv1, è necessario gestire le risorse di hello prima di utilizzarli. toolearn come tooconfigure e gestire ASEv1, vedere [configurare un v1 di ambiente del servizio App][ConfigureASEv1]. rest Hello di questo articolo è incentrato sui ASEv2.
>
>

È possibile distribuire un ambiente del servizio app (sia ASEv1 che ASEv2) con un indirizzo VIP esterno o interno per l'accesso app. distribuzione Hello con un indirizzo VIP esterno viene comunemente definita un ASE esterno. versione interna Hello viene chiamato hello ASE ILB perché utilizza un servizio di bilanciamento del carico interno (ILB). toolearn ulteriori informazioni su hello ASE di bilanciamento del carico interno, vedere [creare e usare un ASE ILB][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Creare un'app Web in un ambiente del servizio app ##

un'app web in un ASE toocreate, utilizzare hello stessa procedura quando si crea, in genere, ma con alcune piccole differenze. Quando si crea un nuovo piano di servizio app:

- Anziché scegliere una posizione geografica in cui toodeploy l'app, un ASE è scegliere come posizione di.
- Tutti i piani di servizio app creati in un ambiente del servizio app devono essere in un piano tariffario isolato.

Se non si dispone di un tipo di base, è possibile creare una seguendo le istruzioni hello [creare un ambiente del servizio App][MakeExternalASE].

un'app web in un ASE toocreate:

1. Selezionare **Nuovo** > **Web e dispositivi mobili** > **App Web**.

2. Immettere un nome per l'app web hello. Se è già stato selezionato un piano di servizio App in un tipo di base, il nome di dominio hello per app hello riflette il nome di dominio hello di hello ASE.

    ![Selezione del nome per l'app Web][1]

3. Selezionare una sottoscrizione.

4. Selezionare o immettere un nome per un nuovo gruppo di risorse **utilizzare esistente** e selezionarne uno dall'elenco a discesa hello.

5. Selezionare un piano di servizio app esistente nell'ambiente del servizio app o crearne uno nuovo con la procedura seguente:

    a. Selezionare **Crea nuovo**.

    b. Immettere il nome di hello per il piano di servizio App.

    c. Selezionare il ASE hello **percorso** elenco a discesa.

    d. Selezionare un piano tariffario **Isolato**. Scegliere **Seleziona**.

    e. Selezionare **OK**.
    
    ![Piani tariffari isolati][2]

6. Selezionare **Crea**.

## <a name="how-scale-works"></a>Come funziona il ridimensionamento ##

Ogni app del servizio app viene eseguita in un piano di servizio app. modello di contenitore Hello è ambienti contengono i piani di servizio App e i piani di servizio App contengono le app. Quando si scala un'app, si scala hello piano di servizio App e quindi ridimensionare tutte le app hello in hello stesso piano.

In ASEv2, quando si ridimensiona un piano di servizio App, viene aggiunto automaticamente infrastruttura hello necessita. Si verifica un ritardo di tempo tooscale operazioni durante l'aggiunta di infrastruttura hello. In ASEv1, è necessario aggiungere infrastruttura hello necessita prima di poter creare o scalabilità al piano di servizio App. 

In multitenant hello servizio App, il ridimensionamento è in genere immediato perché un pool di risorse è immediatamente disponibile toosupport è. In un ambiente del servizio app tale buffer non è disponibile e le risorse vengono allocate quando se ne presenta la necessità.

In un tipo di base, è possibile ridimensionare le istanze di too100. Queste 100 istanze possono essere tutte in un solo piano di servizio app o distribuite in più piani di servizio app.

## <a name="ip-addresses"></a>Indirizzi IP ##

Servizio app deve hello possibilità tooallocate un'app tooan di indirizzo IP dedicata. Questa funzionalità è disponibile dopo la configurazione SSL basato su IP, come descritto in [associare un esistente SSL certificato tooAzure web App personalizzate][ConfigureSSL]. Tuttavia, in un ambiente del servizio app vi è un'eccezione. Non è possibile aggiungere ulteriori IP indirizzi toobe utilizzato per SSL basato su IP in una base di bilanciamento del carico interno.

In ASEv1, è necessario gli indirizzi IP di hello tooallocate come risorse prima di utilizzarli. In ASEv2, utilizzarli dall'app, come avviene in multitenant hello servizio App. È sempre un indirizzo riserva ASEv2 degli indirizzi IP too30. Ogni volta che se ne usa uno, ne viene aggiunto un altro, in modo che sia sempre disponibile un indirizzo da usare. Un tempo di ritardo è necessario tooallocate un altro indirizzo IP, che impedisce l'aggiunta di IP indirizzi in rapida successione.

## <a name="front-end-scaling"></a>Scalabilità front-end ##

In ASEv2, quando scala in orizzontale i piani di servizio App, thread di lavoro vengono automaticamente aggiunti toosupport li. Ogni ambiente del servizio app viene creato con due front-end. Inoltre, front-end hello automaticamente scalabilità orizzontale a una velocità di un front-end per tutte le istanze del 15 nei piani di servizio App. Se ad esempio si hanno 15 istanze, si hanno tre front-end. Se si ridimensiona too30 istanze, è necessario quattro front-end e così via.

Questo numero di front-end deve essere più che sufficiente per la maggior parte degli scenari. Tuttavia, è possibile scalare orizzontalmente a una maggiore velocità. È possibile modificare il rapporto di hello tooas bassa come un front-end per ogni cinque istanze. È un addebito per la modifica delle proporzioni hello. Per altre informazioni, vedere [Prezzi del Servizio app di Azure][Pricing].

Risorse front-end sono endpoint HTTP/HTTPS hello per hello ASE. Con la configurazione front-end predefinita hello, utilizzo della memoria per front-end è costantemente circa 60%. I carichi di lavoro del cliente non vengono eseguiti in un front-end. Hello fattore chiave per un front-end con tooscale riguardo è CPU hello, che si basa principalmente sul traffico HTTPS.

## <a name="app-access"></a>Accesso all'app ##

In un ASE esterno, dominio hello utilizzato durante la creazione di applicazioni è diversa da multi-tenant hello servizio App. Include il nome di hello di hello ASE. Per ulteriori informazioni su come toocreate un ASE esterni, vedere [creare un ambiente del servizio App][MakeExternalASE]. nome di dominio Hello in un ASE esterno è simile a *.&lt; asename&gt;. p.azurewebsites.net*. Ad esempio, se il tipo di base è denominato _esterno ase_ e ospitare un'applicazione denominata _contoso_ in tale ASE, verrà visualizzata in hello URL seguenti:

- contoso.external-ase.p.azurewebsites.net
- contoso.scm.external-ase.p.azurewebsites.net

Hello URL contoso.scm.external-ase.p.azurewebsites.net è console Kudu di hello tooaccess utilizzati o per la pubblicazione distribuire l'app usando web. Per informazioni sulla console Kudu hello, vedere [console Kudu per il servizio App di Azure][Kudu]. Hello Kudu console offre un'interfaccia utente web per il debug, caricamento di file, la modifica di file e molto altro ancora.

In una base di bilanciamento del carico interno, dominio hello viene determinato in fase di distribuzione. Per ulteriori informazioni su come toocreate un bilanciamento del carico interno ASE, vedere [creare e usare un ASE ILB][MakeILBASE]. Se si specifica il nome di dominio hello _ilb ase.info_, hello App ASE utilizzare tale dominio durante la creazione di app. Per l'applicazione hello denominata _contoso_, hello URL sono:

- contoso.ilb-ase.info
- contoso.scm.ilb-ase.info

## <a name="publishing"></a>Pubblicazione ##

Come con multi-tenant hello servizio App, in un ASE è possibile pubblicare con:

- Distribuzione Web.
- FTP.
- Integrazione continua.
- Trascinare e rilasciare nella console Kudu hello.
- Un ambiente di sviluppo integrato, ad esempio Visual Studio, Eclipse o Intellij IDEA.

Con un ASE esterno, queste opzioni di pubblicazione che si comportano tutti hello stesso. Per altre informazioni, vedere [Distribuzione nel servizio app di Azure][AppDeploy]. 

differenza Hello con la pubblicazione è con tooan riguardo ASE di bilanciamento del carico interno. Con ASE un bilanciamento del carico interno, gli endpoint di pubblicazione di hello sono tutti disponibili solo tramite hello bilanciamento del carico interno. Hello bilanciamento del carico interno è un indirizzo IP privato nella subnet ASE hello nella rete virtuale hello. Se non si dispone di accesso di rete toohello ILB, è possibile pubblicare le applicazioni nella tale ASE. Come indicato nella [creare e usare un ASE ILB][MakeILBASE], è necessario tooconfigure DNS per le app hello nel sistema hello. Che include endpoint SCM hello. Se non definiti correttamente, non è possibile pubblicarli. L'IDE è inoltre necessitano toohave rete accesso toohello ILB in ordine toopublish tooit direttamente.

Poiché l'endpoint di pubblicazione hello non è possibile accedere a Internet, sistemi CI basato su Internet, ad esempio GitHub e Visual Studio Team Services, non funzionano con ASE un bilanciamento del carico interno. In alternativa, è necessario toouse un sistema di elemento di configurazione che utilizza un modello di pull, ad esempio Dropbox.

pubblicazione di endpoint Hello per le App in un bilanciamento del carico interno di ASE utilizzare dominio hello che hello che ase di bilanciamento del carico interno è stato creato con. È possibile visualizzarlo nel profilo di pubblicazione dell'applicazione hello e nel pannello del portale dell'applicazione hello (in **Panoramica** > **Essentials** e anche in **proprietà**). 

## <a name="pricing"></a>Prezzi ##

Hello prezzi SKU chiamato **Isolated** è stato creato per l'uso solo con ASEv2. In tutti i piani di servizio App che sono ospitati in ASEv2 hello Isolated prezzi SKU. I costi del piano di servizio app Isolato possono variare in base all'area. 

Inoltre i piani di prezzo toohello per il servizio App, quindi su una tariffa per ASE stesso. non vengono modificati con dimensione hello del ASE Hello fisse e paga per infrastruttura di hello ASE predefinito scala pari a 1 aggiuntive front-end per tutte le 15 istanze piano di servizio App.  

Se hello predefinito scala pari a 1 front-end per tutte le 15 istanze piano di servizio App non sono sufficientemente veloce, è possibile modificare il rapporto tra hello in cui vengono aggiunti front-end o hello dimensioni di hello front-end.  Quando si modifica il rapporto di hello o dimensioni, si paga per core hello front-end non verrebbero aggiunta per impostazione predefinita.  

Ad esempio, se si modifica hello scala rapporto too10, viene aggiunto un front-end per ogni 10 istanze nei piani di servizio App. tariffa flat Hello viene illustrata una frequenza di scala di un front-end per tutte le istanze del 15. Con un rapporto di scala di 10, addebitato il hello terzo front-end che è aggiunto per hello 10 istanze di piano di servizio App. Non è necessario toopay perché quando si raggiungono le 15 istanze perché è stato aggiunto automaticamente.

Se si dimensioni hello di core too2 front-end di hello regolate ma non modificare il rapporto hello e si paga per hello core aggiuntivi.  Un tipo di base viene creato con 2 server front-end, pertanto anche soglia hello automatico scala che si paga per 2 core aggiuntivi se è stato aumentato hello dimensioni too2 core front-end.

Per altre informazioni, vedere [Prezzi del Servizio app di Azure][Pricing].

## <a name="delete-an-ase"></a>Eliminare un ambiente del servizio app ##

toodelete un ASE: 

1. Utilizzare **eliminare** nella parte superiore di hello di hello **ambiente del servizio App** blade. 

2. Immettere il nome di hello del tooconfirm ASE che si desidera toodelete è. Quando si elimina un ASE, eliminare tutte hello contenuti all'interno di esso. 

    ![Eliminazione dell'ambiente del servizio app][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
