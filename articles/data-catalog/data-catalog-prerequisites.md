---
title: Prerequisiti di Azure Data Catalog | Documentazione Microsoft
description: Informazioni sui prerequisiti necessari per iniziare a usare Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 3fdef7bb58a5cd5dfbe4d37d9baf9c8e392ebe42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="3d3a7-103">Prerequisiti del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="3d3a7-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="3d3a7-104">Prima di poter configurare Azure Data Catalog, sono necessarie alcune operazioni preliminari</span><span class="sxs-lookup"><span data-stu-id="3d3a7-104">You need to take care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="3d3a7-105">che però non richiedono molto tempo.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="3d3a7-106">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="3d3a7-106">Azure subscription</span></span>
<span data-ttu-id="3d3a7-107">Per configurare Data Catalog, l'utente deve essere proprietario o comproprietario di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-107">To set up Data Catalog, you must be the owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="3d3a7-108">Le sottoscrizioni di Azure consentono di organizzare l'accesso alle risorse del servizio cloud, ad esempio Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-108">Azure subscriptions help you organize access to cloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="3d3a7-109">Le sottoscrizioni consentono anche di controllare come l'utilizzo delle risorse viene segnalato, fatturato e pagato.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="3d3a7-110">Ogni sottoscrizione può avere un metodo di fatturazione e pagamento distinto e avere così sottoscrizioni e piani diversi per reparto, progetto, ufficio locale e così via.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="3d3a7-111">Ogni servizio cloud appartiene a una sottoscrizione ed è necessario che la sottoscrizione sia disponibile prima di configurare Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-111">Every cloud service belongs to a subscription, and you need to have a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="3d3a7-112">Per altre informazioni, vedere l'articolo su come [gestire gli account, le sottoscrizioni e i ruoli amministrativi](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3d3a7-112">To learn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="3d3a7-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d3a7-113">Azure Active Directory</span></span>
<span data-ttu-id="3d3a7-114">Per configurare Data Catalog, è necessario accedere con un account utente di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d3a7-114">To set up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="3d3a7-115">Azure AD è un servizio che offre semplici e pratiche funzionalità di gestione delle identità e degli accessi, sia nel cloud sia in locale.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-115">Azure AD provides an easy way for your business to manage identity and access, both in the cloud and on-premises.</span></span> <span data-ttu-id="3d3a7-116">Gli utenti possono usare un singolo account aziendale o dell'istituto di istruzione per eseguire l'accesso Single Sign-On a qualsiasi applicazione Web locale o nel cloud.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-116">Users can use a single work or school account for single sign-in to any cloud and on-premises web application.</span></span> <span data-ttu-id="3d3a7-117">Data Catalog usa Azure AD per autenticare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-117">Data Catalog uses Azure AD to authenticate sign-in.</span></span> <span data-ttu-id="3d3a7-118">Per altre informazioni, vedere [Informazioni su Azure Active Directory](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d3a7-118">To learn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3d3a7-119">Usando il [portale di Azure](http://portal.azure.com/) è possibile eseguire l'accesso con un account Microsoft personale oppure con un account aziendale o dell'istituto di istruzione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-119">By using the [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="3d3a7-120">Per configurare Data Catalog usando il portale di Azure o il [portale di Data Catalog](http://www.azuredatacatalog.com), è necessario eseguire l'accesso con un account di Azure Active Directory, non con un account personale.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-120">To set up Data Catalog by using either the Azure portal or the [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="3d3a7-121">Configurazione dei criteri di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d3a7-121">Active Directory policy configuration</span></span>
<span data-ttu-id="3d3a7-122">In alcune situazioni è possibile accedere al portale di Data Catalog, ma, quando si prova ad accedere allo strumento di registrazione dell'origine dati, viene visualizzato un messaggio di errore che impedisce l'accesso.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-122">You might encounter a situation where you can sign in to the Data Catalog portal, but when you attempt to sign in to the data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="3d3a7-123">Questo errore si verifica solo quando si è nella rete aziendale o ci si connette dall'esterno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-123">This problem behavior might occur only when you're on the company network, or it might occur only when you're connecting from outside the company network.</span></span>

<span data-ttu-id="3d3a7-124">Lo strumento di registrazione dell'origine dati usa l'autenticazione basata su form per convalidare le credenziali degli utenti in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-124">The data source registration tool uses Forms Authentication to validate your user credentials against Active Directory.</span></span> <span data-ttu-id="3d3a7-125">Per eseguire correttamente l'accesso, un amministratore di Azure Active Directory deve abilitare l'autenticazione basata su form nei criteri di autenticazione globali.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-125">To help you sign in successfully, an Active Directory administrator must enable Forms Authentication in the Global Authentication Policy.</span></span>

<span data-ttu-id="3d3a7-126">Nei criteri di autenticazione globali possono essere abilitati metodi di autenticazione separati per connessioni Intranet ed Extranet, come illustrato nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-126">In the Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in the following screenshot.</span></span> <span data-ttu-id="3d3a7-127">Se l'autenticazione basata su form non è abilitata per la rete da cui ci si connette, è possibile che si verifichino errori di accesso.</span><span class="sxs-lookup"><span data-stu-id="3d3a7-127">Sign-in errors might occur if Forms Authentication is not enabled for the network from which you're connecting.</span></span>

 ![Criteri di autenticazione globali di Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="3d3a7-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d3a7-129">Next steps</span></span>
<span data-ttu-id="3d3a7-130">Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d3a7-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
