---
title: aaaSet backup Apache Tomcat in una macchina virtuale Linux | Documenti Microsoft
description: Informazioni su come tooset backup Tomcat7 Apache tramite le macchine virtuali di Azure che eseguono Linux.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="e3693-103">Configurare Tomcat7 in una macchina virtuale Linux con Azure</span><span class="sxs-lookup"><span data-stu-id="e3693-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="e3693-104">Apache Tomcat (o semplicemente Tomcat, anche in precedenza denominato Tomcat Giacarta) è un server web di origine aperti e il contenitore servlet sviluppato da hello Apache Software Foundation ASF ().</span><span class="sxs-lookup"><span data-stu-id="e3693-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="e3693-105">Tomcat implementa hello Servlet Java e le specifiche Java Server Pages (JSP) hello di Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="e3693-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="e3693-106">Tomcat fornisce un ambiente di server web HTTP Java puro in cui toorun codice Java.</span><span class="sxs-lookup"><span data-stu-id="e3693-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="e3693-107">In configurazione più semplice hello Tomcat viene eseguito in un processo unico sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e3693-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="e3693-108">Questo processo esegue una macchina virtuale Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="e3693-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="e3693-109">Ogni richiesta HTTP da un browser di tooTomcat viene elaborato come un thread separato nel processo di Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e3693-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e3693-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e3693-111">Questo articolo descrive come toouse hello modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e3693-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="e3693-112">È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e3693-113">vedere toouse toodeploy di modello un VM Ubuntu con Open JDK e Tomcat, un gestore delle risorse [questo articolo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="e3693-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="e3693-114">In questo articolo si installerà Tomcat7 su un'immagine Linux e la si distribuirà in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3693-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="e3693-115">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3693-115">You will learn:</span></span>  

