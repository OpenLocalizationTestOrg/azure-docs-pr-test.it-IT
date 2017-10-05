---
title: 'Azure Active Directory B2C: creare un tenant di Azure Active Directory B2C | Microsoft Docs'
description: Un argomento su come creare un tenant di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="4f452-103">Creare un tenant di Azure Active Directory B2C nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4f452-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="4f452-104">Modificato da Sipi.</span><span class="sxs-lookup"><span data-stu-id="4f452-104">Edited by Sipi.</span></span>

<span data-ttu-id="4f452-105">Questa guida introduttiva permette di creare un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4f452-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="4f452-106">Al termine, sarà disponibile un tenant B2C da usare per la registrazione di applicazioni B2C.</span><span class="sxs-lookup"><span data-stu-id="4f452-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f452-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f452-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="4f452-108">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="4f452-108">Log in to Azure</span></span>

<span data-ttu-id="4f452-109">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f452-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="4f452-110">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="4f452-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="4f452-111">Le funzionalità B2C non possono essere abilitate nei tenant esistenti.</span><span class="sxs-lookup"><span data-stu-id="4f452-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="4f452-112">A questo scopo, è necessario creare un tenant di Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4f452-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="4f452-113">Congratulazioni, è stato creato un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="4f452-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="4f452-114">L'amministratore globale del tenant</span><span class="sxs-lookup"><span data-stu-id="4f452-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="4f452-115">può aggiungere altri amministratori globali in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="4f452-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="4f452-116">Per passare al nuovo tenant, fare clic sul *collegamento per gestire il nuovo tenant*.</span><span class="sxs-lookup"><span data-stu-id="4f452-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Collegamento per gestire il nuovo tenant](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="4f452-118">Se si prevede di usare un tenant B2C per un'app di produzione, vedere l'articolo sui [tenant B2C a livello di produzione e di anteprima](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="4f452-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="4f452-119">Quando si elimina un tenant B2C esistente e lo si crea di nuovo con lo stesso nome di dominio, si verificano alcuni problemi noti.</span><span class="sxs-lookup"><span data-stu-id="4f452-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="4f452-120">È necessario creare un tenant B2C con un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="4f452-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="4f452-121">Collegare il tenant alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="4f452-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="4f452-122">È necessario collegare il tenant di Azure AD B2C alla sottoscrizione di Azure per abilitare tutte le funzionalità B2C e pagare i costi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4f452-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="4f452-123">Per altre informazioni, vedere [questo articolo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="4f452-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="4f452-124">Se si non collega il tenant di Azure AD B2C alla sottoscrizione di Azure, alcune funzionalità saranno bloccate e verrà visualizzato un messaggio di avviso ("Nessuna sottoscrizione collegata a questo tenant B2C oppure la sottoscrizione richiede attenzione") nelle impostazioni B2C.</span><span class="sxs-lookup"><span data-stu-id="4f452-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="4f452-125">È importante eseguire questo passaggio prima dell'invio delle applicazioni alla produzione.</span><span class="sxs-lookup"><span data-stu-id="4f452-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="4f452-126">Accedere facilmente alle impostazioni</span><span class="sxs-lookup"><span data-stu-id="4f452-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="4f452-127">Per accedere al pannello, è anche possibile immettere `Azure AD B2C` in **Cerca risorse** nella parte superiore del portale.</span><span class="sxs-lookup"><span data-stu-id="4f452-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="4f452-128">Nell'elenco dei risultati selezionare **Azure AD B2C** per accedere al pannello delle impostazioni B2C.</span><span class="sxs-lookup"><span data-stu-id="4f452-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f452-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f452-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f452-130">Registrare l'applicazione B2C in un tenant B2C</span><span class="sxs-lookup"><span data-stu-id="4f452-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
