---
title: applicazione Java con utilizzo intensivo aaaCompute in una macchina virtuale | Documenti Microsoft
description: "Informazioni su come toocreate una macchina virtuale di Azure che esegue un'applicazione Java con utilizzo intensivo di calcolo che può essere monitorata da un'altra applicazione Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="8d313-103">Come attività toorun un uso intensivo di calcolo nel linguaggio in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="8d313-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8d313-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8d313-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8d313-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8d313-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="8d313-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="8d313-107">Con Azure, è possibile utilizzare una macchina virtuale toohandle calcolo intensivo.</span><span class="sxs-lookup"><span data-stu-id="8d313-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="8d313-108">Ad esempio, una macchina virtuale può gestire le attività e recapitare macchine tooclient risultati o applicazioni per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="8d313-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="8d313-109">Dopo aver letto questo articolo, si avrà una conoscenza di come toocreate una macchina virtuale che esegue un'applicazione Java con utilizzo intensivo di calcolo che può essere monitorata da un'altra applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="8d313-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="8d313-110">In questa esercitazione si presuppone che conoscere come applicazioni di console toocreate Java, è possibile importare l'applicazione Java tooyour di librerie e può generare un file Java archive (JAR).</span><span class="sxs-lookup"><span data-stu-id="8d313-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="8d313-111">Non è richiesta alcuna conoscenza di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8d313-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="8d313-112">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d313-112">You will learn:</span></span>

* <span data-ttu-id="8d313-113">Come toocreate una macchina virtuale con Java Development Kit (JDK) già installato.</span><span class="sxs-lookup"><span data-stu-id="8d313-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="8d313-114">Modalità di accesso nella macchina virtuale tooyour tooremotely.</span><span class="sxs-lookup"><span data-stu-id="8d313-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="8d313-115">Come spazio dei nomi del bus toocreate un servizio.</span><span class="sxs-lookup"><span data-stu-id="8d313-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="8d313-116">Come toocreate un'applicazione Java che esegue un'attività a elevato utilizzo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="8d313-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="8d313-117">Toocreate un'applicazione Java che consente di monitorare hello come stato di avanzamento dell'attività a elevato utilizzo di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="8d313-118">Toorun hello come applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="8d313-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="8d313-119">Toostop hello come applicazioni Java.</span><span class="sxs-lookup"><span data-stu-id="8d313-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="8d313-120">In questa esercitazione verrà utilizzato hello problema del commesso viaggiatore per attività complesse hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="8d313-121">Hello Ecco un esempio di hello Java applicazione in esecuzione hello complesse attività.</span><span class="sxs-lookup"><span data-stu-id="8d313-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Risolutore del Problema del commesso viaggiatore][solver_output]

