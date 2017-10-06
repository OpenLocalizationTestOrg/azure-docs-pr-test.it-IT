---
title: "aaaAzure identità e dell'accesso di sicurezza consigliate | Documenti Microsoft"
description: "Questo articolo illustra una serie di procedure consigliate per il controllo di accesso e la gestione delle identità usando le funzionalità integrate di Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Procedure consigliate per la sicurezza con il controllo di accesso e la gestione delle identità di Azure
Molti considerare toobe hello nuovo limite livello identità per la sicurezza, assumendo il ruolo prospettiva hello tradizionali basate su rete. Questa evoluzione di pivot primario di hello per attenzione di sicurezza e gli investimenti provengono da tabelle dei fatti hello che perimetro di una rete è diventate sempre più poroso e tale difesa perimetrale non può essere altrettanto efficace come avveniva una volta toohello precedente esplosione di [BYOD](http://aka.ms/byodcg) dispositivi e applicazioni cloud.

Questo articolo illustra una serie di procedure consigliate per la sicurezza con il controllo di accesso e la gestione delle identità di Azure. Queste procedure consigliate derivano dall'esperienza acquisita con [Azure AD](../active-directory/active-directory-whatis.md) ed esperienze hello dei clienti come manualmente.

Per ogni procedura consigliata verrà illustrato:

* Quali consigliabile hello
* Motivo per cui si desidera tooenable consigliata
* Se non è consigliata di hello tooenable, quale potrebbe essere il risultato di hello
* Procedura consigliata toohello alternative possibili
* Informazioni come procedura consigliata hello tooenable

Questa gestione delle identità di Azure e controllo dell'accesso articolo di procedure consigliate si basa su un parere di consenso e funzionalità della piattaforma Azure e set di funzionalità di sicurezza in cui si trovano in fase di hello in questo articolo è stato scritto. Opinioni e le tecnologie cambiano nel tempo e questo articolo verrà aggiornato in un tooreflect regolarmente le modifiche.

Procedure consigliate per la sicurezza con il controllo di accesso e la gestione delle identità di Azure illustrate in questo articolo:

* Centralizzare la gestione delle identità
* Abilitare il Single Sign-On (SSO)
* Distribuire la gestione delle password
* Applicare l'autenticazione a più fattori (MFA) per gli utenti
* Usare il controllo degli accessi in base al ruolo
* Controllare i percorsi di creazione delle risorse con Resource Manager
* Guida per gli sviluppatori tooleverage identità funzionalità per App SaaS
* Monitorare attivamente le attività sospette

## <a name="centralize-your-identity-management"></a>Centralizzare la gestione delle identità
Un passaggio importante per proteggere la tua identità è tooensure che è possibile gestire gli account da una singola posizione relative in cui è stato creato questo account. Mentre la maggior parte hello delle aziende hello alle organizzazioni IT avrà account principale directory locale, le distribuzioni di cloud ibrido in luogo di hello è importante comprendere come toointegrate locale e le directory del cloud e fornire un esperienza toohello all'utente finale.

tooaccomplish questo [identità ibride](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) scenario si consiglia di due opzioni:

* Sincronizzare la directory locale con la directory cloud usando Azure AD Connect.
* Attuare la federazione dell'identità locale con la directory cloud usando [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS).

Le organizzazioni che non si verificheranno la propria identità locali con la propria identità cloud toointegrate amministrativi un sovraccarico maggiore nella gestione degli account, che aumenta la probabilità di hello di errori e violazioni della protezione.

Per ulteriori informazioni sulla sincronizzazione di Azure AD, leggere l'articolo hello [integrazione delle identità locali con Azure Active Directory](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Abilitare il Single Sign-On (SSO)
Quando si dispone di più directory toomanage, questo diventa un problema di amministrazione non solo per l'IT, ma anche per gli utenti finali che avrà tooremember più password. Utilizzando [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) si consentirà agli utenti hello di utilizzare hello stesso insieme di credenziali toosign-in e accedere alle risorse di hello necessari, indipendentemente dal fatto che in questa risorsa è situata in locale o nel cloud hello.

Utilizzare SSO tooenable utenti tooaccess loro [applicazioni SaaS](../active-directory/active-directory-appssoaccess-whatis.md) in base al proprio account aziendale in Azure AD. Questo vale non solo per le app SaaS Microsoft, ma anche per altre app come [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) e [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). L'applicazione può essere configurato toouse AD Azure come un [basato su SAML identity](../active-directory/fundamentals-identity.md) provider. Come un controllo di sicurezza, non Azure AD emetta un token consentendo toosign in un'applicazione hello a meno che non hanno ottenuto l'accesso tramite Azure AD. L'accesso può essere concesso direttamente agli utenti o attraverso un gruppo di cui sono membri.

> [!NOTE]
> Hello decisione toouse SSO avrà un impatto sulle modalità di integrazione directory locale con la directory cloud. Se si desidera SSO, sarà necessario toouse federazione, perché la sincronizzazione delle directory fornirà solo [stessa esperienza di accesso](../active-directory/active-directory-aadconnect.md).
>
>

Le organizzazioni che non consentono l'applicazione SSO per i relativi utenti e applicazioni sono più tooscenarios esposto in cui gli utenti avranno più password direttamente aumenta la probabilità di hello utenti del riutilizzo delle password o l'utilizzo di password vulnerabili.

Maggiori informazioni su SSO AD Azure, leggere l'articolo hello [personalizzazione con Azure AD Connect e gestione di ADFS](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Distribuire la gestione delle password
In scenari in cui si dispone di più tenant o si desidera che gli utenti tooenable troppo[reimpostare le proprie password](../active-directory/active-directory-passwords-update-your-own-password.md), è importante utilizzare abuso tooprevent criteri di sicurezza appropriate. In Azure è possibile sfruttare funzionalità di reimpostazione della password self-service hello e personalizzare toomeet opzioni di sicurezza hello i requisiti aziendali.

È particolarmente importante tooobtain feedback da questi utenti e imparare da loro esperienze affrontate tooperform questi passaggi. In base a queste esperienze, elaborare un piano toomitigate potenziali problemi che possono verificarsi durante la distribuzione di hello per un gruppo di dimensioni maggiore. È inoltre consigliabile utilizzare hello [report attività di registrazione reimpostazione Password](../active-directory/active-directory-passwords-get-insights.md) utenti hello toomonitor che siano registrando.

Le organizzazioni che vogliono password tooavoid modificare chiamate al supporto tecnico, ma abilitare gli utenti tooreset le proprie password è più sensibili tooa superiore chiamata volume toohello assistenza a causa di problemi di toopassword. In organizzazioni che dispongono di più tenant, è importante implementare questo tipo di funzionalità e consentire agli utenti tooperform la reimpostazione della password all'interno dei limiti di sicurezza che sono stati stabiliti nel criterio di protezione hello.

Sono disponibili ulteriori informazioni sulla password reimpostata, leggere l'articolo hello [la distribuzione di gestione delle Password e formazione utenti toouse è](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Applicare l'autenticazione a più fattori (MFA) per gli utenti
Per le organizzazioni che devono rispettare gli standard del settore, ad esempio toobe [PCI DSS versione 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), multi-factor authentication è necessario disporre di funzionalità per autenticare gli utenti. Oltre a essere conformi agli standard di settore, imporre agli utenti MFA tooauthenticate consente inoltre le organizzazioni toomitigate furto il tipo di credenziali di attacco, ad esempio [Pass-the-Hash (PtH)](http://aka.ms/PtHPaper).

Abilitando l'autenticazione a più fattori di Azure per gli utenti, si aggiunge un secondo livello di sicurezza toouser accessi e le transazioni. In questo caso, una transazione potrebbe accedere a un documento che si trova in un file server o in SharePoint Online. Azure MFA consente inoltre di probabilità di hello tooreduce IT che una credenziale compromessa avranno i dati del tooorganization di accesso.

Ad esempio: si attiva Azure MFA per gli utenti e lo configura toouse una telefonata o un SMS come verifica. Se le credenziali dell'utente hello compromessi autore dell'attacco hello non essere in grado di tooaccess qualsiasi risorsa poiché non sarà possibile phone dell'accesso toouser. Le organizzazioni che non si aggiungono livelli aggiuntivi di protezione di identità sono più vulnerabile agli attacchi di furto delle credenziali, con conseguente rischio di compromissione toodata.

Un'alternativa per le organizzazioni che vogliono controllo intero processo di autenticazione di hello tookeep locale non è toouse [Server Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), detta anche autenticazione a più fattori locale. Tramite questo metodo, sarà comunque in grado di tooenforce autenticazione a più fattori, mantenendo hello MFA server locale.

Per ulteriori informazioni sull'autenticazione a più fattori di Azure, leggere l'articolo hello [Introduzione ad Azure multi-Factor Authentication nel cloud hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Usare il controllo degli accessi in base al ruolo
Limitazione dell'accesso basato su hello [necessario tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principi di sicurezza è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati. Azure Role-Based Access controllo (RBAC) può essere utilizzato tooassign autorizzazioni toousers, gruppi e applicazioni in un determinato ambito. ambito Hello un'assegnazione di ruolo può essere una sottoscrizione, un gruppo di risorse o una singola risorsa.

È possibile sfruttare [incorporata RBAC](../active-directory/role-based-access-built-in-roles.md) ruoli in Azure tooassign privilegi toousers. È consigliabile utilizzare *collaboratore di Account di archiviazione* per gli operatori di cloud che necessitano di account di archiviazione toomanage e *collaboratore di Account di archiviazione classico* gli account di archiviazione classico toomanage di ruolo. Per gli operatori di cloud che necessita di macchine virtuali toomanage e account di archiviazione, è consigliabile aggiungerli troppo*collaboratore alla macchina virtuale* ruolo.

Le organizzazioni che non si applicano il controllo di accesso ai dati tramite le funzionalità, ad esempio RBAC possono essere concesse più privilegi rispetto agli utenti di tootheir necessarie. Questo può causare la compromissione toodata consente agli utenti l'accesso per tipi toocertain di tipi di dati (ad esempio, alto impatto aziendale) che sono non deve in primo luogo hello.

Maggiori informazioni su Azure RBAC leggendo l'articolo hello [gestire il controllo di accesso](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Controllare i percorsi di creazione delle risorse con Resource Manager
Abilitazione di cloud operatori tooperform attività mentre impedisce di rilievo convenzioni che sono necessari toomanage risorse dell'organizzazione è molto importante. Le organizzazioni che vogliono percorsi hello toocontrol in cui le risorse vengono create devono codificare questi percorsi.

tooachieve, le organizzazioni possono creare criteri di sicurezza che dispongono di definizioni che descrivono le azioni di hello o risorse che vengono negate in modo specifico. Assegnare le definizioni dei criteri nell'ambito di hello desiderato, ad esempio hello sottoscrizione, gruppo di risorse o una singola risorsa.

> [!NOTE]
> Questo non è hello stesso come RBAC, sfrutta effettivamente agli utenti di hello tooauthenticate RBAC che dispongono di privilegi toocreate tali risorse.
>
>

Usare [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) criteri personalizzati toocreate anche per scenari in cui le operazioni di hello organizzazione desidera tooallow solo quando hello centro di costo appropriato è associato; in caso contrario, si consentirà il richiesta hello.

Le organizzazioni che non controlla le modalità di creazione delle risorse sono toousers più sensibili che potrebbe abusare servizio hello creando più risorse di quante hanno bisogno. Protezione avanzata dei processo di creazione risorsa hello è un toosecure importante passaggio uno scenario di multi-tenant.

Sono disponibili ulteriori informazioni sulla creazione di criteri con Gestione risorse di Azure leggendo l'articolo hello [risorse toomanage criteri di utilizzo e controllare l'accesso](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Guida per gli sviluppatori tooleverage identità funzionalità per App SaaS
L'identità dell'utente viene usata in molti scenari quando gli utenti accedono ad [app SaaS](https://azure.microsoft.com/marketplace/active-directory/all/) che possono essere integrate in directory locali o cloud. In primo luogo, è consigliabile che gli sviluppatori utilizzino una toodevelop metodologia sicura queste App, ad esempio [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx). Azure AD semplifica l'autenticazione per gli sviluppatori fornendo le identità come servizio, con il supporto per protocolli standard del settore come [OAuth 2.0](http://oauth.net/2/) e [OpenID Connect](http://openid.net/connect/), nonché librerie open source per diverse piattaforme.

Rendere tooregister che tutte le applicazioni che usano l'outsourcing per l'autenticazione tooAzure Active Directory, si tratta di una routine obbligatoria. Hello motivazioni è poiché Azure AD necessita di una comunicazione di hello toocoordinate con un'applicazione hello quando Gestione sign-on (SSO) o lo scambio di token. la sessione dell'utente Hello scade quando scade la durata hello di hello token rilasciati da Azure AD. Valutare sempre se tale periodo di validità è necessario per l'applicazione o se è possibile ridurlo. Riduzione della durata di hello può fungere da una misura di sicurezza che forzerà toosign utenti out in base a un periodo di inattività.

Le organizzazioni che non applicano App tooaccess controllo di identità non sugli Guida e gli sviluppatori come toosecurely integrare applicazioni con il sistema di gestione di identità possono essere più vulnerabile tipo furto di toocredential di attacco, ad esempio [debole gestione di autenticazione e sessione descritta in Open Web applicazione sicurezza progetto (OWASP) primi 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

Per altre informazioni sugli scenari di autenticazione per app SaaS, vedere [Scenari di autenticazione per Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Monitorare attivamente le attività sospette
In base troppo[report Verizon 2016 dati violazione](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), violazione delle credenziali è ancora in luogo di hello e diventi delle aziende più remunerative hello criminali informatici. Per questo motivo, è importante toohave un sistema di monitoraggio active identità in grado di rilevare attività sospette comportamento e attivare un avviso per ulteriori indagini rapidamente. Azure AD offre due importanti funzionalità che consentono alle organizzazioni di monitorare le identità: i [report anomalie](../active-directory/active-directory-view-access-usage-reports.md) di Azure AD Premium e Azure AD [Identity Protection](../active-directory/active-directory-identityprotection.md).

Verificare che toouse hello anomalie report tooidentify tentativi toosign in [senza tracciamento](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [attacchi di forza bruta](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) gli attacchi contro un account specifico, toosign tentativi in da più posizioni, accedi da [dispositivi infetti](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) e gli indirizzi IP sospetti. Tenere presente che si tratta di report. In altre parole, è necessario disporre dei processi e procedure di inserire tali report per toorun gli amministratori IT su base giornaliera hello o su richiesta (in genere in uno scenario di risposta agli eventi imprevisti).

Al contrario, la protezione dell'identità di Azure AD è un sistema di monitoraggio attivo e contrassegnerà hello possibili rischi nel proprio dashboard. e invia notifiche di riepilogo giornaliere tramite posta elettronica. È consigliabile modificare il livello di rischio hello in base a tooyour requisiti aziendali. livello di rischio Hello per un evento di rischio è un'indicazione della gravità hello dell'evento di rischio hello (alta, Media o bassa). livello di rischio Hello consente agli utenti di protezione dell'identità priorità azioni hello deve accettano organizzazione di tootheir tooreduce hello rischio.

Le organizzazioni che non monitorano attivamente i sistemi di identità sono esposti al rischio di compromissione delle credenziali utente. Insaputa dell'utente che siano eseguendo le attività sospette posizionare utilizzando queste credenziali, le organizzazioni non saranno in grado di toomitigate questo tipo di minaccia.
Per altre informazioni in merito, vedere [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md).
