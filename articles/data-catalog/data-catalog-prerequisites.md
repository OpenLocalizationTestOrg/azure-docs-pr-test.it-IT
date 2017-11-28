---
title: prerequisiti di catalogo dati aaaAzure | Documenti Microsoft
description: "Informazioni sui prerequisiti di hello che è necessario tooget avviato con Azure Data Catalog."
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
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a><span data-ttu-id="016a6-103">Prerequisiti del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="016a6-103">Azure Data Catalog prerequisites</span></span>

<span data-ttu-id="016a6-104">È necessario tootake cure alcuni aspetti prima di configurare Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="016a6-104">You need tootake care of a few things before you can set up Azure Data Catalog.</span></span> <span data-ttu-id="016a6-105">che però non richiedono molto tempo.</span><span class="sxs-lookup"><span data-stu-id="016a6-105">Don’t worry, this process does not take long.</span></span>

## <a name="azure-subscription"></a><span data-ttu-id="016a6-106">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="016a6-106">Azure subscription</span></span>
<span data-ttu-id="016a6-107">tooset catalogo dati, è necessario essere proprietario di hello o Comproprietario di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="016a6-107">tooset up Data Catalog, you must be hello owner or co-owner of an Azure subscription.</span></span>

<span data-ttu-id="016a6-108">Le sottoscrizioni di Azure consentono di organizzare toocloud-service di accedere alle risorse, ad esempio catalogo dati.</span><span class="sxs-lookup"><span data-stu-id="016a6-108">Azure subscriptions help you organize access toocloud-service resources such as Data Catalog.</span></span> <span data-ttu-id="016a6-109">Le sottoscrizioni consentono anche di controllare come l'utilizzo delle risorse viene segnalato, fatturato e pagato.</span><span class="sxs-lookup"><span data-stu-id="016a6-109">Subscriptions also help you control how resource usage is reported, billed, and paid for.</span></span> <span data-ttu-id="016a6-110">Ogni sottoscrizione può avere un metodo di fatturazione e pagamento distinto e avere così sottoscrizioni e piani diversi per reparto, progetto, ufficio locale e così via.</span><span class="sxs-lookup"><span data-stu-id="016a6-110">Each subscription can have a separate billing and payment setup, so you can have subscriptions and plans that vary by department, project, regional office, and so on.</span></span> <span data-ttu-id="016a6-111">Ogni servizio cloud appartiene tooa sottoscrizione ed è necessario toohave una sottoscrizione prima di impostare il catalogo dati.</span><span class="sxs-lookup"><span data-stu-id="016a6-111">Every cloud service belongs tooa subscription, and you need toohave a subscription before you set up Data Catalog.</span></span> <span data-ttu-id="016a6-112">vedere, più toolearn [gestire account, sottoscrizioni e ruoli amministrativi](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="016a6-112">toolearn more, see [Manage accounts, subscriptions, and administrative roles](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="016a6-113">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="016a6-113">Azure Active Directory</span></span>
<span data-ttu-id="016a6-114">tooset catalogo dati, è necessario essere connessi con un account utente di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="016a6-114">tooset up Data Catalog, you must be signed in with an Azure Active Directory (Azure AD) user account.</span></span>

