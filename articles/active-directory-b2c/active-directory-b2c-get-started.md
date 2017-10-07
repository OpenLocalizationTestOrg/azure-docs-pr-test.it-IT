---
title: 'Azure Active Directory B2C: creare un tenant di Azure Active Directory B2C | Microsoft Docs'
description: Un argomento su come toocreate un B2C di Azure Active Directory del tenant
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
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="ed7c0-103">Creare un tenant di Azure Active Directory B2C in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ed7c0-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="ed7c0-104">Modificato da Sipi.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-104">Edited by Sipi.</span></span>

<span data-ttu-id="ed7c0-105">Questa guida introduttiva permette di creare un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="ed7c0-106">Al termine, si dispone di un toouse tenant B2C per la registrazione delle applicazioni B2C.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed7c0-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ed7c0-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="ed7c0-108">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="ed7c0-108">Log in tooAzure</span></span>

<span data-ttu-id="ed7c0-109">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ed7c0-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="ed7c0-110">Creare un tenant di Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ed7c0-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="ed7c0-111">Le funzionalità B2C non possono essere abilitate nei tenant esistenti.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="ed7c0-112">È necessario toocreate un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="ed7c0-113">Congratulazioni, è stato creato un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="ed7c0-114">Si è un amministratore globale del tenant hello.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="ed7c0-115">può aggiungere altri amministratori globali in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="ed7c0-116">tooyour tooswitch nuovo tenant, fare clic su hello *gestire il nuovo collegamento di tenant*.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Collegamento per gestire il nuovo tenant](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="ed7c0-118">Se si intende toouse un tenant B2C per un'app di produzione, leggere l'articolo hello su [scala di produzione e i tenant anteprima B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="ed7c0-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="ed7c0-119">Vi sono problemi noti quando si elimina un B2C esistenti del tenant e ricrearlo con hello stesso nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="ed7c0-120">È necessario toocreate un tenant B2C con un nome di dominio diverso.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="ed7c0-121">Collegare la sottoscrizione tooyour tenant</span><span class="sxs-lookup"><span data-stu-id="ed7c0-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="ed7c0-122">È necessario toolink il AD B2C Azure tenant tooyour sottoscrizione di Azure tooenable B2C tutte le funzionalità e pagare gli addebiti di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="ed7c0-123">leggere più, toolearn [questo articolo](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="ed7c0-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="ed7c0-124">Se si non collega il tooyour tenant di Azure Active Directory B2C sottoscrizione di Azure, alcune funzionalità è bloccata e viene visualizzato un messaggio di avviso ("alcuna sottoscrizione collegata toothis B2C tenant o hello sottoscrizione non richiede attenzione.") nelle impostazioni di hello B2C.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="ed7c0-125">È importante eseguire questo passaggio prima dell'invio delle applicazioni alla produzione.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="ed7c0-126">Un accesso semplice toosettings</span><span class="sxs-lookup"><span data-stu-id="ed7c0-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="ed7c0-127">È inoltre possibile accedere pannello hello immettendo `Azure AD B2C` in **individuare risorse** nella parte superiore di hello del portale hello.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="ed7c0-128">Selezionare dall'elenco risultati hello **Azure Active Directory B2C** tooaccess hello pannello impostazioni B2C.</span><span class="sxs-lookup"><span data-stu-id="ed7c0-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed7c0-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed7c0-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed7c0-130">Registrare l'applicazione B2C in un tenant B2C</span><span class="sxs-lookup"><span data-stu-id="ed7c0-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
