---
title: 'Azure Active Directory B2C: reimpostazione password self-service | Documentazione Microsoft'
description: "Un argomento che illustra la modalità di reimpostazione tooset di password self-service per consentire agli utenti in Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="b93c0-103">Azure Active Directory B2C: configurare la reimpostazione password self-service per gli utenti</span><span class="sxs-lookup"><span data-stu-id="b93c0-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="b93c0-104">Con hello funzionalità di reimpostazione password self-service, il consumer (che hanno effettuato l'iscrizione per gli account locali) possono reimpostare la password in modo autonomo.</span><span class="sxs-lookup"><span data-stu-id="b93c0-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="b93c0-105">Questo riduce notevolmente onere hello per il personale di supporto, soprattutto se l'applicazione dispone di milioni di clienti utilizzarlo a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="b93c0-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="b93c0-106">Attualmente, è supportato solo l’utilizzo di un indirizzo di posta elettronica verificato come metodo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b93c0-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="b93c0-107">Metodi di ripristino aggiuntivi (numero di telefono verificato, domande di sicurezza e così via) verrà aggiunto in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="b93c0-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="b93c0-108">Questo articolo riguarda tooself-service password reset usata nel contesto di hello di criteri di accesso.</span><span class="sxs-lookup"><span data-stu-id="b93c0-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="b93c0-109">Se è necessario richiamare dall'app criteri di reimpostazione delle password completamente personalizzabili, vedere [questo articolo](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="b93c0-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="b93c0-110">Per impostazione predefinita, la directory non avrà la reimpostazione password self-service attivata.</span><span class="sxs-lookup"><span data-stu-id="b93c0-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="b93c0-111">Utilizzare hello seguendo i passaggi tooturn su:</span><span class="sxs-lookup"><span data-stu-id="b93c0-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="b93c0-112">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) come hello amministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b93c0-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="b93c0-113">Si tratta di hello stesso lavoro o scuola account o hello stesso account Microsoft usato toocreate della directory.</span><span class="sxs-lookup"><span data-stu-id="b93c0-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="b93c0-114">Passare l'estensione Active Directory toohello sulla barra di spostamento hello sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="b93c0-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="b93c0-115">Trovare la directory in hello **Directory** scheda e farvi clic sopra.</span><span class="sxs-lookup"><span data-stu-id="b93c0-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="b93c0-116">Fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="b93c0-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="b93c0-117">Scorrere verso il basso toohello **criteri di reimpostazione password utente** hello sezione e attiva/disattiva **utenti abilitati per la reimpostazione della password** opzione troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="b93c0-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="b93c0-118">Si noti che hello **indirizzo di posta elettronica alternativo** opzione è selezionata, rimane invariato.</span><span class="sxs-lookup"><span data-stu-id="b93c0-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Reimpostazione della password self-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="b93c0-120">Fare clic su **salvare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b93c0-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="b93c0-121">L'operazione è completata.</span><span class="sxs-lookup"><span data-stu-id="b93c0-121">You're done!</span></span>

<span data-ttu-id="b93c0-122">tootest, utilizzo funzionalità "Esegui" hello in un criterio di accesso con account locali come provider di identità.</span><span class="sxs-lookup"><span data-stu-id="b93c0-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="b93c0-123">Hello LocalAccount Accedi pagina (in cui si immette un indirizzo di posta elettronica e password, o un nome utente e password), fare clic su **non è possibile accedere all'account?** esperienza di tooverify hello consumer.</span><span class="sxs-lookup"><span data-stu-id="b93c0-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="b93c0-124">Hello pagine di reimpostazione della password self-service possono essere personalizzate tramite hello [funzionalità di branding aziendale](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="b93c0-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

