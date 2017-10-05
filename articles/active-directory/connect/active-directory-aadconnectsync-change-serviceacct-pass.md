---
title: 'Servizio di sincronizzazione Azure AD Connect: modifica dell''account del servizio di sincronizzazione Azure AD Connect | Microsoft Docs'
description: Questo argomento descrive la chiave di crittografia e come abbandonarla dopo la modifica della password.
services: active-directory
keywords: Account del servizio Azure AD Sync, password
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="5c229-104">Modifica della password dell'account del servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5c229-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="5c229-105">Se si modifica la password dell'account del servizio di sincronizzazione Azure AD Connect, il servizio di sincronizzazione non verrà avviato correttamente finché non si abbandona la chiave di crittografia e non si reinizializza la password dell'account del servizio.</span><span class="sxs-lookup"><span data-stu-id="5c229-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="5c229-106">Azure AD Connect, parte dei servizi di sincronizzazione, usa una chiave di crittografia per archiviare le password degli account di servizio Active Directory Domain Services e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c229-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="5c229-107">Questi account vengono crittografati prima di essere archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="5c229-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="5c229-108">La chiave di crittografia usata viene protetta con [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c229-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="5c229-109">DPAPI protegge la chiave di crittografia usando la **password dell'account del servizio di sincronizzazione Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="5c229-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="5c229-110">Se è necessario modificare la password dell'account del servizio, è possibile usare le procedure contenute in [Abbandono della chiave di crittografia del servizio di sincronizzazione Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key).</span><span class="sxs-lookup"><span data-stu-id="5c229-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="5c229-111">Queste procedure devono essere usate anche se è necessario abbandonare la chiave di crittografia per qualsiasi altro motivo.</span><span class="sxs-lookup"><span data-stu-id="5c229-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="5c229-112">Problemi derivati dalla modifica della password</span><span class="sxs-lookup"><span data-stu-id="5c229-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="5c229-113">Quando si modifica la password dell'account del servizio, è necessario eseguire due operazioni.</span><span class="sxs-lookup"><span data-stu-id="5c229-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="5c229-114">Prima di tutto, è necessario modificare la password in Gestione controllo servizi di Windows.</span><span class="sxs-lookup"><span data-stu-id="5c229-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="5c229-115">Finché non si risolve questo problema, verranno visualizzati gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c229-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="5c229-116">Se si prova ad avviare il servizio di sincronizzazione in Gestione controllo servizi di Windows, viene visualizzato l'errore "**Impossibile avviare il servizio Microsoft Azure AD Sync su computer locale**".</span><span class="sxs-lookup"><span data-stu-id="5c229-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="5c229-117">**Errore 1069: Il servizio non è stato avviato a causa di un errore in fase di accesso**".</span><span class="sxs-lookup"><span data-stu-id="5c229-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="5c229-118">Nel Visualizzatore eventi di Windows il registro eventi di sistema contiene un errore con **ID evento 7038** e il messaggio "**Il servizio ADSync non è stato in grado di accedere con la password al momento configurata, a causa del seguente errore: Password o nome utente errato**".</span><span class="sxs-lookup"><span data-stu-id="5c229-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="5c229-119">In secondo luogo, se in condizioni specifiche la password viene aggiornata, il servizio di sincronizzazione non può più recuperare la chiave di crittografia tramite DPAPI.</span><span class="sxs-lookup"><span data-stu-id="5c229-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="5c229-120">Senza la chiave di crittografia, il servizio di sincronizzazione non può decrittografare le password necessarie per eseguire la sincronizzazione a/da Active Directory e Azure AD locali.</span><span class="sxs-lookup"><span data-stu-id="5c229-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="5c229-121">Verranno visualizzati gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="5c229-121">You will see errors such as:</span></span>

