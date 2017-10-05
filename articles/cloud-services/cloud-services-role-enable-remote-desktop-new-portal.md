---
title: Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure | Microsoft Docs
description: Come configurare l'applicazione del servizio cloud di Azure per consentire le connessioni Desktop remoto
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="287eb-103">Impostare una connessione Desktop remoto per un ruolo nei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="287eb-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="287eb-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="287eb-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="287eb-105">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="287eb-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="287eb-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="287eb-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="287eb-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="287eb-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="287eb-108">Desktop remoto consente di accedere al desktop di un ruolo in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="287eb-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="287eb-109">È possibile usare una connessione Desktop remoto per risolvere e diagnosticare i problemi dell'applicazione mentre è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="287eb-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="287eb-110">È possibile abilitare una connessione Desktop remoto nel ruolo durante lo sviluppo includendo i moduli di Desktop remoto nella definizione del servizio o è possibile scegliere di abilitare Desktop remoto tramite la relativa estensione.</span><span class="sxs-lookup"><span data-stu-id="287eb-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="287eb-111">L'approccio migliore consiste nell'usare l'estensione di Desktop remoto, in quanto è possibile abilitare Desktop remoto anche dopo che l'applicazione viene distribuita senza doverla ridistribuire.</span><span class="sxs-lookup"><span data-stu-id="287eb-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="287eb-112">Configurare Desktop remoto dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="287eb-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="287eb-113">Il portale di Azure usa l'approccio dell'estensione di Desktop remoto in modo da poter abilitare Desktop remoto anche dopo la distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="287eb-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="287eb-114">Il pannello **Desktop remoto** per il servizio cloud consente di abilitare Desktop remoto, modificare l'account amministratore locale usato per connettersi alle macchine virtuali e il certificato usato nell'autenticazione e impostare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="287eb-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="287eb-115">Fare clic su **Servizi cloud**, quindi sul nome del servizio cloud e infine su **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="287eb-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="287eb-117">Scegliere se si vuole abilitare Desktop remoto per un singolo ruolo o per tutti i ruoli, quindi modificare il valore del commutatore su **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="287eb-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="287eb-118">Compilare i campi obbligatori per nome utente, password, scadenza e certificato.</span><span class="sxs-lookup"><span data-stu-id="287eb-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="287eb-120">Tutte le istanze del ruolo verranno riavviate la prima volta che si abilita Desktop remoto e si fa clic su OK (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="287eb-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="287eb-121">Per evitare un riavvio, è necessario che nel ruolo sia installato il certificato usato per crittografare la password.</span><span class="sxs-lookup"><span data-stu-id="287eb-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="287eb-122">Per evitare un riavvio, [caricare un certificato per il servizio cloud](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e quindi tornare alla finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="287eb-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="287eb-123">In **Ruolo** selezionare il ruolo da aggiornare oppure selezionare **Tutti** per tutti i ruoli.</span><span class="sxs-lookup"><span data-stu-id="287eb-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="287eb-124">Al termine degli aggiornamenti della configurazione, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="287eb-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="287eb-125">Ci vorranno alcuni minuti affinché le istanze del ruolo siano pronte a ricevere le connessioni.</span><span class="sxs-lookup"><span data-stu-id="287eb-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="287eb-126">Accedere in remoto alle istanze del ruolo</span><span class="sxs-lookup"><span data-stu-id="287eb-126">Remote into role instances</span></span>
<span data-ttu-id="287eb-127">Dopo aver abilitato Desktop remoto nei ruoli, è possibile avviare una connessione direttamente dal portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="287eb-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="287eb-128">Fare clic su **Istanze** per aprire il pannello **Istanze**.</span><span class="sxs-lookup"><span data-stu-id="287eb-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="287eb-129">Selezionare un'istanza del ruolo per cui è configurato Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="287eb-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="287eb-130">Fare clic su **Connetti** per scaricare un file RDP per l'istanza del ruolo.</span><span class="sxs-lookup"><span data-stu-id="287eb-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Servizi cloud per Desktop remoto](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="287eb-132">Fare clic su **Apri** e quindi su **Connetti** per avviare la connessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="287eb-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="287eb-133">Se il servizio cloud si trova dietro un gruppo di sicurezza di rete, potrebbe essere necessario creare regole che consentano il traffico sulle porte **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="287eb-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="287eb-134">Desktop remoto usa la porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="287eb-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="287eb-135">Dato che alle istanze del servizio cloud viene applicato il bilanciamento del carico, non è possibile controllare direttamente a quale istanza connettersi.</span><span class="sxs-lookup"><span data-stu-id="287eb-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="287eb-136">Gli agenti *RemoteForwarder* e *RemoteAccess* gestiscono il traffico RDP e consentono al client di inviare un cookie RDP e specificare una singola istanza a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="287eb-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="287eb-137">Gli agenti *RemoteForwarder* e *RemoteAccess* richiedono che la porta **20000***, che potrebbe essere bloccata in presenza di un gruppo di sicurezza di rete, sia aperta.</span><span class="sxs-lookup"><span data-stu-id="287eb-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="287eb-138">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="287eb-138">Additional resources</span></span>

<span data-ttu-id="287eb-139">[Come configurare i servizi cloud](cloud-services-how-to-configure.md)
[Domande frequenti sui servizi cloud - Desktop remoto](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="287eb-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
