---
title: 'Azure AD Connect: Selezionare il tipo di installazione | Documentazione Microsoft'
description: Questo argomento descrive come selezionare il tipo di installazione da usare per Azure AD Connect
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="ec157-103">Selezionare il tipo di installazione da usare per Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="ec157-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="ec157-104">Per Azure AD Connect sono disponibili due tipi di installazione: rapida e personalizzata.</span><span class="sxs-lookup"><span data-stu-id="ec157-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="ec157-105">Questo argomento consente di decidere quale opzione usare durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="ec157-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="ec157-106">Express</span><span class="sxs-lookup"><span data-stu-id="ec157-106">Express</span></span>
<span data-ttu-id="ec157-107">L'installazione rapida è l'opzione più comune e viene usata per circa il 90% di tutte le nuove installazioni.</span><span class="sxs-lookup"><span data-stu-id="ec157-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="ec157-108">È stata progettata per fornire una configurazione adatta per la maggior parte degli scenari dei clienti.</span><span class="sxs-lookup"><span data-stu-id="ec157-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="ec157-109">Richiede:</span><span class="sxs-lookup"><span data-stu-id="ec157-109">It assumes:</span></span>

- <span data-ttu-id="ec157-110">Una singola foresta Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="ec157-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="ec157-111">Un account di amministratore dell'organizzazione che può essere usato per l'installazione.</span><span class="sxs-lookup"><span data-stu-id="ec157-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="ec157-112">Meno di 100.000 oggetti nell'istanza locale di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec157-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="ec157-113">Offre:</span><span class="sxs-lookup"><span data-stu-id="ec157-113">You get:</span></span>

- <span data-ttu-id="ec157-114">[Sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) da locale ad Azure AD per l'accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="ec157-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="ec157-115">Una configurazione che consente di sincronizzare [utenti, gruppi, contatti e computer Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="ec157-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="ec157-116">Sincronizzazione di tutti gli oggetti idonei in tutti i domini e tutte le unità organizzative.</span><span class="sxs-lookup"><span data-stu-id="ec157-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="ec157-117">[Aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) abilitato per garantire che venga usata sempre la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="ec157-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="ec157-118">Casi in cui è comunque possibile usare l'installazione rapida:</span><span class="sxs-lookup"><span data-stu-id="ec157-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="ec157-119">Se non si desidera sincronizzare tutte le unità organizzative, è comunque possibile usare l'installazione rapida, deselezionando **Avviare il processo di sincronizzazione...** * nell'ultima pagina.</span><span class="sxs-lookup"><span data-stu-id="ec157-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="ec157-120">Eseguire quindi di nuovo l'Installazione guidata, modificare le unità organizzative nelle [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e abilitare la sincronizzazione pianificata.</span><span class="sxs-lookup"><span data-stu-id="ec157-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="ec157-121">Si desidera abilitare una delle funzionalità in Azure AD Premium, ad esempio il writeback delle password.</span><span class="sxs-lookup"><span data-stu-id="ec157-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="ec157-122">Completare innanzitutto l'intera procedura di installazione rapida iniziale.</span><span class="sxs-lookup"><span data-stu-id="ec157-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="ec157-123">Eseguire quindi di nuovo l'Installazione guidata e modificare le [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="ec157-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="ec157-124">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="ec157-124">Custom</span></span>
<span data-ttu-id="ec157-125">Il percorso personalizzato offre molte più opzioni rispetto a quello rapido</span><span class="sxs-lookup"><span data-stu-id="ec157-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="ec157-126">e deve essere usato in tutti i casi in cui l'organizzazione non dispone della configurazione indicata nella sezione precedente per l'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="ec157-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="ec157-127">Usare questo tipo nei seguenti casi:</span><span class="sxs-lookup"><span data-stu-id="ec157-127">Use when:</span></span>

- <span data-ttu-id="ec157-128">Non si ha accesso a un account amministratore dell'organizzazione in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec157-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="ec157-129">Si dispone di più foreste o si prevede di sincronizzare più foreste in futuro.</span><span class="sxs-lookup"><span data-stu-id="ec157-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="ec157-130">Alcuni domini nella foresta non sono raggiungibili dal server Connect.</span><span class="sxs-lookup"><span data-stu-id="ec157-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="ec157-131">Si prevede di usare la federazione o l'autenticazione pass-through per l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="ec157-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="ec157-132">Si hanno più di 100.000 oggetti ed è necessario usare un'istanza completa di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ec157-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="ec157-133">Si prevede di usare i filtri in base al gruppo oltre a quelli in base a dominio o unità organizzativa.</span><span class="sxs-lookup"><span data-stu-id="ec157-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="ec157-134">Aggiornamento da DirSync</span><span class="sxs-lookup"><span data-stu-id="ec157-134">Upgrade from DirSync</span></span>
<span data-ttu-id="ec157-135">Se si usa DirSync, seguire la procedura in [Eseguire l'aggiornamento da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) per aggiornare la configurazione esistente.</span><span class="sxs-lookup"><span data-stu-id="ec157-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="ec157-136">Sono disponibili due diverse opzioni di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="ec157-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="ec157-137">Aggiornamento sul posto, per installare Connect sullo stesso server.</span><span class="sxs-lookup"><span data-stu-id="ec157-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="ec157-138">Distribuzione parallela, per installare Connect in un nuovo server mentre il server DirSync esistente è ancora operativo.</span><span class="sxs-lookup"><span data-stu-id="ec157-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="ec157-139">Aggiornamento da Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="ec157-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="ec157-140">Se si usa Azure AD Sync, è possibile seguire la [stessa procedura](active-directory-aadconnect-upgrade-previous-version.md) usata per eseguire l'aggiornamento a una versione più recente di Connect.</span><span class="sxs-lookup"><span data-stu-id="ec157-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="ec157-141">Sono disponibili due diverse opzioni di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="ec157-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="ec157-142">Aggiornamento sul posto, per installare Connect sullo stesso server.</span><span class="sxs-lookup"><span data-stu-id="ec157-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="ec157-143">Migrazione swing, per installare Connect in un nuovo server mentre il server Azure AD Sync esistente è ancora operativo.</span><span class="sxs-lookup"><span data-stu-id="ec157-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="ec157-144">Migrazione da FIM2010 o MIM2016</span><span class="sxs-lookup"><span data-stu-id="ec157-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="ec157-145">Se si usa Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con Azure AD Connector, l'unica opzione disponibile è una migrazione.</span><span class="sxs-lookup"><span data-stu-id="ec157-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="ec157-146">Seguire la procedura descritta in [swing-migration (Migrazione Swing)](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="ec157-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="ec157-147">Durante i passaggi, sostituire tutti i riferimenti ad Azure AD Sync con FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="ec157-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec157-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ec157-148">Next steps</span></span>
<span data-ttu-id="ec157-149">In base all'opzione scelta, usare i contenuti a sinistra per trovare l'articolo con i passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="ec157-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
