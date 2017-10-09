---
title: 'Azure AD Connect: installazione personalizzata | Documentazione Microsoft'
description: Questo documento illustra in dettaglio le opzioni di installazione personalizzata hello per Azure AD Connect. Utilizzare queste tooinstall istruzioni Active Directory tramite Azure AD Connect.
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Installazione personalizzata di Azure AD Connect
Azure AD Connect **impostazioni personalizzate** viene utilizzato quando si desiderano più opzioni per l'installazione di hello. Se si dispone di più insiemi di strutture o se si desidera tooconfigure funzionalità opzionali non trattate in Installazione rapida hello viene utilizzato. Viene utilizzata in tutti i casi in cui hello [ **express installazione** ](active-directory-aadconnect-get-started-express.md) opzione non soddisfa la topologia o alla distribuzione.

Prima di iniziare l'installazione di Azure AD Connect, verificare che sia troppo[scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e prerequisito hello completato i passaggi [Azure AD Connect: prerequisiti Hardware e](active-directory-aadconnect-prerequisites.md). Verificare anche che siano disponibili gli account obbligatori descritti in [Autorizzazioni e account di Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Se le impostazioni personalizzate non corrisponde a una topologia, ad esempio tooupgrade DirSync, vedere [correlati documentazione](#related-documentation) per altri scenari.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Installazione di Impostazioni personalizzate di Azure AD Connect
### <a name="express-settings"></a>Impostazioni rapide
In questa pagina, fare clic su **Personalizza** toostart un'installazione di impostazioni personalizzate.

### <a name="install-required-components"></a>Installare i componenti necessari
Quando si installa Servizi di sincronizzazione hello, è possibile lasciare deselezionata la sezione di configurazione facoltativa hello e Azure AD Connect consente di impostare tutti gli elementi automaticamente. Imposta un'istanza di SQL Server 2012 Express LocalDB, creare gruppi appropriati hello e assegnare le autorizzazioni. Se si desiderano toochange hello predefinite, è possibile utilizzare hello seguenti tabella toounderstand hello configurazione facoltativa opzioni sono disponibili.

