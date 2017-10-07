---
title: aaaConfigure SSO AD Azure per le applicazioni | Documenti Microsoft
description: Informazioni su come tooself servizio connettersi tooAzure App Active Directory utilizzando SAML e SSO basato su password
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione
In questo articolo riguarda una funzionalità che consente agli amministratori tooconfigure single sign-on tooapplications non presente nella raccolta di app di Azure Active Directory hello *senza scrivere codice*. Questa funzionalità è stata rilasciata dall'anteprima tecnica il 18 novembre 2015 ed è inclusa in [Azure Active Directory Premium](active-directory-editions.md). Se invece desiderata per le istruzioni per gli sviluppatori su come toointegrate App personalizzate con Azure AD tramite codice, vedere [scenari di autenticazione per Azure AD](active-directory-authentication-scenarios.md).

Hello raccolta di applicazioni per Azure Active Directory fornisce un elenco di applicazioni che sono note toosupport una forma di single sign-on con Azure Active Directory, come descritto in [questo articolo](active-directory-appssoaccess-whatis.md). Dopo aver (come un IT specialista o sistema integratore all'interno dell'organizzazione) trovato un'applicazione hello desiderate tooconnect, è possibile iniziare da seguire hello fornite istruzioni dettagliate presentate in hello Azure management tooenable portale accesso single sign-on.

I clienti con licenze [Azure Active Directory Premium](active-directory-editions.md) ottengono anche le funzionalità aggiuntive seguenti:

