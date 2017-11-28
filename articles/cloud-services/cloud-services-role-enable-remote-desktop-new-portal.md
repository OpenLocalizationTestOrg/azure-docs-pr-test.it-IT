---
title: aaaEnable connessione Desktop remoto per un ruolo in servizi Cloud di Azure | Documenti Microsoft
description: "La modalità di cloud di azure di tooconfigure connessioni desktop remoto tooallow all'applicazione di servizio"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="5b628-103">Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="5b628-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b628-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b628-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="5b628-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="5b628-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="5b628-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b628-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="5b628-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b628-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="5b628-108">Desktop remoto consente desktop hello tooaccess di un ruolo in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="5b628-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="5b628-109">È possibile utilizzare un tootroubleshoot connessione Desktop remoto e diagnosticare i problemi dell'applicazione mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5b628-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="5b628-110">È possibile abilitare una connessione Desktop remoto nel ruolo durante lo sviluppo includendo i moduli di Desktop remoto hello nella definizione del servizio oppure è possibile scegliere tooenable Desktop remoto tramite hello estensione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="5b628-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="5b628-111">Hello approccio consigliato è toouse hello Desktop remoto estensione come è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello senza tooredeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b628-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="5b628-112">Configurare Desktop remoto dal portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5b628-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="5b628-113">portale di Azure Hello utilizza l'approccio di estensione Desktop remoto di hello in cui è possibile abilitare Desktop remoto anche dopo la distribuzione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b628-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="5b628-114">Hello **Desktop remoto** pannello per il servizio cloud consente tooenable Desktop remoto, account di amministratore locale modifica hello usata tooconnect toohello le macchine virtuali, certificato hello usati nell'autenticazione e imposta hello Data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="5b628-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="5b628-115">Fare clic su **servizi Cloud**, fare clic sul nome del servizio cloud hello hello e quindi fare clic su **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="5b628-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="5b628-117">Scegliere se si desidera tooenable Desktop remoto per un singolo ruolo o per tutti i ruoli, quindi modifica il valore di hello di hello selezione troppo**abilitato**.</span><span class="sxs-lookup"><span data-stu-id="5b628-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="5b628-118">Compilare i campi necessario hello per nome utente, password, scadenza e certificati.</span><span class="sxs-lookup"><span data-stu-id="5b628-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="5b628-120">Tutte le istanze del ruolo verranno riavviate la prima volta che si abilita Desktop remoto e si fa clic su OK (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="5b628-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="5b628-121">tooprevent un riavvio, la password di hello hello certificato tooencrypt utilizzato deve essere installato nel ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="5b628-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="5b628-122">un riavvio, tooprevent [caricare un certificato per il servizio cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e restituirne toothis finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="5b628-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="5b628-123">In **ruoli**selezionare ruolo hello desiderato tooupdate **tutti** per tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="5b628-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="5b628-124">Al termine degli aggiornamenti della configurazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5b628-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="5b628-125">Saranno necessari alcuni minuti prima che le istanze del ruolo siano pronti tooreceive connessioni.</span><span class="sxs-lookup"><span data-stu-id="5b628-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="5b628-126">Accedere in remoto alle istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="5b628-126">Remote into role instances</span></span>
<span data-ttu-id="5b628-127">Dopo aver abilitato Desktop remoto per i ruoli di hello, è possibile avviare una connessione direttamente dal portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="5b628-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="5b628-128">Fare clic su **istanze** tooopen hello **istanze** blade.</span><span class="sxs-lookup"><span data-stu-id="5b628-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="5b628-129">Selezionare un'istanza del ruolo per cui è configurato Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="5b628-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="5b628-130">Fare clic su **Connetti** toodownload un RDP file per l'istanza del ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="5b628-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="5b628-132">Fare clic su **aprire** e quindi **Connetti** toostart hello connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="5b628-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="5b628-133">Se il servizio cloud si trova dietro a un gruppo, potrebbe essere necessario toocreate regole che consentano il traffico sulle porte **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="5b628-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="5b628-134">Desktop remoto usa la porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="5b628-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="5b628-135">Le istanze del servizio cloud sono con carico bilanciato, pertanto non è possibile controllare direttamente quale tooconnect istanza di.</span><span class="sxs-lookup"><span data-stu-id="5b628-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="5b628-136">Hello *RemoteForwarder* e *RemoteAccess* gli agenti di gestire il traffico RDP e consentire hello client toosend un cookie RDP e specificare tooconnect una singola istanza di.</span><span class="sxs-lookup"><span data-stu-id="5b628-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="5b628-137">Hello *RemoteForwarder* e *RemoteAccess* agenti richiedono tale porta **20000*** aperto, che può essere bloccato se si dispone di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="5b628-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5b628-138">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="5b628-138">Additional resources</span></span>

<span data-ttu-id="5b628-139">[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="5b628-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
