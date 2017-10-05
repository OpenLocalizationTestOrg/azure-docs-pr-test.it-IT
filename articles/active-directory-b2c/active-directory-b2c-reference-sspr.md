---
title: 'Azure Active Directory B2C: reimpostazione password self-service | Documentazione Microsoft'
description: Un argomento che dimostra come configurare la reimpostazione della password self-service per gli utenti in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="f944d-103">Azure Active Directory B2C: configurare la reimpostazione password self-service per gli utenti</span><span class="sxs-lookup"><span data-stu-id="f944d-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="f944d-104">La funzione di reimpostazione password self-service consente agli utenti che hanno effettuato la registrazione agli account locali di reimpostare le password in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="f944d-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="f944d-105">Questo riduce notevolmente il carico per lo staff di supporto, soprattutto se l'applicazione dispone di milioni di clienti che la utilizzano regolarmente.</span><span class="sxs-lookup"><span data-stu-id="f944d-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="f944d-106">Attualmente, è supportato solo l’utilizzo di un indirizzo di posta elettronica verificato come metodo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f944d-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="f944d-107">Verranno aggiunti metodi di ripristino aggiuntivi (numero di telefono verificato, domande di sicurezza e così via) in futuro.</span><span class="sxs-lookup"><span data-stu-id="f944d-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="f944d-108">Questo articolo si applica alla reimpostazione delle password self-service nel contesto di un criterio di accesso.</span><span class="sxs-lookup"><span data-stu-id="f944d-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="f944d-109">Se è necessario richiamare dall'app criteri di reimpostazione delle password completamente personalizzabili, vedere [questo articolo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="f944d-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="f944d-110">Per impostazione predefinita, la directory non avrà la reimpostazione password self-service attivata.</span><span class="sxs-lookup"><span data-stu-id="f944d-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="f944d-111">Usare i passaggi seguenti per attivarla:</span><span class="sxs-lookup"><span data-stu-id="f944d-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="f944d-112">Accedere al [portale di Azure classico](https://manage.windowsazure.com/) come amministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f944d-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="f944d-113">Si tratta dello stesso account aziendale o dell'istituto d'istruzione o dello stesso account Microsoft usato per la creazione della directory.</span><span class="sxs-lookup"><span data-stu-id="f944d-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="f944d-114">Passare all'estensione Active Directory sulla barra di spostamento sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="f944d-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="f944d-115">Trovare la directory nella scheda **Directory** e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="f944d-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="f944d-116">Fare clic sulla scheda **Configure** .</span><span class="sxs-lookup"><span data-stu-id="f944d-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="f944d-117">Scorrere verso il basso fino alla sezione **Criteri di reimpostazione password utente** e impostare l'opzione **Utenti abilitati per la reimpostazione della password** su **SÌ**.</span><span class="sxs-lookup"><span data-stu-id="f944d-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="f944d-118">Si noti che l'opzione **Indirizzo di posta elettronica alternativo** è selezionata. Non modificarla.</span><span class="sxs-lookup"><span data-stu-id="f944d-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Reimpostazione della password self-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="f944d-120">Fare clic su **Save** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="f944d-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="f944d-121">L'operazione è completata.</span><span class="sxs-lookup"><span data-stu-id="f944d-121">You're done!</span></span>

<span data-ttu-id="f944d-122">Per eseguire il test, usare la funzionalità "Esegui adesso" in ogni criterio di accesso che include gli account locali come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="f944d-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="f944d-123">Nella pagina di accesso dell'account locale in cui si immettono l'indirizzo di posta elettronica e la password o il nome utente e la password, fare clic su **Problemi di accesso all'account?** per verificare l'esperienza dell'utente.</span><span class="sxs-lookup"><span data-stu-id="f944d-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="f944d-124">Le pagine di reimpostazione della password self-service possono essere personalizzate con la [funzionalità di aggiunta di informazioni distintive dell'azienda](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="f944d-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

