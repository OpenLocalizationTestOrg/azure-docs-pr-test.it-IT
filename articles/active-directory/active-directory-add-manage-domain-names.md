---
title: Gestione dei nomi di dominio personalizzati in Azure Active Directory | Microsoft Docs
description: Concetti relativi alla gestione e procedure dettagliate per gestire un dominio personalizzato in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="1e463-103">Gestione dei nomi di dominio personalizzati in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e463-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="1e463-104">Un nome di dominio può essere un identificatore importante per molte risorse della directory, come parte di:</span><span class="sxs-lookup"><span data-stu-id="1e463-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="1e463-105">Un nome utente o un indirizzo di posta elettronica di un utente</span><span class="sxs-lookup"><span data-stu-id="1e463-105">A user name or email address for a user</span></span>
* <span data-ttu-id="1e463-106">L'indirizzo di un gruppo</span><span class="sxs-lookup"><span data-stu-id="1e463-106">The address for a group</span></span>
* <span data-ttu-id="1e463-107">L'URI ID app di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1e463-107">The app ID URI for an application</span></span>

<span data-ttu-id="1e463-108">Una risorsa in Azure Active Directory (Azure AD) può includere un nome di dominio già verificato come di proprietà della directory contenente il servizio.</span><span class="sxs-lookup"><span data-stu-id="1e463-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="1e463-109">Solo un amministratore globale può eseguire attività di gestione del dominio in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e463-110">Microsoft consiglia di gestire Azure AD usando l'[interfaccia di amministrazione di Azure AD](https://aad.portal.azure.com) nel portale di Azure invece di usare il portale di Azure classico citato nel presente articolo.</span><span class="sxs-lookup"><span data-stu-id="1e463-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="1e463-111">Per informazioni su come gestire i nomi di dominio nell'interfaccia di amministrazione di Azure AD, vedere [Gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e463-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="1e463-112">Impostare il nome di dominio primario per la directory di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e463-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="1e463-113">Quando viene creata la directory, il nome di dominio iniziale, ad esempio 'contoso.onmicrosoft.com', è anche il nome di dominio primario per la directory.</span><span class="sxs-lookup"><span data-stu-id="1e463-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="1e463-114">Il dominio primario è il nome di dominio predefinito per un nuovo utente quando viene creato nel [portale di Azure classico](https://manage.windowsazure.com/)o in altri portali, ad esempio il portale dell'amministratore di Office 365.</span><span class="sxs-lookup"><span data-stu-id="1e463-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="1e463-115">Questo contribuisce a semplificare il processo di creazione dei nuovi utenti per gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="1e463-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="1e463-116">Per cambiare il nome di dominio primario per la directory:</span><span class="sxs-lookup"><span data-stu-id="1e463-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="1e463-117">Accedere al [portale di Azure classico](https://manage.windowsazure.com/) con un account utente amministratore globale per la directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="1e463-118">Selezionare **Active Directory** sulla barra di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1e463-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="1e463-119">Aprire la directory.</span><span class="sxs-lookup"><span data-stu-id="1e463-119">Open your directory.</span></span>
4. <span data-ttu-id="1e463-120">Selezionare la scheda **Domini** .</span><span class="sxs-lookup"><span data-stu-id="1e463-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="1e463-121">Fare clic sul pulsante **Modifica primario** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1e463-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="1e463-122">Selezionare il dominio da impostare come nuovo dominio primario per la directory.</span><span class="sxs-lookup"><span data-stu-id="1e463-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="1e463-123">Per il nome di dominio primario per la directory è possibile impostare qualsiasi dominio personalizzato verificato che non sia federato.</span><span class="sxs-lookup"><span data-stu-id="1e463-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="1e463-124">La modifica del dominio primario per la directory non comporta la modifica dei nomi utente per gli utenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="1e463-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="1e463-125">Aggiungere nomi di dominio personalizzati alla directory di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e463-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="1e463-126">È possibile aggiungere fino a 900 nomi di dominio personalizzati a ogni directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="1e463-127">Per [aggiungere altri nomi di dominio personalizzati](active-directory-add-domain.md) è sufficiente seguire la stessa procedura usata per aggiungere il primo nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1e463-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="1e463-128">Aggiungere sottodomini di un dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="1e463-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="1e463-129">Per aggiungere un nome di dominio di terzo livello, ad esempio 'europe.contoso.com' alla directory, è prima necessario aggiungere e verificare il dominio di secondo livello, ovvero contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1e463-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="1e463-130">Il sottodominio verrà automaticamente verificato da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="1e463-131">Per ottenere la conferma dell'avvenuta verifica del dominio appena aggiunto, aggiornare la pagina del browser in cui sono visualizzati i domini della directory.</span><span class="sxs-lookup"><span data-stu-id="1e463-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="1e463-132">Cosa fare se si modifica il registrar DNS per il nome di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="1e463-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="1e463-133">Se si modifica il registrar DNS per il nome di dominio personalizzato, è possibile continuare a usare il nome di dominio personalizzato in Azure AD senza interruzioni e senza ulteriori attività di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1e463-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="1e463-134">Se si usa il nome di dominio personalizzato con Office 365, Intune o altri servizi che si basano sui nomi di dominio personalizzati in Azure AD, vedere la documentazione per tali servizi.</span><span class="sxs-lookup"><span data-stu-id="1e463-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="1e463-135">Eliminare un nome di dominio personalizzato</span><span class="sxs-lookup"><span data-stu-id="1e463-135">Delete a custom domain name</span></span>
<span data-ttu-id="1e463-136">È possibile eliminare da Azure AD i nomi di dominio personalizzati che l'organizzazione non usa più o che vuole usare in un'altra directory di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="1e463-137">Per eliminare un nome di dominio personalizzato, è prima necessario assicurarsi che nella directory non siano presenti risorse che si basano sul nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="1e463-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="1e463-138">Non è possibile eliminare un nome di dominio dalla directory nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1e463-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="1e463-139">Sono presenti utenti con un nome utente, un indirizzo di posta elettronica o un indirizzo proxy che include il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="1e463-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="1e463-140">Sono presenti gruppi con un indirizzo di posta elettronica o un indirizzo proxy che include il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="1e463-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="1e463-141">In Azure AD sono presenti applicazioni con un URI di ID app che include il nome di dominio.</span><span class="sxs-lookup"><span data-stu-id="1e463-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="1e463-142">È necessario modificare o eliminare tali risorse dalla directory di Azure AD prima di poter eliminare il nome di dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1e463-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="1e463-143">Usare API Graph o PowerShell per gestire i nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="1e463-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="1e463-144">La maggior parte delle attività di gestione per i nomi di dominio in Azure Active Directory può anche essere completata usando Microsoft PowerShell oppure a livello di codice usando l'API Graph di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e463-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="1e463-145">Uso di PowerShell per gestire i nomi di dominio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e463-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="1e463-146">Uso dell'API Graph per gestire i nomi di dominio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e463-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="1e463-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e463-147">Next steps</span></span>
* [<span data-ttu-id="1e463-148">Informazioni sui nomi di dominio in Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e463-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="1e463-149">Gestire i nomi di dominio personalizzati</span><span class="sxs-lookup"><span data-stu-id="1e463-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

