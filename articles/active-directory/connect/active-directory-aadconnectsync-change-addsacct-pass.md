---
title: "Sincronizzazione Azure AD Connect: modifica della password dell’account AD DS | Microsoft Docs"
description: Il documento di questo argomento descrive come aggiornare Azure AD Connect dopo aver modificato la password dell'account Active Directory Domain Services.
services: active-directory
keywords: account Active Directory Domain Services, account di Active Directory, password
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
ms.openlocfilehash: 14e16a238e60ecfeeb3cbf88c3922a79349dcc75
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="e7cb7-104">Modifica della password dell'account Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="e7cb7-104">Changing the AD DS account password</span></span>
<span data-ttu-id="e7cb7-105">L'account Active Directory Domain Services fa riferimento all'account utente usato da Azure AD Connect per comunicare con Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-105">The AD DS account refers to the user account used by Azure AD Connect to communicate with on-premises Active Directory.</span></span> <span data-ttu-id="e7cb7-106">Se si modifica la password dell'account Active Directory Domain Services, è necessario aggiornare il servizio di sincronizzazione servizio Azure AD Connect con la nuova password.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-106">If you change the password of the AD DS account, you must update Azure AD Connect Synchronization Service with the new password.</span></span> <span data-ttu-id="e7cb7-107">In caso contrario, la sincronizzazione non verrà più eseguita in maniera corretta con Active Directory locale e si verificheranno gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="e7cb7-107">Otherwise, the Synchronization can no longer synchronize correctly with the on-premises Active Directory and you will encounter the following errors:</span></span>

* <span data-ttu-id="e7cb7-108">In Synchronization Service Manager, qualsiasi operazione di importazione o esportazione con AD locale ha esito negativo con errore **no-start-credentials**.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-108">In the Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="e7cb7-109">In Visualizzatore eventi di Windows, il registro eventi dell'applicazione contiene un errore con **Event ID 6000** e il messaggio **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-109">Under Windows Event Viewer, the application event log contains an error with **Event ID 6000** and message **'The management agent "contoso.com" failed to run because the credentials were invalid'**.</span></span>


## <a name="how-to-update-the-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="e7cb7-110">Come aggiornare il servizio di sincronizzazione con la nuova password per l’account Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="e7cb7-110">How to update the Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="e7cb7-111">Per aggiornare il servizio di sincronizzazione con la nuova password:</span><span class="sxs-lookup"><span data-stu-id="e7cb7-111">To update the Synchronization Service with the new password:</span></span>

1. <span data-ttu-id="e7cb7-112">Avviare Synchronization Service Manager (START → Synchronization Service).</span><span class="sxs-lookup"><span data-stu-id="e7cb7-112">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="e7cb7-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="e7cb7-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="e7cb7-114">Passare alla scheda **Connettori**.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-114">Go to the **Connectors** tab.</span></span>

3. <span data-ttu-id="e7cb7-115">Selezionare il **connettore AD** che corrisponde all'account Active Directory Domain Services per cui è stata modificata la password.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-115">Select the **AD Connector** that corresponds to the AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="e7cb7-116">In **Azioni** selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="e7cb7-117">Nella finestra di dialogo popup, selezionare **Connetti a Foresta Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="e7cb7-117">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>

6. <span data-ttu-id="e7cb7-118">Immettere la nuova password dell'account Active Directory Domain Services nella casella di testo **Password**.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-118">Enter the new password of the AD DS account in the **Password** textbox.</span></span>

7. <span data-ttu-id="e7cb7-119">Fare clic su **OK** per salvare la nuova password e chiudere la finestra di dialogo popup.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-119">Click **OK** to save the new password and close the pop-up dialog.</span></span>

8. <span data-ttu-id="e7cb7-120">Riavviare il servizio di sincronizzazione Azure AD Connect in Gestione controllo servizi di Windows.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-120">Restart the Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="e7cb7-121">In questo modo si garantisce che qualsiasi riferimento alla vecchia password venga rimosso dalla cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="e7cb7-121">This is to ensure that any reference to the old password is removed from the memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7cb7-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e7cb7-122">Next steps</span></span>
<span data-ttu-id="e7cb7-123">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="e7cb7-123">**Overview topics**</span></span>

* [<span data-ttu-id="e7cb7-124">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="e7cb7-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="e7cb7-125">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e7cb7-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
