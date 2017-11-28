---
title: "società specifiche della lingua aaaAdd tooyour nella pagina di accesso in hello Azure Active Directory di branding | Documenti Microsoft"
description: Informazioni su come un linguaggio specifico di tooadd aziendale personalizzazione immagini e testo tooan Accedi Azure pagina
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="c2061-103">Aggiungere personalizzazione tooyour nella pagina di accesso in hello Azure Active Directory della società specifiche della lingua</span><span class="sxs-lookup"><span data-stu-id="c2061-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="c2061-104">tooavoid confusione, molte società desidera tooapply un aspetto coerente in tutti i siti Web di hello e i servizi gestiti.</span><span class="sxs-lookup"><span data-stu-id="c2061-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="c2061-105">Azure Active Directory fornisce questa funzionalità, consentendo l'aspetto di hello toocustomize di hello nella pagina di accesso con il logo della società e combinazioni di colori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="c2061-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c2061-106">pagina di accesso Hello è hello pagina viene visualizzata quando si accede tooOffice 365 o altre applicazioni basate su web che usano Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c2061-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c2061-107">Si interagiscono con tooenter questa pagina delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="c2061-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="c2061-108">Personalizzazione hello-pagina di accesso per un'altra lingua</span><span class="sxs-lookup"><span data-stu-id="c2061-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="c2061-109">È possibile aggiungere elementi specifici della lingua tooyour personalizzato nella pagina di accesso solo se è già stato creato una pagina di accesso personalizzata come descritto in [aggiungere personalizzazione pagina di accesso tooyour della società](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c2061-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="c2061-110">È possibile configurare una pagina di accesso per ogni directory con un set predefinito di elementi personalizzabili.</span><span class="sxs-lookup"><span data-stu-id="c2061-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="c2061-111">Dopo aver configurato i set di hello predefinito degli elementi di pagina, è possibile configurare più versioni per impostazioni locali diverse.</span><span class="sxs-lookup"><span data-stu-id="c2061-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="c2061-112">È anche possibile combinare e abbinare diversi elementi.</span><span class="sxs-lookup"><span data-stu-id="c2061-112">You can also mix and match various elements.</span></span> <span data-ttu-id="c2061-113">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c2061-113">For example, you could:</span></span>

* <span data-ttu-id="c2061-114">Creare un' **immagine della pagina di accesso** predefinita adatta per tutte le impostazioni cultura, quindi creare versioni specifiche per l'inglese e il francese.</span><span class="sxs-lookup"><span data-stu-id="c2061-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="c2061-115">Quando si imposta il tooone browser di queste due lingue, hello specifiche della lingua immagine viene visualizzata, mentre l'immagine predefinita hello viene visualizzata per tutti gli altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="c2061-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="c2061-116">Configurare loghi diversi per l'organizzazione, ad esempio una versione giapponese o ebraica.</span><span class="sxs-lookup"><span data-stu-id="c2061-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="c2061-117">È consigliabile mantenere il numero di hello di variazioni nel linguaggio basso, per motivi di prestazioni e manutenzione.</span><span class="sxs-lookup"><span data-stu-id="c2061-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="c2061-118">**directory tooadd aziendale personalizzazione tooyour:**</span><span class="sxs-lookup"><span data-stu-id="c2061-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="c2061-119">Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.</span><span class="sxs-lookup"><span data-stu-id="c2061-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c2061-120">Selezionare **più servizi**, immettere **utenti e gruppi** nella casella di testo hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="c2061-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="c2061-122">In hello **utenti e gruppi** pannello seleziona **personalizzazione specifica della società**.</span><span class="sxs-lookup"><span data-stu-id="c2061-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c2061-123">In hello **utenti e gruppi - personalizzazione specifica della società** blade, seleziona hello **Aggiungi lingua** comando.</span><span class="sxs-lookup"><span data-stu-id="c2061-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![Aggiungere elementi personalizzati distintivi dell'azienda specifiche della lingua](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="c2061-125">Modificare gli elementi di hello desiderati toocustomize.</span><span class="sxs-lookup"><span data-stu-id="c2061-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="c2061-126">Tutti gli elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="c2061-126">All elements are optional.</span></span>
6. <span data-ttu-id="c2061-127">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c2061-127">Click **Save**.</span></span>

<span data-ttu-id="c2061-128">Potrebbe essere necessaria fino tooan ora per tutte le modifiche apportate toohello Accedi pagina tooappear personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="c2061-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2061-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2061-129">Next steps</span></span>
[<span data-ttu-id="c2061-130">Aggiungere personalizzazione pagina di accesso tooyour della società</span><span class="sxs-lookup"><span data-stu-id="c2061-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
