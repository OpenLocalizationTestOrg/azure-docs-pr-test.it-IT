---
title: Domande frequenti su Azure Active Directory | Microsoft Docs
description: Domande frequenti su Azure Active Directory offre risposte a domande relative all'accesso ad Azure e Azure Active Directory, alla gestione delle password e all'accesso alle applicazioni.
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
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="00fdd-103">Domande frequenti su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fdd-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="00fdd-104">Azure Active Directory (Azure AD) è una soluzione IDaaS (Identity as a Service) completa che si estende a tutti gli aspetti relativi a identità, gestione degli accessi e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="00fdd-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="00fdd-105">Per altre informazioni, vedere [Informazioni su Azure Active Directory](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="00fdd-106">Accedere ad Azure e Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fdd-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="00fdd-107">**D: Perché viene visualizzato il messaggio "Non sono state trovate sottoscrizioni" quando si prova ad accedere ad Azure AD nel portale di Azure classico?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal?**</span></span>

<span data-ttu-id="00fdd-108">**A:** Per accedere al portale di Azure classico, ogni utente deve avere autorizzazioni per una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00fdd-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="00fdd-109">Se si ha una sottoscrizione di Office 365 o Azure AD a pagamento, accedere a [http://aka.ms/accessAAD](http://aka.ms/accessAAD) per un passaggio di attivazione una tantum.</span><span class="sxs-lookup"><span data-stu-id="00fdd-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="00fdd-110">In caso contrario sarà necessario attivare un [account Azure](https://azure.microsoft.com/pricing/free-trial/) gratuito o una sottoscrizione a pagamento.</span><span class="sxs-lookup"><span data-stu-id="00fdd-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="00fdd-111">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="00fdd-111">For more information, see:</span></span>

* [<span data-ttu-id="00fdd-112">Associare le sottoscrizioni di Azure ad Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fdd-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="00fdd-113">Gestire la directory per la sottoscrizione di Office 365 in Azure</span><span class="sxs-lookup"><span data-stu-id="00fdd-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="00fdd-114">**D: Qual è la relazione tra Azure AD, Office 365 e Azure?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="00fdd-115">**R:** Azure AD offre funzionalità comuni di gestione delle identità e dell'accesso in tutti i servizi Web.</span><span class="sxs-lookup"><span data-stu-id="00fdd-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="00fdd-116">Se si usa Office 365, Microsoft Azure, Intune o altri servizi, si usa già Azure AD per abilitare la gestione dell'accesso per tutti questi servizi.</span><span class="sxs-lookup"><span data-stu-id="00fdd-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="00fdd-117">Tutti gli utenti abilitati all'uso dei servizi Web sono definiti come account utente in una o più istanze di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fdd-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="00fdd-118">È possibile configurare questi account per funzionalità di Azure AD gratuite come l'accesso alle applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="00fdd-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="00fdd-119">I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.</span><span class="sxs-lookup"><span data-stu-id="00fdd-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="00fdd-120">**D: Perché è possibile accedere al portale di Azure, ma non al portale di Azure classico?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="00fdd-121">**R:** Per il portale di Azure non è necessaria una sottoscrizione valida, che è invece necessaria per il portale classico.</span><span class="sxs-lookup"><span data-stu-id="00fdd-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="00fdd-122">Senza una sottoscrizione non è possibile accedere al portale classico.</span><span class="sxs-lookup"><span data-stu-id="00fdd-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="00fdd-123">**D: Qual è la differenza tra Amministratore della sottoscrizione e Amministratore directory?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="00fdd-124">**R:** Per impostazione predefinita, al momento dell'iscrizione ad Azure all'utente viene assegnato il ruolo di Amministratore della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="00fdd-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="00fdd-125">L'amministratore della sottoscrizione può usare un account Microsoft oppure un account aziendale o dell'istituto di istruzione della directory a cui è associata la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00fdd-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="00fdd-126">Questo ruolo è autorizzato a gestire i servizi nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="00fdd-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="00fdd-127">Se altri utenti devono accedere ai servizi con la stessa sottoscrizione, è possibile aggiungerli come coamministratori.</span><span class="sxs-lookup"><span data-stu-id="00fdd-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="00fdd-128">Questo ruolo ha gli stessi privilegi di accesso dell'amministratore del servizio, ma non può modificare l'associazione di sottoscrizioni alle directory di Azure.</span><span class="sxs-lookup"><span data-stu-id="00fdd-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="00fdd-129">Per altre informazioni sugli amministratori della sottoscrizione, vedere [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) (Come aggiungere o modificare i ruoli Amministratore di Azure) e [Associare le sottoscrizioni di Azure ad Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="00fdd-130">In Azure AD è invece disponibile un set di ruoli amministrativi diverso per gestire la directory e le funzionalità relative alle identità.</span><span class="sxs-lookup"><span data-stu-id="00fdd-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="00fdd-131">Questi amministratori avranno accesso a diverse funzionalità nel portale di Azure o nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="00fdd-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="00fdd-132">Il ruolo dell'amministratore determina le operazioni consentite, ad esempio creare o modificare gli utenti, assegnare ruoli amministrativi ad altri, reimpostare le password utente, gestire le licenze utente o gestire i domini.</span><span class="sxs-lookup"><span data-stu-id="00fdd-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="00fdd-133">Per altre informazioni sugli amministratori della directory di AD e i loro ruoli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="00fdd-134">I servizi a pagamento di Azure AD, ad esempio Enterprise Mobility + Security, sono complementari ad altri servizi Web come Office 365 e Microsoft Azure, con soluzioni di gestione e di sicurezza complete di scala aziendale.</span><span class="sxs-lookup"><span data-stu-id="00fdd-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="00fdd-135">**D: è disponibile un report che indica la scadenza delle licenze utente di Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="00fdd-136">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="00fdd-136">**A:** No.</span></span>  <span data-ttu-id="00fdd-137">Non è attualmente disponibile.</span><span class="sxs-lookup"><span data-stu-id="00fdd-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="00fdd-138">Introduzione alla gestione ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fdd-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="00fdd-139">**D: Come si abbandona un tenant quando si viene aggiunti come collaboratore?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="00fdd-140">**R:** Quando si viene aggiunti a un altro tenant dell'organizzazione come collaboratore, è possibile usare la "selezione tenant" in alto a destra per passare da un tenant all'altro.</span><span class="sxs-lookup"><span data-stu-id="00fdd-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="00fdd-141">Non è attualmente possibile abbandonare l'organizzazione che ha emesso l'invito, ma Microsoft prevede di offrire questa funzionalità in futuro.</span><span class="sxs-lookup"><span data-stu-id="00fdd-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="00fdd-142">Fino a quando questa funzionalità non sarà disponibile, è possibile rivolgersi all'organizzazione che ha emesso l'invito per chiedere di essere rimossi dal tenant.</span><span class="sxs-lookup"><span data-stu-id="00fdd-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="00fdd-143">**D: Come si può connettere la directory locale ad Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="00fdd-144">**R:** È possibile connettere la directory locale ad Azure AD usando Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="00fdd-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="00fdd-145">Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="00fdd-146">**D: Come si configura l'accesso Single Sign-On tra la directory locale e le applicazioni cloud?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="00fdd-147">**R:** È sufficiente configurare l'accesso Single Sign-On (SSO) tra la directory locale e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fdd-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="00fdd-148">Se si accede alle applicazioni cloud tramite Azure AD, il servizio richiederà automaticamente agli utenti di eseguire l'autenticazione corretta con le credenziali locali.</span><span class="sxs-lookup"><span data-stu-id="00fdd-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="00fdd-149">L'implementazione dell'accesso Single Sign-On dall'ambiente locale può essere ottenuta facilmente con soluzioni di federazione come Active Directory Federation Services (AD FS) o con la configurazione della sincronizzazione dell'hash delle password. È possibile distribuire con facilità entrambe le opzioni usando la configurazione guidata di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="00fdd-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="00fdd-150">Per altre informazioni, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="00fdd-151">**D: Azure AD offre un portale self-service per gli utenti dell'organizzazione?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="00fdd-152">**R:** Sì, in Azure AD è disponibile il [pannello di accesso di Azure AD](http://myapps.microsoft.com) per l'accesso degli utenti alle funzionalità self-service e alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="00fdd-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="00fdd-153">I clienti di Office 365 possono trovare molte funzionalità analoghe nel portale di Office 365.</span><span class="sxs-lookup"><span data-stu-id="00fdd-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="00fdd-154">Per altre informazioni, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="00fdd-155">**D: Azure AD semplifica la gestione dell'infrastruttura locale?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="00fdd-156">**R:** Sì.</span><span class="sxs-lookup"><span data-stu-id="00fdd-156">**A:** Yes.</span></span> <span data-ttu-id="00fdd-157">Azure AD Premium Edition include Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="00fdd-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="00fdd-158">Azure AD Connect Health consente di monitorare e ottenere informazioni dettagliate sull'infrastruttura di gestione delle identità locale e sui servizi di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="00fdd-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="00fdd-159">Per altre informazioni, vedere [Monitorare l'infrastruttura di gestione delle identità locale e i servizi di sincronizzazione nel cloud](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="00fdd-160">Gestione delle password</span><span class="sxs-lookup"><span data-stu-id="00fdd-160">Password management</span></span>
<span data-ttu-id="00fdd-161">**D: È possibile usare il writeback delle password di Azure AD senza la sincronizzazione password? In questo scenario è possibile usare la reimpostazione della password self-service (SSPR) di Azure AD con writeback delle password senza memorizzare le password nel cloud?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="00fdd-162">**R:** Non è necessario sincronizzare le password di Active Directory con Azure AD per abilitare il writeback.</span><span class="sxs-lookup"><span data-stu-id="00fdd-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="00fdd-163">In un ambiente federato, l'accesso Single Sign-On (SSO) di Azure AD si basa sulla directory locale per autenticare l'utente.</span><span class="sxs-lookup"><span data-stu-id="00fdd-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="00fdd-164">Questo scenario non richiede la verifica della password locale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fdd-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="00fdd-165">**D: Quanto tempo è necessario per il writeback di una password nell'istanza locale di Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="00fdd-166">**R:** Il writeback delle password viene eseguito in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="00fdd-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="00fdd-167">Per altre informazioni, vedere [Introduzione alla gestione delle password](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="00fdd-168">**D: È possibile usare il writeback delle password con password gestite da un amministratore?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="00fdd-169">**R:** Sì. Se il writeback delle password è abilitato, le operazioni relative alle password eseguite da un amministratore vengono sottoposte a writeback nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="00fdd-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="00fdd-170">Per altre risposte a domande relative alle password, vedere [Domande frequenti sulla gestione delle password](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="00fdd-171">**D: Cosa si può fare se non si ricorda la password di Office 365/Azure AD esistente durante il tentativo di modificare la password?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="00fdd-172">**R:** In situazioni di questo tipo è possibile procedere in due modi.</span><span class="sxs-lookup"><span data-stu-id="00fdd-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="00fdd-173">Usare la reimpostazione password self-service (SSPR), se disponibile.</span><span class="sxs-lookup"><span data-stu-id="00fdd-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="00fdd-174">La disponibilità della funzione SSPR dipende dalla sua configurazione.</span><span class="sxs-lookup"><span data-stu-id="00fdd-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="00fdd-175">Per altre informazioni, vedere [Funzionamento del portale di reimpostazione delle password](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-175">For more information, see [How does the password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="00fdd-176">Per gli utenti di Office 365, l'amministratore può reimpostare la password seguendo la procedura descritta in [Reimpostare le password degli utenti](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="00fdd-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="00fdd-177">Per gli account Azure AD, gli amministratori possono reimpostare le password in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="00fdd-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="00fdd-178">Reimpostare gli account nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="00fdd-178">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="00fdd-179">Reimpostare gli account nel portale classico</span><span class="sxs-lookup"><span data-stu-id="00fdd-179">Reset accounts in the classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="00fdd-180">Uso di PowerShell</span><span class="sxs-lookup"><span data-stu-id="00fdd-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="00fdd-181">Sicurezza</span><span class="sxs-lookup"><span data-stu-id="00fdd-181">Security</span></span>
<span data-ttu-id="00fdd-182">**D: Gli account vengono bloccati dopo un numero specifico di tentativi non riusciti o la strategia usata è più sofisticata?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="00fdd-183">La strategia usata per bloccare gli account è più sofisticata e</span><span class="sxs-lookup"><span data-stu-id="00fdd-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="00fdd-184">si basa sull'indirizzo IP della richiesta e le password immesse.</span><span class="sxs-lookup"><span data-stu-id="00fdd-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="00fdd-185">La durata del blocco aumenta anche in base alla probabilità che sia in corso un attacco.</span><span class="sxs-lookup"><span data-stu-id="00fdd-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="00fdd-186">**Q: Alcune password (comuni) vengono rifiutate con messaggi indicanti che la password è stata usata molte volte; si fa riferimento alle password usate nell'istanza corrente di Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="00fdd-187">Si fa riferimento alle password comuni a livello globale, ad esempio tutte le varianti di "Password" e "123456".</span><span class="sxs-lookup"><span data-stu-id="00fdd-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="00fdd-188">**D: Una richiesta di accesso proveniente da origini sospette (botnet, endpoint tor) sarà bloccata in un tenant B2C o è necessario un tenant della Basic Edition o della Premium Edition?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="00fdd-189">Esiste un gateway che filtra le richieste e fornisce un livello di protezione da botnet e che viene applicato per tutti i tenant B2C.</span><span class="sxs-lookup"><span data-stu-id="00fdd-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="00fdd-190">Accesso all'applicazione</span><span class="sxs-lookup"><span data-stu-id="00fdd-190">Application access</span></span>
<span data-ttu-id="00fdd-191">**D: Dove si può trovare un elenco di applicazioni preintegrate con Azure AD e delle rispettive funzionalità?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="00fdd-192">**D:** Azure AD include più di 2.600 applicazioni preintegrate di Microsoft, application service provider o partner.</span><span class="sxs-lookup"><span data-stu-id="00fdd-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="00fdd-193">Tutte le applicazioni preintegrate supportano l'accesso Single Sign-On,</span><span class="sxs-lookup"><span data-stu-id="00fdd-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="00fdd-194">che consente di usare le credenziali aziendali per accedere alle app.</span><span class="sxs-lookup"><span data-stu-id="00fdd-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="00fdd-195">Alcune applicazioni supportano anche il provisioning e il deprovisioning automatici.</span><span class="sxs-lookup"><span data-stu-id="00fdd-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="00fdd-196">Per un elenco completo delle applicazioni preintegrate, vedere il [Marketplace di Active Directory](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="00fdd-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="00fdd-197">**D: Che cosa accade se l'applicazione cercata non è disponibile nel Marketplace di Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="00fdd-198">**R:** Azure AD Premium consente di aggiungere e configurare qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="00fdd-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="00fdd-199">In base alle funzionalità dell'applicazione e alle preferenze dell'utente, è possibile configurare l'accesso Single Sign-On e il provisioning automatico.</span><span class="sxs-lookup"><span data-stu-id="00fdd-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="00fdd-200">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="00fdd-200">For more information, see:</span></span>

* [<span data-ttu-id="00fdd-201">Configurazione del servizio Single Sign-On in applicazioni non presenti nella raccolta di applicazioni di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fdd-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="00fdd-202">Uso di SCIM per abilitare il provisioning automatico di utenti e gruppi da Azure Active Directory alle applicazioni</span><span class="sxs-lookup"><span data-stu-id="00fdd-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="00fdd-203">**D: In che modo gli utenti possono accedere alle applicazioni tramite Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="00fdd-204">**R:** Azure AD consente agli utenti di visualizzare e accedere alle applicazioni in molti modi, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="00fdd-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="00fdd-205">Pannello di accesso di Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fdd-205">The Azure AD access panel</span></span>
* <span data-ttu-id="00fdd-206">Applicazione di avvio di Office 365</span><span class="sxs-lookup"><span data-stu-id="00fdd-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="00fdd-207">Accesso diretto alle applicazioni federate</span><span class="sxs-lookup"><span data-stu-id="00fdd-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="00fdd-208">Collegamenti diretti per applicazioni federate, basate su password o esistenti</span><span class="sxs-lookup"><span data-stu-id="00fdd-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="00fdd-209">Per altre informazioni, vedere [Distribuzione di applicazioni integrate di Azure AD agli utenti](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="00fdd-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="00fdd-210">**D: Quali sono le diverse modalità usate da Azure AD per abilitare l'autenticazione e l'accesso Single Sign-On alle applicazioni?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="00fdd-211">**R:** Azure AD supporta molti protocolli standardizzati per l'autenticazione e l'autorizzazione, ad esempio SAML 2.0, OpenID Connect, OAuth 2.0 e WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="00fdd-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="00fdd-212">Azure AD supporta anche funzionalità relative all'insieme di credenziali delle password e all'accesso automatico per le app che supportano solo l'autenticazione basata su form.</span><span class="sxs-lookup"><span data-stu-id="00fdd-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="00fdd-213">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="00fdd-213">For more information, see:</span></span>

* [<span data-ttu-id="00fdd-214">Scenari di autenticazione per Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fdd-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="00fdd-215">Protocolli di autenticazione di Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fdd-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="00fdd-216">Come funziona Single Sign-On con Azure Active Directory (PHP)?</span><span class="sxs-lookup"><span data-stu-id="00fdd-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="00fdd-217">**D: È possibile aggiungere applicazioni in esecuzione in locale?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="00fdd-218">**R:** Il proxy di applicazione di Azure AD offre un accesso semplice e sicuro alle applicazioni Web locali scelte.</span><span class="sxs-lookup"><span data-stu-id="00fdd-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="00fdd-219">È possibile accedere a queste applicazioni in modo analogo all'accesso alle app SaaS in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fdd-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="00fdd-220">Non è necessario avere una VPN o modificare l'infrastruttura di rete.</span><span class="sxs-lookup"><span data-stu-id="00fdd-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="00fdd-221">Per altre informazioni, vedere [Come fornire l'accesso remoto sicuro alle applicazioni locali](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="00fdd-222">**D: Come si richiede l'autenticazione Multi-Factor Authentication per gli utenti che accedono a un'applicazione specifica?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="00fdd-223">**R:** L'accesso condizionale di Azure AD consente di assegnare criteri di accesso univoci per ogni applicazione.</span><span class="sxs-lookup"><span data-stu-id="00fdd-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="00fdd-224">Nel criterio è possibile richiedere sempre l'autenticazione Multi-Factor Authentication o solo quando gli utenti non sono connessi alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="00fdd-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="00fdd-225">Per altre informazioni, vedere [Protezione dell'accesso a Office 365 e ad altre app connesse ad Azure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="00fdd-226">**D: Che cos'è il provisioning utenti automatizzato per le app SaaS?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="00fdd-227">**R:** Azure AD consente di automatizzare la creazione, la manutenzione e la rimozione delle identità utente in molte app cloud SaaS comuni.</span><span class="sxs-lookup"><span data-stu-id="00fdd-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="00fdd-228">Per altre informazioni, vedere [Automatizzare il provisioning e il deprovisioning utenti in applicazioni SaaS con Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="00fdd-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="00fdd-229">**D: È possibile configurare una connessione LDAP sicura con Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="00fdd-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="00fdd-230">**R:** No.</span><span class="sxs-lookup"><span data-stu-id="00fdd-230">**A:**  No.</span></span> <span data-ttu-id="00fdd-231">Azure AD non supporta il protocollo LDAP.</span><span class="sxs-lookup"><span data-stu-id="00fdd-231">Azure AD does not support the LDAP protocol.</span></span>
