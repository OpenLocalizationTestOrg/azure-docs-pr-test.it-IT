---
title: Connettori nell'interfaccia utente di Synchronization Service Manager per Azure AD | Microsoft Docs
description: Comprendere la scheda Connettori in Synchronization Service Manager di Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="dd986-103">Uso dei connettori con Sync Service Manager di Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="dd986-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="dd986-105">La scheda Connettori consente di gestire tutti i sistemi a cui il motore di sincronizzazione è connesso.</span><span class="sxs-lookup"><span data-stu-id="dd986-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="dd986-106">Azioni del connettore</span><span class="sxs-lookup"><span data-stu-id="dd986-106">Connector actions</span></span>
| <span data-ttu-id="dd986-107">Azione</span><span class="sxs-lookup"><span data-stu-id="dd986-107">Action</span></span> | <span data-ttu-id="dd986-108">Commento</span><span class="sxs-lookup"><span data-stu-id="dd986-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="dd986-109">Create</span><span class="sxs-lookup"><span data-stu-id="dd986-109">Create</span></span> |<span data-ttu-id="dd986-110">Non usare.</span><span class="sxs-lookup"><span data-stu-id="dd986-110">Do not use.</span></span> <span data-ttu-id="dd986-111">Per la connessione ad altre foreste AD, usare l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="dd986-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="dd986-112">Proprietà</span><span class="sxs-lookup"><span data-stu-id="dd986-112">Properties</span></span> |<span data-ttu-id="dd986-113">Si usa per i filtri di unità organizzativa e dominio.</span><span class="sxs-lookup"><span data-stu-id="dd986-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="dd986-114">Eliminazione</span><span class="sxs-lookup"><span data-stu-id="dd986-114">Delete</span></span>](#delete) |<span data-ttu-id="dd986-115">Si usa per eliminare i dati nello spazio connettore o per eliminare la connessione a una foresta.</span><span class="sxs-lookup"><span data-stu-id="dd986-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="dd986-116">Configura profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="dd986-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="dd986-117">Fatta eccezione per i filtri di dominio, qui non è richiesta alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="dd986-118">Questa azione consente di visualizzare i profili di esecuzione già configurati.</span><span class="sxs-lookup"><span data-stu-id="dd986-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="dd986-119">Esegui</span><span class="sxs-lookup"><span data-stu-id="dd986-119">Run</span></span> |<span data-ttu-id="dd986-120">Si usa per avviare l'esecuzione occasionale di un profilo.</span><span class="sxs-lookup"><span data-stu-id="dd986-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="dd986-121">Arresto</span><span class="sxs-lookup"><span data-stu-id="dd986-121">Stop</span></span> |<span data-ttu-id="dd986-122">Arresta un connettore che sta eseguendo attualmente un profilo.</span><span class="sxs-lookup"><span data-stu-id="dd986-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="dd986-123">Esporta connettore</span><span class="sxs-lookup"><span data-stu-id="dd986-123">Export Connector</span></span> |<span data-ttu-id="dd986-124">Non usare.</span><span class="sxs-lookup"><span data-stu-id="dd986-124">Do not use.</span></span> |
| <span data-ttu-id="dd986-125">Importa connettore</span><span class="sxs-lookup"><span data-stu-id="dd986-125">Import Connector</span></span> |<span data-ttu-id="dd986-126">Non usare.</span><span class="sxs-lookup"><span data-stu-id="dd986-126">Do not use.</span></span> |
| <span data-ttu-id="dd986-127">Aggiorna connettore</span><span class="sxs-lookup"><span data-stu-id="dd986-127">Update Connector</span></span> |<span data-ttu-id="dd986-128">Non usare.</span><span class="sxs-lookup"><span data-stu-id="dd986-128">Do not use.</span></span> |
| <span data-ttu-id="dd986-129">Aggiorna schema</span><span class="sxs-lookup"><span data-stu-id="dd986-129">Refresh Schema</span></span> |<span data-ttu-id="dd986-130">Aggiorna lo schema memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="dd986-130">Refreshes the cached schema.</span></span> <span data-ttu-id="dd986-131">È preferibile usare l'opzione nell'installazione guidata perché aggiorna anche le regole di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="dd986-132">Spazio connettore di ricerca</span><span class="sxs-lookup"><span data-stu-id="dd986-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="dd986-133">Consente di trovare oggetti e [seguire un oggetto e i relativi dati attraverso il sistema](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="dd986-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="dd986-134">Eliminazione</span><span class="sxs-lookup"><span data-stu-id="dd986-134">Delete</span></span>
<span data-ttu-id="dd986-135">L'azione di eliminazione viene usata per due scopi diversi.</span><span class="sxs-lookup"><span data-stu-id="dd986-135">The delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="dd986-137">L'opzione **Delete connector space only** (Elimina solo lo spazio connettore) rimuove tutti i dati, ma mantiene la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="dd986-138">L'opzione **Delete Connector and connector space** (Elimina connettore e spazio connettore) rimuove i dati e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="dd986-139">Questa opzione viene usata quando non si intende più connettersi a una foresta.</span><span class="sxs-lookup"><span data-stu-id="dd986-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="dd986-140">Entrambe le opzioni sincronizzano tutti gli oggetti e aggiornano gli oggetti del metaverse.</span><span class="sxs-lookup"><span data-stu-id="dd986-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="dd986-141">L'esecuzione di questa azione richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="dd986-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="dd986-142">Configura profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="dd986-142">Configure Run Profiles</span></span>
<span data-ttu-id="dd986-143">Questa opzione consente di visualizzare i profili di esecuzione configurati per un connettore.</span><span class="sxs-lookup"><span data-stu-id="dd986-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="dd986-145">Spazio connettore di ricerca</span><span class="sxs-lookup"><span data-stu-id="dd986-145">Search Connector Space</span></span>
<span data-ttu-id="dd986-146">L’azione Cerca spazio connettore è utile per trovare oggetti e risolvere problemi relativi ai dati.</span><span class="sxs-lookup"><span data-stu-id="dd986-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="dd986-148">Iniziare selezionando un **ambito**.</span><span class="sxs-lookup"><span data-stu-id="dd986-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="dd986-149">È possibile eseguire ricerche in base ai dati (RDN, DN, Ancoraggio, Sottoalbero) o allo stato dell'oggetto (tutte le altre opzioni).</span><span class="sxs-lookup"><span data-stu-id="dd986-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="dd986-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="dd986-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="dd986-151">Se ad esempio si esegue una ricerca nel sottoalbero, si ottengono tutti gli oggetti in una OU.</span><span class="sxs-lookup"><span data-stu-id="dd986-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="dd986-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="dd986-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="dd986-153">Da questa griglia è possibile selezionare un oggetto, selezionare le **proprietà** e [seguirlo](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) dallo spazio connettore di origine attraverso il metaverse e fino allo spazio connettore di destinazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="dd986-154">Modifica della password dell'account Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="dd986-154">Changing the AD DS account password</span></span>
<span data-ttu-id="dd986-155">Se si modifica la password dell'account, il servizio di sincronizzazione non sarà più in grado di importare/esportare le modifiche in Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="dd986-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="dd986-156">Potrebbe verificarsi quanto segue:</span><span class="sxs-lookup"><span data-stu-id="dd986-156">You may see the following:</span></span>