- <span data-ttu-id="5c229-122">Se in Gestione controllo servizi di Windows si prova ad avviare il servizio di sincronizzazione e questo non riesce a recuperare la chiave di crittografia, viene restituito l'errore "**Impossibile avviare il servizio Microsoft Azure AD Sync su computer locale.</span><span class="sxs-lookup"><span data-stu-id="5c229-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="5c229-123">Per maggiori informazioni, consultare il registro eventi di sistema.</span><span class="sxs-lookup"><span data-stu-id="5c229-123">For more information, review the System Event log.</span></span> <span data-ttu-id="5c229-124">Se non si tratta di un servizio Microsoft, contattare il fornitore del servizio e fare riferimento al codice di errore **-21451857952****".</span><span class="sxs-lookup"><span data-stu-id="5c229-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="5c229-125">Nel Visualizzatore eventi di Windows il registro eventi dell'applicazione contiene un errore con **ID evento 6028** e il messaggio di errore *"**Impossibile accedere alla chiave di crittografia del server**".*</span><span class="sxs-lookup"><span data-stu-id="5c229-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="5c229-126">Per assicurarsi di non ricevere più questi errori, seguire le procedure contenute in [Abbandono della chiave di crittografia del servizio di sincronizzazione Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) quando si modifica la password.</span><span class="sxs-lookup"><span data-stu-id="5c229-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="5c229-127">Abbandono della chiave di crittografia del servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="5c229-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="5c229-128">Le procedure seguenti si applicano solo ad Azure AD Connect build 1.1.443.0 o precedenti.</span><span class="sxs-lookup"><span data-stu-id="5c229-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="5c229-129">Usare le procedure seguenti per abbandonare la chiave di crittografia.</span><span class="sxs-lookup"><span data-stu-id="5c229-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="5c229-130">Che cosa fare se è necessario abbandonare la chiave di crittografia</span><span class="sxs-lookup"><span data-stu-id="5c229-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="5c229-131">Se è necessario abbandonare la chiave di crittografia, usare le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="5c229-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="5c229-132">Abbandonare la chiave di crittografia esistente</span><span class="sxs-lookup"><span data-stu-id="5c229-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="5c229-133">Specificare la password dell'account Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="5c229-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="5c229-134">Reinizializzare la password dell'account Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="5c229-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="5c229-135">Avviare il servizio di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="5c229-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="5c229-136">Abbandonare la chiave di crittografia esistente</span><span class="sxs-lookup"><span data-stu-id="5c229-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="5c229-137">Abbandonare la chiave di crittografia esistente per poterne creare una nuova:</span><span class="sxs-lookup"><span data-stu-id="5c229-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="5c229-138">Accedere al server Azure AD Connect come amministratore.</span><span class="sxs-lookup"><span data-stu-id="5c229-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="5c229-139">Avviare una nuova sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c229-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="5c229-140">Passare alla cartella `$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="5c229-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="5c229-141">Eseguire il comando `./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="5c229-141">Run the command: `./miiskmu.exe /a`</span></span>

![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="5c229-143">Specificare la password dell'account Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="5c229-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="5c229-144">Poiché le password esistenti archiviate nel database non possono essere più decrittografate, è necessario immettere nel servizio di sincronizzazione la password dell'account Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5c229-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="5c229-145">Il servizio di sincronizzazione crittografa le password usando la nuova chiave di crittografia:</span><span class="sxs-lookup"><span data-stu-id="5c229-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="5c229-146">Avviare Synchronization Service Manager (START → Servizio di sincronizzazione).</span><span class="sxs-lookup"><span data-stu-id="5c229-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="5c229-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="5c229-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="5c229-148">Passare alla scheda **Connettori**.</span><span class="sxs-lookup"><span data-stu-id="5c229-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="5c229-149">Selezionare il connettore **AD Connector** corrispondente ad Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="5c229-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="5c229-150">Se sono presenti più connettori, ripetere i passaggi seguenti per ognuno.</span><span class="sxs-lookup"><span data-stu-id="5c229-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="5c229-151">In **Azioni** selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5c229-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="5c229-152">Nella finestra di dialogo popup selezionare **Connetti a Foresta Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="5c229-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="5c229-153">Immettere la nuova password dell'account Active Directory Domain Services nella casella di testo **Password**.</span><span class="sxs-lookup"><span data-stu-id="5c229-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="5c229-154">Se non si conosce questa password, è necessario impostarla su un valore noto prima di eseguire questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="5c229-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="5c229-155">Fare clic su **OK** per salvare la nuova password e chiudere la finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="5c229-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="5c229-156">![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="5c229-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="5c229-157">Reinizializzare la password dell'account Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="5c229-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="5c229-158">Non è possibile fornire direttamente la password dell'account del servizio Azure AD al servizio di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="5c229-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="5c229-159">È invece necessario usare il cmdlet **Add-ADSyncAADServiceAccount** per reinizializzare l'account del servizio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c229-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="5c229-160">Il cmdlet reimposta la password dell'account e la rende disponibile al servizio di sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="5c229-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="5c229-161">Avviare una nuova sessione di PowerShell nel server Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5c229-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="5c229-162">Eseguire il cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="5c229-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="5c229-163">Nella finestra di dialogo popup immettere le credenziali di amministratore globale di Azure AD per il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c229-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="5c229-164">![Utilità per la chiave di crittografia del servizio di sincronizzazione Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="5c229-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="5c229-165">Se questo passaggio riesce, verrà visualizzato il prompt dei comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c229-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="5c229-166">Avviare il servizio di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="5c229-166">Start the Synchronization Service</span></span>
<span data-ttu-id="5c229-167">Ora che il servizio di sincronizzazione ha accesso alla chiave di crittografia e a tutte le password necessarie, è possibile riavviare il servizio in Gestione controllo servizi di Windows:</span><span class="sxs-lookup"><span data-stu-id="5c229-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="5c229-168">Passare a Gestione controllo servizi di Windows (START → Servizi).</span><span class="sxs-lookup"><span data-stu-id="5c229-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="5c229-169">Selezionare **Microsoft Azure AD Sync** e fare clic su Riavvia.</span><span class="sxs-lookup"><span data-stu-id="5c229-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c229-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5c229-170">Next steps</span></span>
<span data-ttu-id="5c229-171">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="5c229-171">**Overview topics**</span></span>

* [<span data-ttu-id="5c229-172">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="5c229-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="5c229-173">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c229-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
