---
title: Gestione dei gruppi in Azure Active Directory | Documentazione Microsoft
description: Come creare e gestire gruppi per gestire gli utenti di Azure con Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 2cc2b63312b331a19c61cd7b59a4cac78edf32e6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="41c47-103">Gestione dei gruppi in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41c47-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41c47-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="41c47-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="41c47-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="41c47-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="41c47-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="41c47-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="41c47-107">Una delle funzionalità di gestione utente di Azure Active Directory (Azure AD) è la possibilità di creare gruppi di utenti.</span><span class="sxs-lookup"><span data-stu-id="41c47-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="41c47-108">I gruppi vengono usati per eseguire attività di gestione come l'assegnazione di licenze o autorizzazioni per diversi utenti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="41c47-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="41c47-109">È anche possibile usare i gruppi per assegnare l'autorizzazione di accesso a</span><span class="sxs-lookup"><span data-stu-id="41c47-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="41c47-110">Risorse, ad esempio oggetti nella directory.</span><span class="sxs-lookup"><span data-stu-id="41c47-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="41c47-111">Risorse esterne alla directory, ad esempio applicazioni SaaS, servizi di Azure, siti di SharePoint o risorse locali.</span><span class="sxs-lookup"><span data-stu-id="41c47-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="41c47-112">Il proprietario di una risorsa può anche assegnare l'accesso a una risorsa a un gruppo di Azure AD di proprietà di altri.</span><span class="sxs-lookup"><span data-stu-id="41c47-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="41c47-113">Questa assegnazione concede l'accesso alla risorsa ai membri di tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="41c47-114">Il proprietario del gruppo gestisce quindi l'appartenenza al gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="41c47-115">Di fatto, il proprietario della risorsa delega al proprietario del gruppo l'autorizzazione ad assegnare gli utenti alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="41c47-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41c47-116">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="41c47-116">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="41c47-117">Per informazioni su come gestire i gruppi nell'interfaccia di amministrazione di Azure AD, vedere [Creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="41c47-117">For how to manage groups in the Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="41c47-118">Come si crea un gruppo?</span><span class="sxs-lookup"><span data-stu-id="41c47-118">How do I create a group?</span></span>
<span data-ttu-id="41c47-119">A seconda dei servizi a cui l'organizzazione ha effettuato la sottoscrizione, è possibile creare un gruppo usando uno degli strumenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="41c47-119">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="41c47-120">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="41c47-120">the Azure classic portal</span></span>
* <span data-ttu-id="41c47-121">portale dell'account di Office 365</span><span class="sxs-lookup"><span data-stu-id="41c47-121">the Office 365 account portal</span></span>
* <span data-ttu-id="41c47-122">portale dell'account di Windows Intune</span><span class="sxs-lookup"><span data-stu-id="41c47-122">the Windows Intune account portal</span></span>

<span data-ttu-id="41c47-123">Questo articolo descrive l'esecuzione delle attività nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="41c47-123">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="41c47-124">Per altre informazioni sull'uso di portali non di Azure per gestire una directory di Azure AD, vedere [Amministrare la directory di Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="41c47-124">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="41c47-125">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi il nome della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="41c47-125">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="41c47-126">Selezionare la scheda **Gruppi** .</span><span class="sxs-lookup"><span data-stu-id="41c47-126">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="41c47-127">Selezionare **Aggiungi gruppo**.</span><span class="sxs-lookup"><span data-stu-id="41c47-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="41c47-128">Nella finestra **Aggiungi gruppo** specificare il nome e la descrizione di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-128">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="41c47-129">Come aggiungere o rimuovere singoli utenti in un gruppo di sicurezza?</span><span class="sxs-lookup"><span data-stu-id="41c47-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="41c47-130">**Per aggiungere un singolo utente a un gruppo**</span><span class="sxs-lookup"><span data-stu-id="41c47-130">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="41c47-131">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi il nome della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="41c47-131">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="41c47-132">Selezionare la scheda **Gruppi** .</span><span class="sxs-lookup"><span data-stu-id="41c47-132">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="41c47-133">Aprire il gruppo a cui si vogliono aggiungere membri.</span><span class="sxs-lookup"><span data-stu-id="41c47-133">Open the group to which you want to add members.</span></span> <span data-ttu-id="41c47-134">Se non è già visualizzata, aprire la scheda **Membri** del gruppo selezionato.</span><span class="sxs-lookup"><span data-stu-id="41c47-134">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="41c47-135">Selezionare **Aggiungi membri**.</span><span class="sxs-lookup"><span data-stu-id="41c47-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="41c47-136">Nella pagina **Aggiungi membri** selezionare il nome dell'utente o di un gruppo che si vuole aggiungere come membro del gruppo corrente.</span><span class="sxs-lookup"><span data-stu-id="41c47-136">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="41c47-137">Verificare che questo nome venga aggiunto al riquadro **Selezionato** .</span><span class="sxs-lookup"><span data-stu-id="41c47-137">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="41c47-138">**Per rimuovere un singolo utente da un gruppo**</span><span class="sxs-lookup"><span data-stu-id="41c47-138">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="41c47-139">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi il nome della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="41c47-139">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="41c47-140">Selezionare la scheda **Gruppi** .</span><span class="sxs-lookup"><span data-stu-id="41c47-140">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="41c47-141">Aprire il gruppo da cui si vogliono rimuovere i membri.</span><span class="sxs-lookup"><span data-stu-id="41c47-141">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="41c47-142">Selezionare la scheda **Membri** e quindi il nome del membro che si vuole rimuovere dal gruppo e infine fare clic su **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="41c47-142">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="41c47-143">Al prompt confermare che si vuole rimuovere questo membro dal gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-143">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="41c47-144">Come è possibile gestire l'appartenenza di un gruppo in modo dinamico?</span><span class="sxs-lookup"><span data-stu-id="41c47-144">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="41c47-145">In Azure AD è molto facile configurare una regola semplice per determinare quali utenti devono essere membri del gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-145">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="41c47-146">Una regola semplice è una regola che esegue un solo confronto.</span><span class="sxs-lookup"><span data-stu-id="41c47-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="41c47-147">Se un gruppo è assegnato a un'applicazione SaaS, ad esempio, è possibile configurare una regola per aggiungere gli utenti con la posizione di "Rappresentante".</span><span class="sxs-lookup"><span data-stu-id="41c47-147">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="41c47-148">Questa regola concede l'accesso all'applicazione SaaS a tutti gli utenti con tale posizione nella directory.</span><span class="sxs-lookup"><span data-stu-id="41c47-148">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="41c47-149">Quando gli attributi di un utente cambiano, il sistema valuta tutte le regole dinamiche del gruppo in una directory per verificare se la modifica degli attributi dell'utente attiverà aggiunte o rimozioni nel gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-149">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="41c47-150">Se un utente soddisfa una regola in un gruppo, viene aggiunto come membro a tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-150">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="41c47-151">Se non soddisfa più la regola di un gruppo di cui è membro, viene rimosso come membro da tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-151">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="41c47-152">È possibile configurare una regola per l'appartenenza dinamica nei gruppi di sicurezza o nei gruppi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="41c47-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="41c47-153">Le appartenenze a gruppi annidati non sono attualmente supportate per l'assegnazione alle applicazioni in base al gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-153">Nested group memberships aren't currently supported for group-based assignment to applications.</span></span>
>
> <span data-ttu-id="41c47-154">Le appartenenze dinamiche ai gruppi richiedono che venga assegnata una licenza Azure AD Premium a:</span><span class="sxs-lookup"><span data-stu-id="41c47-154">Dynamic memberships for groups require an Azure AD Premium license to be assigned to</span></span>
>
> * <span data-ttu-id="41c47-155">L'amministratore che gestisce la regola in un gruppo</span><span class="sxs-lookup"><span data-stu-id="41c47-155">The administrator who manages the rule on a group</span></span>
> * <span data-ttu-id="41c47-156">Tutti i membri del gruppo</span><span class="sxs-lookup"><span data-stu-id="41c47-156">All members of the group</span></span>
>
>

<span data-ttu-id="41c47-157">**Per abilitare l'appartenenza dinamica per un gruppo**</span><span class="sxs-lookup"><span data-stu-id="41c47-157">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="41c47-158">Nel [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**e quindi il nome della directory dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="41c47-158">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="41c47-159">Selezionare la scheda **Gruppi** e aprire il gruppo che si vuole modificare.</span><span class="sxs-lookup"><span data-stu-id="41c47-159">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="41c47-160">Selezionare la scheda **Configura** e quindi impostare **Abilita appartenenze dinamiche** su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="41c47-160">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="41c47-161">Configurare una singola regola semplice per il gruppo per controllare il funzionamento dell'appartenenza dinamica per questo gruppo.</span><span class="sxs-lookup"><span data-stu-id="41c47-161">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="41c47-162">Assicurarsi che l’opzione **Aggiungi utenti in** sia selezionata e quindi selezionare una proprietà utente dall’elenco, ad esempio department, jobTitle e così via.</span><span class="sxs-lookup"><span data-stu-id="41c47-162">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="41c47-163">Selezionare una condizione (Non uguale a, Uguale a, Non inizia con, Inizia con, Non contiene, Contiene, Non corrispondente, Corrispondente).</span><span class="sxs-lookup"><span data-stu-id="41c47-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="41c47-164">Specificare un valore di confronto per la proprietà utente selezionata.</span><span class="sxs-lookup"><span data-stu-id="41c47-164">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="41c47-165">Per informazioni su come creare regole *avanzate* (ovvero regole che possono contenere più confronti) per l'appartenenza dinamica ai gruppi, vedere [Uso di attributi per la creazione di regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="41c47-165">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="41c47-166">Informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="41c47-166">Additional information</span></span>
<span data-ttu-id="41c47-167">Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="41c47-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="41c47-168">Gestione dell'accesso alle risorse tramite i gruppi di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41c47-168">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="41c47-169">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="41c47-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="41c47-170">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41c47-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="41c47-171">Informazioni su Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41c47-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="41c47-172">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41c47-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
