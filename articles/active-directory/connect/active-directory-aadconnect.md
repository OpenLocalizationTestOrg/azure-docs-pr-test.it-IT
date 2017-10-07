---
title: Connettere Active Directory ad Azure Active Directory. | Documentazione Microsoft
description: "Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD."
keywords: "Introduzione tooAzure AD Connect, panoramica di Azure AD Connect, che cos'è Azure AD Connect, active directory di installazione"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Integrare le directory locali con Azure Active Directory
Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per gli utenti per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD. In questo argomento guiderà hello pianificazione, distribuzione e i passaggi di operazione. È una raccolta di collegamenti toohello argomenti correlati toothis area.

> [!IMPORTANT]
> [Azure AD Connect è hello tooconnect modo migliore le directory locali con Azure AD e Office 365. Si tratta di un tooAzure tooupgrade molto tempo AD Connect dalla sincronizzazione Windows Azure Active Directory (DirSync) o Azure AD Sync come questi strumenti sono ora deprecata e verrà raggiunta fine del supporto di 13 aprile 2017.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Cos'è Azure AD Connect](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Perché usare Azure AD Connect
L'integrazione delle directory locali con Azure AD rende gli utenti più produttivi in quanto fornisce un'identità comune per accedere alle risorse cloud e locali. Utenti e organizzazioni possono sfruttare i vantaggi seguenti hello:

* Gli utenti possono usare un singola identità tooaccess le applicazioni locali e cloud services, ad esempio Office 365.
* Singolo strumento tooprovide un'esperienza di semplicità di distribuzione per la sincronizzazione e Accedi.
* Fornisce funzionalità più recenti di hello per gli scenari. Azure AD Connect sostituisce le versioni precedenti degli strumenti di integrazione delle identità, ad esempio DirSync e Azure AD Sync. Per altre informazioni, vedere [Confronto degli strumenti di integrazione directory per la soluzione ibrida di gestione delle identità](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Funzionamento di Azure AD Connect
Azure Active Directory Connect è costituito da tre componenti principali: servizi di sincronizzazione hello, hello facoltativo componente di Active Directory Federation Services e componente di monitoraggio hello denominato [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Stack di Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Sincronizzazione: questo componente è responsabile della creazione di utenti, gruppi e altri oggetti. È inoltre responsabile di garantire che le informazioni di identità per gli utenti locali e i gruppi corrispondenti cloud hello.
* AD FS - Federation è una parte facoltativa di Azure AD Connect e può essere utilizzato tooconfigure un ambiente ibrido usando una locale infrastruttura ADFS. Può essere utilizzato da organizzazioni tooaddress eseguire distribuzioni complesse, ad esempio aggiunta a un dominio SSO, l'applicazione di criteri di Active Directory, accesso e smart card o 3rd party autenticazione a più fattori.
* Monitoraggio integrità - Azure AD Connect Health può fornire monitoraggio affidabile e fornire una posizione centrale in hello tooview portale Azure questa attività. Per altre informazioni, vedere [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Installare Azure AD Connect
È possibile trovare download hello per Azure AD Connect in [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Soluzione | Scenario |
| --- | --- |
| Prima di iniziare: [Hardware e prerequisiti](active-directory-aadconnect-prerequisites.md) |<li>Passaggi toocomplete prima di iniziare tooinstall Azure AD Connect.</li> |
| [Impostazioni rapide](active-directory-aadconnect-get-started-express.md) |<li>Se si dispone di una singola foresta AD quindi questo hello. è consigliabile toouse opzione.</li> <li>Utente l'accesso con hello stesso password mediante la sincronizzazione delle password.</li> |
| [Impostazioni personalizzate](active-directory-aadconnect-get-started-custom.md) |<li>Da usare quando sono presenti più foreste. Supporta numerose [topologie](active-directory-aadconnect-topologies.md) locali.</li> <li>Personalizzare l'opzione di accesso, ad esempio con AD FS per la federazione o un provider di identità di terze parti.</li> <li>Personalizzare le funzionalità di sincronizzazione, ad esempio filtro e writeback.</li> |
| [Aggiornamento da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Da usare se è presente un server DirSync esistente già in esecuzione.</li> |
| [Aggiornamento da Azure AD Sync o Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Sono disponibili diversi metodi.</li> |

[Dopo l'installazione](active-directory-aadconnect-whats-next.md) è necessario verificare funzioni come previsto e assegnare licenze agli utenti di toohello.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Passaggi successivi tooInstall Azure AD Connect
|Argomento |Collegamento|  
| --- | --- |
|Scaricare Azure AD Connect | [Scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Eseguire l'installazione con le Impostazioni rapide | [Installazione rapida di Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Eseguire l'installazione mediante le impostazioni personalizzate | [Installazione personalizzata di Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Aggiornamento da DirSync | [Aggiornamento dallo strumento di sincronizzazione di Azure AD (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Dopo l'installazione | [Verificare l'installazione di hello e assegnare le licenze](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Altre informazioni su come installare Azure AD Connect
È anche opportuno tooprepare per [operativo](active-directory-aadconnectsync-operations.md) problemi. Potrebbe essere necessario un server di standby toohave pertanto è facilmente possibile rientrano se è presente un [emergenza](active-directory-aadconnectsync-operations.md#disaster-recovery). Se si prevede di modifiche alla configurazione frequenti toomake, è necessario pianificare un [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode) server.

|Argomento |Collegamento|  
| --- | --- |
|Topologie supportate | [Topologie per Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Concetti relativi alla progettazione | [Concetti relativi alla progettazione per Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Account usati per l'installazione | [Altre informazioni sulle credenziali e le autorizzazioni di Azure AD Connect](./active-directory-aadconnect-accounts-permissions.md)|
|Pianificazione per la gestione delle attività operative | [Servizio di sincronizzazione Azure AD Connect: Attività operative e considerazioni](active-directory-aadconnectsync-operations.md)|
|Opzioni di accesso utente | [Opzioni di accesso utente di Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Configurare le funzionalità di sincronizzazione
Azure AD Connect include numerose funzionalità che è possibile abilitare o che sono abilitate per impostazione predefinita. Alcune funzionalità possono talvolta richiedere più attività di configurazione in topologie e scenari specifici.

[Filtro](active-directory-aadconnectsync-configure-filtering.md) viene utilizzato quando si desidera toolimit quali oggetti sono sincronizzati tooAzure Active Directory. Per impostazione predefinita, vengono sincronizzati tutti gli utenti, i contatti, i gruppi e i computer Windows 10. È possibile modificare il filtro di hello basato su attributi, le unità organizzative o domini.

[La sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) Sincronizza l'hash della password hello in Active Directory tooAzure Active Directory. utente finale di Hello può utilizzare hello stessa password locale e nel cloud hello ma solo la gestione in un'unica posizione. Poiché utilizza il servizio Active Directory locale come autorità hello, è possibile utilizzare anche i propri criteri password.

[Writeback delle password](../active-directory-passwords-getting-started.md) verrà consentono il toochange gli utenti e reimpostare la password nel cloud hello e sono applicati i criteri di password locale.

[Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md) consentirà un dispositivo registrato in Azure AD toobe riscritti tooon locale di Active Directory in modo può essere utilizzato per l'accesso condizionale.

Hello [impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) funzionalità è attivata per impostazione predefinita e consente di proteggere la directory cloud da numerose eliminazioni in hello contemporaneamente. Per impostazione predefinita, consente 500 eliminazioni per ogni esecuzione. È possibile modificare questa impostazione in base alle dimensioni dell'organizzazione.

[L'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è abilitata per impostazione predefinita per le installazioni di impostazioni rapide e assicura la connessione AD Azure è sempre attivo toodate con la versione più recente di hello.

### <a name="next-steps-tooconfigure-sync-features"></a>Funzionalità di sincronizzazione tooconfigure passaggi successive
|Argomento |Collegamento|  
| --- | --- |
|Configurare il filtro | [Servizio di sincronizzazione Azure AD Connect: Configurare il filtro](active-directory-aadconnectsync-configure-filtering.md)|
|sincronizzazione delle password | [Servizio di sincronizzazione Azure AD Connect: Implementare la sincronizzazione della password](active-directory-aadconnectsync-implement-password-synchronization.md)|
|writeback delle password | [Introduzione alla gestione delle password](../active-directory-passwords-getting-started.md)|
|writeback dei dispositivi | [Abilitazione del writeback dei dispositivi in Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|prevenzione delle eliminazioni accidentali | [Servizio di sincronizzazione Azure AD Connect: Impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|aggiornamento automatico | [Azure AD Connect: aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Personalizzare il servizio di sincronizzazione Azure AD Connect
Sincronizzazione di Azure AD Connect viene fornito con una configurazione predefinita che è toowork previsto per la maggior parte dei clienti e topologie. Ma esistono sempre situazioni in cui configurazione predefinita di hello non funziona e deve essere regolata. È supportato toomake modifiche come documentati in questa sezione e argomenti collegati.

Se non si è mai lavorato con una topologia di sincronizzazione prima che si desidera nozioni di base di toostart toounderstand hello e termini utilizzati come descritto in hello hello [concetti tecnici](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect è evoluzione hello MIIS2003 ILM2007 e FIM2010. Anche se alcuni elementi sono identici, sono state introdotte numerose modifiche.

Hello [configurazione predefinita](active-directory-aadconnectsync-understanding-default-configuration.md) si presuppone che nella configurazione hello potrebbe essere più di una foresta. In queste topologie un oggetto utente può essere rappresentato come un contatto in un'altra foresta. utente Hello potrebbe anche essere una cassetta postale collegata in un'altra foresta di risorse. viene descritto il comportamento di Hello della configurazione predefinita di hello in [utenti e contatti](active-directory-aadconnectsync-understanding-users-and-contacts.md).

modello di configurazione Hello sincronizzato viene chiamato [provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Hello flussi di attributi avanzate utilizza [funzioni](active-directory-aadconnectsync-functions-reference.md) tooexpress attributo trasformazioni. È possibile visualizzare ed esaminare hello intera configurazione utilizzando strumenti viene fornito con Azure AD Connect. Se è necessario toomake modifiche di configurazione, assicurarsi di seguire hello [consigliate](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) pertanto è più facile tooadopt nuove versioni.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Passaggi successivi di sincronizzazione di toocustomize Azure AD Connect
|Argomento |Collegamento|  
| --- | --- |
|Tutti gli articoli sul servizio di sincronizzazione Azure AD Connect | [Servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|concetti tecnici | [Servizio di sincronizzazione Azure AD Connect: Concetti tecnici](active-directory-aadconnectsync-technical-concepts.md)|
|Informazioni su configurazione predefinita di hello | [Sincronizzazione di Azure AD Connect: informazioni su configurazione predefinita di hello](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Informazioni su utenti e contatti | [Servizio di sincronizzazione Azure AD Connect: Informazioni su utenti e contatti](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|provisioning dichiarativo | [Servizio di sincronizzazione Azure AD Connect: Informazioni sulle espressioni di provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Modificare la configurazione predefinita di hello | [Procedure consigliate per la modifica di configurazione predefinita di hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Configurare le funzionalità di federazione
ADFS può essere configurato toosupport [più domini](active-directory-aadconnect-multiple-domains.md). Ad esempio possibile avere più domini superiore, è necessario toouse per la federazione.

Se il server ADFS non è stato configurato tooautomatically Aggiorna certificati da Azure AD o se si utilizza una soluzione non ADFS, quindi verrà visualizzato un messaggio è troppo[l'aggiornamento dei certificati](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Funzionalità di federazione tooconfigure passaggi successive
|Argomento |Collegamento|  
| --- | --- |
|Tutti gli articoli su AD FS | [Azure AD Connect e federazione](active-directory-aadconnectfed-whatis.md)|
|Configurare AD FS con sottodomini | [Supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Gestire la farm AD FS | [Gestione e personalizzazione di AD FS con Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Aggiornare manualmente i certificati di federazione | [Rinnovo dei certificati di federazione per Office 365 e Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Altri riferimenti e informazioni
|Argomento |Collegamento|  
| --- | --- |
|Cronologia delle versioni | [Cronologia delle versioni](active-directory-aadconnect-version-history.md)|
|Confronto tra DirSync, Azure ADSync e Azure AD Connect | [Confronto degli strumenti di integrazione directory](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Elenco di compatibilità non AD FS per Azure AD | [Elenco di compatibilità di federazione di Azure AD](active-directory-aadconnect-federation-compatibility.md)|
|Configurazione di un IdP SAML 2.0|[Uso di un provider di identità (IdP) SAML 2.0 per l'accesso Single Sign-On](active-directory-aadconnect-federation-saml-idp.md)|
|Attributi sincronizzati | [Attributi sincronizzati](active-directory-aadconnectsync-attributes-synchronized.md)|
|Monitoraggio con Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Domande frequenti | [Domande frequenti su Azure AD Connect](active-directory-aadconnect-faq.md)|

**Risorse aggiuntive**

Si accendono 2015 presentazione sull'estensione cloud toohello directory locale.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

