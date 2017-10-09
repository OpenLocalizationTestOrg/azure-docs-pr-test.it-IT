---
title: "aaaUnderstand identità di Azure | Documenti Microsoft"
description: "Informazioni di base di condizioni di soluzione di identità Microsoft Azure, i concetti e consigli per si toomake hello identità governance decisione migliore per l'organizzazione."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Informazioni sulle soluzioni di gestione delle identità di Azure
Microsoft Azure Active Directory (Azure AD) è una soluzione cloud completa per la gestione delle identità e degli accessi che fornisce servizi di directory, governance delle identità e gestione dell'accesso alle applicazioni. Azure AD rapidamente [Abilita single sign-on (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000 delle App preintegrate commerciali e personalizzate in hello [raccolta di applicazioni Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/). Molte di queste applicazioni sono già in uso, ad esempio Office 365, Salesforce.com, Box, ServiceNow e Workday.

Una singola directory di Azure AD viene associata automaticamente a una sottoscrizione di Azure al momento della sua creazione. Come servizio di identità hello in Azure, quindi di Azure AD fornisce tutte la gestione delle identità e le funzioni di controllo di accesso per le risorse basate su cloud. Queste risorse possono includere gli utenti, applicazioni e gruppi per un singolo tenant (organizzazione), come illustrato nel seguente diagramma hello:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure offre diverse identità di tooleverage modi contenuto come servizio (IDaaS) con livelli di complessità toomeet le singole esigenze dell'organizzazione. rest Hello di questo articolo consente di comprendere la terminologia di base identità di Azure e i concetti, nonché indicazioni si toomake hello migliore scelta delle opzioni disponibili hello.

## <a name="terms-tooknow"></a>Termini tooknow

Prima può stabilire una soluzione di identità di Azure per l'organizzazione, è necessario una conoscenza di base dei termini di hello comunemente utilizzati durante la comunicazione con informazioni sui servizi di identità di Azure.

