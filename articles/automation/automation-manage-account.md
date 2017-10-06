---
title: account di automazione di Azure aaaManage | Documenti Microsoft
description: In questo articolo viene descritto come toomanage hello configurazione dell'account di automazione, ad esempio il rinnovo del certificato, l'eliminazione e la configurazione errata.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="e8a8f-103">Gestire l'account di Automazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e8a8f-103">Manage Azure Automation account</span></span>
<span data-ttu-id="e8a8f-104">A un certo punto prima che scada l'account di automazione, sarà necessario toorenew hello certificato.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="e8a8f-105">Se si ritiene che hello account RunAs sia stata compromessa, è possibile eliminare e ricrearlo.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="e8a8f-106">Questa sezione viene descritto come tooperform queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="e8a8f-107">Rinnovo del certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="e8a8f-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="e8a8f-108">il certificato autofirmato Hello creato per l'account RunAs hello scade un anno dalla data di hello di creazione.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="e8a8f-109">È possibile rinnovarlo in qualsiasi momento prima della scadenza.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="e8a8f-110">Quando si rinnovarlo, certificato valido corrente hello è conservate tooensure che tutti i runbook che vengono messe in coda fino o attivamente in esecuzione e che l'autenticazione con hello account RunAs, non sono influenzati negativamente.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="e8a8f-111">certificato Hello rimane valido fino alla relativa data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="e8a8f-112">Se si utilizza questa opzione è stata configurata l'automazione Run As account toouse un certificato emesso da un'autorità di certificazione dell'organizzazione, certificato aziendale hello verrà sostituito da un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="e8a8f-113">hello toorenew certificati, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8a8f-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="e8a8f-114">Nel portale di Azure hello, aprire l'account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="e8a8f-115">In hello **Account di automazione** pannello in hello **Account proprietà** riquadro, in **impostazioni Account**selezionare **account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Riquadro delle proprietà dell'account di Automazione](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="e8a8f-117">In hello **account RunAs** Pannello proprietà, seleziona entrambi hello eseguiti come account o hello Classic account RunAs che si desidera che il certificato hello toorenew per.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="e8a8f-118">In hello **proprietà** pannello hello account selezionato, fare clic su **Rinnova certificato**.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Rinnovare il certificato per l'account RunAs](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="e8a8f-120">Mentre viene rinnovato il certificato di hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="e8a8f-121">Eliminare un account RunAs o un account RunAs classico</span><span class="sxs-lookup"><span data-stu-id="e8a8f-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="e8a8f-122">Questa sezione viene descritto come toodelete e ricreare un account RunAs o classico runas.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="e8a8f-123">Quando si esegue questa azione, viene mantenuto hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="e8a8f-124">Dopo aver eliminato un account RunAs o classico runas, è possibile crearlo nuovamente in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="e8a8f-125">Nel portale di Azure hello, aprire l'account di automazione hello.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="e8a8f-126">In hello **account di automazione** in hello account riquadro proprietà, seleziona pannello **account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="e8a8f-127">In hello **account RunAs** Pannello proprietà, selezionare entrambi hello account RunAs classico RunAs dell'account che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="e8a8f-128">Quindi, nella hello **proprietà** pannello hello account selezionato, fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Eliminare un account RunAs](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="e8a8f-130">Durante l'eliminazione di account hello in corso, è possibile monitorare i progressi di hello in **notifiche** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="e8a8f-131">Dopo aver eliminato l'account di hello, è possibile crearlo nuovamente su hello **account RunAs** Pannello proprietà selezionando hello opzione create **Azure Account runas**.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Ricreare hello automazione account RunAs](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="e8a8f-133">Errore di configurazione</span><span class="sxs-lookup"><span data-stu-id="e8a8f-133">Misconfiguration</span></span>
<span data-ttu-id="e8a8f-134">Alcuni elementi di configurazione necessari per toofunction di account RunAs o classico runas hello correttamente potrebbe essere stati eliminati o creati in modo non corretto durante l'installazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="e8a8f-135">gli elementi di Hello includono:</span><span class="sxs-lookup"><span data-stu-id="e8a8f-135">hello items include:</span></span>

* <span data-ttu-id="e8a8f-136">Asset del certificato</span><span class="sxs-lookup"><span data-stu-id="e8a8f-136">Certificate asset</span></span>
* <span data-ttu-id="e8a8f-137">Asset di connessione</span><span class="sxs-lookup"><span data-stu-id="e8a8f-137">Connection asset</span></span>
* <span data-ttu-id="e8a8f-138">Account RunAs è stato rimosso dal ruolo di collaboratore hello</span><span class="sxs-lookup"><span data-stu-id="e8a8f-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="e8a8f-139">Entità servizio o applicazione in Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8a8f-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="e8a8f-140">In altre istanze di una configurazione errata e hello precedente hello account di automazione rileva hello cambia e visualizza lo stato di *incompleto* su hello **account RunAs** Pannello proprietà per hello account.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Stato di configurazione Incompleto dell'account RunAs](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="e8a8f-142">Quando si seleziona account RunAs hello, hello account **proprietà** riquadro Visualizza hello seguente messaggio di errore:</span><span class="sxs-lookup"><span data-stu-id="e8a8f-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Messaggio di avviso relativo alla configurazione incompleta dell'account RunAs](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="e8a8f-144">.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-144">.</span></span>

<span data-ttu-id="e8a8f-145">Per risolvere rapidamente i problemi di account RunAs, eliminazione e ricreazione account hello.</span><span class="sxs-lookup"><span data-stu-id="e8a8f-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8a8f-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8a8f-146">Next steps</span></span>
* <span data-ttu-id="e8a8f-147">Per ulteriori informazioni sulle entità servizio, vedere troppo[oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="e8a8f-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="e8a8f-148">Per ulteriori informazioni sul controllo di accesso basato sui ruoli in automazione di Azure, vedere troppo[controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e8a8f-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="e8a8f-149">Per ulteriori informazioni sui certificati e i servizi di Azure, vedere troppo[panoramica dei certificati per servizi Cloud di Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="e8a8f-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
