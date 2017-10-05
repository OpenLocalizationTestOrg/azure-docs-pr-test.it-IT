---
title: 'Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l''iscrizione dell''utente | Documentazione Microsoft'
description: Questo argomento illustra come disabilitare la verifica tramite posta elettronica durante l'iscrizione dell'utente in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="70875-103">Azure Active Directory B2C: disabilitare la verifica tramite posta elettronica durante l'iscrizione dell'utente</span><span class="sxs-lookup"><span data-stu-id="70875-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="70875-104">Quando è abilitato, Azure Active Directory (Azure AD) B2C permette all'utente di iscriversi alle applicazioni specificando un indirizzo di posta elettronica e creando un account locale.</span><span class="sxs-lookup"><span data-stu-id="70875-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="70875-105">Azure AD B2C garantisce la validità degli indirizzi di posta elettronica richiedendone la verifica agli utenti durante il processo di iscrizione.</span><span class="sxs-lookup"><span data-stu-id="70875-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="70875-106">Impedisce anche a processi dannosi automatizzati di generare account fittizi per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="70875-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="70875-107">Alcuni sviluppatori di applicazioni preferiscono ignorare la verifica tramite posta elettronica durante il processo di iscrizione, chiedendo agli utenti di verificare l'indirizzo di posta elettronica in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="70875-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="70875-108">A tale scopo, è possibile configurare Azure AD B2C in modo da disabilitare la verifica tramite posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="70875-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="70875-109">In questo modo si ottiene un processo di iscrizione più semplice e gli sviluppatori hanno la possibilità di distinguere gli utenti che hanno verificato l'indirizzo di posta elettronica da quelli che non lo hanno fatto.</span><span class="sxs-lookup"><span data-stu-id="70875-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="70875-110">Per impostazione predefinita, nei criteri di iscrizione la verifica tramite posta elettronica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="70875-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="70875-111">Per disabilitarla, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="70875-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="70875-112">[Seguire questa procedura per passare al pannello delle funzionalità B2C nel portale di Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="70875-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="70875-113">Fare clic su **Criteri di iscrizione** o su **Criteri di iscrizione o di accesso**, a seconda della configurazione usata per l'iscrizione.</span><span class="sxs-lookup"><span data-stu-id="70875-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="70875-114">Fare clic sul criterio, ad esempio "B2C_1_SiUp", per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="70875-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="70875-115">Fare clic su **Modifica** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="70875-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="70875-116">Fare clic su **Personalizzazione dell'interfaccia utente della pagina**.</span><span class="sxs-lookup"><span data-stu-id="70875-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="70875-117">Fare clic su **Pagina di iscrizione dell'account locale**.</span><span class="sxs-lookup"><span data-stu-id="70875-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="70875-118">Fare clic su **Indirizzo di posta elettronica** nella colonna **Nome** sotto la sezione **Attributi di iscrizione**.</span><span class="sxs-lookup"><span data-stu-id="70875-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="70875-119">Impostare l'opzione **Richiedi la verifica** su **No**.</span><span class="sxs-lookup"><span data-stu-id="70875-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="70875-120">Fare clic su **OK** nella parte inferiore fino a raggiungere il pannello **Modifica criterio**.</span><span class="sxs-lookup"><span data-stu-id="70875-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="70875-121">Fare clic su **Salva** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="70875-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="70875-122">L'operazione è completata.</span><span class="sxs-lookup"><span data-stu-id="70875-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="70875-123">Disabilitando la verifica tramite posta elettronica nel processo di iscrizione si potrebbe ricevere posta indesiderata.</span><span class="sxs-lookup"><span data-stu-id="70875-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="70875-124">Se si disabilita il sistema di verifica predefinito, è consigliabile aggiungerne uno personalizzato.</span><span class="sxs-lookup"><span data-stu-id="70875-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="70875-125">Commenti e suggerimenti sono sempre graditi.</span><span class="sxs-lookup"><span data-stu-id="70875-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="70875-126">In caso di difficoltà con questo argomento o di suggerimenti per migliorarne il contenuto, è possibile lasciare un commento nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="70875-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="70875-127">Le richieste di funzionalità possono essere aggiunte in [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="70875-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>