- <span data-ttu-id="dd986-157">L'operazione di importazione/esportazione per il connettore di Active Directory non riesce con errore "no-start-credentials".</span><span class="sxs-lookup"><span data-stu-id="dd986-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="dd986-158">In Visualizzatore eventi di Windows, il registro eventi dell'applicazione contiene un errore con Event ID 6000 e il messaggio 'The management agent "contoso.com" failed to run because the credentials were invalid'.</span><span class="sxs-lookup"><span data-stu-id="dd986-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="dd986-159">Per risolvere il problema, aggiornare l'account utente di Active Directory Domain Services mediante la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="dd986-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="dd986-160">Avviare Synchronization Service Manager (START → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="dd986-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="dd986-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="dd986-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="dd986-162">Passare alla scheda **Connettori**.</span><span class="sxs-lookup"><span data-stu-id="dd986-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="dd986-163">Selezionare il connettore di Active Directory configurato per usare l'account di Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="dd986-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="dd986-164">In Azioni selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="dd986-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="dd986-165">Nella finestra di dialogo popup, selezionare Connetti a Foresta Active Directory:</span><span class="sxs-lookup"><span data-stu-id="dd986-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="dd986-166">Il nome della foresta indica la corrispondente Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="dd986-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="dd986-167">Il nome utente indica l'account di Active Directory Domain Services usato per la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="dd986-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="dd986-168">Immettere la nuova password dell'account di Active Directory Domain Services nella casella di testo Password ![Utility per la chiave di crittografia per la sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="dd986-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="dd986-169">Fare clic su OK per salvare la nuova password e riavviare il servizio di sincronizzazione per rimuovere la vecchia password dalla cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="dd986-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="dd986-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dd986-170">Next steps</span></span>
<span data-ttu-id="dd986-171">Ulteriori informazioni sulla configurazione della [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd986-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="dd986-172">Ulteriori informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="dd986-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
