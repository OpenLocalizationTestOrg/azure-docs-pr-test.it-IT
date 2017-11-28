---
title: in Azure Active Directory Synchronization Service Manager UI hello aaaConnectors | Microsoft documenti
description: Comprendere scheda Connectors hello in hello Synchronization Service Manager per Azure AD Connect.
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
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="76baf-103">Utilizzo dei connettori con hello Azure AD Connect sincronizzazione Service Manager</span><span class="sxs-lookup"><span data-stu-id="76baf-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="76baf-105">scheda Connectors Hello è usato toomanage motore di sincronizzazione di tutti i sistemi hello è connesso a.</span><span class="sxs-lookup"><span data-stu-id="76baf-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="76baf-106">Azioni del connettore</span><span class="sxs-lookup"><span data-stu-id="76baf-106">Connector actions</span></span>
| <span data-ttu-id="76baf-107">Azione</span><span class="sxs-lookup"><span data-stu-id="76baf-107">Action</span></span> | <span data-ttu-id="76baf-108">Commento</span><span class="sxs-lookup"><span data-stu-id="76baf-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="76baf-109">Create</span><span class="sxs-lookup"><span data-stu-id="76baf-109">Create</span></span> |<span data-ttu-id="76baf-110">Non usare.</span><span class="sxs-lookup"><span data-stu-id="76baf-110">Do not use.</span></span> <span data-ttu-id="76baf-111">Per la connessione AD tooadditional foreste, utilizzare Installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="76baf-112">Proprietà</span><span class="sxs-lookup"><span data-stu-id="76baf-112">Properties</span></span> |<span data-ttu-id="76baf-113">Si usa per i filtri di unità organizzativa e dominio.</span><span class="sxs-lookup"><span data-stu-id="76baf-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="76baf-114">Eliminazione</span><span class="sxs-lookup"><span data-stu-id="76baf-114">Delete</span></span>](#delete) |<span data-ttu-id="76baf-115">Tooeither usato eliminare dati hello hello connettore spazio o toodelete connessione tooa foresta.</span><span class="sxs-lookup"><span data-stu-id="76baf-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="76baf-116">Configura profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="76baf-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="76baf-117">Ad eccezione di dominio di applicazione di filtri, nothing tooconfigure qui.</span><span class="sxs-lookup"><span data-stu-id="76baf-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="76baf-118">È possibile utilizzare questa azione toosee già configurati profili di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="76baf-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="76baf-119">Esegui</span><span class="sxs-lookup"><span data-stu-id="76baf-119">Run</span></span> |<span data-ttu-id="76baf-120">Utilizzare toostart una tantum esecuzione di un profilo.</span><span class="sxs-lookup"><span data-stu-id="76baf-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="76baf-121">Arresto</span><span class="sxs-lookup"><span data-stu-id="76baf-121">Stop</span></span> |<span data-ttu-id="76baf-122">Arresta un connettore che sta eseguendo attualmente un profilo.</span><span class="sxs-lookup"><span data-stu-id="76baf-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="76baf-123">Esporta connettore</span><span class="sxs-lookup"><span data-stu-id="76baf-123">Export Connector</span></span> |<span data-ttu-id="76baf-124">Non usare.</span><span class="sxs-lookup"><span data-stu-id="76baf-124">Do not use.</span></span> |
| <span data-ttu-id="76baf-125">Importa connettore</span><span class="sxs-lookup"><span data-stu-id="76baf-125">Import Connector</span></span> |<span data-ttu-id="76baf-126">Non usare.</span><span class="sxs-lookup"><span data-stu-id="76baf-126">Do not use.</span></span> |
| <span data-ttu-id="76baf-127">Aggiorna connettore</span><span class="sxs-lookup"><span data-stu-id="76baf-127">Update Connector</span></span> |<span data-ttu-id="76baf-128">Non usare.</span><span class="sxs-lookup"><span data-stu-id="76baf-128">Do not use.</span></span> |
| <span data-ttu-id="76baf-129">Aggiorna schema</span><span class="sxs-lookup"><span data-stu-id="76baf-129">Refresh Schema</span></span> |<span data-ttu-id="76baf-130">Aggiorna schema memorizzati nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="76baf-131">Si tratta toouse preferito hello opzione nell'installazione guidata di hello, invece, dopo che anche gli aggiornamenti di sincronizzazione regole.</span><span class="sxs-lookup"><span data-stu-id="76baf-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="76baf-132">Spazio connettore di ricerca</span><span class="sxs-lookup"><span data-stu-id="76baf-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="76baf-133">Gli oggetti toofind utilizzati e troppo[seguire un oggetto e i relativi dati tramite il sistema hello](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="76baf-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="76baf-134">Elimina</span><span class="sxs-lookup"><span data-stu-id="76baf-134">Delete</span></span>
<span data-ttu-id="76baf-135">azione di eliminazione Hello viene utilizzato per due scopi diversi.</span><span class="sxs-lookup"><span data-stu-id="76baf-135">hello delete action is used for two different things.</span></span>  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="76baf-137">opzione Hello **Elimina solo lo spazio connettore** rimuove tutti i dati, ma Mantieni hello configurazione.</span><span class="sxs-lookup"><span data-stu-id="76baf-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="76baf-138">opzione Hello **spazio eliminare connettori e** rimuove hello dati e la configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="76baf-139">Questa opzione viene utilizzata quando non si desidera più tooconnect tooa foresta.</span><span class="sxs-lookup"><span data-stu-id="76baf-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="76baf-140">Entrambe le opzioni di sincronizzazione di tutti gli oggetti e aggiornare gli oggetti metaverse hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="76baf-141">L'esecuzione di questa azione richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="76baf-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="76baf-142">Configura profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="76baf-142">Configure Run Profiles</span></span>
<span data-ttu-id="76baf-143">Questa opzione consente di hello toosee profili configurati per un connettore di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="76baf-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="76baf-145">Spazio connettore di ricerca</span><span class="sxs-lookup"><span data-stu-id="76baf-145">Search Connector Space</span></span>
<span data-ttu-id="76baf-146">azione di spazio connettore ricerca Hello è utile toofind oggetti e risolvere i problemi di dati.</span><span class="sxs-lookup"><span data-stu-id="76baf-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="76baf-148">Iniziare selezionando un **ambito**.</span><span class="sxs-lookup"><span data-stu-id="76baf-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="76baf-149">È possibile eseguire la ricerca in base ai dati (RDN, DN, ancoraggio, sottostruttura ad albero), o dello stato dell'oggetto hello (tutte le altre opzioni).</span><span class="sxs-lookup"><span data-stu-id="76baf-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="76baf-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="76baf-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="76baf-151">Se ad esempio si esegue una ricerca nel sottoalbero, si ottengono tutti gli oggetti in una OU.</span><span class="sxs-lookup"><span data-stu-id="76baf-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="76baf-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="76baf-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="76baf-153">In questa griglia è possibile selezionare un oggetto, selezionare **proprietà**, e [seguono](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) da spazio connettore di origine hello, tramite hello metaverse e toohello destinazione connettore.</span><span class="sxs-lookup"><span data-stu-id="76baf-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="76baf-154">Modifica password dell'account di dominio Active Directory hello Active Directory</span><span class="sxs-lookup"><span data-stu-id="76baf-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="76baf-155">Se si modifica la password dell'account hello, hello servizio di sincronizzazione non sarà più possibile tooimport esportare le modifiche locali tooon Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76baf-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="76baf-156">Viene visualizzato il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="76baf-156">You may see hello following:</span></span>

- <span data-ttu-id="76baf-157">passaggio di importazione/esportazione Hello per hello Active Directory connector non riesce con errore "no-start-credenziali".</span><span class="sxs-lookup"><span data-stu-id="76baf-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="76baf-158">In Visualizzatore eventi di Windows, log eventi dell'applicazione hello contiene un errore con ID evento 6000 e il messaggio "hello toorun di gestione agente"contoso.com"non è riuscita perché hello credenziali non sono valide."</span><span class="sxs-lookup"><span data-stu-id="76baf-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="76baf-159">eseguire tooresolve hello, account utente di aggiornamento hello di dominio Active Directory con hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="76baf-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="76baf-160">Avviare hello Synchronization Service Manager (servizio di sincronizzazione iniziale →).</span><span class="sxs-lookup"><span data-stu-id="76baf-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="76baf-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="76baf-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="76baf-162">Passare toohello **connettori** scheda.</span><span class="sxs-lookup"><span data-stu-id="76baf-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="76baf-163">Selezionare hello Active Directory Connector che è configurato toouse hello account di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76baf-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="76baf-164">In Azioni selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="76baf-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="76baf-165">Nella finestra di dialogo popup hello, selezionare Connetti tooActive Directory foresta:</span><span class="sxs-lookup"><span data-stu-id="76baf-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="76baf-166">nome della foresta Hello indica hello corrispondente locale Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76baf-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="76baf-167">nome utente Hello indica l'account di dominio Active Directory hello AD utilizzato per la sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="76baf-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="76baf-168">Immettere hello nuova password dell'account di dominio Active Directory AD hello nella casella di testo Password hello ![Azure AD Connect sincronizzazione crittografia chiave utilità](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="76baf-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="76baf-169">Fare clic su OK toosave hello nuova password e riavviare hello servizio di sincronizzazione tooremove hello vecchia password dalla cache di memoria.</span><span class="sxs-lookup"><span data-stu-id="76baf-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="76baf-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="76baf-170">Next steps</span></span>
<span data-ttu-id="76baf-171">Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.</span><span class="sxs-lookup"><span data-stu-id="76baf-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="76baf-172">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="76baf-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
