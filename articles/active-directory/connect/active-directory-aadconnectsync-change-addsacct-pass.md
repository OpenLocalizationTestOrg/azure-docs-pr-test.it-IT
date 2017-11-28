---
title: 'Sincronizzazione di Azure AD Connect: la modifica della password di account di dominio Active Directory AD hello | Documenti Microsoft'
description: Il documento di questo argomento viene descritto come tooupdate Azure AD Connect dopo password hello dell'account di dominio Active Directory hello viene modificata.
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="24fef-104">Modifica password dell'account di dominio Active Directory hello Active Directory</span><span class="sxs-lookup"><span data-stu-id="24fef-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="24fef-105">account di dominio Active Directory AD Hello fa riferimento l'account utente toohello utilizzato da Azure AD Connect toocommunicate con Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="24fef-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="24fef-106">Se si modifica la password di hello di hello account di dominio Active Directory, è necessario aggiornare servizio Azure AD Connect sincronizzazione con hello nuova password.</span><span class="sxs-lookup"><span data-stu-id="24fef-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="24fef-107">In caso contrario, la sincronizzazione non è più possibile sincronizzare correttamente con hello hello Active Directory locale e si verificheranno hello gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="24fef-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="24fef-108">In hello operazione Synchronization Service Manager, qualsiasi importazione o esportazione con locale ha esito negativo di Active Directory con **no-start-credenziali** errore.</span><span class="sxs-lookup"><span data-stu-id="24fef-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="24fef-109">In Visualizzatore eventi di Windows, log eventi dell'applicazione hello contiene un errore con **evento ID 6000** e messaggio **'agente di gestione di hello "contoso.com" Impossibile toorun hello credenziali non sono valide'** .</span><span class="sxs-lookup"><span data-stu-id="24fef-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="24fef-110">Come tooupdate hello servizio di sincronizzazione con la nuova password per l'account di dominio Active Directory</span><span class="sxs-lookup"><span data-stu-id="24fef-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="24fef-111">nuova password hello tooupdate hello servizio di sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="24fef-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="24fef-112">Avviare hello Synchronization Service Manager (servizio di sincronizzazione iniziale →).</span><span class="sxs-lookup"><span data-stu-id="24fef-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="24fef-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="24fef-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="24fef-114">Passare toohello **connettori** scheda.</span><span class="sxs-lookup"><span data-stu-id="24fef-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="24fef-115">Seleziona hello **Active Directory Connector** toohello AD account di dominio Active Directory per cui è stata modificata la password corrispondente.</span><span class="sxs-lookup"><span data-stu-id="24fef-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="24fef-116">In **Azioni** selezionare **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="24fef-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="24fef-117">Nella finestra di dialogo popup hello, selezionare **connettersi foresta Directory tooActive**:</span><span class="sxs-lookup"><span data-stu-id="24fef-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="24fef-118">Immettere hello nuova password dell'account di dominio Active Directory hello in hello **Password** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="24fef-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="24fef-119">Fare clic su **OK** toosave hello nuova password e finestra di dialogo popup hello Chiudi.</span><span class="sxs-lookup"><span data-stu-id="24fef-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="24fef-120">Riavvio hello servizio Azure AD Connect sincronizzazione in Gestione controllo servizi di Windows.</span><span class="sxs-lookup"><span data-stu-id="24fef-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="24fef-121">Si tratta di tooensure che qualsiasi password vecchia toohello di riferimento viene rimosso dalla cache di hello in memoria.</span><span class="sxs-lookup"><span data-stu-id="24fef-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24fef-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24fef-122">Next steps</span></span>
<span data-ttu-id="24fef-123">**Argomenti generali**</span><span class="sxs-lookup"><span data-stu-id="24fef-123">**Overview topics**</span></span>

* [<span data-ttu-id="24fef-124">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="24fef-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="24fef-125">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24fef-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
