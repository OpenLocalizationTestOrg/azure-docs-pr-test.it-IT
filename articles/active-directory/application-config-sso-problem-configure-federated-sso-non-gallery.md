---
title: configurazione di single sign-on federato per un'applicazione non raccolta aaaProblem | Documenti Microsoft
description: "Risolvere alcuni dei problemi di hello comuni che riscontrabili durante la configurazione federata single sign-on tooyour personalizzata SAML dell'applicazione che non è elencato nella raccolta di applicazioni Azure AD hello"
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
ms.openlocfilehash: 8c80f0001de01cbc9930ef0441cd804082ee8578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a>Problema nella configurazione dell'accesso Single Sign-On federato per un'applicazione non inclusa nella raccolta di Azure AD

Se si verifica un problema durante la configurazione di un'applicazione. Verificare di aver seguito tutti i passaggi nell'articolo hello hello [configurazione single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)

## <a name="cant-add-another-instance-of-hello-application"></a>Non è possibile aggiungere un'altra istanza di un'applicazione hello

tooadd una seconda istanza di un'applicazione, è necessario poter toobe:

-   Configurare un identificatore univoco per la seconda istanza hello. Non sarà in grado di tooconfigure hello stesso identificatore utilizzato per la prima istanza hello.

-   Configurare un certificato diverso da hello di hello prima istanza.

Se hello applicazione non supporta i hello precedente. Quindi, non sarà in grado di tooconfigure una seconda istanza.

## <a name="where-do-i-set-hello-entityid-user-identifier-format"></a>In cui è possibile impostare il formato di EntityID (ID utente) hello

Sarà formato EntityID (ID utente) di hello tooselect in grado di Azure AD invia toohello applicazione in risposta hello dopo l'autenticazione utente.

Azure AD selezionare hello formato attributo NameID hello (ID utente) in base al valore di hello selezionato o per hello formato richiesto da un'applicazione hello in hello AuthRequest SAML. Per ulteriori informazioni visitare articolo hello [protocollo Single Sign-On SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) nella sezione hello NameIDPolicy,

## <a name="where-do-i-get-hello-application-metadata-or-certificate-from-azure-ad"></a>Dove ottenere i metadati dell'applicazione hello o un certificato da Azure AD

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
