---
title: "aaaChoose una soluzione con identità ibrida di Azure | Documenti Microsoft"
description: "Informazioni di base di soluzioni di gestione identità ibride hello e consigli per si toomake hello identità governance decisione migliore per l'organizzazione."
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4ab8aff314f6308ab32f77e81cf0f07e1f5d7b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-hybrid-identity-solutions"></a>Soluzioni ibride di gestione delle identità
[Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) toosynchronize oggetti di directory locali con Azure AD durante la gestione di utenti locale consentono soluzioni di identità ibride. Quando si pianifica l'in Windows Server Active Directory locale con Azure AD è se si desidera toouse sincronizzato identità o identità federata toosynchronize, Hello prima toomake decisione. Identità sincronizzate e, facoltativamente, gli hash delle password, consentono agli utenti toouse hello stesso tooaccess password locale sia basato su cloud di risorse dell'organizzazione. Per i requisiti di scenario più avanzati, ad esempio single sign-on (SSO) o MFA locale, è necessario identità toofederate di toodeploy Active Directory Federation Services (ADFS). 

Sono disponibili diverse opzioni per la configurazione della gestione di identità ibrida. Questo articolo fornisce informazioni toohelp che prescelto hello più adatto per l'organizzazione in base alla facilità di distribuzione e la gestione di identità e accessi specifica esigenze. Quando si considera il modello di identità migliore adatta alle esigenze dell'organizzazione, è necessario anche toothink sul tempo, infrastruttura esistente, la complessità e costi. Questi fattori variano in base all'organizzazione e possono cambiare nel tempo. Tuttavia, se si modificano i requisiti, è anche il modello di identità diversi tooa di hello flessibilità tooswitch.