<span data-ttu-id="016a6-115">Azure AD fornisce un modo semplice per le identità di business toomanage e l'accesso, sia nel cloud hello e locali.</span><span class="sxs-lookup"><span data-stu-id="016a6-115">Azure AD provides an easy way for your business toomanage identity and access, both in hello cloud and on-premises.</span></span> <span data-ttu-id="016a6-116">Gli utenti possono utilizzare un singolo account aziendale o dell'istituto di istruzione per il cloud tooany single sign-in e applicazione web locale.</span><span class="sxs-lookup"><span data-stu-id="016a6-116">Users can use a single work or school account for single sign-in tooany cloud and on-premises web application.</span></span> <span data-ttu-id="016a6-117">Catalogo dati utilizza Azure AD tooauthenticate Accedi.</span><span class="sxs-lookup"><span data-stu-id="016a6-117">Data Catalog uses Azure AD tooauthenticate sign-in.</span></span> <span data-ttu-id="016a6-118">vedere, più toolearn [che cos'è Azure Active Directory?](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="016a6-118">toolearn more, see [What is Azure Active Directory?](../active-directory/active-directory-whatis.md).</span></span>

> [!NOTE]
> <span data-ttu-id="016a6-119">Utilizzando hello [portale di Azure](http://portal.azure.com/), è possibile accedere con un account Microsoft personale o di Azure Active Directory di lavoro o scuola account.</span><span class="sxs-lookup"><span data-stu-id="016a6-119">By using hello [Azure portal](http://portal.azure.com/), you can sign in with either a personal Microsoft account or an Azure Active Directory work or school account.</span></span> <span data-ttu-id="016a6-120">tooset catalogo dati utilizzando sia hello portale di Azure o hello [portale catalogo dati](http://www.azuredatacatalog.com), è necessario accedere con un account di Azure Active Directory, non un account personale.</span><span class="sxs-lookup"><span data-stu-id="016a6-120">tooset up Data Catalog by using either hello Azure portal or hello [Data Catalog portal](http://www.azuredatacatalog.com), you must sign in with an Azure Active Directory account, not a personal account.</span></span>
>
>

## <a name="active-directory-policy-configuration"></a><span data-ttu-id="016a6-121">Configurazione dei criteri di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="016a6-121">Active Directory policy configuration</span></span>
<span data-ttu-id="016a6-122">Si potrebbe verificarsi una situazione in cui è possibile accedere al portale di catalogo dati toohello, ma quando si tenta di toosign nello strumento di registrazione origine dati toohello, che si verifichi un messaggio di errore che impedisce l'accesso.</span><span class="sxs-lookup"><span data-stu-id="016a6-122">You might encounter a situation where you can sign in toohello Data Catalog portal, but when you attempt toosign in toohello data source registration tool, you encounter an error message that prevents you from signing in.</span></span> <span data-ttu-id="016a6-123">Il comportamento di questo problema potrebbe verificarsi solo quando si è nella rete aziendale hello o potrebbe verificarsi solo quando si connette da una rete aziendale esterna hello.</span><span class="sxs-lookup"><span data-stu-id="016a6-123">This problem behavior might occur only when you're on hello company network, or it might occur only when you're connecting from outside hello company network.</span></span>

<span data-ttu-id="016a6-124">strumento di registrazione di origine dati Hello utilizza l'autenticazione basata su form toovalidate le credenziali dell'utente in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="016a6-124">hello data source registration tool uses Forms Authentication toovalidate your user credentials against Active Directory.</span></span> <span data-ttu-id="016a6-125">toohelp che accedi correttamente, un amministratore di Active Directory deve abilitare autenticazione basata su form in hello criteri di autenticazione globali.</span><span class="sxs-lookup"><span data-stu-id="016a6-125">toohelp you sign in successfully, an Active Directory administrator must enable Forms Authentication in hello Global Authentication Policy.</span></span>

<span data-ttu-id="016a6-126">In Criteri di autenticazione globali hello, metodi di autenticazione possono essere abilitate separatamente per la rete intranet ed extranet connessioni, come illustrato nella seguente schermata hello.</span><span class="sxs-lookup"><span data-stu-id="016a6-126">In hello Global Authentication Policy, authentication methods can be enabled separately for intranet and extranet connections, as shown in hello following screenshot.</span></span> <span data-ttu-id="016a6-127">Se l'autenticazione basata su form non è abilitato per la rete hello da cui si esegue la connessione, potrebbero verificarsi errori di accesso.</span><span class="sxs-lookup"><span data-stu-id="016a6-127">Sign-in errors might occur if Forms Authentication is not enabled for hello network from which you're connecting.</span></span>

 ![Criteri di autenticazione globali di Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a><span data-ttu-id="016a6-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="016a6-129">Next steps</span></span>
<span data-ttu-id="016a6-130">Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="016a6-130">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>
