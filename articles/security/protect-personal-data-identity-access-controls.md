---
title: "Proteggere i dati personali usando l'identità e i controlli di accesso di Azure | Microsoft Docs"
description: "Uso dell'identità e dei controlli di accesso di Azure per proteggere i dati personali"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: b43754efd207679dbe08710f44f56454a5fd20ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="ffcda-103">Azure Active Directory e Multi-Factor Authentication: proteggere i dati personali usando l'identità e i controlli di accesso</span><span class="sxs-lookup"><span data-stu-id="ffcda-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="ffcda-104">Questo articolo fornisce informazioni e procedure utili per proteggere i dati personali usando i servizi e le funzionalità di sicurezza di Azure Active Directory e Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ffcda-104">This article provides information and procedures you can use to protect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="ffcda-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="ffcda-105">Scenario</span></span>

<span data-ttu-id="ffcda-106">Un'importante compagnia di viaggi in crociera, con sede negli Stati Uniti, sta espandendo le proprie operazioni per offrire itinerari nel Mar Mediterraneo e nel Mar Baltico, nonché nelle isole britanniche.</span><span class="sxs-lookup"><span data-stu-id="ffcda-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="ffcda-107">Per supportare tale iniziativa, ha acquistato diverse linee minori con sede in Italia, Germania, Danimarca e Regno Unito.</span><span class="sxs-lookup"><span data-stu-id="ffcda-107">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span> 

<span data-ttu-id="ffcda-108">La società usa Microsoft Azure per archiviare i dati aziendali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="ffcda-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="ffcda-109">Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale,</span><span class="sxs-lookup"><span data-stu-id="ffcda-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="ffcda-110">Include inoltre informazioni sulle risorse umane di tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni.</span><span class="sxs-lookup"><span data-stu-id="ffcda-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="ffcda-111">La linea di crociere gestisce anche un database di grandi dimensioni dei membri dei programmi fedeltà e premi, che include informazioni personali per tenere traccia delle relazioni con i clienti attuali e del passato.</span><span class="sxs-lookup"><span data-stu-id="ffcda-111">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

<span data-ttu-id="ffcda-112">I dipendenti aziendali accedono alla rete dagli uffici remoti della società, mentre agenti di viaggio in tutto il mondo hanno accesso ad alcune risorse aziendali.</span><span class="sxs-lookup"><span data-stu-id="ffcda-112">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="ffcda-113">Presentazione del problema</span><span class="sxs-lookup"><span data-stu-id="ffcda-113">Problem statement</span></span>

<span data-ttu-id="ffcda-114">L'azienda deve proteggere la privacy dei dati personali dei clienti e dei dipendenti da utenti malintenzionati che cercano di usare le identità compromesse per ottenere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ffcda-114">The company must protect the privacy of customers’ and employees’ personal data from attackers seeking to use compromised identities to gain access.</span></span> <span data-ttu-id="ffcda-115">Deve anche assicurare che l'accesso ai dati personali da parte di utenti legittimi sia limitato solo a coloro che necessitano di tale accesso per svolgere le proprie mansioni.</span><span class="sxs-lookup"><span data-stu-id="ffcda-115">They also must ensure that access to personal data by legitimate users is restricted to only those who need it to do their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="ffcda-116">Obiettivo dell'azienda</span><span class="sxs-lookup"><span data-stu-id="ffcda-116">Company goal</span></span>

<span data-ttu-id="ffcda-117">L'obiettivo dell'azienda è garantire che l'accesso ai dati personali sia strettamente controllato.</span><span class="sxs-lookup"><span data-stu-id="ffcda-117">The company’s goal is to ensure that access to personal data is strictly controlled.</span></span> <span data-ttu-id="ffcda-118">È essenziale che le identità degli utenti con accesso ai dati personali siano protette da autenticazione avanzata.</span><span class="sxs-lookup"><span data-stu-id="ffcda-118">It is essential that identities of users with access to personal data be protected by strong authentication.</span></span> <span data-ttu-id="ffcda-119">È necessario applicare un criterio di [privilegi minimi] (https://it.wikipedia.org/wiki/Principio_del_privilegio_minimo) in modo che gli utenti legittimi abbiano esclusivamente il livello di accesso di cui necessitano e non oltre.</span><span class="sxs-lookup"><span data-stu-id="ffcda-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only the level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="ffcda-120">Soluzioni</span><span class="sxs-lookup"><span data-stu-id="ffcda-120">Solutions</span></span>

