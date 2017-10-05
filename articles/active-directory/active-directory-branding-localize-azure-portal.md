---
title: Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua nella pagina di accesso in Azure Active Directory | Microsoft Docs
description: Informazioni su come aggiungere testo e immagini di informazioni personalizzate sull'azienda alla pagina di accesso Azure
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
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="c3e3a-103">Aggiungere informazioni personalizzate distintive dell'azienda specifiche della lingua nella pagina di accesso in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3e3a-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="c3e3a-104">Per evitare confusione, molte aziende vogliono applicare un aspetto coerente a tutti i siti Web e servizi che gestiscono.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="c3e3a-105">Azure Active Directory offre questa funzionalità consentendo di personalizzare l'aspetto delle pagine di accesso, in modo da includere il logo e le combinazioni di colori personalizzate dell'azienda.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="c3e3a-106">La pagina di accesso è la pagina visualizzata quando si accede a Office 365 o ad altre applicazioni basate sul Web che usano Azure AD come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="c3e3a-107">Interagire con questa pagina per immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="c3e3a-108">Personalizzazione della pagina di accesso per un'altra lingua</span><span class="sxs-lookup"><span data-stu-id="c3e3a-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="c3e3a-109">È possibile aggiungere elementi specifici della lingua alla pagina di accesso personalizzata solo se è già stata creata una pagina di accesso personalizzata come descritto in [Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso](active-directory-branding-custom-signon-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c3e3a-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="c3e3a-110">È possibile configurare una pagina di accesso per ogni directory con un set predefinito di elementi personalizzabili.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="c3e3a-111">Dopo avere configurato un set predefinito di elementi di personalizzazione, è possibile configurare altre versioni per impostazioni locali diverse.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="c3e3a-112">È anche possibile combinare e abbinare diversi elementi.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-112">You can also mix and match various elements.</span></span> <span data-ttu-id="c3e3a-113">Ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c3e3a-113">For example, you could:</span></span>

* <span data-ttu-id="c3e3a-114">Creare un' **immagine della pagina di accesso** predefinita adatta per tutte le impostazioni cultura, quindi creare versioni specifiche per l'inglese e il francese.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="c3e3a-115">Quando si impostano i browser su una di queste due lingue, viene visualizzata l'immagine specifica della lingua, mentre per tutte le altre lingue viene visualizzata l'illustrazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="c3e3a-116">Configurare loghi diversi per l'organizzazione, ad esempio una versione giapponese o ebraica.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="c3e3a-117">È consigliabile limitare il numero di varianti linguistiche per facilitare la manutenzione e migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="c3e3a-118">**Per aggiungere informazioni personalizzate distintive dell'azienda alla directory:**</span><span class="sxs-lookup"><span data-stu-id="c3e3a-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="c3e3a-119">Accedere al [portale di Azure](https://portal.azure.com) con un account di amministratore globale per la directory.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c3e3a-120">Selezionare **Altri servizi**, immettere **Utenti e gruppi** nella casella di testo e quindi premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura di Gestione utenti](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="c3e3a-122">Nel pannello **Utenti e gruppi** selezionare **Informazioni personalizzate distintive dell'azienda**.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="c3e3a-123">Nel pannello **Utenti e gruppi - Informazioni personalizzate distintive dell'azienda** selezionare il comando **Aggiungi lingua**.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![Aggiungere elementi personalizzati distintivi dell'azienda specifiche della lingua](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="c3e3a-125">Modificare gli elementi da personalizzare.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="c3e3a-126">Tutti gli elementi sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-126">All elements are optional.</span></span>
6. <span data-ttu-id="c3e3a-127">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-127">Click **Save**.</span></span>

<span data-ttu-id="c3e3a-128">Può trascorrere fino a un'ora prima che qualsiasi modifica apportata per la personalizzazione della pagina di accesso venga visualizzata.</span><span class="sxs-lookup"><span data-stu-id="c3e3a-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3e3a-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3e3a-129">Next steps</span></span>
[<span data-ttu-id="c3e3a-130">Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso</span><span class="sxs-lookup"><span data-stu-id="c3e3a-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