* <span data-ttu-id="e3693-116">Come toocreate una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3693-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="e3693-117">Tooprepare hello come macchina virtuale per Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="e3693-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="e3693-118">Come tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="e3693-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="e3693-119">La procedura presuppone che l'utente disponga già di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3693-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="e3693-120">Se non è possibile iscriversi per una valutazione gratuita in [hello sito Web di Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="e3693-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="e3693-121">Se si ha un abbonamento MSDN, vedere [Offerte speciali di Microsoft Azure: vantaggi per i membri di MSDN, MPN e Bizspark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="e3693-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="e3693-122">toolearn ulteriori informazioni su Azure, vedere [cos'è Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="e3693-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="e3693-123">Questo articolo presuppone che l'utente abbia una conoscenza pratica di base di Tomcat e Linux.</span><span class="sxs-lookup"><span data-stu-id="e3693-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="e3693-124">Fase 1: creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="e3693-124">Phase 1: Create an image</span></span>
<span data-ttu-id="e3693-125">In questa fase si creerà una macchina virtuale usando un'immagine Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3693-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="e3693-126">Passaggio 1: generare una chiave di autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="e3693-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="e3693-127">SSH è uno strumento importante per gli amministratori di sistema.</span><span class="sxs-lookup"><span data-stu-id="e3693-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="e3693-128">Non è consigliabile tuttavia configurare la protezione di accesso in base a una password stabilita da una persona fisica.</span><span class="sxs-lookup"><span data-stu-id="e3693-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="e3693-129">Con un nome utente e una password debole, il sistema può essere esposto all'attacco da parte di utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="e3693-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="e3693-130">buone notizie Hello sono che non esiste un modo tooleave di accesso remoto aprire senza doversi preoccupare delle password.</span><span class="sxs-lookup"><span data-stu-id="e3693-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="e3693-131">Il metodo consiste nell'autenticazione con crittografia asimmetrica.</span><span class="sxs-lookup"><span data-stu-id="e3693-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="e3693-132">Hello chiave privata dell'utente è hello uno che consente l'autenticazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="e3693-133">È anche possibile bloccare hello account utente toonot consentire l'autenticazione di password.</span><span class="sxs-lookup"><span data-stu-id="e3693-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="e3693-134">Un altro vantaggio di questo metodo è che non è necessario toosign password diverse toodifferent server.</span><span class="sxs-lookup"><span data-stu-id="e3693-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="e3693-135">È possibile eseguire l'autenticazione usando la chiave privata personale hello in tutti i server, che consente di evitare tooremember password diversi.</span><span class="sxs-lookup"><span data-stu-id="e3693-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="e3693-136">Seguire questi passaggi toogenerate hello autenticazione la chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="e3693-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="e3693-137">Scaricare e installare PuTTYgen dalla seguente posizione hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="e3693-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="e3693-138">Eseguire Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="e3693-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="e3693-139">Fare clic su **genera** chiavi hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="e3693-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="e3693-140">Nel processo di hello, è possibile aumentare la casualità per lo spostamento del mouse hello sull'area vuota di hello nella finestra di hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="e3693-141">![PuTTY schermata generatore di chiavi che mostra hello generare di nuovo pulsante chiave][1]</span><span class="sxs-lookup"><span data-stu-id="e3693-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="e3693-142">Dopo aver hello genera processo, Puttygen.exe mostrerà la nuova chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="e3693-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Schermata di generatore di chiavi puTTY che mostra nuova chiave pubblica hello e hello salvare pulsante chiave privata][2]
5. <span data-ttu-id="e3693-144">Selezionare e copiare la chiave pubblica di hello e salvarlo in un file denominato publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="e3693-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="e3693-145">Non fare clic su **Salva la chiave pubblica**, poiché hello salvato il formato di file della chiave pubblica è diversa dalla chiave pubblica di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e3693-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="e3693-146">Fare clic su **Save private key** e salvarla in un file denominato privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="e3693-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="e3693-147">Passaggio 2: Creare l'immagine di hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3693-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="e3693-148">In hello [portale](https://portal.azure.com/), fare clic su **New** nel hello attività barra toocreate un'immagine.</span><span class="sxs-lookup"><span data-stu-id="e3693-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="e3693-149">Scegliere l'immagine Linux hello che è in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="e3693-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="e3693-150">Hello esempio seguente Usa immagine Ubuntu 14.04 hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="e3693-151">![Schermata del portale hello che mostra il pulsante nuovo hello][3]</span><span class="sxs-lookup"><span data-stu-id="e3693-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="e3693-152">Per **nome Host**, specificare nome hello URL hello che i client Internet dovranno essere utilizzate dalle tooaccess questa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3693-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="e3693-153">Definire l'ultima parte di hello del nome DNS hello, ad esempio, tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="e3693-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="e3693-154">Azure genera quindi l'URL di hello come tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e3693-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="e3693-155">Per **chiave di autenticazione SSH**, copiarne il valore della chiave hello file publicKey.pem hello che contiene la chiave pubblica hello generata da PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="e3693-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="e3693-156">![Chiave di autenticazione SSH casella nel portale di hello][4]</span><span class="sxs-lookup"><span data-stu-id="e3693-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="e3693-157">Configurare altre impostazioni in base alle esigenze, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e3693-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="e3693-158">Fase 2: preparare la macchina virtuale per Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="e3693-159">In questa fase, si configura un endpoint per il traffico di Tomcat e connettiti tooyour nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3693-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="e3693-160">Passaggio 1: Aprire hello HTTP porta tooallow web access</span><span class="sxs-lookup"><span data-stu-id="e3693-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="e3693-161">Gli endpoint di Azure sono costituiti da un protocollo TCP o UDP, insieme a una porta pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="e3693-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="e3693-162">porta privata Hello è porta hello che hello servizio è in ascolto macchina virtuale di tooon hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="e3693-163">porta pubblica Hello è porta hello hello servizio cloud di Azure è in ascolto tooexternally per il traffico in ingresso, basato su Internet.</span><span class="sxs-lookup"><span data-stu-id="e3693-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="e3693-164">La porta TCP 8080 è numero di porta predefinito hello Tomcat utilizzato toolisten.</span><span class="sxs-lookup"><span data-stu-id="e3693-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="e3693-165">Se si apre questa porta con un endpoint di Azure, l'utente e altri client Internet potranno accedere alle pagine Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="e3693-166">Nel portale di hello, fare clic su **Sfoglia** > **macchine virtuali**, quindi fare clic su hello macchina virtuale in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e3693-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="e3693-167">![Schermata della directory di hello macchine virtuali][5]</span><span class="sxs-lookup"><span data-stu-id="e3693-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="e3693-168">tooadd una macchina virtuale tooyour endpoint, fare clic su hello **endpoint** casella.</span><span class="sxs-lookup"><span data-stu-id="e3693-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="e3693-169">![Schermata che Mostra casella endpoint hello][6]</span><span class="sxs-lookup"><span data-stu-id="e3693-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="e3693-170">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e3693-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="e3693-171">Per l'endpoint di hello, immettere un nome per l'endpoint hello **Endpoint**, quindi immettere 80 in **porta pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e3693-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="e3693-172">Se si imposta la proprietà too80, non è necessario tooinclude numero di porta hello in URL hello utilizzati tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="e3693-173">Ad esempio, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e3693-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="e3693-174">Se si imposta il valore di tooanother, ad esempio 81, è necessario tooadd hello porta numero toohello URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="e3693-175">Ad esempio http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="e3693-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="e3693-176">Digitare 8080 in **Porta privata**.</span><span class="sxs-lookup"><span data-stu-id="e3693-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="e3693-177">Per impostazione predefinita Tomcat è in ascolto sulla porta TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="e3693-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="e3693-178">Se è stata modificata hello predefinito ascolto porta di Tomcat, è necessario aggiornare **porta privata** toobe hello stesso hello porta di ascolto Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="e3693-179">![Schermata dell'interfaccia utente che mostra il comando Aggiungi, Porta pubblica e Porta privata][7]</span><span class="sxs-lookup"><span data-stu-id="e3693-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="e3693-180">Fare clic su **OK** la macchina virtuale tooadd hello endpoint tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3693-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="e3693-181">Passaggio 2: Connettere immagine toohello creato</span><span class="sxs-lookup"><span data-stu-id="e3693-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="e3693-182">È possibile scegliere qualsiasi macchina virtuale SSH strumento tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3693-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="e3693-183">In questo esempio viene usato PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e3693-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="e3693-184">Ottenere il nome DNS hello della macchina virtuale dal portale di hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="e3693-185">Fare clic su **Sfoglia** > **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="e3693-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="e3693-186">Selezionare il nome di hello della macchina virtuale e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="e3693-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="e3693-187">In hello **proprietà** riquadro, cercare in hello **nome di dominio** nome DNS della casella tooget hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="e3693-188">Ottenere il numero di porta hello per le connessioni SSH da hello **SSH** casella.</span><span class="sxs-lookup"><span data-stu-id="e3693-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="e3693-189">![Schermata che mostra i numero di porta di connessione SSH hello][8]</span><span class="sxs-lookup"><span data-stu-id="e3693-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="e3693-190">Scaricare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="e3693-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="e3693-191">Dopo il download, fare clic sul file eseguibile hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="e3693-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="e3693-192">Configurazione PuTTY, configurare le opzioni di base hello con il nome host hello e il numero ottenuto dalla proprietà hello della macchina virtuale porta.</span><span class="sxs-lookup"><span data-stu-id="e3693-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Schermata che mostra l'host di configurazione di PuTTY hello opzioni di nome e la porte][9]

