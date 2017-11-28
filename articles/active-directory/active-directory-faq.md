---
title: domande frequenti di Active Directory aaaAzure | Documenti Microsoft
description: "Azure Active Directory le risposte alle domande relative alla modalità di accesso tooaccess Azure e Azure Active Directory, la gestione delle password e dell'applicazione."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="3f41e-103">Domande frequenti su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f41e-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="3f41e-104">Azure Active Directory (Azure AD) è una soluzione IDaaS (Identity as a Service) completa che si estende a tutti gli aspetti relativi a identità, gestione degli accessi e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="3f41e-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="3f41e-105">Per altre informazioni, vedere [Informazioni su Azure Active Directory](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="3f41e-106">Accedere ad Azure e Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f41e-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="3f41e-107">**D: Perché ricevo "non trovata alcuna sottoscrizione" quando si tenta di tooaccess AD Azure nel portale di Azure classico hello?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-107">**Q: Why do I get “No subscriptions found” when I try tooaccess Azure AD in hello Azure classic portal?**</span></span>

<span data-ttu-id="3f41e-108">**R:** tooaccess hello portale di Azure classico, ogni utente deve avere le autorizzazioni con una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f41e-108">**A:** tooaccess hello Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="3f41e-109">Se si dispone di una sottoscrizione a pagamento di Office 365 o Azure AD, andare troppo[http://aka.ms/accessAAD](http://aka.ms/accessAAD) per un passaggio di attivazione unica.</span><span class="sxs-lookup"><span data-stu-id="3f41e-109">If you have a paid Office 365 or Azure AD subscription, go too[http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="3f41e-110">In caso contrario, sarà necessario tooactivate gratuito [account Azure](https://azure.microsoft.com/pricing/free-trial/) o una sottoscrizione a pagamento.</span><span class="sxs-lookup"><span data-stu-id="3f41e-110">Otherwise, you will need tooactivate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="3f41e-111">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="3f41e-111">For more information, see:</span></span>

