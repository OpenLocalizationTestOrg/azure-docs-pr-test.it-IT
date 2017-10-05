---
title: Eseguire di nuovo l'installazione guidata di Azure AD Connect | Documentazione Microsoft
description: Spiega come funziona la procedura di installazione guidata la seconda volta che viene eseguita.
keywords: L'installazione guidata di Azure AD Connect consente di configurare le impostazioni di manutenzione quando viene eseguita la seconda volta
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="9cc35-104">Servizio di sincronizzazione Azure AD Connect: eseguire l'installazione guidata una seconda volta</span><span class="sxs-lookup"><span data-stu-id="9cc35-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="9cc35-105">La prima volta che si esegue l'installazione guidata di Azure AD Connect, viene illustrata la procedura di configurazione dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="9cc35-106">Se si esegue nuovamente l'installazione guidata, verranno messe a disposizione le opzioni di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="9cc35-107">L'installazione guidata si trova nel menu Start **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="9cc35-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Menu Start](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="9cc35-109">Quando si avvia l'installazione guidata viene visualizzata una pagina con le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9cc35-109">When you start the installation wizard, you see a page with these options:</span></span>

![Pagina con un elenco di attività aggiuntive](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="9cc35-111">Se con Azure AD Connect è stato installato AD FS saranno disponibili ancora più opzioni.</span><span class="sxs-lookup"><span data-stu-id="9cc35-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="9cc35-112">Le opzioni aggiuntive per AD FS sono descritte in [Gestione di AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="9cc35-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="9cc35-113">Selezionare una delle attività e fare clic su **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="9cc35-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cc35-114">Mentre l'installazione guidata è aperta, tutte le operazioni nel motore di sincronizzazione vengono sospese.</span><span class="sxs-lookup"><span data-stu-id="9cc35-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="9cc35-115">Assicurarsi di chiudere l'installazione guidata subito dopo aver completato le modifiche della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="9cc35-116">Visualizzazione della configurazione corrente</span><span class="sxs-lookup"><span data-stu-id="9cc35-116">View current configuration</span></span>
<span data-ttu-id="9cc35-117">Questa opzione consente di visualizzare rapidamente le opzioni attualmente configurate.</span><span class="sxs-lookup"><span data-stu-id="9cc35-117">This option gives you a quick view of your currently configured options.</span></span>

![Pagina con un elenco di tutte le opzioni e il relativo stato](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="9cc35-119">Fare clic su **Indietro** per tornare alla pagina precedente.</span><span class="sxs-lookup"><span data-stu-id="9cc35-119">Click **Previous** to go back.</span></span> <span data-ttu-id="9cc35-120">Se si seleziona **Esci**, l'installazione guidata verrà chiusa.</span><span class="sxs-lookup"><span data-stu-id="9cc35-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="9cc35-121">Personalizzazione delle opzioni di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="9cc35-121">Customize synchronization options</span></span>
<span data-ttu-id="9cc35-122">Questa opzione consente di apportare modifiche alla configurazione della sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="9cc35-123">Viene visualizzato un sottoinsieme di opzioni dal percorso di installazione personalizzato della configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="9cc35-124">Queste opzioni vengono visualizzate anche se inizialmente è stata usata l'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="9cc35-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="9cc35-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Aggiunta di altre directory).</span><span class="sxs-lookup"><span data-stu-id="9cc35-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="9cc35-126">Per rimuovere una directory, vedere [Eliminazione di un connettore](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="9cc35-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="9cc35-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Modifica dei filtri di unità organizzativa e dominio).</span><span class="sxs-lookup"><span data-stu-id="9cc35-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="9cc35-128">Remove Group filtering (Rimozione dei filtri di gruppo).</span><span class="sxs-lookup"><span data-stu-id="9cc35-128">Remove Group filtering.</span></span>
* <span data-ttu-id="9cc35-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Modifica delle funzionalità facoltative).</span><span class="sxs-lookup"><span data-stu-id="9cc35-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="9cc35-130">Le altre opzioni dell'installazione iniziale non possono essere modificate e non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="9cc35-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="9cc35-131">Queste opzioni sono:</span><span class="sxs-lookup"><span data-stu-id="9cc35-131">These options are:</span></span>

* <span data-ttu-id="9cc35-132">Modifica dell'attributo da usare per userPrincipalName e sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="9cc35-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="9cc35-133">Modifica del metodo di abbinamento per gli oggetti di un'altra foresta.</span><span class="sxs-lookup"><span data-stu-id="9cc35-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="9cc35-134">Abilitazione dei filtri basati sui gruppi.</span><span class="sxs-lookup"><span data-stu-id="9cc35-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="9cc35-135">Aggiorna lo schema della directory</span><span class="sxs-lookup"><span data-stu-id="9cc35-135">Refresh directory schema</span></span>
<span data-ttu-id="9cc35-136">Questa opzione viene usata se lo schema è stato modificato in una delle foreste AD DS locali.</span><span class="sxs-lookup"><span data-stu-id="9cc35-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="9cc35-137">Potrebbe ad esempio essere installato Exchange o l'aggiornamento a uno schema di Windows Server 2012 con oggetti dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9cc35-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="9cc35-138">In questo caso è necessario indicare ad Azure AD Connect di leggere nuovamente lo schema da AD DS e aggiornare la propria cache.</span><span class="sxs-lookup"><span data-stu-id="9cc35-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="9cc35-139">Con questa azione verranno anche rigenerate le regole di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="9cc35-140">Se si aggiunge lo schema di Exchange, ad esempio, le regole di sincronizzazione per Exchange vengono aggiunte alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="9cc35-141">Quando si seleziona questa opzione, vengono elencate tutte le directory presenti nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cc35-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="9cc35-142">È possibile mantenere l'impostazione predefinita e aggiornare tutte le foreste oppure deselezionare alcune di esse.</span><span class="sxs-lookup"><span data-stu-id="9cc35-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Pagina con un elenco di tutte le directory nell'ambiente](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="9cc35-144">Configurazione della modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="9cc35-144">Configure staging mode</span></span>
<span data-ttu-id="9cc35-145">Questa opzione consente di abilitare e disabilitare la modalità di gestione temporanea nel server.</span><span class="sxs-lookup"><span data-stu-id="9cc35-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="9cc35-146">Per altre informazioni sull'uso della modalità di gestione temporanea, vedere [Operazioni](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="9cc35-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="9cc35-147">L'opzione indicherà se la gestione temporanea è attualmente abilitata o disabilitata: </span><span class="sxs-lookup"><span data-stu-id="9cc35-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Opzione che visualizza anche lo stato attuale della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="9cc35-149">Per modificare lo stato, selezionare questa opzione e selezionare o deselezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="9cc35-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Opzione che visualizza anche lo stato attuale della modalità di gestione temporanea](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="9cc35-151">Cambia l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="9cc35-151">Change user sign-in</span></span>
<span data-ttu-id="9cc35-152">Questa opzione consente di passare dalla sincronizzazione password alla federazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="9cc35-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="9cc35-153">Non è possibile passare a **Non configurare**.</span><span class="sxs-lookup"><span data-stu-id="9cc35-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="9cc35-154">Per altre informazioni su questa opzione, vedere [Accesso utente](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="9cc35-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc35-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9cc35-155">Next steps</span></span>
* <span data-ttu-id="9cc35-156">Per altre informazioni sul modello di configurazione usato dal servizio di sincronizzazione Azure AD Connect, vedere [Servizio di sincronizzazione Azure AD Connect: Informazioni sul provisioning dichiarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="9cc35-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="9cc35-157">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="9cc35-157">**Overview topics**</span></span>

* [<span data-ttu-id="9cc35-158">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="9cc35-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="9cc35-159">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9cc35-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