5. <span data-ttu-id="e3693-194">Nel riquadro di sinistra hello, fare clic su **connessione** > **SSH** > **Auth**, quindi fare clic su **Sfoglia** toospecify percorso di Hello del file di privateKey.ppk hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="e3693-195">file privateKey.ppk Hello contiene la chiave privata hello generato da PuTTYgen in hello "fase 1: creare un'immagine" sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e3693-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="e3693-196">![Schermata che illustra una gerarchia di directory hello connessione e il pulsante Sfoglia][10]</span><span class="sxs-lookup"><span data-stu-id="e3693-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="e3693-197">Fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="e3693-197">Click **Open**.</span></span> <span data-ttu-id="e3693-198">Si potrebbe ricevere un avviso da una finestra di messaggio.</span><span class="sxs-lookup"><span data-stu-id="e3693-198">You might be alerted by a message box.</span></span> <span data-ttu-id="e3693-199">Se è stato configurato il nome DNS hello e il numero di porta corretto, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="e3693-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="e3693-200">![Schermata che illustra la notifica hello][11]</span><span class="sxs-lookup"><span data-stu-id="e3693-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="e3693-201">Si sono tooenter richiesto il nome utente.</span><span class="sxs-lookup"><span data-stu-id="e3693-201">You are prompted tooenter your username.</span></span>  
![Schermata che mostra dove nome utente tooenter][12]