<span data-ttu-id="ffcda-121">Microsoft Azure offre gli strumenti di gestione di identità e accessi per consentire alle aziende di determinare chi può accedere a risorse che contengono dati personali.</span><span class="sxs-lookup"><span data-stu-id="ffcda-121">Microsoft Azure provides identity and access management tools to help companies control who has access to resources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="ffcda-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffcda-122">Azure Active Directory</span></span>

<span data-ttu-id="ffcda-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gestisce le identità e controlla l'accesso ad Azure e ad altre risorse, applicazioni e dati locali o cloud.</span><span class="sxs-lookup"><span data-stu-id="ffcda-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access to Azure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="ffcda-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) consente agli amministratori di Azure di ridurre al minimo il numero di utenti che hanno accesso a determinate informazioni, ad esempio i dati personali.</span><span class="sxs-lookup"><span data-stu-id="ffcda-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators to minimize the number of people who have access to certain information such as personal data.</span></span> <span data-ttu-id="ffcda-125">Consente di individuare, limitare e monitorare le identità con privilegi e il loro accesso alle risorse e di assegnare diritti amministrativi temporanei Just-In-Time (JIT) agli utenti idonei.</span><span class="sxs-lookup"><span data-stu-id="ffcda-125">It enables them to discover, restrict, and monitor privileged identities and their access to resources, and to assign temporary, Just-In-Time (JIT) administrative rights to eligible users.</span></span> <span data-ttu-id="ffcda-126">Consente anche di ottenere informazioni su coloro che hanno privilegi amministrativi di AAD.</span><span class="sxs-lookup"><span data-stu-id="ffcda-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="ffcda-127">Le attività correlate all'uso di Azure Active Directory Privileged Identity Management includono:</span><span class="sxs-lookup"><span data-stu-id="ffcda-127">The activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="ffcda-128">Abilitazione di Privileged Identity Management per la directory</span><span class="sxs-lookup"><span data-stu-id="ffcda-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="ffcda-129">Uso del dashboard di amministrazione di Privileged Identity Management per visualizzare rapidamente informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="ffcda-129">Using Privileged Identity Management admin dashboard to see important information at a glance</span></span>

- <span data-ttu-id="ffcda-130">Gestione delle identità con privilegi (amministratori) tramite l'aggiunta o la rimozione di amministratori permanenti o idonei a ogni ruolo</span><span class="sxs-lookup"><span data-stu-id="ffcda-130">Managing the privileged identities (administrators) by adding or removing permanent or eligible administrators to each role</span></span>

- <span data-ttu-id="ffcda-131">Configurazione delle impostazioni di attivazione del ruolo</span><span class="sxs-lookup"><span data-stu-id="ffcda-131">Configuring the role activation settings</span></span>

- <span data-ttu-id="ffcda-132">Attivazione dei ruoli</span><span class="sxs-lookup"><span data-stu-id="ffcda-132">Activating roles</span></span>

- <span data-ttu-id="ffcda-133">Verifica dell'attività dei ruoli</span><span class="sxs-lookup"><span data-stu-id="ffcda-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="ffcda-134">Come abilitare Azure Active Directory Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ffcda-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="ffcda-135">Per iniziare a usare Privileged Identity Management per la directory, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffcda-135">To start using PIM for your directory, do the following:</span></span>