> [!TIP]
> Queste soluzioni vengono distribuite da [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="synchronized-identity"></a>Identità sincronizzata 
Identità sincronizzate è toosynchronize modo più semplice hello oggetti directory (utenti e gruppi) in locale con Azure AD. 

![Identità ibrida sincronizzata](./media/choose-hybrid-identity-solution/synchronized-identity.png)

Sebbene identità sincronizzato metodo più semplice e rapido hello, gli utenti devono comunque toomaintain una password diversa per le risorse basate su cloud. tooavoid, è anche possibile (facoltativamente) [sincronizzare un hash delle password utente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-implement-password-synchronization#what-is-password-synchronization) tooyour Azure Active directory. La sincronizzazione password hash consente agli utenti toolog in risorse aziendali basate su toocloud con hello stesso nome utente e password utilizzati in locale. Azure AD Connect controlla periodicamente la directory locale per rilevare eventuali modifiche e mantiene sincronizzata la directory di Azure AD. Quando cambia un attributo utente o una password in Active Directory locale, il valore viene aggiornato automaticamente in Azure AD. 

Per la maggior parte delle organizzazioni che necessitano solo di tooenable toosign i relativi utenti tooOffice 365 applicazioni SaaS e altre risorse di Azure basato su Active Directory, è consigliabile l'opzione di sincronizzazione password predefinito hello. Se il problema persiste per l'utente, è necessario toodecide tra autenticazione pass-through e AD FS.

> [!TIP]
> Le password utente vengono archiviate in locale Windows Server Active Directory sotto forma di hello di un valore hash che rappresenta la password utente effettiva hello. Un valore hash è un risultato di una funzione matematica unidirezionale (Buongiorno algoritmo hash). Non vi è alcun risultato hello toorevert del metodo di una versione di testo normale toohello funzione unidirezionale di una password. Non è possibile utilizzare un toosign hash password nella rete locale tooyour. Se si sceglie toosynchronize password, gli hash delle password di Azure AD Connect estrae da hello Active Directory locale e si applica l'elaborazione di hash della password toohello prima che venga sincronizzato tooAzure AD aggiuntiva di sicurezza. La sincronizzazione delle password nonché insieme password writeback tooenable self-service la reimpostazione della password in Azure AD. Inoltre, è possibile abilitare il single sign-on (SSO) per gli utenti dei computer appartenenti a un dominio che sono toohello connesso alla rete aziendale. Con single sign-on, gli utenti abilitati sufficiente tooenter risorse di cloud un nome utente toosecurely accesso. 

## <a name="pass-through-authentication"></a>Autenticazione pass-through
L'[autenticazione pass-through di Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication) offre una soluzione di convalida delle password semplice per i servizi basati su Azure AD usando Active Directory locale. Se i criteri di conformità e sicurezza per l'organizzazione non consentono l'invio delle password degli utenti, anche in un form con hash, ed è solo necessario toosupport desktop SSO per i dispositivi appartenenti a un dominio, è consigliabile valutare l'autenticazione pass-through. Qualsiasi distribuzione nella rete Perimetrale, che semplifica l'infrastruttura di distribuzione hello quando vengono confrontati con AD FS hello non richiede l'autenticazione pass-through. Quando gli utenti eseguono l'accesso usando Azure AD, questo metodo di autenticazione convalida le loro password direttamente con l'istanza locale di Active Directory.

![Autenticazione pass-through](./media/choose-hybrid-identity-solution/pass-through-authentication.png)

Con l'autenticazione pass-through, non è necessario per un'infrastruttura di rete complessi, e non è necessario toostore password locali nel cloud hello. Combinata con single sign-on, autenticazione pass-through offre un'esperienza integrata durante l'accesso AD tooAzure o altri servizi cloud.

L'autenticazione pass-through può essere configurata tramite Azure AD Connect e usa un semplice agente locale che rimane in ascolto delle richieste di convalida delle password. agente Hello possa essere facilmente distribuiti toomultiple macchine tooprovide la disponibilità elevata e bilanciamento del carico. Poiché tutte le comunicazioni in uscita solo, non vi è alcun requisito per hello connettore toobe installato in una rete Perimetrale. come indicato di seguito sono riportati i requisiti del computer server Hello per connettore hello:

- Windows Server 2012 R2 o versione successiva
- È stato aggiunto tooa dominio nella foresta hello tramite cui vengono convalidati gli utenti

> [!NOTE]
> L'autenticazione pass-through di Azure AD è attualmente in anteprima ed supportata per i client basati su Web browser e i client di Office che supportano l'autenticazione moderna. Per i client che non sono supportati, ad esempio legacy client Office e di Exchange ActiveSync (inclusi i client di posta elettronica native sui dispositivi mobili), è consigliato toouse hello autenticazione moderna equivalente. L'autenticazione moderna non solo consente l'autenticazione pass-through, ma consente inoltre di accesso condizionale criteri toobe applicato, ad esempio l'autenticazione a più fattori. 

Autenticazione pass-through non è attualmente supportata quando i dispositivi Windows 10 aggiunti tooAzure AD. Tuttavia, è possibile utilizzare la sincronizzazione dell'hash password come un toosupport fallback automatico Windows 10 e i client legacy hello indicato in precedenza. Durante l'anteprima di hello, la sincronizzazione hash delle password è abilitata per impostazione predefinita, quando è selezionata l'autenticazione pass-through come hello opzione di accesso in Azure AD Connect.


## <a name="federated-identity-ad-fs"></a>Identità federata (AD FS)
Per un maggiore controllo sul modo in cui gli utenti accedono a Office 365 e ad altri servizi cloud, è possibile impostare la sincronizzazione delle directory con l'accesso Single Sign-On (SSO) usando [Active Directory Federation Services (ADFS)](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server-2016). La federazione accessi dell'utente con AD FS delegati autenticazione tooan server locale che convalida le credenziali utente. In questo modello, le credenziali di Active Directory locale non vengono passate mai tooAzure Active Directory.

![Identità federata](./media/choose-hybrid-identity-solution/federated-identity.png)

Detto anche federazione delle identità, questo metodo di accesso garantisce che tutte le autenticazioni utente controllati in locale e consentono agli amministratori tooimplement i livelli di controllo di accesso più rigorosi. Federazione delle identità con AD FS opzione hello più complicata e richiede la distribuzione di server aggiuntivi nell'ambiente locale. Federazione delle identità inoltre esegue il commit è tooproviding 24x7 supporto per l'infrastruttura di Active Directory e AD FS. Questo livello di supporto elevato è necessario perché se il servizio locale di Internet di accedere, controller di dominio o server AD FS non sono disponibili, gli utenti possono accedere toocloud servizi.

> [!TIP]
> Se si decide di toouse federazione con Active Directory Federation Services (ADFS), è possibile, facoltativamente, impostare la sincronizzazione delle password come backup in caso di errore di infrastruttura di ADFS.


## <a name="common-scenarios-and-recommendations"></a>Scenari comuni e raccomandazioni
Ecco alcune identità ibrida comune e scenari di gestione accesso con le raccomandazioni come opzione di identità ibrida toowhich (o opzioni) potrebbero essere appropriati per ognuno.

|Esigenza:|PWS e SSO<sup>1</sup>| PTA e SSO<sup>2</sup> | AD FS<sup>3</sup>|
|-----|-----|-----|-----|
|Sincronizzare di nuovo utente, contatti e gli account di gruppo creati automaticamente in my cloud toohello di Active Directory locale.|![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)| ![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png) |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Configurare il tenant per scenari ibridi di Office 365|![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)| ![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png) |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Abilitare il toosign gli utenti in e ai servizi cloud utilizzando la password locale|![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)| ![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png) |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Implementare l'accesso SSO usando le credenziali aziendali|![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)| ![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png) |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Verificare che gli hash delle password non vengono archiviati nel cloud hello| |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Abilitare soluzioni di autenticazione a più fattori locali| | |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Supportare l'autenticazione di smart card per gli utenti<sup>4</sup>| | |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|
|Visualizzare le notifiche di scadenza delle password nel portale di Office hello e sul desktop di Windows 10 hello| | |![Consigliato](./media/choose-hybrid-identity-solution/ic195031.png)|

> <sup>1</sup> Sincronizzazione delle password con l'accesso Single Sign-On (SSO) 

> <sup>2</sup> Autenticazione pass-through e accesso Single Sign-On. 

> <sup>3</sup> Accesso Single Sign-On federato con AD FS.

> <sup>4</sup> ADFS può essere integrato con il tooallow di infrastruttura a chiave pubblica dell'organizzazione accesso in ingresso utilizzando i certificati. Questi certificati possono essere certificati software distribuiti tramite canali di provisioning attendibili, ad esempio i certificati di gestione di dispositivi mobili (MDM) o l'oggetto Criteri di gruppo o smart card (comprese le schede PIV/CAC) o Hello for Business (cert-trust). Per altre informazioni sul supporto dell'autenticazione con smart card, vedere [questo blog](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/).


## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni in un ambiente Azure di prova](https://aka.ms/aad-poc)

[Installare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)

[Monitorare la sincronizzazione delle identità ibride](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)

