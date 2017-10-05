---
title: Come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory | Microsoft Docs
description: 'Informazioni su come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory  '
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a><span data-ttu-id="10ff1-103">Come eseguire il debug di single sign-on basato su SAML per applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10ff1-103">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>
<span data-ttu-id="10ff1-104">Durante il debug di un'integrazione di applicazioni basate su SAML, è spesso utile utilizzare uno strumento come [Fiddler](http://www.telerik.com/fiddler) per visualizzare la richiesta SAML, la risposta SAML e il token SAML reale emesso per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10ff1-104">When debugging a SAML-based application integration, it is often helpful to use a tool like [Fiddler](http://www.telerik.com/fiddler) to see the SAML request, the SAML response, and the actual SAML token that is issued to the application.</span></span> <span data-ttu-id="10ff1-105">Esaminando il token SAML, è possibile garantire che tutti gli attributi richiesti, il nome utente nell’oggetto SAML e l'URI dell'autorità emittente vengano ricevuti come previsto.</span><span class="sxs-lookup"><span data-stu-id="10ff1-105">By examining the SAML token, you can ensure that all of the required attributes, the username in the SAML subject, and the issuer URI are coming through as expected.</span></span>

![][1]

<span data-ttu-id="10ff1-106">La risposta di Azure AD che contiene il token SAML è in genere quella che si verifica dopo un reindirizzamento HTTP 302 da https://login.windows.net e viene inviata all'**URL di risposta** configurato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="10ff1-106">The response from Azure AD that contains the SAML token is typically the one that occurs after an HTTP 302 redirect from https://login.windows.net, and is sent to the configured **Reply URL** of the application.</span></span> 

<span data-ttu-id="10ff1-107">È possibile visualizzare il token SAML selezionando la riga e quindi la scheda **Ispettori > WebForms** nel riquadro a destra.</span><span class="sxs-lookup"><span data-stu-id="10ff1-107">You can view the SAML token by selecting this line and then selecting the **Inspectors > WebForms** tab in the right panel.</span></span> <span data-ttu-id="10ff1-108">A questo punto fare clic con il pulsante destro sul valore **SAMLResponse** e selezionare **Invia a TextWizard**.</span><span class="sxs-lookup"><span data-stu-id="10ff1-108">From there, right-click the **SAMLResponse** value and select **Send to TextWizard**.</span></span> <span data-ttu-id="10ff1-109">Quindi selezionare **Da Base64** nel menu **Trasforma** per decodificare il token e visualizzarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="10ff1-109">Then select **From Base64** from the **Transform** menu to decode the token and see its contents.</span></span>

<span data-ttu-id="10ff1-110">**Nota**: per visualizzare il contenuto di questa richiesta HTTP, Fiddler potrebbe richiedere di configurare la decrittografia del traffico HTTPS; è necessario eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="10ff1-110">**Note**: To see the contents of this HTTP request, Fiddler may prompt you to configure decryption of HTTPS traffic, which you will need to do.</span></span>

## <a name="related-articles"></a><span data-ttu-id="10ff1-111">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="10ff1-111">Related Articles</span></span>
* [<span data-ttu-id="10ff1-112">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10ff1-112">Article Index for Application Management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="10ff1-113">Configurazione del servizio Single Sign-On in applicazioni non presenti nella raccolta di applicazioni di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10ff1-113">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../active-directory-saas-custom-apps.md)
* [<span data-ttu-id="10ff1-114">Come personalizzare lle attestazioni rilasciate nel token SAML per le app preintegrate</span><span class="sxs-lookup"><span data-stu-id="10ff1-114">How to Customize Claims Issued in the SAML Token for Pre-Integrated Apps</span></span>](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png