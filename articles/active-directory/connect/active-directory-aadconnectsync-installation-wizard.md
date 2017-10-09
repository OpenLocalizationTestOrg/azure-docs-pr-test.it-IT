---
title: Installazione guidata di rieseguire hello Azure AD Connect | Documenti Microsoft
description: Viene illustrata l'installazione guidata di hello hello alla seconda esecuzione.
keywords: installazione guidata di Hello Azure AD Connect consente di configurare hello le impostazioni di manutenzione alla seconda esecuzione
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="a4112-104">Sincronizzazione di Azure AD Connect: installazione guidata di hello una seconda volta</span><span class="sxs-lookup"><span data-stu-id="a4112-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="a4112-105">Hello prima volta che si esegue l'installazione guidata di hello Azure AD Connect, illustra come tooconfigure l'installazione.</span><span class="sxs-lookup"><span data-stu-id="a4112-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="a4112-106">Se si esegue l'installazione guidata di hello nuovamente, offre opzioni per la manutenzione.</span><span class="sxs-lookup"><span data-stu-id="a4112-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="a4112-107">È possibile trovare l'installazione guidata di hello nel menu start hello denominato **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="a4112-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="a4112-109">Quando si avvia l'installazione guidata di hello, viene visualizzata una pagina con queste opzioni:</span><span class="sxs-lookup"><span data-stu-id="a4112-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Pagina con un elenco di attività aggiuntive](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="a4112-111">Se con Azure AD Connect è stato installato AD FS saranno disponibili ancora più opzioni.</span><span class="sxs-lookup"><span data-stu-id="a4112-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="a4112-112">opzioni aggiuntive disponibili per ADFS sono documentati in Hello [gestione ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="a4112-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="a4112-113">Selezionare una delle attività hello e fare clic su **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a4112-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4112-114">Mentre installazione guidata di hello è aperto, tutte le operazioni nel motore di sincronizzazione hello vengono sospesi.</span><span class="sxs-lookup"><span data-stu-id="a4112-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="a4112-115">Assicurarsi di chiudere installazione guidata di hello subito dopo aver completato le modifiche di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4112-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="a4112-116">Visualizzazione della configurazione corrente</span><span class="sxs-lookup"><span data-stu-id="a4112-116">View current configuration</span></span>
<span data-ttu-id="a4112-117">Questa opzione consente di visualizzare rapidamente le opzioni attualmente configurate.</span><span class="sxs-lookup"><span data-stu-id="a4112-117">This option gives you a quick view of your currently configured options.</span></span>

![Pagina con un elenco di tutte le opzioni e il relativo stato](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="a4112-119">Fare clic su **precedente** toogo back.</span><span class="sxs-lookup"><span data-stu-id="a4112-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="a4112-120">Se si seleziona **uscita**, si chiude l'installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="a4112-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="a4112-121">Personalizzazione delle opzioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="a4112-121">Customize synchronization options</span></span>
<span data-ttu-id="a4112-122">Questa opzione è una configurazione della sincronizzazione toohello modifiche toomake utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a4112-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="a4112-123">Vedrai un subset di opzioni dal percorso di installazione di hello configurazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a4112-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="a4112-124">Queste opzioni vengono visualizzate anche se inizialmente è stata usata l'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="a4112-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="a4112-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Aggiunta di altre directory).</span><span class="sxs-lookup"><span data-stu-id="a4112-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="a4112-126">Per rimuovere una directory, vedere [Eliminazione di un connettore](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="a4112-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="a4112-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Modifica dei filtri di unità organizzativa e dominio).</span><span class="sxs-lookup"><span data-stu-id="a4112-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="a4112-128">Remove Group filtering (Rimozione dei filtri di gruppo).</span><span class="sxs-lookup"><span data-stu-id="a4112-128">Remove Group filtering.</span></span>
* <span data-ttu-id="a4112-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Modifica delle funzionalità facoltative).</span><span class="sxs-lookup"><span data-stu-id="a4112-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="a4112-130">Hello altre opzioni di installazione iniziale di hello non possono essere modificati e non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="a4112-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="a4112-131">Queste opzioni sono:</span><span class="sxs-lookup"><span data-stu-id="a4112-131">These options are:</span></span>

* <span data-ttu-id="a4112-132">Modificare hello toouse di attributo per gli attributi userPrincipalName e sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="a4112-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="a4112-133">Modificare hello aggiunta metodo per gli oggetti da una foresta diversa.</span><span class="sxs-lookup"><span data-stu-id="a4112-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="a4112-134">Abilitazione dei filtri basati sui gruppi.</span><span class="sxs-lookup"><span data-stu-id="a4112-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="a4112-135">Aggiorna lo schema della directory</span><span class="sxs-lookup"><span data-stu-id="a4112-135">Refresh directory schema</span></span>
<span data-ttu-id="a4112-136">Questa opzione viene utilizzata se è stata modificata schema hello in uno dei locale foreste di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4112-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="a4112-137">Ad esempio, si potrebbe essere installato Exchange o aggiornata lo schema tooa Windows Server 2012 con gli oggetti dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a4112-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="a4112-138">In questo caso, è necessario tooinstruct Azure AD Connect tooread hello schema nuovamente da AD DS e aggiornare la cache.</span><span class="sxs-lookup"><span data-stu-id="a4112-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="a4112-139">Questa operazione rigenera anche le regole di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="a4112-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="a4112-140">Se si aggiunta schema Exchange hello, ad esempio, le regole di sincronizzazione hello per Exchange vengono aggiunti toohello configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4112-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="a4112-141">Quando si seleziona questa opzione, vengono elencate tutte le directory hello nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="a4112-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="a4112-142">È possibile mantenere l'impostazione predefinita hello e aggiornare tutte le foreste o deselezionare alcuni di essi.</span><span class="sxs-lookup"><span data-stu-id="a4112-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Pagina con un elenco di tutte le directory nell'ambiente di hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="a4112-144">Configurazione della modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="a4112-144">Configure staging mode</span></span>
<span data-ttu-id="a4112-145">Questa opzione consente di tooenable e disabilitare la modalità di gestione temporanea nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="a4112-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="a4112-146">Per altre informazioni sull'uso della modalità di gestione temporanea, vedere [Operazioni](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="a4112-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="a4112-147">opzione Hello Mostra se gestione temporanea è attualmente abilitato o disabilitato:</span><span class="sxs-lookup"><span data-stu-id="a4112-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Opzione che viene inoltre visualizzato lo stato corrente di hello della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="a4112-149">toochange hello stato, selezionare questa opzione e hello selezionare o deselezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="a4112-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Opzione che viene inoltre visualizzato lo stato corrente di hello della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="a4112-151">Cambia l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="a4112-151">Change user sign-in</span></span>
<span data-ttu-id="a4112-152">Questa opzione consente di toochange da toofederation di sincronizzazione password o viceversa hello.</span><span class="sxs-lookup"><span data-stu-id="a4112-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="a4112-153">Non è possibile modificare troppo**non si configura**.</span><span class="sxs-lookup"><span data-stu-id="a4112-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="a4112-154">Per altre informazioni su questa opzione, vedere [Accesso utente](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="a4112-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4112-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4112-155">Next steps</span></span>
* <span data-ttu-id="a4112-156">Ulteriori informazioni sul modello di configurazione hello utilizzato dalla sincronizzazione di Azure AD Connect in [Provisioning dichiarativo comprensione](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="a4112-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="a4112-157">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="a4112-157">**Overview topics**</span></span>

* [<span data-ttu-id="a4112-158">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="a4112-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="a4112-159">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4112-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
