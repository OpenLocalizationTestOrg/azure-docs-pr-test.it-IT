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
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a><span data-ttu-id="576bf-103">Come toodebug basato su SAML single sign-on tooapplications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="576bf-103">How toodebug SAML-based single sign-on tooapplications in Azure Active Directory</span></span>
<span data-ttu-id="576bf-104">Durante il debug di un'integrazione dell'applicazione basato su SAML, è spesso utile toouse uno strumento come [Fiddler](http://www.telerik.com/fiddler) toosee hello richiesta, risposta SAML hello e token SAML effettivo hello che viene eseguita l'applicazione toohello SAML.</span><span class="sxs-lookup"><span data-stu-id="576bf-104">When debugging a SAML-based application integration, it is often helpful toouse a tool like [Fiddler](http://www.telerik.com/fiddler) toosee hello SAML request, hello SAML response, and hello actual SAML token that is issued toohello application.</span></span> <span data-ttu-id="576bf-105">Esaminando i token SAML hello, è possibile verificare che tutti di hello richiesti gli attributi, nome utente nell'oggetto SAML hello hello e hello issuer URI provengano tramite come previsto.</span><span class="sxs-lookup"><span data-stu-id="576bf-105">By examining hello SAML token, you can ensure that all of hello required attributes, hello username in hello SAML subject, and hello issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="576bf-106">Hello risposta da Azure Active Directory che contiene i token SAML hello è in genere che si verifica dopo un reindirizzamento HTTP 302 da https://login.windows.net hello e sia configurato inviato toohello **URL di risposta** di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="576bf-106">hello response from Azure AD that contains hello SAML token is typically hello one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent toohello configured **Reply URL** of hello application.</span></span> 

<span data-ttu-id="576bf-107">È possibile visualizzare i token SAML hello selezionando la riga e quindi selezionando hello **controlli > WebForms** scheda nel riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="576bf-107">You can view hello SAML token by selecting this line and then selecting hello **Inspectors > WebForms** tab in hello right panel.</span></span> <span data-ttu-id="576bf-108">Da qui, fare doppio clic su hello **SAMLResponse** valore e selezionare **inviare tooTextWizard**.</span><span class="sxs-lookup"><span data-stu-id="576bf-108">From there, right-click hello **SAMLResponse** value and select **Send tooTextWizard**.</span></span> <span data-ttu-id="576bf-109">Selezionare quindi **da Base64** da hello **trasformare** toodecode menu hello token e visualizzarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="576bf-109">Then select **From Base64** from hello **Transform** menu toodecode hello token and see its contents.</span></span>

<span data-ttu-id="576bf-110">**Nota**: richiesta di contenuto hello toosee questo HTTP, Fiddler venga chiesto di decrittografia tooconfigure del traffico HTTPS, che dovrà essere toodo.</span><span class="sxs-lookup"><span data-stu-id="576bf-110">**Note**: toosee hello contents of this HTTP request, Fiddler may prompt you tooconfigure decryption of HTTPS traffic, which you will need toodo.</span></span>

## <a name="related-articles"></a><span data-ttu-id="576bf-111">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="576bf-111">Related Articles</span></span>
* [<span data-ttu-id="576bf-112">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="576bf-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="576bf-113">Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="576bf-113">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="576bf-114">Come emettere attestazioni tooCustomize in hello Token SAML per le app Pre-Integrated</span><span class="sxs-lookup"><span data-stu-id="576bf-114">How tooCustomize Claims Issued in hello SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png