|Termine tooknow| Descrizione|
|-----|-----|
|Sottoscrizione di Azure |Sottoscrizioni sono toopay utilizzato per i servizi cloud di Azure e sono in genere collegati tooa carta di credito. È possibile avere più sottoscrizioni, ma può essere difficile tooshare risorse tra le sottoscrizioni.|
|Tenant di Azure | Un tenant di Azure AD rappresenta un'unica organizzazione. Si tratta di un'istanza attendibile e dedicata di Azure AD che viene creata automaticamente quando un'organizzazione si registra a una sottoscrizione a un servizio cloud Microsoft, ad esempio Azure, Intune o Office 365. I tenant possono ottenere accesso tooservices in un ambiente dedicato (tenant singolo) o in un ambiente condiviso con altre organizzazioni (multi-tenant).|
|Directory di Azure AD | Ogni tenant di Azure ha un Azure dedicato, attendibile directory di Active Directory che contiene gli utenti, gruppi e le applicazioni del tenant hello. Si tratta di funzioni di gestione di identità e accessi tooperform utilizzato per le risorse tenant. Poiché un univoco directory di Azure AD viene automaticamente eseguito il provisioning toorepresent dell'organizzazione quando effettua l'iscrizione per un servizio cloud di Microsoft Azure, Microsoft Intune o Office 365, talvolta vedrai termini hello *tenant*, *AD azure*, e *directory di Azure AD* usato in modo intercambiabile. |
|Dominio personalizzato | Quando ci si registra per la prima volta a una sottoscrizione a un servizio cloud Microsoft il tenant (organizzazione) usa un nome di dominio *.onmicrosoft.com*. Tuttavia, molte organizzazioni dispongono di uno o più nomi di dominio che sono utilizzati toodo business e che gli utenti finali utilizzano alle risorse aziendali tooaccess. È possibile aggiungere il tooAzure nome di dominio personalizzato AD in modo che hello nome di dominio sia gli utenti tooyour familiarità, ad esempio  *alice@contoso.com*  anziché  *alice@contoso.onmicrosoft.com* . |
|Account Azure AD | Si tratta delle identità create tramite Azure AD o un altro servizio cloud Microsoft, ad esempio Office 365. Sono archiviati in Azure AD e accessibile tooany di sottoscrizioni a servizi cloud dell'organizzazione hello. |
|Amministratore della sottoscrizione di Azure| amministratore dell'account Hello è hello persona iscritti a o acquistati hello sottoscrizione di Azure. Utilizzo di hello [centro Account](https://account.windowsazure.com/Home/Index) tooperform varie attività di gestione, come creare sottoscrizioni, annullare sottoscrizioni, modificare la fatturazione hello per una sottoscrizione o modificare hello amministratore del servizio. |
|Amministrazione globale di Azure AD | Gli amministratori globali di Azure AD avere le funzionalità amministrative di Azure AD tooall accesso completo. Hello chi effettua l'iscrizione per una sottoscrizione al servizio cloud Microsoft, automaticamente diventa un amministratore globale per impostazione predefinita. È possibile avere più di un amministratore globale, ma solo gli amministratori globali possono assegnare uno qualsiasi degli [hello altri ruoli di amministratore](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Account Microsoft | Gli account Microsoft (creati dall'utente per uso personale) forniscono accesso orientata ai servizi tooconsumer Microsoft prodotti e servizi cloud, come Outlook (Hotmail), OneDrive, Xbox LIVE o Office 365. Queste identità vengono create e archiviate nel sistema di Microsoft consumer identità account gestito da Microsoft hello.|
|Account aziendali o dell'istituto di istruzione | Gli account aziendali o dell'istituto di istruzione (emessi da un amministratore per l'utilizzo di business/academic) forniscono accesso tooenterprise a livello aziendale servizi cloud Microsoft, ad esempio Office 365, Intune o Azure.|


## <a name="concepts-toounderstand"></a>Concetti toounderstand

Ora che si conoscono i termini di identità di Azure basic hello, imparare ulteriori informazioni su questi concetti di identità di Azure che consentono di prendere una decisione di servizio informate identità di Azure.

|Concetto toounderstand |Descrizione|
|-----|-----|
|[Associare le sottoscrizioni di Azure ad Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Ogni sottoscrizione Azure ha una relazione di trust con di Azure AD directory tooauthenticate utenti, servizi e dispositivi. *Più sottoscrizioni possono considerare attendibile directory hello stesso Azure Active Directory, ma una sottoscrizione considererà attendibili solo una singola directory di Azure AD*. Questa relazione di trust è diversa dalla relazione hello che dispone di una sottoscrizione con altre risorse di Azure (siti Web, database e così via), che sono piuttosto risorse figlio di una sottoscrizione. Se una sottoscrizione scade, quindi tooresources di accesso associato alla sottoscrizione hello diverso da Azure AD anche si arresta. Directory di Azure AD hello rimane tuttavia in Azure, in modo che è possibile associare un'altra sottoscrizione a tale directory e continuare toomanage risorse del tenant.|
|[Come funzionano le licenze di Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Quando si acquistano o attivare Enterprise Mobility Suite, Azure AD Premium o Azure AD Basic, la directory viene aggiornati con sottoscrizione di hello, incluso il periodo di validità e licenze prepagato. Una volta sottoscrizione hello è attivo, servizio hello può essere gestito dagli amministratori globali di Azure AD e utilizzato dagli utenti con licenza. Le informazioni di sottoscrizione, tra cui hello numero di licenze assegnate o disponibile, sono disponibile nel portale di Azure da hello hello **Azure Active Directory** > **licenze** blade. Anche questo è hello toomanage sul posto migliore le assegnazioni delle licenze.|
|[Controllo di accesso basato sui ruoli nel portale di Azure hello](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Il controllo di accesso in base al ruolo aiuta nella gestione specifica degli accessi per le risorse di Azure. Numero eccessivo di autorizzazioni possono esporre e tooattackers dell'account. Un numero di autorizzazioni insufficiente ostacola l'efficienza del lavoro dei dipendenti. Usa tale controllo, è possibile assegnare i dipendenti hello esatta delle autorizzazioni necessarie in base a tre ruoli di base che si applicano i gruppi di risorse tooall: proprietario, collaboratore e lettore. È inoltre possibile creare backup too2, 000 personalizzati [ruoli RBAC personalizzati](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet le specifiche esigenze. |
|[Identità ibrida](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|L'identità ibrida viene ottenuta tramite l'integrazione di AD DS locale con Azure AD tramite [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). In questo modo tooprovide un'identità comune per gli utenti di Office 365, Azure e applicazioni locali o applicazioni SaaS integrata con Azure AD. Con identità ibrida, è efficace estendere locale cloud toohello ambiente per l'accesso e identità.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>differenza Hello tra servizi di dominio di Windows Server Active Directory e Azure AD
Sia Azure Active Directory (Azure AD) che Active Directory locale (Active Directory Domain Services o AD DS) sono sistemi che archiviano i dati nella directory e gestiscono le comunicazioni tra utenti e risorse, compresi processi di accesso degli utenti, autenticazione e ricerche nelle directory.

Se si ha già familiarità con locale Windows Server Active Directory Domain Services (AD DS), introdotta con Windows 2000 Server, quindi è probabilmente comprendere concetti di base hello di un servizio di identità. Tuttavia, è anche importante toounderstand che Azure AD non è semplicemente un controller di dominio nel cloud hello. È un modo completamente nuovo di fornire l'identità come servizio (IDaaS) in Azure che richiede un modo completamente nuovo funzionalità pensare toofully critici basati su cloud e protezione l'organizzazione da eventuali minacce più recenti. 

AD DS è un ruolo server in Windows Server; ciò significa che può essere distribuito in macchine virtuali o fisiche. Dispone di una struttura gerarchica basata su X.500. Usa DNS per l'individuazione degli oggetti, supporta interazioni tramite LDAP e usa principalmente Kerberos per l'autenticazione. Active Directory consente di unità organizzative (OU) e oggetti Criteri di gruppo (GPO) toojoining macchine toohello domini e trust vengono create anche tra domini.

I reparti IT hanno protetto per anni il proprio perimetro di sicurezza usando AD DS, ma le aziende odierne, senza più confini perimetrali e impegnate a supportare le esigenze di gestione delle identità di dipendenti, clienti e partner, esigono nuovi piani di controllo. Azure AD è la risposta a questa esigenza. Protezione è stato spostato oltre cloud toohello di firewall aziendale hello in Azure AD consente di proteggere risorse della società e accesso fornendo un'identità comune per gli utenti (in locale o nel cloud hello). In questo modo il toosecurely flessibilità di hello utenti accesso hello App che necessarie tooget proprio lavoro da quasi qualsiasi dispositivo. I controlli di protezione dati basati sui rischi trasparente, supportati da funzionalità di machine learning e la segnalazione dettagliata, sono inoltre disponibili società tookeep esigenze IT della protezione dei dati.

Azure AD è un servizio directory pubblico a più clienti, il che significa che in Azure AD è possibile creare un tenant per i server cloud e le applicazioni come Office 365. Utenti e gruppi vengono creati in una struttura piatta senza unità organizzative o oggetti Criteri di gruppo. L'autenticazione viene eseguita tramite protocolli, come SAML, WS-Federation e OAuth. È possibile tooquery Azure AD, ma anziché utilizzare LDAP è necessario utilizzare un'API REST chiamata API Graph di AD. Tutte queste operazioni possono essere eseguite su HTTP e HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Estendere le funzionalità di gestione e protezione di Office 365
Siete già utenti di Office 365? È possibile accelerare la trasformazione digitale mediante l'estensione tutte le risorse di Office 365 integrate con Azure AD toosecure compromettere la produttività sicura il personale. Quando si usa Azure AD, inoltre tooOffice 365 funzionalità, è possibile proteggere il portfolio di tutta l'applicazione con un'identità che abilita single sign-on per tutte le app. Le funzionalità di accesso condizionale sono ampliabili non solo in base allo stato del dispositivo, ma in base all'utente, alla posizione, all'applicazione e anche al rischio. Le funzionalità multi-factor authentication (MFA) sono in grado di offrire ulteriore protezione quando necessario. Aggiungono capacità di supervisione dei privilegi utente e forniscono l'accesso amministrativo su richiesta, just-in-time. Gli utenti verranno essere più produttivi e creare ticket di supporto tecnico meno, funzionalità self-service toohello grazie AD Azure fornisce ad esempio la reimpostazione delle password dimenticata, le richieste di accesso dell'applicazione, nonché la creazione e gestione dei gruppi.

> [!TIP]
> Desidera toolearn ulteriori informazioni sull'utilizzo di gestione delle identità di Azure AD con Office 365? [Ottenere hello e-book](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Soluzioni di gestione delle identità di Microsoft Azure

Microsoft Azure offre diversi modi toomanage identità degli utenti se vengono gestiti completamente in locale, solo in hello cloud o anche una posizione al suo interno. Tali opzioni includono AD DS "fai da te" in Azure, Azure Active Directory (Azure AD), Soluzione ibrida di gestione delle identità e Azure AD Domain Services.

### <a name="do-it-yourself-diy-ad-ds"></a>AD DS "fai da te"
Per le aziende che necessitano solo di un footprint ridotto nel cloud hello, **fai da te (DIY) AD DS** in Azure può essere utilizzato. Questa opzione supporta numerosi scenari con Windows Server AD DS, particolarmente adatti per la distribuzione di macchine virtuali (VM) in Azure. Ad esempio, è possibile creare una macchina virtuale di Azure come controller di dominio in esecuzione in un Data Center lontani di rete remota toohello connesso. Da qui, hello VM potrebbe essere in grado di toosupport le richieste di autenticazione dagli utenti remoti e migliorare le prestazioni. Questa opzione è inoltre ideale come un siti di ripristino di emergenza costosi toootherwise substitute relativamente basso costo per l'hosting di un numero esiguo di controller di dominio e una singola rete virtuale in Azure. Infine, si potrebbe essere necessario toodeploy un'applicazione in Azure, ad esempio SharePoint, che richiede i servizi di dominio di Windows Server Active Directory, ma non sono presenti dipendenze nella rete locale hello o hello Windows Server Active Directory aziendale. In questo caso, è possibile distribuire una foresta isolata in requisiti di Azure toomeet hello SharePoint server farm. È anche supportato toodeploy applicazioni di rete che richiedono una rete locale di connettività toohello e hello Active Directory locale.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD standalone** è una soluzione basata sul cloud globale e autonoma per la gestione delle identità e dell'accesso come servizio (IDaaS). Azure AD offre un set affidabile di funzionalità toomanage utenti e gruppi. Consente di proteggere l'accesso locale tooon cloud e applicazioni, compresi servizi web di Microsoft come Office 365 e numerose applicazioni software non Microsoft come applicazioni di servizio (SaaS). Azure AD è disponibile in tre edizioni: gratuita, Basic e Premium. Azure AD aumenta l'efficacia dell'organizzazione ed estende oltre hello perimetrale firewall tooa nuovo piano di controllo protetto da Azure machine learning e altre funzionalità di sicurezza avanzate.

### <a name="hybrid-identity"></a>Identità ibrida
Invece di scegliere tra le soluzioni di identità basati su cloud o locali, molti forni CIO e le aziende, che ha iniziato prevedendo direzione a lungo termine della propria azienda, estende locale cloud toohello directory tramite **identità ibride** soluzioni. Con identità ibrida, si ottiene un'identità davvero globale e soluzione di gestione di accesso che fornisce l'accesso sicuro e produttivo toohello agli utenti di applicazioni deve toodo i processi.

> [!TIP]
> altre informazioni sulle toolearn come CIO apportate Azure Active Directory parte centrale di strategie IT download hello [tooAzure Guida CIO Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Servizi di dominio Azure Active Directory
**Servizi di dominio AD Azure** vengono forniti i requisiti di identità locale toouse un'opzione basato su cloud di dominio Active Directory per il controllo di configurazione di macchina virtuale di Azure leggero e toomeet un modo per lo sviluppo di applicazioni di rete e il test. Servizi di dominio Active Directory di Azure non è stato progettato toolift e spostare locale di dominio Active Directory infrastruttura tooAzure macchine virtuali gestiti da servizi di dominio Active Directory di Azure. In alternativa, hello macchine virtuali di Azure nei domini gestiti deve essere utilizzato toosupport hello sviluppo, test e lo spostamento di applicazioni locali che richiedono cloud toohello metodi autenticazione di dominio Active Directory.

## <a name="common-scenarios-and-recommendations"></a>Scenari comuni e raccomandazioni

Ecco alcuni scenari comuni di identità e accessi ai consigli come toowhich opzione identità Azure potrebbero essere più appropriata per ognuno.

|Scenario di gestione delle identità| Raccomandazione|
|-----|-----|
|L'organizzazione ha grandi investimenti in locale Windows Server Active Directory, ma desideriamo cloud toohello di tooextend identità.| soluzione di identità Azure Hello più diffuse [identità ibride](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Se sono già state apportate investimenti in locale di dominio Active Directory, è possibile estendere facilmente cloud toohello identità con Azure AD Connect.|
|La mia azienda è nato nel cloud hello e non abbiamo investimenti in soluzioni di identità locali.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) migliore hello per le aziende solo cloud senza investimenti in locale.|
|È necessario lightweight macchina virtuale di Azure configurazione e controllo toomeet locale i requisiti di identità per lo sviluppo di app e il test.|[Servizi di dominio AD Azure](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) è una buona scelta per toouse di dominio Active Directory per il controllo della configurazione macchina virtuale di Azure lightweight o ricerca toodevelop o eseguire la migrazione cloud toohello di applicazioni legacy, in grado di riconoscere directory locale.|  
|È necessario toosupport poche macchine virtuali in Azure, ma la mia azienda è ancora ampiamente investito in locale di Active Directory (AD DS).|Utilizzare [DIY AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse macchine virtuali di Azure quando è necessario toosupport poche macchine virtuali e si dispone di grandi dimensioni di dominio Active Directory gli investimenti in locale. |

## <a name="where-can-i-learn-more"></a>Altre informazioni
Sono disponibili moltissime toohelp di numerose risorse online tutte le informazioni su Azure AD. Di seguito è riportato un elenco di articoli grande tooget che è stato avviato:

* [Abilitazione della directory per la gestione ibrida con Azure AD Connect](active-directory-aadconnect.md)
* [Sicurezza aggiuntiva per un mondo sempre connesso](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Introduzione ad Azure AD Report](active-directory-reporting-getting-started.md)
* [Gestire le password da qualsiasi posizione](active-directory-passwords.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Automatizzare Provisioning e Deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Come tooprovide proteggere l'accesso remoto applicazioni tooon locali](active-directory-application-proxy-get-started.md)
* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Che cosa sono le licenze di Microsoft Azure Active Directory?](active-directory-licensing-what-is.md)
* [Come individuare app cloud non autorizzate usate nell'organizzazione](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Passaggi successivi

Ora che comprendere concetti di identità di Azure e tooyou di hello opzioni disponibili, è possibile utilizzare hello dopo risorse tooget avviato implementazione hello opzione scelta:

[Altre informazioni sulle soluzioni per la gestione delle identità ibride di Azure](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Altre informazioni in un ambiente Azure di prova](https://aka.ms/aad-poc)

[Distribuire Azure AD nell'ambiente di produzione](https://aka.ms/aad-onboard)
