---
title: Eseguire server applicazioni Java in una macchina virtuale di Azure classica | Documentazione Microsoft
description: Questa esercitazione usa le risorse create con il modello di distribuzione classica e illustra come creare una macchina virtuale di Windows e configurarla per eseguire il server dell'applicazione Apache Tomcat.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="ed02a-103">Come eseguire un server di applicazione di Java in una macchina virtuale creata con il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="ed02a-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ed02a-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed02a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed02a-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="ed02a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ed02a-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="ed02a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ed02a-107">Per un modello di Resource Manager con cui distribuire un'app Web con Java 8 e Tomcat, vedere [qui](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="ed02a-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="ed02a-108">Con Azure è possibile utilizzare una macchina virtuale per fornire funzionalità di server.</span><span class="sxs-lookup"><span data-stu-id="ed02a-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="ed02a-109">Si può ad esempio configurare una macchina virtuale in esecuzione in Azure per ospitare un server applicazioni Java, come Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ed02a-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="ed02a-110">Una volta completata la lettura di questa guida, si disporrà di tutte le informazioni necessarie per creare una macchina virtuale in esecuzione in Azure e configurarla per eseguire un server applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="ed02a-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="ed02a-111">Verranno illustrate ed eseguite le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="ed02a-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="ed02a-112">Come creare una macchina virtuale che dispone di un Java Development Kit (JDK) già installato.</span><span class="sxs-lookup"><span data-stu-id="ed02a-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="ed02a-113">Come accedere in remoto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="ed02a-114">Come installare un server applicazioni Java, Apache Tomcat, sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="ed02a-115">Creare un endpoint per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="ed02a-116">Aprire una porta nel firewall per il server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ed02a-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="ed02a-117">Il completamento dell'installazione comporta l'esecuzione di Tomcat su una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Macchina virtuale che esegue Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="ed02a-119">Per creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed02a-119">To create a virtual machine</span></span>
1. <span data-ttu-id="ed02a-120">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed02a-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="ed02a-121">Fare clic su **Nuovo**, **Calcola**, quindi fare clic su **See all** (Vedi tutto) in **App in primo piano**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="ed02a-122">Fare clic su **JDK**, quindi su **JDK 8** nel riquadro **JDK**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="ed02a-123">Se si dispone di applicazioni legacy non ancora predisposte per l'esecuzione in JDK 8, sono disponibili macchine virtuali che supportano **JDK 6** e **JDK 7**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="ed02a-124">Nel riquadro di JDK 8, selezionare **Classico**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="ed02a-125">Nel pannello **Informazioni di base**:</span><span class="sxs-lookup"><span data-stu-id="ed02a-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="ed02a-126">Specificare un nome per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="ed02a-127">Immettere un nome per l'amministratore nel campo **User Name** .</span><span class="sxs-lookup"><span data-stu-id="ed02a-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="ed02a-128">Ricordare questo nome e la password associata che segue nel campo successivo.</span><span class="sxs-lookup"><span data-stu-id="ed02a-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="ed02a-129">Saranno necessarie per l'accesso da remoto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="ed02a-130">Immettere una password nel campo **Nuova password** e reimmetterla nel campo **Conferma password**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="ed02a-131">Si tratta della password dell'account dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="ed02a-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="ed02a-132">Scegliere la **Sottoscrizione** appropriata.</span><span class="sxs-lookup"><span data-stu-id="ed02a-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="ed02a-133">Per **Gruppo di risorse** fare clic su **Crea nuovo** e immettere il nome del nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ed02a-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="ed02a-134">In alternativa fare clic su **Use existing** (Usa esistente) e selezionare uno dei gruppi di risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="ed02a-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="ed02a-135">Selezionare la località in cui risiede la macchina virtuale, ad esempio **Stati Uniti centro-meridionali**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="ed02a-136">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-136">Click **Next**.</span></span>
7. <span data-ttu-id="ed02a-137">Nel pannello **Virtual machine image size** (Dimensioni dell'immagine della macchina virtuale), selezionare **A1 Standard** (A1 Standard) o un'altra immagine appropriata.</span><span class="sxs-lookup"><span data-stu-id="ed02a-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="ed02a-138">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-138">Click **Select**.</span></span>

9. <span data-ttu-id="ed02a-139">Nel pannello **Impostazioni** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="ed02a-140">È possibile usare i valori predefiniti generati da Azure.</span><span class="sxs-lookup"><span data-stu-id="ed02a-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="ed02a-141">Nel pannello **Riepilogo** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="ed02a-142">Per accedere in remoto alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed02a-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="ed02a-143">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed02a-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ed02a-144">Fare clic su **Macchine virtuali (classico)**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="ed02a-145">Se necessario, fare clic su **Altri servizi** nell'angolo in basso a sinistra nelle categorie di servizi.</span><span class="sxs-lookup"><span data-stu-id="ed02a-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="ed02a-146">La voce **Macchine virtuali (classico)** è elencata nel gruppo **Calcola**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="ed02a-147">Fare clic sul nome della macchina virtuale a cui si desidera accedere.</span><span class="sxs-lookup"><span data-stu-id="ed02a-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="ed02a-148">Dopo aver avviato la macchina virtuale, è possibile eseguire le connessioni tramite un menu nella parte superiore del riquadro.</span><span class="sxs-lookup"><span data-stu-id="ed02a-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="ed02a-149">Fare clic su **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-149">Click **Connect**.</span></span>
6. <span data-ttu-id="ed02a-150">Rispondere ai prompt visualizzati per connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="ed02a-151">In generale l'utente deve salvare o aprire il file con estensione RDP che contiene i dettagli della connessione.</span><span class="sxs-lookup"><span data-stu-id="ed02a-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="ed02a-152">Potrebbe essere necessario copiare url:port nell'ultima parte della prima riga del file .rdp e incollarlo in un'applicazione di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="ed02a-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="ed02a-153">Per installare un server applicazioni Java sulla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed02a-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="ed02a-154">È possibile copiare un server applicazioni Java sulla macchina virtuale oppure installarlo tramite un programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="ed02a-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="ed02a-155">In questa esercitazione Tomcat viene usato come server per le applicazioni Java da installare.</span><span class="sxs-lookup"><span data-stu-id="ed02a-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="ed02a-156">Una volta eseguito l’accesso alla macchina virtuale, aprire una sessione del browser alla pagina [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="ed02a-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="ed02a-157">Fare doppio clic sul collegamento per **32-bit/64-bit Windows Service Installer**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="ed02a-158">Questa tecnica consente di installare Tomcat come servizio di Windows.</span><span class="sxs-lookup"><span data-stu-id="ed02a-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="ed02a-159">Quando richiesto, scegliere di eseguire il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="ed02a-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="ed02a-160">Nella procedura guidata **Apache Tomcat Setup** attenersi ai prompt per installare Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ed02a-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="ed02a-161">Ai fini di questa esercitazione, è possibile accettare le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="ed02a-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="ed02a-162">Quando si arriva alla finestra di dialogo **Completing the Apache Tomcat Setup Wizard** (Completamento della configurazione guidata di Apache Tomcat), è possibile selezionare **Run Apache Tomcat** (Esegui Apache Tomcat) per avviare subito Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ed02a-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="ed02a-163">Fare clic su **Finish** per completare il processo di installazione di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="ed02a-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="ed02a-164">Per avviare Tomcat</span><span class="sxs-lookup"><span data-stu-id="ed02a-164">To start Tomcat</span></span>

<span data-ttu-id="ed02a-165">È possibile avviare manualmente Tomcat aprendo un prompt dei comandi nella macchina virtuale ed eseguendo il comando **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="ed02a-166">Quando Tomcat è in esecuzione, è possibile accedere a Tomcat immettendo l'URL <http://localhost:8080> nel browser della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="ed02a-167">Per vedere Tomcat in esecuzione da macchine esterne, è necessario creare un endpoint e aprire una porta.</span><span class="sxs-lookup"><span data-stu-id="ed02a-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="ed02a-168">Per creare un endpoint per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed02a-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="ed02a-169">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ed02a-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ed02a-170">Fare clic su **Macchine virtuali (classico)**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="ed02a-171">Fare clic sul nome della macchina virtuale che esegue il server applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="ed02a-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="ed02a-172">Fare clic su **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="ed02a-173">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-173">Click **Add**.</span></span>
6. <span data-ttu-id="ed02a-174">Nella finestra di dialogo **Aggiungi endpoint**:</span><span class="sxs-lookup"><span data-stu-id="ed02a-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="ed02a-175">Specificare un nome per l'endpoint, ad esempio **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="ed02a-176">Selezionare **TCP** per il protocollo.</span><span class="sxs-lookup"><span data-stu-id="ed02a-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="ed02a-177">Specificare **80** per la porta pubblica.</span><span class="sxs-lookup"><span data-stu-id="ed02a-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="ed02a-178">Specificare **8080** per la porta privata.</span><span class="sxs-lookup"><span data-stu-id="ed02a-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="ed02a-179">Selezionare **Disattivato** per l'indirizzo IP mobile.</span><span class="sxs-lookup"><span data-stu-id="ed02a-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="ed02a-180">Lasciare l'elenco di controllo di accesso com'è.</span><span class="sxs-lookup"><span data-stu-id="ed02a-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="ed02a-181">Fare clic sul pulsante **OK** per chiudere la finestra di dialogo e creare l'endpoint.</span><span class="sxs-lookup"><span data-stu-id="ed02a-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="ed02a-182">Per aprire nel firewall una porta per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ed02a-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="ed02a-183">Accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="ed02a-184">Fare clic sul pulsante **Start**di Windows.</span><span class="sxs-lookup"><span data-stu-id="ed02a-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="ed02a-185">Fare clic su **Pannello di controllo**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="ed02a-186">Fare clic su **Sistema e sicurezza**, quindi su **Windows Firewall** e infine su **Impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="ed02a-187">Fare clic su **Regole connessioni in entrata** quindi su **Nuova regola**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="ed02a-188">![Nuova regola connessioni in entrata][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="ed02a-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="ed02a-189">Per **Tipo regola**, selezionare **Porta**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="ed02a-190">![Porta della nuova regola connessioni in entrata][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="ed02a-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="ed02a-191">Nella schermata **Protocollo e porte** selezionare **TCP**, specificare **8080** come **Specific local port** (Porta locale specifica), quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="ed02a-192">![Nuova regola connessioni in entrata][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="ed02a-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="ed02a-193">Nella schermata **Azione** selezionare **Consenti la connessione**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="ed02a-194">![Operazione per nuova regola connessioni in entrata][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="ed02a-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="ed02a-195">Nella schermata **Profilo** verificare che le opzioni **Dominio**, **Privato** e **Pubblico** siano selezionate, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="ed02a-196">![Profilo per nuova regola connessioni in entrata][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="ed02a-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="ed02a-197">Nella schermata **Nome** specificare un nome per la regola, come **HttpIn** (non è tuttavia necessario che il nome della regola coincida con quello dell'endpoint), quindi fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="ed02a-198">![Nome della nuova regola connessioni in entrata][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="ed02a-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="ed02a-199">A questo punto, il sito Web Tomcat dovrebbe essere visibile da un browser esterno.</span><span class="sxs-lookup"><span data-stu-id="ed02a-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="ed02a-200">Nella finestra di indirizzi del browser, digitare un URL nel formato  **http://*il\_DNS\_nome*. cloudapp.net**, in cui ***il\_DNS\_nome*** è il nome DNS specificato al momento della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="ed02a-201">Considerazioni sul ciclo di vita delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="ed02a-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="ed02a-202">È possibile creare il proprio archivio di applicazioni Web (WAR) e aggiungerlo alla cartella **webapps** .</span><span class="sxs-lookup"><span data-stu-id="ed02a-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="ed02a-203">Ad esempio, creare un progetto Web dinamico di una pagina JSP (Java Service Page) di base ed esportarlo come file con estensione WAR.</span><span class="sxs-lookup"><span data-stu-id="ed02a-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="ed02a-204">Successivamente, copiare il file con estensione WAR nella cartella **webapps** di Apache Tomcat nella macchina virtuale e quindi eseguirlo in un browser.</span><span class="sxs-lookup"><span data-stu-id="ed02a-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="ed02a-205">Per impostazione predefinita, quando viene installato, il servizio Tomcat è impostato per l'avvio manuale.</span><span class="sxs-lookup"><span data-stu-id="ed02a-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="ed02a-206">È possibile passare a esso per avviare automaticamente tramite lo snap-in Servizi.</span><span class="sxs-lookup"><span data-stu-id="ed02a-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="ed02a-207">Avviare lo snap-in Servizi facendo clic su **Start di Windows**, **Strumenti di amministrazione**, **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="ed02a-208">Fare doppio clic sul servizio **Apache Tomcat** e impostare **Tipo di avvio** su **Automatico**.</span><span class="sxs-lookup"><span data-stu-id="ed02a-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Impostazione di un servizio per l'avvio automatico][service_automatic_startup]

    <span data-ttu-id="ed02a-210">L'impostazione di Tomcat per l'avvio automatico può risultare utile in quanto in caso di riavvio della macchina virtuale, ad esempio dopo l'installazione di aggiornamenti software che richiedono un riavvio, il servizio verrà riavviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ed02a-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed02a-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed02a-211">Next steps</span></span>
<span data-ttu-id="ed02a-212">Per informazioni su altri servizi, ad esempio Archiviazione, Service Bus e Database SQL di Azure che può essere utile includere nelle applicazioni Java,</span><span class="sxs-lookup"><span data-stu-id="ed02a-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="ed02a-213">fare riferimento alle informazioni disponibili all'indirizzo in [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="ed02a-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