<span data-ttu-id="8d313-123">Hello Ecco un esempio di hello Java applicazione hello complesse l'attività di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="8d313-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Client del Problema del commesso viaggiatore][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="8d313-125">toocreate una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="8d313-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="8d313-126">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8d313-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8d313-127">Fare clic su **Nuovo**, **Calcolo**, **Macchina virtuale** e quindi su **Da raccolta**.</span><span class="sxs-lookup"><span data-stu-id="8d313-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="8d313-128">In hello **selezionare immagine di macchina virtuale** nella finestra di dialogo **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="8d313-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="8d313-129">Si noti che **JDK 6 Windows Server 2012** è disponibile nel caso in cui si dispone di applicazioni legacy che non sono ancora pronti toorun JDK 7.</span><span class="sxs-lookup"><span data-stu-id="8d313-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="8d313-130">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8d313-130">Click **Next**.</span></span>
5. <span data-ttu-id="8d313-131">In hello **configurazione della macchina virtuale** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="8d313-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="8d313-132">Specificare un nome per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="8d313-133">Specificare hello toouse di dimensioni per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="8d313-134">Immettere un nome per l'amministratore di hello in hello **nome utente** campo.</span><span class="sxs-lookup"><span data-stu-id="8d313-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="8d313-135">Prendere nota della password nome e hello che passerà successivamente, verranno utilizzati quando si accede in remoto nella macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="8d313-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="8d313-136">Immettere una password in hello **nuova password** campo e immettere nuovamente in hello **conferma** campo.</span><span class="sxs-lookup"><span data-stu-id="8d313-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="8d313-137">Si tratta di password dell'account amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="8d313-138">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8d313-138">Click **Next**.</span></span>
6. <span data-ttu-id="8d313-139">In hello Avanti **configurazione della macchina virtuale** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="8d313-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="8d313-140">Per **servizio Cloud**, utilizzare hello predefinito **creare un nuovo servizio cloud**.</span><span class="sxs-lookup"><span data-stu-id="8d313-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="8d313-141">valore per Hello **nome DNS del servizio Cloud** deve essere univoco in cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="8d313-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="8d313-142">Se necessario, modificarlo in modo che sia indicato come univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d313-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="8d313-143">Specificare un'area, un gruppo di affinità o una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8d313-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="8d313-144">Ai fini di questa esercitazione, specificare come area **West US**.</span><span class="sxs-lookup"><span data-stu-id="8d313-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="8d313-145">Nella casella **Account di archiviazione** selezionare **Usa un account di archiviazione generato automaticamente** .</span><span class="sxs-lookup"><span data-stu-id="8d313-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="8d313-146">Nella casella **Set di disponibilità** selezionare **(Nessuno)**.</span><span class="sxs-lookup"><span data-stu-id="8d313-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="8d313-147">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="8d313-147">Click **Next**.</span></span>
7. <span data-ttu-id="8d313-148">In hello finale **configurazione della macchina virtuale** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="8d313-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="8d313-149">Accettare le voci di endpoint di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="8d313-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="8d313-150">Fare clic su **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8d313-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="8d313-151">log tooremotely nella macchina virtuale tooyour</span><span class="sxs-lookup"><span data-stu-id="8d313-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="8d313-152">Accesso toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8d313-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8d313-153">Fare clic su **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="8d313-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="8d313-154">Fare clic su nome hello della macchina virtuale hello che si desidera toolog in.</span><span class="sxs-lookup"><span data-stu-id="8d313-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="8d313-155">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="8d313-155">Click **Connect**.</span></span>
5. <span data-ttu-id="8d313-156">Risposta toohello chiede come macchina virtuale di toohello tooconnect necessari.</span><span class="sxs-lookup"><span data-stu-id="8d313-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="8d313-157">Quando viene richiesta la password e il nome amministratore hello, usare valori hello forniti al momento della creazione macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="8d313-158">Si noti che la funzionalità di Azure Service Bus hello richiede toobe di certificato radice Baltimore CyberTrust hello installato come parte di JRE **cacerts** archiviare.</span><span class="sxs-lookup"><span data-stu-id="8d313-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="8d313-159">Questo certificato viene inclusa automaticamente in hello Java Runtime Environment (JRE) utilizzato da questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8d313-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="8d313-160">Se non è il certificato nel JRE **cacerts** archiviare, vedere [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java] [ add_ca_cert] per informazioni sull'aggiunta del modello (così come informazioni sulla visualizzazione di hello certificati nell'archivio cacerts).</span><span class="sxs-lookup"><span data-stu-id="8d313-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="8d313-161">Come spazio dei nomi del bus toocreate un servizio</span><span class="sxs-lookup"><span data-stu-id="8d313-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="8d313-162">utilizzo di Service Bus toobegin le code in Azure, è innanzitutto necessario creare uno spazio dei nomi del servizio.</span><span class="sxs-lookup"><span data-stu-id="8d313-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="8d313-163">che fornisce un contenitore di ambito per fare riferimento alle risorse del bus di servizio all'interno dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d313-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="8d313-164">toocreate uno spazio dei nomi servizio:</span><span class="sxs-lookup"><span data-stu-id="8d313-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="8d313-165">Accesso toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8d313-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="8d313-166">Nel riquadro di navigazione a sinistra hello di hello portale di Azure classico, fare clic su **Service Bus, Access Control e la memorizzazione nella cache**.</span><span class="sxs-lookup"><span data-stu-id="8d313-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="8d313-167">Nel riquadro superiore sinistro di hello di hello portale di Azure classico, fare clic su hello **Bus di servizio** nodo, quindi fare clic su hello **New** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8d313-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="8d313-168">![Schermata nodo bus di servizio][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="8d313-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="8d313-169">In hello **creare un nuovo Namespace servizio** finestra di dialogo immettere un **Namespace**, e quindi assicurarsi che sia univoco, toomake il **verifica disponibilità** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8d313-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="8d313-170">![Schermata Create a New Namespace][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="8d313-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="8d313-171">Dopo aver verificato il nome di spazio dei nomi hello è disponibile, scegliere il paese o regione in cui deve essere ospitato lo spazio dei nomi e quindi fare clic su hello **creare Namespace** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8d313-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="8d313-172">spazio dei nomi di Hello creato verrà visualizzato nel portale di Azure classico hello e accetta un tooactivate momento.</span><span class="sxs-lookup"><span data-stu-id="8d313-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="8d313-173">Attendere fino a quando non è stato hello **Active** prima di procedere al passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="8d313-174">Ottenere hello predefinito le credenziali di gestione per lo spazio dei nomi hello</span><span class="sxs-lookup"><span data-stu-id="8d313-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="8d313-175">Nelle operazioni di gestione tooperform ordine, ad esempio la creazione di una coda, in hello nuovo spazio dei nomi, sono necessarie le credenziali di gestione di tooobtain hello per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8d313-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="8d313-176">Nel riquadro di spostamento a sinistra di hello, fare clic su hello **Bus di servizio** nodo per visualizzare l'elenco di hello degli spazi dei nomi disponibili.</span><span class="sxs-lookup"><span data-stu-id="8d313-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="8d313-177">![Schermata relativa agli spazi dei nomi disponibili][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="8d313-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="8d313-178">Selezionare lo spazio dei nomi hello che appena create dall'elenco di hello illustrato.</span><span class="sxs-lookup"><span data-stu-id="8d313-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="8d313-179">![Schermata relativa all'elenco degli spazi dei nomi][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="8d313-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="8d313-180">Hello destro **proprietà** riquadro contiene proprietà hello per il nuovo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8d313-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="8d313-181">![Schermata pannello Proprietà][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="8d313-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="8d313-182">Hello **chiave predefinita** è nascosto.</span><span class="sxs-lookup"><span data-stu-id="8d313-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="8d313-183">Fare clic su hello **vista** pulsante credenziali di sicurezza toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="8d313-184">![Schermata Default Key][default_key]</span><span class="sxs-lookup"><span data-stu-id="8d313-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="8d313-185">Prendere nota di hello **autorità di certificazione predefinita** hello e **chiave predefinita** come utilizzare queste informazioni di sotto di tooperform operazioni con lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8d313-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="8d313-186">Come toocreate un'applicazione Java che esegue un'attività a elevato utilizzo di calcolo</span><span class="sxs-lookup"><span data-stu-id="8d313-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="8d313-187">Nel computer di sviluppo (che non dispone di macchina virtuale di hello toobe creato), download hello [Azure SDK per Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="8d313-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="8d313-188">Creare un'applicazione console Java mediante il codice di esempio hello alla fine di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="8d313-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="8d313-189">In questa esercitazione si userà **TSPSolver.java** come nome del file hello Java.</span><span class="sxs-lookup"><span data-stu-id="8d313-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="8d313-190">Modificare hello **il\_servizio\_bus\_dello spazio dei nomi**, **il\_servizio\_bus\_proprietario**e **il\_servizio\_bus\_chiave** toouse segnaposto del bus di servizio **dello spazio dei nomi**, **autorità di certificazione predefinita** e  **Chiave predefinita** rispettivamente i valori.</span><span class="sxs-lookup"><span data-stu-id="8d313-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="8d313-191">Dopo la generazione di codice, esportazione hello applicazione tooa eseguibile Java archive (JAR) hello pacchetto necessari e librerie in hello generato JAR.</span><span class="sxs-lookup"><span data-stu-id="8d313-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="8d313-192">In questa esercitazione si userà **TSPSolver.jar** come nome di file JAR hello generato.</span><span class="sxs-lookup"><span data-stu-id="8d313-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="8d313-193">Come un'applicazione Java che esegue il monitoraggio toocreate hello lo stato di avanzamento dell'attività complesse hello</span><span class="sxs-lookup"><span data-stu-id="8d313-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="8d313-194">Nel computer di sviluppo, creare un'applicazione console Java mediante il codice di esempio hello alla fine di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="8d313-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="8d313-195">In questa esercitazione si userà **TSPClient.java** come nome del file hello Java.</span><span class="sxs-lookup"><span data-stu-id="8d313-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="8d313-196">Come illustrato in precedenza, modificare hello **il\_servizio\_bus\_dello spazio dei nomi**, **il\_servizio\_bus\_proprietario**, e **il\_servizio\_bus\_chiave** toouse segnaposto del bus di servizio **dello spazio dei nomi**, **autorità di certificazione predefinita**e **chiave predefinita** rispettivamente i valori.</span><span class="sxs-lookup"><span data-stu-id="8d313-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="8d313-197">Esportare tooa applicazione hello JAR eseguibili, hello pacchetto è necessario e librerie in hello generato JAR.</span><span class="sxs-lookup"><span data-stu-id="8d313-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="8d313-198">In questa esercitazione si userà **TSPClient.jar** come nome di file JAR hello generato.</span><span class="sxs-lookup"><span data-stu-id="8d313-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="8d313-199">Come toorun hello applicazioni Java</span><span class="sxs-lookup"><span data-stu-id="8d313-199">How toorun hello Java applications</span></span>
<span data-ttu-id="8d313-200">Eseguire un'applicazione hello complesse, prima coda di hello toocreate quindi toosolve hello in viaggio Saleseman problema, che aggiungerà hello corrente migliore route toohello coda di service bus.</span><span class="sxs-lookup"><span data-stu-id="8d313-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="8d313-201">Hello durante l'applicazione con utilizzo intensivo di calcolo è in esecuzione o in un secondo momento, risultati di esecuzione hello client toodisplay dalla coda di service bus hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="8d313-202">applicazione hello complesse toorun</span><span class="sxs-lookup"><span data-stu-id="8d313-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="8d313-203">Accedere a macchina virtuale tooyour.</span><span class="sxs-lookup"><span data-stu-id="8d313-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="8d313-204">Creare una cartella in cui eseguire l'applicazione,</span><span class="sxs-lookup"><span data-stu-id="8d313-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="8d313-205">ad esempio **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="8d313-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="8d313-206">Copia **TSPSolver.jar** troppo**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="8d313-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="8d313-207">Creare un file denominato **c:\TSP\cities.txt** con hello seguente contenuto.</span><span class="sxs-lookup"><span data-stu-id="8d313-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="8d313-208">Al prompt dei comandi, modificare le directory tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="8d313-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="8d313-209">Verificare che nella cartella bin di JRE hello sia nella variabile di ambiente PATH hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="8d313-210">Coda del bus di servizio toocreate hello è necessario prima di eseguire le permutazioni Risolutore di hello problema del commesso Viaggiatore.</span><span class="sxs-lookup"><span data-stu-id="8d313-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="8d313-211">Comando che segue di hello esecuzione coda toocreate hello service bus.</span><span class="sxs-lookup"><span data-stu-id="8d313-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="8d313-212">Dopo aver creato hello coda, è possibile eseguire le permutazioni Risolutore di hello problema del commesso Viaggiatore.</span><span class="sxs-lookup"><span data-stu-id="8d313-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="8d313-213">Ad esempio, eseguire hello seguendo il Risolutore di comando toorun hello per le 8 città.</span><span class="sxs-lookup"><span data-stu-id="8d313-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="8d313-214">Se non si specifica un numero, il risolutore verrà eseguito per 10 città.</span><span class="sxs-lookup"><span data-stu-id="8d313-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="8d313-215">Come Risolutore di hello rileva route più brevi corrente, li aggiunge toohello coda.</span><span class="sxs-lookup"><span data-stu-id="8d313-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="8d313-216">Hello maggiore hello numero specificato, verrà eseguito il Risolutore di hello più hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="8d313-217">Ad esempio, l'esecuzione per 14 città potrebbe richiedere diversi minuti, mentre l'esecuzione per 15 città potrebbe richiedere parecchie ore.</span><span class="sxs-lookup"><span data-stu-id="8d313-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="8d313-218">Giorni di runtime (infine settimane, mesi e anni) potrebbe causare aumentando too16 o più città.</span><span class="sxs-lookup"><span data-stu-id="8d313-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="8d313-219">Ciò è dovuto toohello rapido aumento hello numero di permutazioni ritenuti dal Risolutore di hello hello aumentare del numero di città.</span><span class="sxs-lookup"><span data-stu-id="8d313-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="8d313-220">Come toorun hello monitoraggio dell'applicazione client</span><span class="sxs-lookup"><span data-stu-id="8d313-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="8d313-221">Accedere tooyour macchina in cui si eseguirà l'applicazione client hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="8d313-222">Non è necessario toobe hello stesso computer che esegue hello **TSPSolver** un'applicazione, sebbene possa essere.</span><span class="sxs-lookup"><span data-stu-id="8d313-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="8d313-223">Creare una cartella in cui eseguire l'applicazione,</span><span class="sxs-lookup"><span data-stu-id="8d313-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="8d313-224">ad esempio **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="8d313-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="8d313-225">Copia **TSPClient.jar** troppo**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="8d313-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="8d313-226">Verificare che nella cartella bin di JRE hello sia nella variabile di ambiente PATH hello.</span><span class="sxs-lookup"><span data-stu-id="8d313-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="8d313-227">Al prompt dei comandi, modificare le directory tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="8d313-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="8d313-228">Eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8d313-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="8d313-229">Facoltativamente, specificare il numero di hello di toosleep minuti tra il controllo coda hello, passando un argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8d313-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="8d313-230">Hello sospensione periodo predefinito per il controllo coda hello è 3 minuti, che viene utilizzato se nessun argomento della riga di comando è passato troppo**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="8d313-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="8d313-231">Se si desidera toouse un valore diverso per intervallo di inattività hello, ad esempio, un minuto, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="8d313-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="8d313-232">Hello client verrà eseguito finché riceve un messaggio nella coda di "Completa".</span><span class="sxs-lookup"><span data-stu-id="8d313-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="8d313-233">Si noti che se si eseguono più occorrenze di Risolutore di hello senza eseguire il client di hello, potrebbe essere necessario client hello toorun coda vuota hello di toocompletely più volte.</span><span class="sxs-lookup"><span data-stu-id="8d313-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="8d313-234">In alternativa, è possibile eliminare la coda hello e quindi crearlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="8d313-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="8d313-235">coda di hello toodelete, eseguire il seguente hello **TSPSolver** (non **TSPClient**) comando.</span><span class="sxs-lookup"><span data-stu-id="8d313-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="8d313-236">Risolutore di Hello verrà eseguito fino al termine dell'analisi di tutte le route.</span><span class="sxs-lookup"><span data-stu-id="8d313-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="8d313-237">Come toostop hello applicazioni Java</span><span class="sxs-lookup"><span data-stu-id="8d313-237">How toostop hello Java applications</span></span>
<span data-ttu-id="8d313-238">Risolutore di hello e nelle applicazioni client, è possibile premere **Ctrl + C** tooexit se si desidera tooend toonormal precedente completamento.</span><span class="sxs-lookup"><span data-stu-id="8d313-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