![Componenti richiesti](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configurazione facoltativa | Descrizione |
| --- | --- |
| Usare un server SQL esistente |Consente di toospecify hello SQL Server e il nome di istanza hello. Scegliere questa opzione se si dispone già di un server di database che si desidera toouse. Immettere il nome di istanza hello seguito da un virgola e numero di porta in **nome dell'istanza** se SQL Server non ha la funzionalità di navigazione. |
| Usare un account di servizio esistente |Per impostazione predefinita Azure AD Connect utilizza un account servizio virtuale toouse servizi di sincronizzazione hello. Se si utilizza un server SQL remoto o un proxy che richiede l'autenticazione, è necessario toouse un **account del servizio gestito** oppure utilizzare un account del servizio nel dominio hello e conoscere la password hello. In questi casi, immettere toouse account hello. Verificare che l'utente hello che esegue l'installazione di hello è un'associazione di sicurezza in SQL, pertanto è possibile creare un account di accesso per l'account del servizio hello. Vedere [Autorizzazioni e account di Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Specificare i gruppi di sincronizzazione personalizzati |Per impostazione predefinita Connetti AD Azure crea quattro gruppi di server locali toohello quando vengono installati i servizi di sincronizzazione hello. Questi gruppi sono: gruppo Administrators, gruppo di operatori, gruppo Sfoglia e hello gruppo Reimposta Password. È possibile specificare qui i gruppi personalizzati. gruppi di Hello devono essere locali nel server di hello e non possono trovarsi nel dominio hello. |

### <a name="user-sign-in"></a>Accesso utente
Dopo l'installazione dei componenti di hello necessario, viene chiesto tooselect utenti single sign-on metodo. Hello nella tabella seguente fornisce una breve descrizione delle opzioni disponibili hello. Per una descrizione completa dei metodi di accesso hello, vedere [account utente](active-directory-aadconnect-user-signin.md).

![Accesso utente](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Opzione Single Sign-On | Descrizione |
| --- | --- |
| Sincronizzazione delle password |Gli utenti sono in grado di toosign in servizi cloud tooMicrosoft, ad esempio Office 365, utilizzando hello stessa password usata nella propria rete locale. le password di utenti Hello sono sincronizzati tooAzure Active Directory come un hash della password e l'autenticazione viene eseguita nel cloud hello. Per altre informazioni, vedere [Sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) . |
|Autenticazione pass-through (anteprima)|Gli utenti sono in grado di toosign in servizi cloud tooMicrosoft, ad esempio Office 365, utilizzando hello stessa password usata nella propria rete locale.  password utente Hello viene passata tramite toobe controller Active Directory locale di toohello convalidato.
| Federazione con ADFS |Gli utenti sono in grado di toosign in servizi cloud tooMicrosoft, ad esempio Office 365, utilizzando hello stessa password usata nella propria rete locale.  vengono reindirizzati gli utenti di Hello tootheir toosign di istanza di AD FS in locale e l'autenticazione viene eseguita in locale. |
| Non configurare |Nessuna funzionalità verrà installata e configurata. Scegliere questa opzione se si dispone già di un server federativo di terze parti o di un'altra soluzione esistente installata. |
|Abilita Single Sign-On|Questa opzione è disponibile con la sincronizzazione delle password e l'autenticazione pass-through e offre un unico segno sull'esperienza per gli utenti desktop rete aziendale hello.  Per altre informazioni, vedere [Single Sign-On](active-directory-aadconnect-sso.md) (Accesso Single Sign-On). </br>Nota per i clienti AD FS questa opzione non è disponibile perché ADFS già offerte hello dello stesso livello di Single sign-on.</br>(se PTA non viene rilasciato in hello contemporaneamente)
|Opzione Accesso|Questa opzione è disponibile per i clienti di sincronizzazione password e fornisce un accesso single sign sull'esperienza per utenti desktop nella rete aziendale hello.  </br>Per altre informazioni, vedere [Single Sign-On](active-directory-aadconnect-sso.md) (Accesso Single Sign-On). </br>Nota per i clienti AD FS questa opzione non è disponibile perché ADFS già offerte hello dello stesso livello di Single sign-on.


### <a name="connect-tooazure-ad"></a>Connettersi AD tooAzure
Nella schermata di tooAzure AD Connect hello, immettere un account di amministratore globale e una password. Se si seleziona **federazione con ADFS** pagina precedente, hello non accedere con un account in un dominio si prevede di tooenable per la federazione. Si consiglia di un account predefinito hello toouse **onmicrosoft.com** dominio, che viene fornito con la directory di Azure AD.

Questo account è solo toocreate utilizzato un account del servizio in Azure AD e non viene utilizzato una volta completata la procedura guidata hello.  
![Accesso utente](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Se l'account amministratore globale è abilitato con autenticazione a più fattori, è necessario password hello tooprovide nel popup di accesso hello e hello completa la richiesta di autenticazione a più fattori. potrebbe essere richiesta Hello fornendo un codice di verifica o una chiamata telefonica.  
![Accesso utente in MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

account di amministratore globale di Hello può anche avere [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) abilitato.

Se viene visualizzato un errore e si hanno problemi di connettività, vedere [Risolvere i problemi di connettività](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Pagine nella sezione hello sincronizzazione

### <a name="connect-your-directories"></a>Connessione delle directory
Azure AD Connect tooconnect tooyour servizi di dominio Active Directory, è necessario il nome di foresta hello e le credenziali di un account con autorizzazioni sufficienti.

![Directory di connessione](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Dopo aver immesso il nome di foresta hello e facendo clic su **Aggiungi Directory**, una finestra di dialogo popup viene visualizzata e viene chiesto di hello le opzioni seguenti:

| Opzione | Descrizione |
| --- | --- |
| Usare l'account esistente | Selezionare questa opzione se si desidera account tooprovide un dominio di Active Directory esistente toobe utilizzati Azure AD Connect per la connessione AD toohello foresta durante la sincronizzazione delle directory. È possibile immettere parte del dominio hello in formato FQDN o NetBios, vale a dire FABRIKAM\syncuser o fabrikam.com\syncuser. Questo account può essere un account utente normale, perché sono necessarie solo le autorizzazioni di lettura predefinite hello. Tuttavia, a seconda dello scenario, potrebbero essere necessarie autorizzazioni aggiuntive. Per altre informazioni, vedere [Azure AD Connect: account e autorizzazioni](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Crea un nuovo account | Selezionare questa opzione se si desidera l'account di Azure AD Connect guidata toocreate hello di dominio Active Directory richiesti da Azure AD Connect per connessione foresta di Active Directory toohello durante la sincronizzazione della directory. Quando questa opzione è selezionata, immettere nome utente hello e una password per un account di amministratore dell'organizzazione. Hello enterprise admin specificato verrà utilizzato l'account da Azure AD Connect hello toocreate guidata richiesto l'account di dominio Active Directory. È possibile immettere parte del dominio hello in formato FQDN o NetBios, vale a dire FABRIKAM\administrator o fabrikam.com\administrator. |

![Directory di connessione](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Configurazione dell'accesso ad Azure AD
Questa pagina consente tooreview domini UPN di hello presenti in locale di dominio Active Directory e che sono state verificate in Azure AD. Questa pagina consente inoltre tooconfigure hello attributo toouse per hello userPrincipalName.

![Domini non verificati](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Verificare ogni dominio contrassegnato come **Non aggiunto** e **Non verificato**. Assicurarsi che i domini usati siano stati verificati in Azure AD. Dopo avere verificato i domini, fare clic su simboli aggiornamento hello. Per ulteriori informazioni, vedere [aggiungere e verificare il dominio hello](../active-directory-add-domain.md)

**UserPrincipalName** -hello attributo userPrincipalName è utenti di attributo hello utilizzano quando effettuano l'accesso in tooAzure AD e Office 365. domini Hello utilizzato, noto anche come suffisso UPN hello, deve essere verificato in Azure AD prima di hello utenti sono sincronizzati. Microsoft consiglia di tookeep hello predefinito attributo userPrincipalName. Se questo attributo non è instradabile e non può essere verificato, quindi è possibile tooselect un altro attributo. È possibile selezionare, ad esempio posta elettronica come attributo hello tenendo hello ID di accesso. Un attributo diverso da userPrincipalName viene definito **ID alternativo**. valore dell'attributo ID alternativo Hello deve seguire hello RFC822 standard. È possibile usare un ID alternativo con la sincronizzazione password e la federazione.

>[!NOTE]
> Quando si abilita l'autenticazione pass-through è necessario disporre di almeno un dominio verificato in ordine toocontinue guidata hello.

> [!WARNING]
> L'uso di un ID alternativo non è compatibile con tutti i carichi di lavoro di Office 365. Per ulteriori informazioni, vedere troppo[la configurazione di ID di accesso alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtro unità organizzativa e dominio
Per impostazione predefinita, vengono sincronizzati tutti i domini e le unità organizzative. Se sono presenti alcuni domini o unità organizzative toosynchronize tooAzure Active Directory non si desidera, è possibile deselezionare questi domini e unità organizzative.  
![Filtro DomainOU](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Questa pagina nella creazione guidata hello consiste nella configurazione di applicazione di filtri basati su dominio e unità Organizzativa. Se si prevede di toomake modifiche, vedere [il filtro basato su dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) e [il filtro basato su unità organizzativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) prima di apportare queste modifiche. Alcune unità organizzative sono essenziali per la funzionalità di hello e non devono essere deselezionate.

Se si usa il filtro basato sull'unità organizzativa con una versione di Azure AD Connect precedente alla 1.1.524.0, le nuove unità organizzative aggiunte successivamente vengono sincronizzate per impostazione predefinita. Se si desidera che la nuova comportamento hello non devono essere sincronizzate unità organizzative, quindi è possibile configurare una volta completata la procedura guidata hello con [il filtro basato su unità organizzativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Per Azure AD Connect versione 1.1.524.0 o dopo, è possibile indicare se si desidera nuovo toobe unità organizzative sincronizzato o meno.

Se si prevede di toouse [filtraggio basato su un gruppo](#sync-filtering-based-on-groups), quindi verificare che hello unità Organizzativa con gruppo hello sia incluso e non filtrato con filtro unità Organizzativa. Il filtro basato sull'unità organizzativa viene valutato prima del filtro basato sul gruppo.

È anche possibile che alcuni domini non sono raggiungibili a causa di restrizioni toofirewall. Questi domini vengono deselezionati per impostazione predefinita e viene visualizzato un avviso.  
![Domini non raggiungibili](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Se viene visualizzato questo avviso, assicurarsi che questi domini non sono raggiungibili effettivamente e avviso hello è previsto.

### <a name="uniquely-identifying-your-users"></a>Identificazione univoca degli utenti

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Selezionare la modalità di identificazione degli utenti nelle directory locali
Hello corrispondenza tra foreste consente toodefine come utenti le foreste di Active Directory sono rappresentati in Azure AD. Un utente può essere rappresentato solo una volta in tutte le foreste oppure disporre di una combinazione di account abilitati e disabilitati. utente Hello potrebbe anche essere rappresentato come un contatto in alcuni insiemi di strutture.

![Univoco](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Impostazione | Descrizione |
| --- | --- |
| [Gli utenti vengono rappresentati solo una volta nel numero totale delle foreste](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Tutti gli utenti vengono creati come singoli oggetti in Azure AD. non sono aggiunti gli oggetti Hello hello metaverse. |
| [Attributo di posta](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Questa opzione consente di abbinare utenti e contatti se l'attributo mail hello è hello stesso valore in foreste diverse. Usare questa opzione quando i contatti sono stati creati mediante GALSync. Se si sceglie questa opzione, gli oggetti utente il cui attributo di posta elettronica non vengono popolati non sarà sincronizzato tooAzure Active Directory. |
| [ObjectSID e msExchangeMasterAccountSID/msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Questa opzione unisce un utente abilitato in una foresta di account a un utente disabilitato in una foresta di risorse. In Exchange questa configurazione è definita cassetta postale collegata. Questa opzione può essere utilizzata anche se si utilizza solo Lync ed Exchange non è presente nella foresta di risorse hello. |
| sAMAccountName e MailNickName |Questa opzione Crea un join tra gli attributi di cui è previsto hello-ID di accesso utente hello è reperibile. |
| Attributo specifico |Questa opzione consente di tooselect un attributo personalizzato. Se si sceglie questa opzione, gli oggetti utente il cui attributo (selezionata) non vengono popolati non sarà sincronizzato tooAzure Active Directory. **Limitazione:** rendere toopick che un attributo che già è reperibile nel metaverse hello. Se si seleziona un attributo personalizzato (non nel metaverse hello), non può completare la procedura guidata hello. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Selezionare la modalità di identificazione degli utenti con Azure AD: ancoraggio di origine
Hello attributo sourceAnchor è un attributo che non è modificabile nel corso della durata hello di un oggetto utente. È una chiave primaria di hello collegamento utente locale hello con utente hello in Azure AD.

| Impostazione | Descrizione |
| --- | --- |
| Consentire ad Azure di gestire l'ancoraggio di origine hello per me | Selezionare questa opzione se si desidera attributo hello toopick di Azure AD per l'utente. Se si seleziona questa opzione, la procedura guidata Azure AD Connect si applica la logica selezione attributo sourceAnchor hello descritta nella sezione articolo [Azure AD Connect: concetti - utilizzando l'attributo msDS-ConsistencyGuid come sourceAnchor progettare](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). la procedura guidata Hello informa l'attributo è stato selezionato come attributo di ancoraggio di origine hello al termine dell'installazione personalizzata. |
| Attributo specifico | Selezionare questa opzione se si desidera toospecify un attributo di Active Directory esistente come attributo sourceAnchor hello. |

Poiché hello non può essere modificato, è necessario pianificare toouse un attributo valido. objectGUID è un candidato valido. Questo attributo non viene modificato, a meno che l'account utente di hello viene spostato tra foreste o domini. In un ambiente a più foreste in cui spostare account tra foreste, un altro attributo deve essere usato, ad esempio un attributo con hello employeeID. Evitare gli attributi che subirebbero modifiche in caso di matrimonio o nuova assegnazione dell'utente. Non è possibile usare attributi con @-sign, quindi non è possibile usare email e userPrincipalName. attributo di Hello è anche distinzione maiuscole/minuscole pertanto quando si sposta un oggetto tra foreste, assicurarsi che toopreserve hello lettere maiuscole e. Gli attributo binari hanno una codifica di tipo base64, ma altri tipi di attributi mantengono lo stato non codificato. Negli scenari di federazione e in alcune interfacce di Azure AD questo attributo è noto anche come immutableID. Ulteriori informazioni su ancoraggio di origine hello sono reperibile in hello [progettare concetti](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtro di sincronizzazione basato sui gruppi
Hello filtrare la funzionalità gruppi di consente toosync solo un piccolo subset di oggetti per un progetto pilota. toouse tale funzionalità, creare un gruppo per questo scopo in Active Directory locale. Aggiungere quindi gli utenti e gruppi che devono essere sincronizzati tooAzure Active Directory come membri diretti. In un secondo momento, è possibile aggiungere e rimuovere utenti toothis gruppo toomaintain hello elenco di oggetti che devono essere presenti in Azure AD. Tutti gli oggetti che si desidera toosynchronize devono essere un membro del gruppo di hello diretto. ad esempio utenti, gruppi, contatti e computer/dispositivi. L'appartenenza ai gruppi annidati non viene risolta. Quando si aggiunge un gruppo con l'aggiunta di un membro, un solo gruppo hello stesso e non i relativi membri.

![Filtro sincronizzazione](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Questa funzionalità è previsto toosupport solo una distribuzione pilota. Non usarla in una distribuzione di produzione completa.
>
>

In una distribuzione di produzione completo, sarà toobe rigido toomaintain un singolo gruppo con tutti gli oggetti toosynchronize. È invece necessario utilizzare uno dei metodi di hello in [Configura filtro](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Funzionalità facoltative
Questa schermata consente di funzionalità facoltative di hello tooselect per gli scenari specifici.

![Funzionalità facoltative](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Se si dispone attualmente di DirSync o Azure AD Sync è attivo, non attivare le funzionalità di writeback hello in Azure AD Connect.
>
>

| Funzionalità facoltative | Descrizione |
| --- | --- |
| Distribuzione ibrida di Exchange |Hello funzionalità distribuzione ibrida di Exchange permette hello coesistenza delle cassette postali di Exchange sia in locale e in Office 365. Azure AD Connect sincronizza un set specifico di [attributi](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) da Azure AD alla directory locale. |
| Cartelle pubbliche della posta di Exchange | funzionalità delle cartelle pubbliche di posta elettronica di Exchange Hello consente toosynchronize abilitati alla posta gli oggetti di cartelle pubbliche dal tooAzure di Active Directory locale AD. |
| Filtro attributi e app di Azure AD |Abilita il filtro attributi e app di Azure AD, hello set di attributi sincronizzati possono essere personalizzati. Questa opzione aggiunge due altre configurazione pagine toohello guidata. Per altre informazioni, vedere [Filtro attributi e app Azure AD](#azure-ad-app-and-attribute-filtering). |
| Sincronizzazione delle password |Se si seleziona la federazione come soluzione di accesso hello, è possibile abilitare questa opzione. La sincronizzazione delle password può quindi essere usata come opzione di backup. Per altre informazioni, vedere [Sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Se l'autenticazione pass-through è stata selezionata questa opzione è abilitata per impostazione predefinita tooensure supporto per i client legacy e come opzione di backup. Per altre informazioni, vedere [Sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Writeback delle password |Abilita il writeback delle password, modifiche delle password eseguite in Azure AD vengono riscritti directory locale tooyour. Per altre informazioni, vedere [Introduzione alla gestione delle password](../active-directory-passwords-getting-started.md). |
| Writeback dei gruppi |Se si utilizza hello **gruppi di Office 365** funzionalità, è possibile che questi gruppi rappresentati in Active Directory locale. Questa opzione è disponibile solo se si dispone di Exchange in Active Directory locale. Per altre informazioni, vedere [Writeback dei gruppi](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Writeback dispositivi |Consente gli oggetti dispositivo toowriteback in Azure AD tooyour Active Directory locale per gli scenari di accesso condizionale. Per altre informazioni, vedere [Abilitazione del writeback dei dispositivi in Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Sincronizzazione attributi estensione della directory |Abilita sincronizzazione attributo estensioni delle directory, gli attributi specificati vengono sincronizzati tooAzure Active Directory. Per altre informazioni, vedere [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Filtro attributi e app di Azure AD
Se si desidera toolimit quali tooAzure toosynchronize attributi Active Directory, quindi avviare selezionare i servizi in uso. Se si apportano modifiche alla configurazione in questa pagina, un nuovo servizio è toobe selezionato in modo esplicito eseguendo nuovamente l'installazione guidata di hello.

![Funzionalità facoltative: app](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Basato su servizi hello selezionati nel passaggio precedente hello, questa pagina vengono visualizzati tutti gli attributi che vengono sincronizzati. Questo elenco è una combinazione di tutti i tipi di oggetti da sincronizzare. Se sono presenti attributi specifici che è necessario toonot sincronizzare, è possibile deselezionare gli attributi.

![Funzionalità facoltative: attributi](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> La rimozione degli attributi può influire sulle funzionalità. Per procedure consigliate e indicazioni, vedere gli [attributi sincronizzati](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Sincronizzazione attributi estensione della directory
È possibile estendere schema hello in Azure AD con gli attributi personalizzati aggiunti dall'organizzazione o altri attributi in Active Directory. toouse questa funzionalità, seleziona **sincronizzazione attributo estensione Directory** su hello **funzionalità facoltative** pagina. È possibile selezionare più attributi toosync in questa pagina.

![Estensioni della directory](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Per altre informazioni, vedere [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Abilitazione di Single Sign-On (SSO)
Configurazione di single sign-on per l'utilizzo con l'autenticazione pass-through o di sincronizzazione Password è un processo semplice che è necessario solo toocomplete una volta per ogni foresta che viene sincronizzata tooAzure Active Directory. La configurazione comporta due passaggi, come indicato di seguito:

1.  Creare account computer necessario hello in Active Directory locale.
2.  Configurare l'area intranet hello dei computer client hello toosupport singolo accesso.

#### <a name="create-hello-computer-account-in-active-directory"></a>Creare account computer hello in Active Directory
Per ogni foresta che è stata aggiunta in Azure AD Connect, sarà necessario toosupply le credenziali di amministratore di dominio in modo che sia possibile creare account computer hello in ogni foresta. credenziali Hello sono solo account di hello toocreate utilizzato e non sono archiviate o utilizzate per qualsiasi altra operazione. Aggiungere semplicemente le credenziali di hello in hello **accesso Enable Single** pagina della procedura guidata Connetti di hello Azure AD come illustrato:

![Abilita Single Sign-On](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Se non si desidera toouse Single sign-on con tale foresta, è possibile ignorare un determinato insieme di strutture.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Configurare l'area Intranet hello per i computer client
tooensure che hello client accessi automaticamente in intranet hello zona è necessario che due URL fanno parte dell'area intranet hello tooensure. In questo modo i computer aggiunti a un dominio hello viene inviato automaticamente un tooAzure ticket Kerberos Active Directory quando è toohello connesso alla rete aziendale.
In un computer con gli strumenti di gestione di criteri di gruppo hello.

1.  Aprire Strumenti di gestione criteri di gruppo hello
2.  Modificare i criteri di gruppo hello che verrà applicato tooall utenti. Ad esempio, hello criterio dominio predefinito.
3.  Passare troppo**utente Configurazione computer\Modelli amministrativi\Componenti di Windows\Internet Explorer\Pannello controllo Internet\pagina** e selezionare **tooZone elenco di assegnazione sito** per ogni immagine hello di seguito.
4.  Abilitare i criteri di hello e immettere i seguenti due elementi nella finestra di dialogo hello hello.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Che dovrebbe essere simile toohello seguenti:  
![Aree Intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Fare clic su **OK** due volte.

## <a name="configuring-federation-with-ad-fs"></a>Configurazione della federazione con ADFS
Configurare ADFS con Azure AD Connect è semplice e richiede l'esecuzione di pochi passaggi. prima configurazione hello è necessario seguente Hello.

* Un server di Windows Server 2012 R2 per il server federativo hello con abilitata la gestione remota
* Un server di Windows Server 2012 R2 per il server Proxy applicazione Web hello con abilitata la gestione remota
* Un certificato SSL per la federazione hello Nome intendi toouse (ad esempio sts.contoso.com) del servizio

### <a name="ad-fs-configuration-pre-requisites"></a>Prerequisiti di configurazione di AD FS
tooconfigure ADFS con Azure AD Connect della farm, verificare che WinRM è abilitato nei server remoti hello. Inoltre, passare a requisito di hello porte elencata nella [tabella 3 - Azure AD Connect e WAP/server federativo](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Creare una nuova farm ADFS o usare una farm ADFS esistente
È possibile utilizzare una farm ADFS esistente oppure è possibile scegliere toocreate una nuova farm ADFS. Se si sceglie toocreate uno nuovo, si è certificato SSL di hello tooprovide obbligatorio. Se il certificato SSL hello è protetto da password, viene chiesto di password hello.

![Farm ADFS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Se si sceglie toouse una farm ADFS esistente, si passa direttamente toohello relazione di trust hello tra ADFS e Azure AD schermata di configurazione.

### <a name="specify-hello-ad-fs-servers"></a>Specificare i server ADFS hello
Immettere il server hello che si desidera includere tooinstall AD FS. È possibile aggiungere uno o più server in base alle esigenze di pianificazione della capacità. Aggiungere tutti i server tooActive Directory prima di eseguire questa configurazione. È consigliabile installare un singolo server AD FS per distribuzioni di test e pilota. Successivamente, aggiungere e distribuire più server toomeet le esigenze di scalabilità mediante l'esecuzione di Azure AD Connect nuovamente dopo la configurazione iniziale.

> [!NOTE]
> Verificare che tutti i server siano unite in join tooan AD dominio prima di eseguire questa configurazione.
>
>

![Server ADFS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Specificare i server Proxy applicazione Web hello
Immettere il server hello che si vuole usare come server proxy applicazione Web. server proxy applicazione web di Hello viene distribuito nella rete Perimetrale (con connessione extranet) e supporta le richieste di autenticazione da hello extranet. È possibile aggiungere uno o più server in base alle esigenze di pianificazione della capacità. È consigliabile installare un singolo server proxy applicazione Web per distribuzioni di test e pilota. Successivamente, aggiungere e distribuire più server toomeet le esigenze di scalabilità mediante l'esecuzione di Azure AD Connect nuovamente dopo la configurazione iniziale. È consigliabile avere un numero equivalente dell'autenticazione del proxy server toosatisfy dalla rete intranet hello.

> [!NOTE]
> <li> Se hello l'account utilizzato non è un amministratore locale nei server ADFS hello, viene richiesto per le credenziali di amministratore.</li>
> <li> Verificare che vi sia connettività HTTP/HTTPS tra il server di Azure AD Connect hello e hello Proxy applicazione Web prima di eseguire questo passaggio.</li>
> <li> Verificare che sia presente la connettività HTTP/HTTPS tra il Server applicazioni Web hello e hello AD FS server tooallow autenticazione richieste tooflow tramite.</li>
>

![App Web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Sono le credenziali richieste tooenter hello server applicazioni web possono stabilire un connessione sicura toohello AD FS server. Queste credenziali è necessario un amministratore locale nel server AD FS hello toobe.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Specificare l'account del servizio hello hello servizio AD FS
servizio di Hello AD FS, è necessario un dominio del servizio agli utenti di account tooauthenticate e cercare le informazioni utente in Active Directory. Supporta due tipi di account di servizio:

* **Account del servizio gestito del gruppo** : introdotto in Servizi di dominio Active Directory con Windows Server 2012. Questo tipo di account fornisce servizi, ad esempio AD FS, un singolo account senza password dell'account hello tooupdate regolarmente. Utilizzare questa opzione se si dispone già di controller di dominio di Windows Server 2012 nel dominio hello appartenenti al server ADFS.
* **Account utente di dominio** -questo tipo di account è necessario tooprovide una password e regolarmente hello aggiornamento della password alla modifica di password hello o alla scadenza. Utilizzare questa opzione solo quando non si dispone i controller di dominio di Windows Server 2012 nel dominio hello appartenenti al server ADFS.

Se è stato selezionato l'account del servizio gestito del gruppo e questa funzionalità non è mai stata usata in Active Directory, vengono richieste anche le credenziali di amministratore dell'organizzazione. Queste credenziali vengono utilizzati tooinitiate archivio delle chiavi hello e abilitare la funzionalità di hello in Active Directory.

> [!NOTE]
> Se il servizio di hello AD ADFS è già registrato come un SPN nel dominio hello, Azure AD Connect esegue toodetect un controllo.  Active Directory non sarà possibile toobe duplicati SPN registrato in una sola volta.  Se viene trovato un SPN duplicati, non sarà in grado di tooproceed ulteriormente fino a quando non viene rimosso hello SPN.

![Account del servizio ADFS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Selezionare il dominio di hello Azure AD che si desidera toofederate
Questa configurazione è una relazione di federazione hello toosetup utilizzato tra ADFS e Azure AD. Configura ADFS tooissue sicurezza token tooAzure AD e configura i token di Azure AD tootrust hello da questa specifica istanza di AD FS. Questa pagina consente solo un singolo dominio all'installazione iniziale di hello tooconfigure. È possibile configurare altri domini in un secondo momento, eseguendo di nuovo Azure AD Connect.

![Dominio di Azure AD](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Verificare il dominio hello Azure AD selezionato per la federazione
Quando si seleziona hello toobe di dominio federato, Azure AD Connect offre le informazioni necessarie tooverify un dominio non verificato. Vedere [Aggiungi e verifica dominio hello](../active-directory-add-domain.md) come toouse queste informazioni.

![Dominio di Azure AD](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Il dominio Active Directory Connect tentativi tooverify hello durante hello configurare fase. Se si continua tooconfigure senza aggiungere record DNS necessari hello, procedura guidata hello configurazione non è in grado di toocomplete hello.
>
>

## <a name="configure-and-verify-pages"></a>Configurare e verificare le pagine
configurazione di Hello avviene in questa pagina.

> [!NOTE]
> Se è stata configurata la federazione, prima di continuare l'installazione assicurarsi di avere configurato la [Risoluzione dei nomi per i server federativi](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Tooconfigure pronto](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Modalità di gestione temporanea
È possibile toosetup un nuovo server di sincronizzazione in parallelo con modalità di gestione temporanea. È solo toohave supportato un server di sincronizzazione esportazione tooone directory nel cloud hello. Ma se si desidera toomove da un altro server, ad esempio un in esecuzione DirSync, è possibile abilitare Azure AD Connect in modalità di gestione temporanea. Quando abilitata, sincronizzazione hello importazione del motore e sincronizzare i dati come di consueto, ma non viene esportato alcun elemento tooAzure Active Directory o Active Directory. Hello funzionalità sincronizzazione password e il writeback delle password sono disabilitate in modalità di gestione temporanea.

![Modalità di gestione temporanea](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

In modalità di gestione temporanea, è motore di sincronizzazione toohello toomake possibili modifiche necessarie e verificare su toobe esportato. Quando si verificano problemi configurazione hello, eseguire di nuovo l'installazione guidata di hello e disabilitare la modalità di gestione temporanea. I dati sono ora esportato tooAzure AD dal server. Verificare che toodisable hello hello stesso tempo, pertanto solo uno server di esportazione attivamente altri server.

Per altre informazioni, vedere [Modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Verificare la configurazione della federazione
Azure AD Connect consente di verificare le impostazioni DNS hello automaticamente quando si fa clic sul pulsante Verifica hello.

**Controlli della connettività Intranet**

* Risolvere il FQDN di federazione: Azure AD Connect controlla se la connettività tooensure DNS può essere risolti federazione hello FQDN. Se Azure AD Connect non è possibile risolvere il FQDN hello, verifica hello avrà esito negativo. Verificare che un record DNS sia presente per FQDN servizio federativo hello ordine toosuccessfully hello completo di verifica.
* Record DNS A: Azure AD Connect controlla se è presente un record A per il servizio federativo. In assenza di hello di un record A, verifica hello avrà esito negativo. Creare un record e non record CNAME per il FQDN di federazione in ordine toosuccessfully completare la verifica di hello.

**Controlli della connettività Extranet**

* Risolvere il FQDN di federazione: Azure AD Connect controlla se la connettività tooensure DNS può essere risolti federazione hello FQDN.

![Complete](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verificare](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Inoltre, eseguire hello seguendo i passaggi di verifica:

* Convalida che è possibile effettuare l'accesso da un browser da un computer aggiunti a un dominio intranet hello: connettere toohttps://myapps.microsoft.com e verificare hello Accedi con l'account connesso. account di amministratore di dominio Active Directory Hello annunci integrato non è sincronizzato e non può essere utilizzato per la verifica.
* Convalida che è possibile effettuare l'accesso da un dispositivo da hello extranet. In un computer di casa o un dispositivo mobile, connettersi toohttps://myapps.microsoft.com e fornire le credenziali.
* Convalidare l'accesso rich client. Connessione toohttps://testconnectivity.microsoft.com, scegliere hello **Office 365** hello scheda e scegliere **Office 365 Single Sign-On Test**.

## <a name="next-steps"></a>Passaggi successivi
Una volta completata l'installazione di hello, disconnettersi e accedere nuovamente tooWindows prima di usare Synchronization Service Manager o l'Editor delle regole di sincronizzazione.

Dopo avere installato di Azure AD Connect è possibile [verificare l'installazione di hello e assegnare licenze](active-directory-aadconnect-whats-next.md).

Altre informazioni su queste funzionalità, che sono state abilitate con installazione hello: [impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Altre informazioni su questi argomenti comuni: [dell'utilità di pianificazione e la modalità di sincronizzazione tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
