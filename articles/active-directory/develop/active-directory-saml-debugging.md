---
title: aaaHow toodebug basato su SAML single sign-on tooapplications in Azure Active Directory | Documenti Microsoft
description: 'Informazioni su come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory '
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory
Durante il debug di un'integrazione dell'applicazione basato su SAML, è spesso utile toouse uno strumento come [Fiddler](http://www.telerik.com/fiddler) toosee hello richiesta, risposta SAML hello e token SAML effettivo hello che viene eseguita l'applicazione toohello SAML. Esaminando i token SAML hello, è possibile verificare che tutti di hello richiesti gli attributi, nome utente nell'oggetto SAML hello hello e hello issuer URI provengano tramite come previsto.

![][1]

Hello risposta da Azure Active Directory che contiene i token SAML hello è in genere che si verifica dopo un reindirizzamento HTTP 302 da https://login.windows.net hello e sia configurato inviato toohello **URL di risposta** di un'applicazione hello. 

È possibile visualizzare i token SAML hello selezionando la riga e quindi selezionando hello **controlli > WebForms** scheda nel riquadro di destra hello. Da qui, fare doppio clic su hello **SAMLResponse** valore e selezionare **inviare tooTextWizard**. Selezionare quindi **da Base64** da hello **trasformare** toodecode menu hello token e visualizzarne il contenuto.

**Nota**: richiesta di contenuto hello toosee questo HTTP, Fiddler venga chiesto di decrittografia tooconfigure del traffico HTTPS, che dovrà essere toodo.

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](../active-directory-apps-index.md)
* [Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione](../active-directory-saas-custom-apps.md)
* [Come emettere attestazioni tooCustomize in hello Token SAML per le app Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png