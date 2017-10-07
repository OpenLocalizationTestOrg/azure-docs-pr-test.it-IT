---
title: la configurazione di single sign-on federato per un'applicazione Azure AD raccolta aaaProblem | Documenti Microsoft
description: "Risolvere alcuni dei problemi più comuni di hello che si verifichino quando configurazione federata single sign-on tramite SAML per le applicazioni che sono elencate nella raccolta di applicazioni Azure AD hello"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2ae1e511bd49b19159e1ab83cf79a7db5403b9a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-an-azure-ad-gallery-application"></a>Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione nella raccolta di Azure AD

Se si verifica un problema durante la configurazione di un'applicazione. Verificare di che aver seguito tutti i passaggi di hello in esercitazione hello per un'applicazione hello. Nella configurazione dell'applicazione hello, si dispone della documentazione in linea in modalità tooconfigure hello applicazione. Inoltre, è possibile accedere hello [elenco di esercitazioni sull'App SaaS toointegrate con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) per una Guida di dettaglio.

## <a name="cant-add-another-instance-of-hello-application"></a>Non è possibile aggiungere un'altra istanza di un'applicazione hello

tooadd una seconda istanza di un'applicazione, è necessario poter toobe:

-   Configurare un identificatore univoco per la seconda istanza hello. Non sarà in grado di tooconfigure hello stesso identificatore utilizzato per la prima istanza hello.

-   Configurare un certificato diverso da hello di hello prima istanza.

Se hello applicazione non supporta i hello precedente. Quindi, non sarà in grado di tooconfigure una seconda istanza.

## <a name="cant-add-hello-identifier-or-hello-reply-url"></a>Non è possibile aggiungere l'identificatore hello o hello URL di risposta

Se non si è in grado di tooconfigure hello identificatore o URL di risposta hello, confermare l'identificatore hello e valori di URL di risposta corrispondono a criteri di hello preconfigurati per l'applicazione hello.

modelli di hello tooknow preconfigurati per l'applicazione hello:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.** Passare toostep 7. Se già presenti nel Pannello di configurazione dell'applicazione hello Azure AD.

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare l'applicazione hello tooconfigure single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Selezionare **basato su SAML Sign-on** da hello **modalità** elenco a discesa.

9.  Passare toohello **identificatore** o **URL di risposta** casella di testo, in hello **sezione URL e di dominio.**

10. Esistono tre modi diversi modelli di tooknow hello è supportato per un'applicazione hello:

   * Nella casella di testo hello hello supportato criteri viene visualizzato come segnaposto *esempio:* <https://contoso.com>.

   * Se hello pattern non è supportato, viene visualizzato un punto esclamativo rosso quando si tenta di valore hello tooenter nella casella di testo hello. Se si posiziona il puntatore del mouse sul punto esclamativo rosso hello, visualizzare i modelli di hello è supportato.

   * Nell'esercitazione di hello per un'applicazione hello, è anche possibile ottenere informazioni sui pattern di hello è supportato. In hello **Configura Azure AD single sign-on** sezione. Passaggio toohello passare i valori hello configurata in hello **dominio e gli URL** sezione.

Se i valori hello non corrispondano con i modelli di hello preconfigurati in Azure AD. È possibile:

-   Lavorare con i valori tooget fornitore dell'applicazione hello che corrispondono a criterio hello preconfigurato in Azure AD

-   In alternativa, è possibile contattare il team di Azure AD < aadapprequest@microsoft.com > o lasciare un commento nell'aggiornamento di hello toorequest esercitazione hello dei modelli di hello è supportato per un'applicazione hello

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>In cui è possibile impostare il formato di EntityID (ID utente) hello

Sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.

Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) nella sezione hello NameIDPolicy,

## <a name="cant-find-hello-azure-ad-metadata-toocomplete-hello-configuration-with-hello-application"></a>Impossibile trovare la configurazione hello Azure AD metadati toocomplete hello con un'applicazione hello

i metadati dell'applicazione hello toodownload o un certificato da Azure AD, procedura hello riportata di seguito:

1.  Aprire hello [ **portale Azure** ](https://portal.azure.com/) e accedere come un **amministratore globale** o **Co-amministratore.**

2.  Aprire hello **estensione di Azure Active Directory** facendo **più servizi** nella parte inferiore di hello del menu di navigazione a sinistra principale hello.

3.  Digitare **"Azure Active Directory**" nella casella di ricerca di filtro hello e seleziona hello **Azure Active Directory** elemento.

4.  Fare clic su **applicazioni aziendali** dal menu di navigazione a sinistra di hello Azure Active Directory.

5.  Fare clic su **tutte le applicazioni** tooview un elenco di tutte le applicazioni.

   * Se non viene visualizzata l'applicazione hello da visualizzare qui, utilizzare hello **filtro** controllo nella parte superiore di hello di hello **elenco di tutte le applicazioni** e set hello **Mostra** opzione troppo **Tutte le applicazioni.**

6.  Selezionare un'applicazione hello è stato configurato single sign-on.

7.  Una volta che un'applicazione hello caricato, fare clic su hello **Single sign-on** dal menu di navigazione a sinistra dell'applicazione hello.

8.  Andare troppo**certificato di firma SAML** sezione, quindi fare clic su **scaricare** valore della colonna. A seconda di quale applicazione hello richiede la configurazione di single sign-on, vedere uno toodownload opzione hello hello Metadata XML o hello certificato.

Azure AD non fornisce i metadati hello tooget URL. Hello metadati possono essere recuperati solo come un file XML.

## <a name="dont-know-how-toocustomize-saml-claims-sent-tooan-application"></a>Non conosce la modalità di invio applicazione tooan attestazioni SAML toocustomize

toolearn come le attestazioni degli attributi toocustomize hello SAML inviato tooyour applicazione, vedere [attestazioni mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) per ulteriori informazioni.

## <a name="next-steps"></a>Passaggi successivi
[Gestione di applicazioni con Azure Active Directory](active-directory-enable-sso-scenario.md)
