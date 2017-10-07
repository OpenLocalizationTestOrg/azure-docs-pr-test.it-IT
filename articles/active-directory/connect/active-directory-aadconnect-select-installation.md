---
title: 'Azure AD Connect: Selezionare il tipo di installazione | Documentazione Microsoft'
description: "Questo argomento viene illustrata la modalità installazione hello tooselect digitare toouse per Azure AD Connect"
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
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="f1051-103">Selezionare quali toouse di tipo di installazione per Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f1051-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="f1051-104">Per Azure AD Connect sono disponibili due tipi di installazione: rapida e personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f1051-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="f1051-105">In questo argomento contribuisce di toodecide quale opzione toouse durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="f1051-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="f1051-106">Express</span><span class="sxs-lookup"><span data-stu-id="f1051-106">Express</span></span>
<span data-ttu-id="f1051-107">Express è l'opzione più comuni di hello e viene utilizzato circa il 90% di tutte le nuove installazioni.</span><span class="sxs-lookup"><span data-stu-id="f1051-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="f1051-108">È stato progettato tooprovide una configurazione adatta per scenari più comuni di clienti hello.</span><span class="sxs-lookup"><span data-stu-id="f1051-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="f1051-109">Richiede:</span><span class="sxs-lookup"><span data-stu-id="f1051-109">It assumes:</span></span>

- <span data-ttu-id="f1051-110">Una singola foresta Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="f1051-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="f1051-111">Si dispone di un account di amministratore dell'organizzazione che è possibile utilizzare per l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f1051-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="f1051-112">Meno di 100.000 oggetti nell'istanza locale di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1051-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="f1051-113">Offre:</span><span class="sxs-lookup"><span data-stu-id="f1051-113">You get:</span></span>

- <span data-ttu-id="f1051-114">[La sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) da on-premise tooAzure AD per single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f1051-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="f1051-115">Una configurazione che consente di sincronizzare [utenti, gruppi, contatti e computer Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="f1051-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="f1051-116">Sincronizzazione di tutti gli oggetti idonei in tutti i domini e tutte le unità organizzative.</span><span class="sxs-lookup"><span data-stu-id="f1051-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="f1051-117">[L'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è abilitato toomake è necessario utilizzare sempre hello versione più recente disponibile.</span><span class="sxs-lookup"><span data-stu-id="f1051-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="f1051-118">Casi in cui è comunque possibile usare l'installazione rapida:</span><span class="sxs-lookup"><span data-stu-id="f1051-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="f1051-119">Se non si desidera toosynchronize tutte le unità organizzative, è possibile comunque utilizzare Express e sull'ultima pagina hello, deselezionare **avviare il processo di sincronizzazione hello...** *.</span><span class="sxs-lookup"><span data-stu-id="f1051-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="f1051-120">Quindi eseguire di nuovo l'installazione guidata di hello e modificare le unità organizzative hello [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) e attivare la sincronizzazione pianificata.</span><span class="sxs-lookup"><span data-stu-id="f1051-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="f1051-121">Si desidera tooenable una delle funzionalità di hello in Azure AD Premium, ad esempio il writeback delle Password.</span><span class="sxs-lookup"><span data-stu-id="f1051-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="f1051-122">Vengono prima sottoposti installazione iniziale hello tooget express completata.</span><span class="sxs-lookup"><span data-stu-id="f1051-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="f1051-123">Quindi eseguire di nuovo l'installazione guidata di hello e modificare hello [opzioni di configurazione](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="f1051-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="f1051-124">Personalizzate</span><span class="sxs-lookup"><span data-stu-id="f1051-124">Custom</span></span>
<span data-ttu-id="f1051-125">percorso personalizzato Hello consente molte più opzioni rispetto alla versione express.</span><span class="sxs-lookup"><span data-stu-id="f1051-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="f1051-126">Deve essere utilizzata in tutti i casi in cui configurazione hello descritta nella sezione precedente per le edizioni express non è rappresentativo dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="f1051-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="f1051-127">Usare questo tipo nei seguenti casi:</span><span class="sxs-lookup"><span data-stu-id="f1051-127">Use when:</span></span>

- <span data-ttu-id="f1051-128">Account di accesso tooan enterprise admin non è in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f1051-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="f1051-129">Si dispone di più di una foresta o toosynchronize si prevede più di una foresta in hello future.</span><span class="sxs-lookup"><span data-stu-id="f1051-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="f1051-130">Sono presenti domini della foresta non è raggiungibile dal server di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="f1051-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="f1051-131">Si prevede di federazione toouse o autenticazione pass-through per l'accesso utente.</span><span class="sxs-lookup"><span data-stu-id="f1051-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="f1051-132">Si dispone di più di 100.000 oggetti ed è necessario toouse una versione completa di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1051-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="f1051-133">Si prevede di filtraggio basato su un gruppo di toouse e non solo dominio o il filtro basato su unità Organizzativa.</span><span class="sxs-lookup"><span data-stu-id="f1051-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="f1051-134">Aggiornamento da DirSync</span><span class="sxs-lookup"><span data-stu-id="f1051-134">Upgrade from DirSync</span></span>
<span data-ttu-id="f1051-135">Se si utilizza DirSync, quindi seguire hello [l'aggiornamento da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade la configurazione esistente.</span><span class="sxs-lookup"><span data-stu-id="f1051-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="f1051-136">Sono disponibili due diverse opzioni di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="f1051-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="f1051-137">Connettersi tooinstall aggiornamento sul posto in hello stesso server.</span><span class="sxs-lookup"><span data-stu-id="f1051-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="f1051-138">Parallela distribuzione tooinstall Connect in un nuovo server mentre il server DirSync esistente di hello è ancora operativo.</span><span class="sxs-lookup"><span data-stu-id="f1051-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="f1051-139">Aggiornamento da Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="f1051-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="f1051-140">Se si utilizza Azure AD Sync, quindi è possibile seguire hello [stessi passaggi](active-directory-aadconnect-upgrade-previous-version.md) come quando esegue l'aggiornamento da una connessione versione tooa più recente.</span><span class="sxs-lookup"><span data-stu-id="f1051-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="f1051-141">Sono disponibili due diverse opzioni di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="f1051-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="f1051-142">Connettersi tooinstall aggiornamento sul posto in hello stesso server.</span><span class="sxs-lookup"><span data-stu-id="f1051-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="f1051-143">Migrazione di attività tooinstall Connect in un nuovo server mentre il server di Azure AD Sync esistente hello è ancora operativo.</span><span class="sxs-lookup"><span data-stu-id="f1051-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="f1051-144">Migrazione da FIM2010 o MIM2016</span><span class="sxs-lookup"><span data-stu-id="f1051-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="f1051-145">Se si usano attualmente Forefront Identity Manager 2010 o Microsoft Identity Manager 2016 con hello connettore Azure AD, l'unica possibilità è una migrazione.</span><span class="sxs-lookup"><span data-stu-id="f1051-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="f1051-146">Seguire i passaggi di hello descritti in [apertura migrazione](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="f1051-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="f1051-147">Nei passaggi hello, sostituire tutti i riferimenti di Azure AD Sync con FIM2010/MIM2016.</span><span class="sxs-lookup"><span data-stu-id="f1051-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1051-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1051-148">Next steps</span></span>
<span data-ttu-id="f1051-149">A seconda opzione hello selezionato toouse, utilizzare la tabella hello di toofind sinistro toohello contenuto dell'articolo con hello passaggi dettagliati.</span><span class="sxs-lookup"><span data-stu-id="f1051-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