* [<span data-ttu-id="3f41e-112">Associare le sottoscrizioni di Azure ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f41e-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="3f41e-113">Gestire directory hello per la sottoscrizione di Office 365 in Azure</span><span class="sxs-lookup"><span data-stu-id="3f41e-113">Manage hello directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="3f41e-114">**D: qual è la relazione hello tra AD Azure, Office 365 e Azure?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-114">**Q: What’s hello relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="3f41e-115">**R:** Azure AD fornisce funzionalità comuni di identità e accessi tooall i servizi web.</span><span class="sxs-lookup"><span data-stu-id="3f41e-115">**A:** Azure AD provides you with common identity and access capabilities tooall web services.</span></span> <span data-ttu-id="3f41e-116">Se si utilizza Office 365, Microsoft Azure, Intune, o altri utenti, si sta già usando Azure AD toohelp attivare la gestione sign-on e l'accesso per tutti questi servizi.</span><span class="sxs-lookup"><span data-stu-id="3f41e-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD toohelp turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="3f41e-117">Tutti gli utenti vengono impostati i servizi web toouse sono definiti come account utente in una o più istanze di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f41e-117">All users who are set up toouse web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="3f41e-118">È possibile configurare questi account per funzionalità di Azure AD gratuite come l'accesso alle applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="3f41e-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="3f41e-119">I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.</span><span class="sxs-lookup"><span data-stu-id="3f41e-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="3f41e-120">**D: perché è possibile accedere toohello portale di Azure ma non hello portale di Azure classico?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-120">**Q:  Why can I sign in toohello Azure portal but not hello Azure classic portal?**</span></span>

<span data-ttu-id="3f41e-121">**R:** hello portale di Azure non richiede una sottoscrizione valida e portale classico hello richiede una sottoscrizione valida.</span><span class="sxs-lookup"><span data-stu-id="3f41e-121">**A:**  hello Azure portal does not require a valid subscription, and hello classic portal does require a valid subscription.</span></span>  <span data-ttu-id="3f41e-122">Se non si dispone di una sottoscrizione, è possibile accedere nel portale classico toohello.</span><span class="sxs-lookup"><span data-stu-id="3f41e-122">If you do not have a subscription, you can't sign in toohello classic portal.</span></span>
- - -
<span data-ttu-id="3f41e-123">**D: quali sono le differenze di hello tra l'amministratore della sottoscrizione e l'amministratore di Directory?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-123">**Q:  What are hello differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="3f41e-124">**R:** per impostazione predefinita, è assegnato il ruolo di amministratore della sottoscrizione hello quando effettua l'iscrizione per Azure.</span><span class="sxs-lookup"><span data-stu-id="3f41e-124">**A:** By default, you are assigned hello Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="3f41e-125">Un amministratore della sottoscrizione è possibile utilizzare un account Microsoft o un lavoro o scuola account dalla directory hello che hello sottoscrizione di Azure è associato.</span><span class="sxs-lookup"><span data-stu-id="3f41e-125">A subscription admin can use either a Microsoft account or a work or school account from hello directory that hello Azure subscription is associated with.</span></span>  <span data-ttu-id="3f41e-126">Questo ruolo è servizi autorizzati toomanage hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3f41e-126">This role is authorized toomanage services in hello Azure portal.</span></span>

<span data-ttu-id="3f41e-127">Se altri necessario toosign in e accedere ai servizi da utilizzando hello stessa sottoscrizione, è possibile aggiungerli come coamministratori.</span><span class="sxs-lookup"><span data-stu-id="3f41e-127">If others need toosign in and access services by using hello same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="3f41e-128">Questo ruolo hello dispone di privilegi di accesso come servizio salve, ma non è possibile modificare l'associazione di hello delle directory tooAzure sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="3f41e-128">This role has hello same access privileges as hello service admin, but can’t change hello association of subscriptions tooAzure directories.</span></span>  <span data-ttu-id="3f41e-129">Per ulteriori informazioni su amministratori della sottoscrizione, vedere [come tooadd o modificare i ruoli di amministratore di Azure](../billing-add-change-azure-subscription-administrator.md) e [delle sottoscrizioni Azure sono associate con Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-129">For additional information on subscription admins, see [How tooadd or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="3f41e-130">Azure AD include un set diverso di amministrazione ruoli toomanage hello directory e le funzionalità relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="3f41e-130">Azure AD has a different set of admin roles toomanage hello directory and identity-related features.</span></span>  <span data-ttu-id="3f41e-131">Questi amministratori saranno le funzionalità di accesso toovarious nel portale di Azure hello o hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="3f41e-131">These admins will have access toovarious features in hello Azure portal or hello Azure classic portal.</span></span> <span data-ttu-id="3f41e-132">ruolo dell'amministratore di Hello determina le operazioni consentite, come creare o modificare gli utenti, assegnare ruoli amministrativi tooothers, reimpostare le password utente, gestire le licenze utente o gestire i domini.</span><span class="sxs-lookup"><span data-stu-id="3f41e-132">hello admin's role determines what they can do, like create or edit users, assign administrative roles tooothers, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="3f41e-133">Per altre informazioni sugli amministratori della directory di AD e i loro ruoli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="3f41e-134">I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.</span><span class="sxs-lookup"><span data-stu-id="3f41e-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="3f41e-135">**D: è disponibile un report che indica la scadenza delle licenze utente di Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="3f41e-136">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="3f41e-136">**A:** No.</span></span>  <span data-ttu-id="3f41e-137">Non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="3f41e-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="3f41e-138">Introduzione alla gestione ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f41e-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="3f41e-139">**D: Come si abbandona un tenant quando si viene aggiunti come collaboratore?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="3f41e-140">**R:** quando vengono aggiunti tenant dell'organizzazione tooanother come un collaboratore, è possibile utilizzare hello "tenant selezione" in tooswitch destra superiore hello tra tenant.</span><span class="sxs-lookup"><span data-stu-id="3f41e-140">**A:** When you are added tooanother organization's tenant as a collaborator, you can use hello "tenant switcher" in hello upper right tooswitch between tenants.</span></span>  <span data-ttu-id="3f41e-141">Attualmente, non vi è alcun hello di tooleave modo si invitano organizzazione e Microsoft sta lavorando tale funzionalità.</span><span class="sxs-lookup"><span data-stu-id="3f41e-141">Currently, there is no way tooleave hello inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="3f41e-142">Fino a quando questa funzionalità è disponibile, è possibile chiedere hello si invitano tooremove organizzazione dal tenant.</span><span class="sxs-lookup"><span data-stu-id="3f41e-142">Until this feature is available, you can ask hello inviting organization tooremove you from their tenant.</span></span>
- - -
<span data-ttu-id="3f41e-143">**D: come è possibile collegare il tooAzure di directory Active Directory locale?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-143">**Q: How can I connect my on-premises directory tooAzure AD?**</span></span>

<span data-ttu-id="3f41e-144">**R:** è possibile connettersi il tooAzure di directory Active Directory locale con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3f41e-144">**A:** You can connect your on-premises directory tooAzure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="3f41e-145">Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="3f41e-146">**D: Come si configura l'accesso Single Sign-On tra la directory locale e le applicazioni cloud?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="3f41e-147">**R:** è solo necessario tooset di single sign-on (SSO) tra la directory locale e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f41e-147">**A:** You only need tooset up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="3f41e-148">Purché si accedere alle applicazioni cloud tramite Azure AD, servizio hello unità automaticamente gli utenti toocorrectly l'autenticazione con le credenziali locali.</span><span class="sxs-lookup"><span data-stu-id="3f41e-148">As long as you access your cloud applications through Azure AD, hello service automatically drives your users toocorrectly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="3f41e-149">L'implementazione dell'accesso Single Sign-On dall'ambiente locale può essere ottenuta facilmente con soluzioni di federazione come Active Directory Federation Services (AD FS) o con la configurazione della sincronizzazione dell'hash delle password. È possibile distribuire facilmente entrambe le opzioni utilizzando Configurazione guidata di hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3f41e-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using hello Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="3f41e-150">Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="3f41e-151">**D: Azure AD offre un portale self-service per gli utenti dell'organizzazione?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="3f41e-152">**R:** Sì, Azure AD fornisce hello [Pannello di accesso AD Azure](http://myapps.microsoft.com) per l'accesso alle applicazioni e utente self-service.</span><span class="sxs-lookup"><span data-stu-id="3f41e-152">**A:** Yes, Azure AD provides you with hello [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="3f41e-153">Nel caso di un cliente di Office 365, sono disponibili numerosi hello stesse funzionalità nel portale di Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="3f41e-153">If you are an Office 365 customer, you can find many of hello same capabilities in hello Office 365 portal.</span></span>

<span data-ttu-id="3f41e-154">Per ulteriori informazioni, vedere [introduzione toohello Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-154">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="3f41e-155">**D: Azure AD semplifica la gestione dell'infrastruttura locale?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="3f41e-156">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="3f41e-156">**A:** Yes.</span></span> <span data-ttu-id="3f41e-157">edizione di Azure AD Premium Hello fornisce con Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="3f41e-157">hello Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="3f41e-158">Azure AD Connect Health consente di monitorare e approfondire la propria identità locale hello e l'infrastruttura servizi di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="3f41e-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and hello synchronization services.</span></span>  

<span data-ttu-id="3f41e-159">Per ulteriori informazioni, vedere [monitorare l'identità dell'infrastruttura e sincronizzazione servizi locali nel cloud hello](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="3f41e-160">Gestione delle password</span><span class="sxs-lookup"><span data-stu-id="3f41e-160">Password management</span></span>
<span data-ttu-id="3f41e-161">**D: È possibile usare il writeback delle password di Azure AD senza la sincronizzazione password? (In questo scenario, è possibile toouse Azure AD la reimpostazione della password self-service (SSPR) con password writeback e non archiviare password nel cloud hello?)**</span><span class="sxs-lookup"><span data-stu-id="3f41e-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible toouse Azure AD self-service password reset (SSPR) with password write-back and not store passwords in hello cloud?)**</span></span>

<span data-ttu-id="3f41e-162">**R:** non è necessario toosynchronize l'Active Directory password tooAzure AD tooenable writeback.</span><span class="sxs-lookup"><span data-stu-id="3f41e-162">**A:** You do not need toosynchronize your Active Directory passwords tooAzure AD tooenable write-back.</span></span> <span data-ttu-id="3f41e-163">In un ambiente federato, Azure AD single sign-on (SSO) si basa su hello locale directory tooauthenticate hello di utenti.</span><span class="sxs-lookup"><span data-stu-id="3f41e-163">In a federated environment, Azure AD single sign-on (SSO) relies on hello on-premises directory tooauthenticate hello user.</span></span> <span data-ttu-id="3f41e-164">Questo scenario non richiede hello locale password toobe registrato in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f41e-164">This scenario does not require hello on-premises password toobe tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="3f41e-165">**D: come tempo occorre per toobe una password riscritti tooActive Directory in locale?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-165">**Q: How long does it take for a password toobe written back tooActive Directory on-premises?**</span></span>

<span data-ttu-id="3f41e-166">**R:** Il writeback delle password viene eseguito in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="3f41e-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="3f41e-167">Per altre informazioni, vedere [Introduzione alla gestione delle password](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="3f41e-168">**D: È possibile usare il writeback delle password con password gestite da un amministratore?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="3f41e-169">**R:** Sì, se si dispone di writeback delle password abilitato, le operazioni di password hello eseguite da un amministratore vengono scritte tooyour nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="3f41e-169">**A:** Yes, if you have password write-back enabled, hello password operations performed by an admin are written back tooyour on-premises environment.</span></span>  

<span data-ttu-id="3f41e-170">Per ulteriori domande toopassword, vedere [domande frequenti sulla gestione delle Password](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-170">For more answers toopassword-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="3f41e-171">**D: che cosa può fare se non si ricorda password Office 365 o Azure Active Directory esistente durante il tentativo di toochange password?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying toochange my password?**</span></span>

<span data-ttu-id="3f41e-172">**R:** In situazioni di questo tipo è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="3f41e-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="3f41e-173">Usare la reimpostazione password self-service (SSPR), se disponibile.</span><span class="sxs-lookup"><span data-stu-id="3f41e-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="3f41e-174">La disponibilità della funzione SSPR dipende dalla sua configurazione.</span><span class="sxs-lookup"><span data-stu-id="3f41e-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="3f41e-175">Per ulteriori informazioni, vedere [come password hello reimpostare lavoro portale](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-175">For more information, see [How does hello password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="3f41e-176">Per gli utenti di Office 365, l'amministratore può reimpostare password hello utilizzando i passaggi descritti nella procedura hello [reimpostare le password utente](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="3f41e-176">For Office 365 users, your admin can reset hello password by using hello steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="3f41e-177">Per gli account di Azure AD, gli amministratori possono reimpostare le password utilizzando uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="3f41e-177">For Azure AD accounts, admins can reset passwords by using one of hello following:</span></span>

- [<span data-ttu-id="3f41e-178">Reimpostare gli account nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3f41e-178">Reset accounts in hello Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="3f41e-179">Reimpostare gli account nel portale classico hello</span><span class="sxs-lookup"><span data-stu-id="3f41e-179">Reset accounts in hello classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="3f41e-180">Tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f41e-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="3f41e-181">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="3f41e-181">Security</span></span>
<span data-ttu-id="3f41e-182">**D: Gli account vengono bloccati dopo un numero specifico di tentativi non riusciti o la strategia usata è più sofisticata?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="3f41e-183">Viene usato un account di toolock strategia più sofisticate.</span><span class="sxs-lookup"><span data-stu-id="3f41e-183">We use a more sophisticated strategy toolock accounts.</span></span>  <span data-ttu-id="3f41e-184">Si basa sulla hello IP della richiesta di hello e password hello immesse.</span><span class="sxs-lookup"><span data-stu-id="3f41e-184">This is based on hello IP of hello request and hello passwords entered.</span></span> <span data-ttu-id="3f41e-185">durata Hello del blocco di hello aumenta anche in base alle probabilità hello è costituito da un attacco.</span><span class="sxs-lookup"><span data-stu-id="3f41e-185">hello duration of hello lockout also increases based on hello likelihood that it is an attack.</span></span>  

<span data-ttu-id="3f41e-186">**D: determinati password (comune) rifiutate con hello messaggi 'questa password è stata utilizzata toomany volte', questo riferimento toopasswords utilizzato in active directory corrente hello?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-186">**Q:  Certain (common) passwords get rejected with hello messages ‘this password has been used toomany times’, does this refer toopasswords used in hello current active directory?**</span></span></br>
<span data-ttu-id="3f41e-187">Si riferisce toopasswords globale comuni, ad esempio tutte le varianti di "Password" e "123456".</span><span class="sxs-lookup"><span data-stu-id="3f41e-187">This refers toopasswords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="3f41e-188">**D: Una richiesta di accesso proveniente da origini sospette (botnet, endpoint tor) sarà bloccata in un tenant B2C o è necessario un tenant della Basic Edition o della Premium Edition?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="3f41e-189">Esiste un gateway che filtra le richieste e fornisce un livello di protezione da botnet e che viene applicato per tutti i tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="3f41e-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="3f41e-190">Accesso all'applicazione</span><span class="sxs-lookup"><span data-stu-id="3f41e-190">Application access</span></span>
<span data-ttu-id="3f41e-191">**D: Dove si può trovare un elenco di applicazioni preintegrate con Azure AD e delle rispettive funzionalità?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="3f41e-192">**D:** Azure AD include più di 2.600 applicazioni preintegrate di Microsoft, application service provider o partner.</span><span class="sxs-lookup"><span data-stu-id="3f41e-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="3f41e-193">Tutte le applicazioni preintegrate supportano l'accesso Single Sign-On,</span><span class="sxs-lookup"><span data-stu-id="3f41e-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="3f41e-194">SSO consente di utilizzare le credenziali aziendali di tooaccess le app.</span><span class="sxs-lookup"><span data-stu-id="3f41e-194">SSO lets you use your organizational credentials tooaccess your apps.</span></span> <span data-ttu-id="3f41e-195">Alcune applicazioni hello supportano anche automatizzati provisioning e deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="3f41e-195">Some of hello applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="3f41e-196">Per un elenco completo di applicazioni preintegrate hello, vedere hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="3f41e-196">For a complete list of hello pre-integrated applications, see hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="3f41e-197">**D: cosa accade se hello applicazione che è necessario non è in marketplace di Azure AD hello?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-197">**Q: What if hello application I need is not in hello Azure AD marketplace?**</span></span>

<span data-ttu-id="3f41e-198">**R:** Azure AD Premium consente di aggiungere e configurare qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="3f41e-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="3f41e-199">In base alle funzionalità dell'applicazione e alle preferenze dell'utente, è possibile configurare l'accesso Single Sign-On e il provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="3f41e-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="3f41e-200">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="3f41e-200">For more information, see:</span></span>

* [<span data-ttu-id="3f41e-201">Configurazione di single sign-on tooapplications non presenti nella raccolta di hello Azure Active Directory dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="3f41e-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="3f41e-202">Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="3f41e-202">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="3f41e-203">**D: come utenti Accedi tooapplications grazie ad Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-203">**Q: How do users sign in tooapplications by using Azure AD?**</span></span>

<span data-ttu-id="3f41e-204">**R:** Azure AD sono disponibili diversi metodi per gli utenti tooview e accedere alle applicazioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3f41e-204">**A:** Azure AD provides several ways for users tooview and access their applications, such as:</span></span>

* <span data-ttu-id="3f41e-205">Pannello di accesso Hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f41e-205">hello Azure AD access panel</span></span>
* <span data-ttu-id="3f41e-206">avvio applicazione Hello Office 365</span><span class="sxs-lookup"><span data-stu-id="3f41e-206">hello Office 365 application launcher</span></span>
* <span data-ttu-id="3f41e-207">App toofederated accesso diretto</span><span class="sxs-lookup"><span data-stu-id="3f41e-207">Direct sign-in toofederated apps</span></span>
* <span data-ttu-id="3f41e-208">Toofederated di collegamenti diretti, basato su password, o le app di esistenti</span><span class="sxs-lookup"><span data-stu-id="3f41e-208">Deep links toofederated, password-based, or existing apps</span></span>

<span data-ttu-id="3f41e-209">Per ulteriori informazioni, vedere [integrato di distribuzione di Azure AD applicazioni toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="3f41e-209">For more information, see [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="3f41e-210">**D: quali sono i modi hello Azure AD consente l'autenticazione e single sign-on tooapplications?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-210">**Q: What are hello different ways Azure AD enables authentication and single sign-on tooapplications?**</span></span>

<span data-ttu-id="3f41e-211">**R:** Azure AD supporta molti protocolli standardizzati per l'autenticazione e l'autorizzazione, ad esempio SAML 2.0, OpenID Connect, OAuth 2.0 e WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="3f41e-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="3f41e-212">Azure AD supporta anche funzionalità relative all'insieme di credenziali delle password e all'accesso automatico per le app che supportano solo l'autenticazione basata su form.</span><span class="sxs-lookup"><span data-stu-id="3f41e-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="3f41e-213">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="3f41e-213">For more information, see:</span></span>

* [<span data-ttu-id="3f41e-214">Scenari di autenticazione per Azure AD</span><span class="sxs-lookup"><span data-stu-id="3f41e-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="3f41e-215">Protocolli di autenticazione di Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f41e-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="3f41e-216">Come funziona Single Sign-On con Azure Active Directory (PHP)?</span><span class="sxs-lookup"><span data-stu-id="3f41e-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="3f41e-217">**D: È possibile aggiungere applicazioni in esecuzione in locale?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="3f41e-218">**R:** Proxy dell'applicazione Azure AD offre un accesso facile e sicuro applicazioni web locali tooon in cui si scelgono.</span><span class="sxs-lookup"><span data-stu-id="3f41e-218">**A:** Azure AD Application Proxy provides you with easy and secure access tooon-premises web applications that you choose.</span></span> <span data-ttu-id="3f41e-219">È possibile accedere a queste applicazioni in hello allo stesso modo di accedere il software come un servizio (SaaS) app di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3f41e-219">You can access these applications in hello same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="3f41e-220">Non è necessario per una VPN o toochange l'infrastruttura di rete.</span><span class="sxs-lookup"><span data-stu-id="3f41e-220">There is no need for a VPN or toochange your network infrastructure.</span></span>  

<span data-ttu-id="3f41e-221">Per ulteriori informazioni, vedere [come tooprovide proteggere l'accesso remoto applicazioni locali tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-221">For more information, see [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="3f41e-222">**D: Come si richiede l'autenticazione Multi-Factor Authentication per gli utenti che accedono a un'applicazione specifica?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="3f41e-223">**R:** L'accesso condizionale di Azure AD consente di assegnare criteri di accesso univoci per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="3f41e-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="3f41e-224">Nei criteri, è possibile richiedere sempre l'autenticazione a più fattori, oppure quando gli utenti non sono connessi toohello rete locale.</span><span class="sxs-lookup"><span data-stu-id="3f41e-224">In your policy, you can require multi-factor authentication always, or when users are not connected toohello local network.</span></span>  

<span data-ttu-id="3f41e-225">Per ulteriori informazioni, vedere [protezione dell'accesso tooOffice 365 e altre App connessa tooAzure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-225">For more information, see [Securing access tooOffice 365 and other apps connected tooAzure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="3f41e-226">**D: Che cos'è il provisioning utenti automatizzato per le app SaaS?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="3f41e-227">**R:** creazione hello tooautomate usano Azure AD, la manutenzione e la rimozione delle identità utente in molte applicazioni SaaS di cloud più diffusi.</span><span class="sxs-lookup"><span data-stu-id="3f41e-227">**A:** Use Azure AD tooautomate hello creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="3f41e-228">Per ulteriori informazioni, vedere [automatizzare provisioning e deprovisioning tooSaaS applicazioni con Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="3f41e-228">For more information, see [Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="3f41e-229">**D: È possibile configurare una connessione LDAP sicura con Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="3f41e-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="3f41e-230">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="3f41e-230">**A:**  No.</span></span> <span data-ttu-id="3f41e-231">Azure AD non supporta il protocollo LDAP hello.</span><span class="sxs-lookup"><span data-stu-id="3f41e-231">Azure AD does not support hello LDAP protocol.</span></span>