* Integrazione self-service di qualsiasi applicazione che supporta i provider di identità SAML 2.0 (avviato dal provider di servizi o dal provider di identità)
* Integrazione self-service di qualsiasi applicazione Web con una pagina di accesso basata su HTML con [SSO basato su password](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Self-service di connessione delle applicazioni che utilizzano il protocollo SCIM hello per il provisioning dell'utente ([descritto qui](active-directory-scim-provisioning.md))
* Capacità tooadd collegamenti tooany applicazione hello [avvio app di Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) o hello [Pannello di accesso di Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Può trattarsi di applicazioni SaaS utilizzare, ma non è ancora stato toohello boarded nella raccolta di applicazioni Azure AD non solo, ma le applicazioni web di terze parti che l'organizzazione ha distribuito tooservers che controllare, nel cloud hello o locale.

Queste funzionalità, note anche come *modelli di integrazione di app*, forniscono punti di connessione basati sugli standard per le app che supportano SAML, SCIM o l'autenticazione basata su moduli e includono opzioni e impostazioni flessibili per assicurare la compatibilità con numerosissime applicazioni. 

## <a name="adding-an-unlisted-application"></a>Aggiunta di un'applicazione non pubblicata
tooconnect un'applicazione utilizzando un modello di integrazione dell'applicazione, accedere al portale di gestione di Azure hello con l'account di amministratore di Azure Active Directory e passare toohello **Active Directory > [Directory] > applicazioni**selezionare **Aggiungi**e quindi **aggiungere un'applicazione dalla raccolta di hello**. 

![][1]

Nella raccolta di app hello, è possibile aggiungere un'app non elencata usando hello **personalizzato** categoria a sinistra di hello o selezionando hello **aggiungere un'applicazione non pubblicata** collegamento disponibile nella finestra di ricerca hello risultati se l'app desiderata non è stato trovato. Dopo aver immesso un nome per l'applicazione, è possibile configurare opzioni hello single sign-on e comportamento. 

**Suggerimento rapido**: come procedura consigliata, utilizzare hello ricerca funzione toocheck toosee se hello applicazione esiste già nella raccolta di applicazioni hello. Se viene trovato l'applicazione hello e la relativa descrizione vengono citate "Single sign-on", quindi un'applicazione hello già è supportata per single sign-on federato. 

![][2]

Aggiunta di un'applicazione in questo modo fornisce un toohello esperienza molto simili uno a disposizione per le applicazioni pre-integrate. toostart, selezionare **configurare Single Sign-On**. Nella schermata successiva Hello presenta hello seguenti tre opzioni per la configurazione dell'accesso single sign on, descritte nelle sezioni che seguono hello.

![][3]

## <a name="azure-ad-single-sign-on"></a>Single Sign-On di Microsoft Azure AD
Selezionare questa opzione tooconfigure basato su SAML l'autenticazione per un'applicazione hello. Ciò richiede che hello SAML 2.0 per il supporto delle applicazioni e raccogliere informazioni su come toouse hello funzionalità SAML dell'applicazione hello prima di continuare. Dopo aver selezionato **Avanti**, sarà richiesta tooenter tre URL diversi endpoint SAML toohello per un'applicazione hello corrispondente. 

![][4]

Si tratta di:

* **URL di accesso (SP-initiated solo)** : in cui l'utente di hello non toothis toosign-nell'applicazione. Se è configurata l'applicazione hello singolo avviato dal provider di servizi di tooperform accedere, quindi quando l'utente passa toothis URL, il provider di servizi di hello verrà hello reindirizzamento necessarie tooAzure AD tooauthenticate e accesso utente hello in. Se questo campo viene popolato, Azure AD utilizzerà l'applicazione hello toolaunch di URL da Office 365 e hello Pannello di accesso AD Azure. Se questo campo è ommited, Azure AD eseguirà invece il provider di identità-avvio sign-on quando hello app viene avviata da Office 365, hello Pannello di accesso AD Azure o da hello Azure AD single sign-on URL (copiable dalla scheda Dashboard hello).
* **URL autorità di certificazione** -URL autorità di certificazione hello deve identificare in modo univoco un'applicazione hello per il singolo accesso è stata configurata. Questo è il valore di hello che Azure AD invia tooapplication indietro come hello **destinatari** parametro del token SAML hello e un'applicazione hello è toovalidate previsto è. Questo valore viene inoltre visualizzato come hello **ID entità** in qualsiasi metadati SAML forniti da un'applicazione hello. Controllare la documentazione SAML dell'applicazione hello per ulteriori informazioni su cosa è ID entità o è il valore di destinatari. Di seguito è riportato un esempio di come hello URL pubblico viene visualizzato in un'applicazione hello SAML token toohello restituito:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **URL di risposta** -URL di risposta di hello è in un'applicazione hello prevede token SAML di hello tooreceive. Si tratta di cui viene fatto riferimento tooas hello **URL servizio Consumer di asserzione (ACS)**. Controllare la documentazione SAML dell'applicazione hello per informazioni dettagliate sul relativo URL di risposta token SAML o ACS è.
  Dopo avere immesso queste, fare clic su **Avanti** tooproceed toohello nella schermata successiva. Questa schermata fornisce informazioni su quali toobe esigenze configurato su hello applicazione lato tooenable tooaccept un token SAML da Azure AD. 

![][5]

Sono necessari i valori che verranno variano a seconda dell'applicazione hello, controllare la documentazione SAML dell'applicazione hello per informazioni dettagliate. Hello **Sign-On** e **disconnessione** URL del servizio sia risolvere toohello stesso endpoint, ovvero endpoint di gestione delle richieste SAML hello per l'istanza di Azure AD. Hello URL autorità di certificazione è il valore di hello viene visualizzato come hello "Issuer" all'interno di hello applicazione toohello emessi token SAML. 

Dopo aver configurato l'applicazione, fare clic su **Avanti** pulsante e quindi hello **completa** finestra di dialogo tooclose hello. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Assegnazione di utenti e applicazioni di gruppi tooyour SAML
Dopo l'applicazione è stata configurata toouse Azure AD come provider di identità basato su SAML, è quasi pronti tootest. Come un controllo di sicurezza, non Azure AD emetta un token consentendo toosign in un'applicazione hello a meno che non hanno ottenuto l'accesso tramite Azure AD. L'accesso può essere concesso direttamente agli utenti o attraverso un gruppo di cui sono membri. 

tooassign un'applicazione tooyour utente o gruppo, fare clic su hello **assegnare gli utenti** pulsante. Selezionare hello utente o gruppo desidera tooassign e quindi selezionare hello **assegnare** pulsante. 

![][6]

Assegnazione di un utente consentirà AD Azure tooissue un token per l'utente hello, nonché a causa di un riquadro per tooappear questa applicazione nel Pannello di accesso dell'utente hello. Un riquadro dell'applicazione verrà visualizzata anche nell'utilità di avvio applicazione di Office 365 hello se hello utente Usa Office 365. 

È possibile caricare un logo icona per l'applicazione hello utilizzando hello **carica Logo** pulsante hello **configura** scheda per un'applicazione hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Personalizzazione di attestazioni di hello rilasciate nel token SAML hello
Quando un utente esegue l'autenticazione dell'applicazione toohello, Azure AD emetta una app toohello token SAML che contiene informazioni (o attestazioni) sull'utente hello che li identifica in modo univoco. Per impostazione predefinita sono inclusi il nome utente dell'utente hello, indirizzo di posta elettronica, nome e cognome. 

È possibile visualizzare o modificare attestazioni hello inviate in hello applicazione toohello token SAML in hello **attributi** scheda. 

![][7]

Esistono due possibili motivi per cui potrebbe essere necessario attestazioni di hello tooedit rilasciate nel token SAML hello: •hello applicazione è stato scritto toorequire un diverso set di URI di richiesta o richiedere valori •Your applicazione è stata distribuita in un modo che richieda hello NameIdentifier attestazione toobe diverso dal nome utente hello (nome dell'entità utente AKA) archiviati in Azure Active Directory. 

Per informazioni su come tooadd e modificare le attestazioni per questi scenari, vedere questo [articolo sulla personalizzazione di attestazioni](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Test di un'applicazione hello SAML
Dopo aver configurati l'URL di SAML hello e certificato in Azure AD e in un'applicazione hello, utenti o gruppi assegnati toohello applicazione in Azure, le attestazioni hello verificate e modificare se necessario, quindi utente hello è pronto toosign in hello applicazione. 

tootest, semplicemente sign-in Pannello di accesso di Azure AD a https://myapps.microsoft.com utilizzando un account utente è assegnato l'applicazione toohello hello e quindi fare clic sul riquadro hello per tookick applicazione hello processo hello single sign-on. In alternativa, è possibile visualizzare direttamente toohello URL Sign-On per un'applicazione hello sign-in e da lì. 

Per suggerimenti relativi al debug, vedere questo [articolo su come toodebug basato su SAML single sign-on tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Password Single Sign-On
Selezionare questa opzione tooconfigure [basato su password single sign-on](active-directory-appssoaccess-whatis.md) per un'applicazione web che dispone di una pagina di accesso HTML. SSO basato su password, anche la password di cui viene fatto riferimento tooas di archiviazione, consente toomanage accesso e password tooweb le applicazioni utente che non supportano la federazione delle identità. È inoltre utile per scenari dove più utenti devono tooshare un singolo account, ad esempio account di app di social networking tooyour dell'organizzazione. 

Dopo aver selezionato **Avanti**, sarà richiesta tooenter hello URL della pagina dell'applicazione hello basata sul web Accedi. Si noti che deve essere pagina hello che include campi inpui hello nome utente e password. Una volta immesse, Azure AD avvia una processo tooparse hello-pagina di accesso per un input di nome utente e password da immettere. Se il processo di hello non viene completato, quindi vengono attraverso un processo di installazione di un'estensione browser (richiede Internet Explorer, Chrome o Firefox) che consentirà di campi di hello acquisizione toomanually alternativo.

Una volta acquisita hello nella pagina di accesso, utenti e gruppi possono essere assegnati e credenziali criteri possono essere impostati come normali [App basate su password SSO](active-directory-appssoaccess-whatis.md).

Nota: È possibile caricare un logo icona per l'applicazione hello utilizzando hello **carica Logo** pulsante hello **configura** scheda per un'applicazione hello. 

## <a name="existing-single-sign-on"></a>Single Sign-On esistente
Selezionare questa opzione tooadd portale Pannello di accesso AD Azure o Office 365 dell'organizzazione un collegamento tooan applicazione tooyour. È possibile utilizzare questa App tooadd collegamenti toocustom web che ne fanno uso di Azure Active Directory Federation Services (o altro servizio federativo) invece di Azure AD per l'autenticazione. In alternativa, è possibile aggiungere le pagine di SharePoint toospecific collegamenti diretti o altre pagine web che si desidera tooappear in pannelli di accesso dell'utente. 

Dopo aver selezionato **Avanti**, sarà richiesta tooenter hello URL di toolink applicazione hello per. Una volta completato, gli utenti e gruppi possono essere assegnati l'applicazione toohello, che provoca tooappear applicazione hello hello [avvio app di Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) o hello [Pannello di accesso AD Azure](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) per gli utenti.

Nota: È possibile caricare un logo icona per l'applicazione hello utilizzando hello **carica Logo** pulsante hello **configura** scheda per un'applicazione hello.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Come emettere attestazioni tooCustomize in hello Token SAML per le app Pre-Integrated](active-directory-saml-claims-customization.md)
* [Risoluzione dei problemi dell'accesso Single Sign-On basato su SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