1. <span data-ttu-id="ffcda-136">Accedere al portale di Azure come amministratore globale della directory.</span><span class="sxs-lookup"><span data-stu-id="ffcda-136">Sign in to the Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="ffcda-137">Se l'organizzazione ha più directory, selezionare il proprio nome utente nell'angolo superiore destro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcda-137">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="ffcda-138">Selezionare la directory in cui si userà Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ffcda-138">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="ffcda-139">Selezionare **Altri servizi** e usare la casella di testo **Filtro** per cercare Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ffcda-139">Select **More services** and use the **Filter** textbox to search for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="ffcda-140">Selezionare **Aggiungi al dashboard** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-140">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="ffcda-141">Verrà aperta l'applicazione Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="ffcda-141">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="ffcda-142">Dopo la configurazione di Azure AD Privileged Identity Management, a ogni apertura dell'applicazione viene visualizzato il pannello di spostamento.</span><span class="sxs-lookup"><span data-stu-id="ffcda-142">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="ffcda-143">Per altre informazioni e istruzioni su come iniziare a usare Azure Active Directory Privileged Identity Management, vedere [Iniziare ad usare Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ffcda-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="ffcda-144">Controllo degli accessi in base al ruolo di Azure</span><span class="sxs-lookup"><span data-stu-id="ffcda-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="ffcda-145">Il [controllo degli accessi in base al ruolo di Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) consente agli amministratori di Azure di gestire l'accesso alle risorse di Azure, concedendo l'accesso in base al ruolo assegnato all'utente.</span><span class="sxs-lookup"><span data-stu-id="ffcda-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access to Azure resources by enabling the granting of access based on the user’s assigned role.</span></span> <span data-ttu-id="ffcda-146">È possibile separare i compiti all'interno di un team e concedere a utenti, gruppi e applicazioni solo il livello di accesso necessario per svolgere le proprie attività.</span><span class="sxs-lookup"><span data-stu-id="ffcda-146">You can segregate duties within a team and grant only the amount of access to users, groups and applications that they need to perform their jobs.</span></span>

<span data-ttu-id="ffcda-147">L'accesso in base al ruolo può essere concesso agli utenti tramite il portale di Azure, gli strumenti da riga di comando di Azure o le API di gestione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcda-147">Role-based access can be granted to users using the Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="ffcda-148">Per altre informazioni sul controllo degli accessi in base al ruolo di Azure, vedere [Introduzione al controllo degli accessi in base al ruolo nel portale di Azure](https://docs.microsoft.com/active-directory/role-based-access-control-what-is).</span><span class="sxs-lookup"><span data-stu-id="ffcda-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in the Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="ffcda-149">Come gestire il controllo degli accessi in base al ruolo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffcda-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="ffcda-150">È possibile usare i cmdlet di PowerShell per gestire il controllo degli accessi in base al ruolo di Azure, incluse le attività di gestione seguenti:</span><span class="sxs-lookup"><span data-stu-id="ffcda-150">You can use PowerShell cmdlets to manage Azure RBAC, including the following management tasks:</span></span>

- <span data-ttu-id="ffcda-151">Elenco dei ruoli</span><span class="sxs-lookup"><span data-stu-id="ffcda-151">List roles</span></span>

- <span data-ttu-id="ffcda-152">Assegnazioni di accesso</span><span class="sxs-lookup"><span data-stu-id="ffcda-152">See who has access</span></span>

- <span data-ttu-id="ffcda-153">Concedere l'accesso</span><span class="sxs-lookup"><span data-stu-id="ffcda-153">Grant access</span></span>

- <span data-ttu-id="ffcda-154">Rimuovere un accesso</span><span class="sxs-lookup"><span data-stu-id="ffcda-154">Remove access</span></span>

- <span data-ttu-id="ffcda-155">Creare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="ffcda-155">Create a custom role</span></span>

- <span data-ttu-id="ffcda-156">Ottenere le azioni per un provider di risorse</span><span class="sxs-lookup"><span data-stu-id="ffcda-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="ffcda-157">Modificare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="ffcda-157">Modify a custom role</span></span>

- <span data-ttu-id="ffcda-158">Eliminare un ruolo personalizzato</span><span class="sxs-lookup"><span data-stu-id="ffcda-158">Delete a custom role</span></span>

- <span data-ttu-id="ffcda-159">Elencare ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="ffcda-159">List custom roles</span></span>

<span data-ttu-id="ffcda-160">Per istruzioni su come gestire il controllo degli accessi in base al ruolo di Azure con PowerShell, vedere [Gestire il controllo degli accessi in base al ruolo con Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="ffcda-160">For instructions on how to manage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="ffcda-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ffcda-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="ffcda-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/), o MFA, è una soluzione per la verifica in due passaggi che consente di proteggere l'accesso ai dati e alle applicazioni, garantendo al tempo stesso agli utenti una procedura di accesso semplice.</span><span class="sxs-lookup"><span data-stu-id="ffcda-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access to data and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ffcda-163">Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="ffcda-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="ffcda-164">Per distribuire Multi-Factor Authentication nel cloud di Azure, è prima necessario abilitare il servizio e quindi attivare la verifica in due passaggi per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="ffcda-164">To deploy MFA in the Azure cloud, you need to first enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-to-use-mfa"></a><span data-ttu-id="ffcda-165">Come abilitare Azure per l'uso di Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ffcda-165">How do I enable Azure to use MFA?</span></span>

<span data-ttu-id="ffcda-166">Se gli utenti hanno licenze che comprendono Azure Multi-Factor Authentication, non è necessario eseguire operazioni per attivare Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="ffcda-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="ffcda-167">In caso contrario sarà necessario creare un provider di Multi-Factor Authentication nella directory.</span><span class="sxs-lookup"><span data-stu-id="ffcda-167">If not, you need to create a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="ffcda-168">A questo scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffcda-168">To do this, follow these steps:</span></span>

1. <span data-ttu-id="ffcda-169">Accedere al portale di Azure classico come amministratore e selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-169">Select **Active Directory** in the Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="ffcda-170">Selezionare **Provider di Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="ffcda-171">Selezionare **Nuovo** e quindi **Provider di Multi-Factor Authentication** in **Servizi app**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="ffcda-172">Selezionare **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="ffcda-173">Compilare il campo del nome e selezionare un modello di utilizzo, ovvero per autenticazione o per utente abilitato.</span><span class="sxs-lookup"><span data-stu-id="ffcda-173">Fill in the name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="ffcda-174">Designare una directory a cui associare il provider di Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ffcda-174">Designate a directory with which the MFA Provider is associated.</span></span>

7. <span data-ttu-id="ffcda-175">Selezionare il pulsante **Create** .</span><span class="sxs-lookup"><span data-stu-id="ffcda-175">Click the **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="ffcda-176">Per altre istruzioni su come gestire i provider di Multi-Factor Authentication, vedere [Introduzione all'uso di un provider di Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider).</span><span class="sxs-lookup"><span data-stu-id="ffcda-176">For more instructions on how to manage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="ffcda-177">Come attivare la verifica in due passaggi per gli utenti</span><span class="sxs-lookup"><span data-stu-id="ffcda-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="ffcda-178">È possibile applicare la verifica in due passaggi per tutti gli accessi o creare criteri di accesso condizionale per richiedere la verifica in due passaggi solo in presenza di condizioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="ffcda-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="ffcda-179">L'abilitazione di Azure MFA modificando gli stati utente è l'approccio tradizionalmente usato per richiedere la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="ffcda-179">Enabling Azure MFA by changing user states is the traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="ffcda-180">Tutti gli utenti abilitati devono effettuare la verifica in due passaggi ogni volta che accedono.</span><span class="sxs-lookup"><span data-stu-id="ffcda-180">All the users that you enable will have the same requirement to perform two-step verification every time they sign in.</span></span> <span data-ttu-id="ffcda-181">L'abilitazione di un utente sostituisce eventuali criteri di accesso condizionale in vigore per l'utente.</span><span class="sxs-lookup"><span data-stu-id="ffcda-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="ffcda-182">L'abilitazione di Azure MFA con criteri di accesso condizionale è un approccio più flessibile per richiedere la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="ffcda-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="ffcda-183">È possibile creare criteri di accesso condizionale da applicare sia a gruppi che a singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="ffcda-183">You can create conditional access policies that apply to groups as well as individual users.</span></span> <span data-ttu-id="ffcda-184">È possibile, ad esempio, assegnare ai gruppi ad alto rischio più restrizioni rispetto ai gruppi a basso rischio oppure richiedere la verifica in due passaggi solo per le app cloud ad alto rischio e non per quelle a basso rischio.</span><span class="sxs-lookup"><span data-stu-id="ffcda-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="ffcda-185">L'accesso condizionale è tuttavia una funzionalità a pagamento di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ffcda-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="ffcda-186">Per abilitare MFA modificando lo stato utente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffcda-186">To enable MFA by changing user state, do the following:</span></span>

1. <span data-ttu-id="ffcda-187">Accedre al portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ffcda-187">Sign in to the Azure portal as an administrator.</span></span>
2. <span data-ttu-id="ffcda-188">Passare ad **Azure Active Directory \> Utenti e gruppi \> Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-188">Go to **Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="ffcda-189">Selezionare **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="ffcda-190">Trovare l'utente che si vuole abilitare per Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="ffcda-190">Find the user that you want to enable for Azure MFA.</span></span> <span data-ttu-id="ffcda-191">Potrebbe essere necessario modificare la visualizzazione nella parte superiore.</span><span class="sxs-lookup"><span data-stu-id="ffcda-191">You may need to change the view at the top.</span></span>
5. <span data-ttu-id="ffcda-192">Selezionare la casella accanto al nome dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ffcda-192">Check the box next to the user’s name.</span></span>
6. <span data-ttu-id="ffcda-193">A destra scegliere **Abilita** sotto Azioni rapide.</span><span class="sxs-lookup"><span data-stu-id="ffcda-193">On the right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="ffcda-194">Confermare la selezione nella finestra popup che viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="ffcda-194">Confirm your selection in the pop-up window that opens.</span></span>  <span data-ttu-id="ffcda-195">Gli utenti per i quali è stata abilitata la funzionalità Multi-Factor Authentication devono eseguire la registrazione all'accesso successivo.</span><span class="sxs-lookup"><span data-stu-id="ffcda-195">Users for whom MFA has been enabled will be asked to register the next time they sign in.</span></span>

<span data-ttu-id="ffcda-196">Per abilitare Azure MFA con criteri di accesso condizionale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ffcda-196">To enable Azure MFA with a conditional access policy, do the following:</span></span>

1. <span data-ttu-id="ffcda-197">Accedre al portale di Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="ffcda-197">Sign in to the Azure portal as an administrator.</span></span>

2. <span data-ttu-id="ffcda-198">Passare ad **Azure Active Directory \> Accesso condizionale**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-198">Go to **Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="ffcda-199">Selezionare **Nuovi criteri**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-199">Select **New policy**.</span></span>

4. <span data-ttu-id="ffcda-200">In **Assegnazioni** selezionare **Utenti e gruppi**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="ffcda-201">Usare le schede **Includi** ed **Escludi** per specificare quali utenti e i gruppi dovranno essere gestiti dai criteri.</span><span class="sxs-lookup"><span data-stu-id="ffcda-201">Use the **Include** and     **Exclude** tabs to specify which users and groups will be managed by the policy.</span></span>

5. <span data-ttu-id="ffcda-202">In **Assegnazioni** selezionare **App cloud**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="ffcda-203">Scegliere di includere **Tutte le app cloud**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-203">Choose to **include All cloud apps**.</span></span>
6.  <span data-ttu-id="ffcda-204">In **Controlli di accesso** selezionare **Concedi**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="ffcda-205">Selezionare **Richiedi autenticazione a più fattori**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="ffcda-206">Impostare **Abilita criterio** su **On** e quindi selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ffcda-206">Turn **Enable policy** to **On** and then select **Save**.</span></span>

<span data-ttu-id="ffcda-207">Per informazioni su come configurare le impostazioni di Azure MFA per definire gli avvisi di illecito, creare un bypass monouso, usare messaggi vocali personalizzati, configurare il caching, specificare indirizzi IP attendibili, creare password per le app, abilitare la memorizzazione dell'autenticazione per i dispositivi attendibili degli utenti e selezionare metodi di verifica, vedere [Configurare le impostazioni di Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next).</span><span class="sxs-lookup"><span data-stu-id="ffcda-207">For information on how to configure Azure MFA settings to set up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffcda-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ffcda-208">Next steps</span></span>

- [<span data-ttu-id="ffcda-209">Protezione dell'accesso con privilegi in Azure AD</span><span class="sxs-lookup"><span data-stu-id="ffcda-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="ffcda-210">Domande frequenti su Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ffcda-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="ffcda-211">Risoluzione dei problemi del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="ffcda-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="ffcda-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="ffcda-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
