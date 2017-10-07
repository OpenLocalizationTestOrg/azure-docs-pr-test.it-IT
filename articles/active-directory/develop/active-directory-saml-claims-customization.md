---
title: attestazioni aaaCustomizing rilasciate nel token SAML hello per le app preintegrate in Azure Active Directory | Documenti Microsoft
description: Informazioni su come toocustomize hello attestazioni rilasciate in hello token SAML per le app preintegrate in Azure Active Directory
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Personalizzazione di attestazioni emesse in hello token SAML per le app preintegrate in Azure Active Directory
Oggi Azure Active Directory supporta migliaia di applicazioni già integrate nella raccolta di applicazioni AD Azure, tra cui superiori a 360 che supportano l'accesso single sign-on hello protocollo hello SAML 2.0. Quando un utente esegue l'autenticazione tooan applicazione tramite Azure AD usando SAML, Azure AD invia un'applicazione toohello token (mediante un HTTP POST). E quindi, un'applicazione hello convalida e utilizza hello toolog token hello utente anziché richiedere un nome utente e password. I token SAML contengono informazioni sull'utente, hello noto come "attestazioni".

Parlando di identità, un'attestazione"" informazioni relative a un provider di identità su un utente all'interno di hello token rilasciati per tale utente. In [token SAML](http://en.wikipedia.org/wiki/SAML_2.0), questi dati sono in genere sono contenuti nell'istruzione di attributi SAML hello. Hello ID univoco dell'utente viene rappresentato in genere in hello che SAML Subject nota anche come nome di identificatore.

Per impostazione predefinita, Azure Active Directory rilascia un'applicazione tooyour token SAML che contiene un'attestazione NameIdentifier, con un valore del nome utente dell'utente hello (nome dell'entità utente AKA) in Azure AD. Questo valore può identificare in modo univoco l'utente hello. token SAML Hello contiene inoltre le attestazioni aggiuntive contenente l'indirizzo di posta elettronica dell'utente hello, nome e cognome.

tooview o modificare attestazioni hello rilasciato in hello applicazione toohello token SAML, un'applicazione hello Apri nel portale di Azure. Selezionare quindi hello **visualizzazione e modificare tutti gli altri attributi utente** casella di controllo in hello **gli attributi utente** sezione dell'applicazione hello.

![Sezione Attributi utente][1]

Esistono due possibili motivi per cui potrebbe essere necessario attestazioni di hello tooedit rilasciate nel token SAML hello:
* un'applicazione Hello è stato scritto toorequire un diverso set di URI di attestazione o i valori di attestazione.
* un'applicazione Hello è stata distribuita in modo che richiede un valore diverso da hello username (nome dell'entità utente AKA) archiviati in Azure Active Directory toobe di attestazione NameIdentifier hello.

È possibile modificare uno dei valori di attestazione predefiniti hello. Selezionare una riga attestazione hello nella tabella di attributi del token SAML hello. Verrà visualizzata hello **Modifica attributo** sezione e quindi è possibile modificare nome attestazione, valore e lo spazio dei nomi associata all'attestazione hello.

![Modifica attributo utente][2]

È inoltre possibile rimuovere attestazioni (ad eccezione della NameIdentifier) utilizzando hello menu di scelta rapida, visualizzato facendo clic su hello **...**  icona.  È inoltre possibile aggiungere nuove attestazioni usando hello **Aggiungi attributo** pulsante.

![Modifica attributo utente][3]

## <a name="editing-hello-nameidentifier-claim"></a>La modifica di attestazione NameIdentifier hello
problema di hello toosolve in cui è stata distribuita un'applicazione hello utilizzando un nome utente diverso, fare clic su hello **identificatore utente** elenco a discesa in hello **gli attributi utente** sezione. Verrà visualizzata una finestra di dialogo con diverse opzioni:

![Modifica attributo utente][4]

Nell'elenco a discesa hello, selezionare **user.mail** tooset hello NameIdentifier attestazione indirizzo di posta elettronica dell'utente di hello toobe nella directory hello. In alternativa, selezionare **user.onpremisessamaccountname** tooset toohello SAM nome dell'Account utente che è stato sincronizzato da locale AD Azure.

È inoltre possibile utilizzare speciale hello **ExtractMailPrefix()** suffisso di funzione tooremove hello dominio dall'indirizzo di posta elettronica hello, nome Account SAM o nome dell'entità utente hello. Ciò consente di estrarre solo prima parte di hello dell'utente hello Nome passati tramite (ad esempio, "joe_smith" invece di joe_smith@contoso.com).

![Modifica attributo utente][5]

Ora è stata anche aggiunta hello **join** hello toojoin funzione verificato dominio con valore dell'identificatore utente hello. Quando si seleziona funzione di join hello in hello **identificatore utente** prima istruzione select hello identificatore utente come nome dell'entità di posta elettronica utente o indirizzo e quindi selezionare il dominio verificato in hello secondo discesa. Se si seleziona l'indirizzo di posta elettronica hello con dominio verificato hello e Azure AD estrae hello username da hello primo valore joe_smith da joe_smith@contoso.com e lo aggiunge con contoso.onmicrosoft.com. Vedere hello di esempio seguente:

![Modifica attributo utente][6]

## <a name="adding-claims"></a>Aggiunta di attestazioni
Quando si aggiunge un'attestazione, è possibile specificare nome dell'attributo hello (che non deve necessariamente un modello di URI in base alle specifiche SAML hello toofollow). Impostare l'attributo hello valore tooany utente che viene archiviato nella directory hello.

![Aggiungi attributo utente][7]

Ad esempio, è necessario toosend reparto hello che hello utente appartiene tooin organizzazione come attestazione (ad esempio, le vendite). Immettere il nome di attestazione hello come previsto dall'applicazione hello e quindi selezionare **Department** come valore di hello.

> [!NOTE]
> Se per un determinato utente è presente alcun valore archiviato per un attributo selezionato, quindi tale attestazione non è vengono rilasciati token di hello.

> [!TIP]
> Hello **user.onpremisesecurityidentifier** e **user.onpremisesamaccountname** sono supportate solo quando la sincronizzazione dei dati utente da Active Directory locale usando hello [Azure Strumento di connessione AD](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Attestazioni con restrizioni

Esistono alcune attestazioni con restrizioni in SAML. Se si aggiungono queste attestazioni, Azure AD non le invia. Di seguito sono hello SAML limitato set di attestazioni:

    | Tipo di attestazione (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>Passaggi successivi
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](../active-directory-apps-index.md)
* [Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione](../active-directory-saas-custom-apps.md)
* [Risoluzione dei problemi dell'accesso Single Sign-On basato su SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png