8. <span data-ttu-id="e3693-203">Immettere un nome utente hello utilizzato macchina virtuale di toocreate hello in hello "fase 1: creare un'immagine" sezione più indietro in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e3693-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="e3693-204">Si noterà simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e3693-204">You will see something like hello following:</span></span>  
![Schermata che Mostra conferma authentication hello][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="e3693-206">Fase 3: installare il software</span><span class="sxs-lookup"><span data-stu-id="e3693-206">Phase 3: Install software</span></span>
<span data-ttu-id="e3693-207">In questa fase, installare Java runtime environment di hello Tomcat7 e altri componenti Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="e3693-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="e3693-208">Ambiente di runtime Java</span><span class="sxs-lookup"><span data-stu-id="e3693-208">Java runtime environment</span></span>
<span data-ttu-id="e3693-209">Tomcat è scritto in Java.</span><span class="sxs-lookup"><span data-stu-id="e3693-209">Tomcat is written in Java.</span></span> <span data-ttu-id="e3693-210">Esistono due tipi di Java Development Kit (JDK): OpenJDK e Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="e3693-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="e3693-211">È possibile scegliere hello quello desiderato.</span><span class="sxs-lookup"><span data-stu-id="e3693-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="e3693-212">Sia JDK sono quasi hello stesso codice per le classi hello hello API Java, ma il codice hello per la macchina virtuale hello è diverso.</span><span class="sxs-lookup"><span data-stu-id="e3693-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="e3693-213">OpenJDK tende librerie aperte toouse, mentre tende Oracle JDK toouse chiuso quelle.</span><span class="sxs-lookup"><span data-stu-id="e3693-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="e3693-214">Oracle JDK dispone di più classi e include alcuni bug corretti, inoltre è più stabile di OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="e3693-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="e3693-215">Installare OpenJDK</span><span class="sxs-lookup"><span data-stu-id="e3693-215">Install OpenJDK</span></span>  

<span data-ttu-id="e3693-216">Comando che segue di hello utilizzare toodownload OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="e3693-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="e3693-217">toocreate toocontain una directory hello file JDK:</span><span class="sxs-lookup"><span data-stu-id="e3693-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="e3693-218">file JDK tooextract hello in hello usr/lib/jvm/directory:</span><span class="sxs-lookup"><span data-stu-id="e3693-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="e3693-219">Installare Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="e3693-219">Install Oracle JDK</span></span>


<span data-ttu-id="e3693-220">Utilizzare hello seguente toodownload comando Oracle JDK dal sito Web Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="e3693-221">toocreate toocontain una directory hello file JDK:</span><span class="sxs-lookup"><span data-stu-id="e3693-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="e3693-222">file JDK tooextract hello in hello usr/lib/jvm/directory:</span><span class="sxs-lookup"><span data-stu-id="e3693-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="e3693-223">tooset Oracle JDK come hello predefinito Java virtual machine:</span><span class="sxs-lookup"><span data-stu-id="e3693-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="e3693-224">Verificare che l'installazione di Java sia riuscita</span><span class="sxs-lookup"><span data-stu-id="e3693-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="e3693-225">È possibile utilizzare un comando simile hello seguente tootest se hello Java runtime environment sia installato correttamente:</span><span class="sxs-lookup"><span data-stu-id="e3693-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="e3693-226">Se è installato OpenJDK, si verrà visualizzato un messaggio hello seguente: ![messaggio di installazione ha esito positivo OpenJDK][14]</span><span class="sxs-lookup"><span data-stu-id="e3693-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="e3693-227">Se è installato Oracle JDK, si verrà visualizzato un messaggio hello seguente: ![messaggio di installazione ha esito positivo Oracle JDK][15]</span><span class="sxs-lookup"><span data-stu-id="e3693-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="e3693-228">Installare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-228">Install Tomcat7</span></span>
<span data-ttu-id="e3693-229">Utilizzare hello successivo comando tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="e3693-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="e3693-230">Se non si utilizza Tomcat7, utilizzare la variante appropriata di hello di questo comando.</span><span class="sxs-lookup"><span data-stu-id="e3693-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="e3693-231">Verificare che l'installazione di Tomcat7 sia riuscita</span><span class="sxs-lookup"><span data-stu-id="e3693-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="e3693-232">Se è stata installata Tomcat7, toocheck Sfoglia nome DNS del server Tomcat tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3693-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="e3693-233">In questo articolo, l'URL di esempio hello è http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="e3693-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="e3693-234">Se viene visualizzato un messaggio hello seguente, Tomcat7 sia installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e3693-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="e3693-235">![Messaggio con l'avviso che l'installazione di Tomcat7 è riuscita][16]</span><span class="sxs-lookup"><span data-stu-id="e3693-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="e3693-236">Installare altri componenti di Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="e3693-237">Esistono altri componenti facoltativi di Tomcat che è possibile installare.</span><span class="sxs-lookup"><span data-stu-id="e3693-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="e3693-238">Hello utilizzare **sudo apt della cache di ricerca tomcat7** toosee comando tutti i componenti disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="e3693-239">Utilizzare hello comandi che seguono tooinstall alcuni componenti utili.</span><span class="sxs-lookup"><span data-stu-id="e3693-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="e3693-240">Fase 4: configurare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="e3693-241">In questa fase si amministra Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="e3693-242">Avviare e arrestare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="e3693-243">Hello Tomcat7 avviata automaticamente durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="e3693-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="e3693-244">È inoltre possibile avviare con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e3693-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="e3693-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="e3693-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="e3693-246">stato di hello tooview di Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="e3693-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="e3693-247">servizi di Tomcat toorestart:</span><span class="sxs-lookup"><span data-stu-id="e3693-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="e3693-248">Amministrazione di Tomcat7</span><span class="sxs-lookup"><span data-stu-id="e3693-248">Tomcat7 administration</span></span>
<span data-ttu-id="e3693-249">È possibile modificare hello Tomcat utente configurazione file tooset backup le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="e3693-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="e3693-250">Utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e3693-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="e3693-251">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="e3693-251">Here is an example:</span></span>  
![Schermata che mostra l'output del comando vi hello sudo][17]  

> [!NOTE]
> <span data-ttu-id="e3693-253">Creare una password complessa per nome utente amministratore hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="e3693-254">Dopo avere modificato questo file, è necessario riavviare servizi Tomcat7 con hello comando tooensure che le modifiche di hello abbiano l'effetto seguente:</span><span class="sxs-lookup"><span data-stu-id="e3693-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="e3693-255">Aprire il browser e immettere **http://<your tomcat server DNS name>manager/html** come hello URL.</span><span class="sxs-lookup"><span data-stu-id="e3693-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="e3693-256">Ad esempio hello in questo articolo, l'URL hello è http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="e3693-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="e3693-257">Dopo la connessione, verrà visualizzato un codice simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3693-257">After connecting, you should see something similar toohello following:</span></span>  
![Schermata di gestione di applicazioni Web Tomcat hello][18]

## <a name="common-issues"></a><span data-ttu-id="e3693-259">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="e3693-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="e3693-260">Non è possibile accedere a hello la macchina virtuale con Tomcat e Moodle hello Internet</span><span class="sxs-lookup"><span data-stu-id="e3693-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="e3693-261">Sintomo</span><span class="sxs-lookup"><span data-stu-id="e3693-261">Symptom</span></span>  
  <span data-ttu-id="e3693-262">Tomcat è in esecuzione ma non è possibile visualizzare pagina predefinita di Tomcat hello con il browser.</span><span class="sxs-lookup"><span data-stu-id="e3693-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="e3693-263">Possibile causa principale</span><span class="sxs-lookup"><span data-stu-id="e3693-263">Possible root cause</span></span>   

  * <span data-ttu-id="e3693-264">porta di ascolto Hello Tomcat non è hello come porta privata di hello dell'endpoint della macchina virtuale per il traffico di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="e3693-265">Controllare la porta pubblica e privata endpoint impostazioni porta e verificare la porta privata hello è hello uguali a quelli di Tomcat hello porta di ascolto.</span><span class="sxs-lookup"><span data-stu-id="e3693-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="e3693-266">Per istruzioni sulla configurazione degli endpoint per la macchina virtuale vedere la sezione di questo articolo "Fase 1: creare un'immagine".</span><span class="sxs-lookup"><span data-stu-id="e3693-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="e3693-267">hello toodetermine Tomcat porta di ascolto, aprire /etc/httpd/conf/httpd.conf (Red Hat versione) o /etc/tomcat7/server.xml (Debian versione).</span><span class="sxs-lookup"><span data-stu-id="e3693-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="e3693-268">Per impostazione predefinita, la porta di ascolto Tomcat hello è 8080.</span><span class="sxs-lookup"><span data-stu-id="e3693-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="e3693-269">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="e3693-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="e3693-270">Se si utilizza una macchina virtuale come Debian o Ubuntu e si desidera toochange hello predefinito porta di Tomcat ascolto (ad esempio 8081), è necessario aprire anche la porta hello per sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="e3693-271">Prima di tutto, aprire il profilo di hello:</span><span class="sxs-lookup"><span data-stu-id="e3693-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="e3693-272">Quindi rimuovere l'ultima riga hello e modificare "no" troppo "yes".</span><span class="sxs-lookup"><span data-stu-id="e3693-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="e3693-273">firewall Hello è disabilitato hello porta di ascolto di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="e3693-274">È possibile visualizzare solo pagina predefinita di Tomcat hello dall'host locale hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="e3693-275">problema di Hello è molto probabile che la porta hello, vale a dire ascoltato tooby Tomcat, è bloccata da firewall hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="e3693-276">È possibile utilizzare la pagina hello hello w3m strumento toobrowse.</span><span class="sxs-lookup"><span data-stu-id="e3693-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="e3693-277">Hello seguenti comandi installare w3m e passare pagina predefinita di Tomcat toohello:</span><span class="sxs-lookup"><span data-stu-id="e3693-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="e3693-278">sudo yum install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="e3693-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="e3693-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="e3693-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="e3693-280">Soluzione</span><span class="sxs-lookup"><span data-stu-id="e3693-280">Solution</span></span>

  * <span data-ttu-id="e3693-281">Se la porta di ascolto Tomcat hello è non hello stesso come porta privata di hello dell'endpoint hello per la macchina virtuale di traffico toohello, è necessario modificare la porta privata hello toobe hello stesso hello porta di ascolto Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e3693-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="e3693-282">Se il problema di hello è determinato dal firewall/iptables, aggiungere hello seguenti righe troppo/ecc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="e3693-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="e3693-283">seconda riga Hello è necessaria solo per il traffico https:</span><span class="sxs-lookup"><span data-stu-id="e3693-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="e3693-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="e3693-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="e3693-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="e3693-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="e3693-286">Verificare che le righe precedenti hello vengono posizionate sopra tutte le righe che verrebbero globale limitare l'accesso, come illustrato di seguito hello: - A -j REJECT - rifiuto-con icmp-host-consentito di INPUT</span><span class="sxs-lookup"><span data-stu-id="e3693-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="e3693-287">tooreload hello iptables, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e3693-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="e3693-288">Questa installazione è stata effettuata su CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="e3693-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="e3693-289">Autorizzazione negata quando si carica progetto file troppo/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="e3693-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="e3693-290">Sintomo</span><span class="sxs-lookup"><span data-stu-id="e3693-290">Symptom</span></span>
  <span data-ttu-id="e3693-291">Quando si usa una macchina virtuale SFTP client (ad esempio FileZilla) tooconnect tooyour e passare troppo/var/lib/tomcat7/webapps/toopublish del sito, verrà un errore messaggio simili toohello segue:</span><span class="sxs-lookup"><span data-stu-id="e3693-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="e3693-292">Possibile causa principale</span><span class="sxs-lookup"><span data-stu-id="e3693-292">Possible root cause</span></span>
  <span data-ttu-id="e3693-293">È non presente alcuna cartella di /var/lib/tomcat7/webapps hello tooaccess autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="e3693-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="e3693-294">Soluzione</span><span class="sxs-lookup"><span data-stu-id="e3693-294">Solution</span></span>  
  <span data-ttu-id="e3693-295">Sono necessarie autorizzazioni tooget dall'account radice hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="e3693-296">È possibile modificare la proprietà hello della cartella dal nome utente toohello radice utilizzato quando è stato effettuato il provisioning macchina hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="e3693-297">Di seguito è riportato un esempio con il nome di account azureuser hello:</span><span class="sxs-lookup"><span data-stu-id="e3693-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="e3693-298">Utilizzare autorizzazioni hello di hello -R opzione tooapply anche per tutti i file all'interno di una directory.</span><span class="sxs-lookup"><span data-stu-id="e3693-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="e3693-299">Questo comando funziona anche per le directory.</span><span class="sxs-lookup"><span data-stu-id="e3693-299">This command also works for directories.</span></span> <span data-ttu-id="e3693-300">le modifiche all'opzione -R Hello salve le autorizzazioni per tutti i file e directory all'interno della directory hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="e3693-301">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="e3693-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="e3693-302">Questo comando modifica la proprietà (utente e gruppo) per tutti i file e directory che sono all'interno della directory hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="e3693-303">Hello comando seguente cambia solo autorizzazione hello di directory della cartella hello.</span><span class="sxs-lookup"><span data-stu-id="e3693-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="e3693-304">Hello file e cartelle all'interno della directory hello non vengono modificate.</span><span class="sxs-lookup"><span data-stu-id="e3693-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
