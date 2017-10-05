---
title: Configurare Apache Tomcat su una macchina virtuale Linux | Documentazione Microsoft
description: Informazioni su come configurare Apache Tomcat7 usando macchine virtuali di Azure che eseguono Linux.
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
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="c2d2a-103">Configurare Tomcat7 in una macchina virtuale Linux con Azure</span><span class="sxs-lookup"><span data-stu-id="c2d2a-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="c2d2a-104">Apache Tomcat (o semplicemente Tomcat, precedentemente chiamato anche Jakarta Tomcat) è un server Web e contenitore di servlet open source sviluppato da Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="c2d2a-105">Tomcat implementa le specifiche Java Servlet e Java Server Pages (JSP) di Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="c2d2a-106">Tomcat fornisce un ambiente server Web HTTP Java puro in cui eseguire codice Java.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="c2d2a-107">Nella configurazione più semplice, Tomcat viene eseguito in un singolo processo del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="c2d2a-108">Questo processo esegue una macchina virtuale Java (JVM).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="c2d2a-109">Ogni richiesta HTTP da un browser a Tomcat viene elaborata nel processo di Tomcat come un thread separato.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c2d2a-110">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e classico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c2d2a-111">Questo articolo descrive come usare il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="c2d2a-112">Per le distribuzioni più recenti si consiglia di usare il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c2d2a-113">Per informazioni su come usare un modello di Resource Manager per distribuire una VM Ubuntu con Openjdk e Tomcat, vedere [questo articolo](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="c2d2a-114">In questo articolo si installerà Tomcat7 su un'immagine Linux e la si distribuirà in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="c2d2a-115">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-115">You will learn:</span></span>  

* <span data-ttu-id="c2d2a-116">Come creare una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="c2d2a-117">Come preparare la macchina virtuale per Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="c2d2a-118">Come installare Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-118">How to install Tomcat7.</span></span>

<span data-ttu-id="c2d2a-119">La procedura presuppone che l'utente disponga già di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="c2d2a-120">In caso contrario è possibile registrarsi per una versione di valutazione gratuita sul [sito Web di Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="c2d2a-121">Se si ha un abbonamento MSDN, vedere [Offerte speciali di Microsoft Azure: vantaggi per i membri di MSDN, MPN e Bizspark](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="c2d2a-122">Per altre informazioni su Azure, vedere [Cos'è Microsoft Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="c2d2a-123">Questo articolo presuppone che l'utente abbia una conoscenza pratica di base di Tomcat e Linux.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="c2d2a-124">Fase 1: creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-124">Phase 1: Create an image</span></span>
<span data-ttu-id="c2d2a-125">In questa fase si creerà una macchina virtuale usando un'immagine Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="c2d2a-126">Passaggio 1: generare una chiave di autenticazione SSH</span><span class="sxs-lookup"><span data-stu-id="c2d2a-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="c2d2a-127">SSH è uno strumento importante per gli amministratori di sistema.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="c2d2a-128">Non è consigliabile tuttavia configurare la protezione di accesso in base a una password stabilita da una persona fisica.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="c2d2a-129">Con un nome utente e una password debole, il sistema può essere esposto all'attacco da parte di utenti malintenzionati.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="c2d2a-130">L'aspetto positivo è che esiste un modo per lasciare aperto l'accesso remoto e non doversi preoccupare delle password.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="c2d2a-131">Il metodo consiste nell'autenticazione con crittografia asimmetrica.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="c2d2a-132">La chiave privata dell'utente è quella che concede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="c2d2a-133">È anche possibile bloccare l'account dell'utente per impedire l'autenticazione tramite password.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="c2d2a-134">Un altro vantaggio di questo metodo è che non sono necessarie password diverse per accedere a server diversi.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="c2d2a-135">È possibile autenticarsi tramite la chiave privata personale in tutti i server, perciò non è necessario ricordare diverse password.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="c2d2a-136">Attenersi a questa procedura per generare la chiave di autenticazione SSH.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="c2d2a-137">Scaricare e installare PuTTYgen dal percorso seguente: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="c2d2a-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="c2d2a-138">Eseguire Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="c2d2a-139">Fare clic su **Generate** per generare le chiavi.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="c2d2a-140">Nel processo è possibile aumentare la casualità spostando il puntatore del mouse sull'area vuota della finestra.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="c2d2a-141">![Schermata di PuTTY Key Generator che mostra il pulsante per generare una nuova chiave][1]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="c2d2a-142">Dopo il processo di generazione Puttygen.exe visualizzerà la nuova chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Schermata di PuTTY Key Generator che mostra la nuova chiave pubblica e il pulsante per salvare la chiave privata][2]
5. <span data-ttu-id="c2d2a-144">Selezionare e copiare la chiave pubblica e salvarla in un file denominato publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="c2d2a-145">Non fare clic su **Save public key**, poiché il formato di file della chiave pubblica salvata è diverso dalla chiave pubblica richiesta.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="c2d2a-146">Fare clic su **Save private key** e salvarla in un file denominato privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="c2d2a-147">Passaggio 2: creare l'immagine nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c2d2a-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="c2d2a-148">Nel [portale](https://portal.azure.com/) fare clic su **Nuovo** nella barra delle applicazioni per creare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="c2d2a-149">Scegliere quindi l'immagine Linux in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="c2d2a-150">Il seguente esempio usa l'immagine Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="c2d2a-151">![Schermata del portale che mostra il pulsante Nuovo][3]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="c2d2a-152">In **Nome host** specificare il nome per l'URL che verrà usato dall'utente e dai client Internet per accedere a questa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="c2d2a-153">Definire l'ultima parte del nome DNS, ad esempio tomcatdemo.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="c2d2a-154">Azure genera quindi l'URL tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="c2d2a-155">In **Chiave di autenticazione SSH** copiare il valore della chiave dal file publicKey.pem che contiene la chiave pubblica generata da PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="c2d2a-156">![Casella Chiave di autenticazione SSH nel portale][4]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="c2d2a-157">Configurare altre impostazioni in base alle esigenze, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="c2d2a-158">Fase 2: preparare la macchina virtuale per Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="c2d2a-159">In questa fase si configurerà un endpoint per il traffico in Tomcat e ci si connetterà alla nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="c2d2a-160">Passaggio 1: aprire la porta HTTP per consentire l'accesso web</span><span class="sxs-lookup"><span data-stu-id="c2d2a-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="c2d2a-161">Gli endpoint di Azure sono costituiti da un protocollo TCP o UDP, insieme a una porta pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="c2d2a-162">La porta privata è la porta ascoltata dal servizio sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="c2d2a-163">La porta pubblica è la porta ascoltata esternamente dal servizio cloud di Azure per il traffico in ingresso basato su Internet.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="c2d2a-164">La porta TCP 8080 è la porta predefinita su cui Tomcat è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="c2d2a-165">Se si apre questa porta con un endpoint di Azure, l'utente e altri client Internet potranno accedere alle pagine Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="c2d2a-166">Nel portale di Azure fare clic su **Sfoglia** > **Macchine virtuali** e quindi fare clic sulla macchina virtuale che è stata creata.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="c2d2a-167">![Schermata della directory Macchine virtuali][5]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="c2d2a-168">Per aggiungere un endpoint alla macchina virtuale, scegliere la casella **Endpoint** .</span><span class="sxs-lookup"><span data-stu-id="c2d2a-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="c2d2a-169">![Schermata che mostra la casella Endpoint][6]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="c2d2a-170">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="c2d2a-171">In **Endpoint** digitare un nome per l'endpoint, quindi digitare 80 nel campo **Porta pubblica**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="c2d2a-172">Se la porta viene impostata su 80, non occorre includere il numero di porta nell'URL che si usa per accedere a Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="c2d2a-173">Ad esempio, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="c2d2a-174">Se si imposta la porta su un altro valore, come 81, è necessario aggiungere il numero di porta all'URL per accedere a Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="c2d2a-175">Ad esempio http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="c2d2a-176">Digitare 8080 in **Porta privata**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="c2d2a-177">Per impostazione predefinita Tomcat è in ascolto sulla porta TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="c2d2a-178">Se è stata modificata la porta di ascolto predefinita di Tomcat, è necessario aggiornare la **porta privata** in modo che corrisponda alla porta di ascolto di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="c2d2a-179">![Schermata dell'interfaccia utente che mostra il comando Aggiungi, Porta pubblica e Porta privata][7]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="c2d2a-180">Fare clic su **OK** per aggiungere l'endpoint alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="c2d2a-181">Passaggio 2: effettuare la connessione all'immagine creata</span><span class="sxs-lookup"><span data-stu-id="c2d2a-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="c2d2a-182">È possibile scegliere qualsiasi strumento SSH per connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="c2d2a-183">In questo esempio viene usato PuTTY.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="c2d2a-184">Ottenere il nome DNS della macchina virtuale dal portale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="c2d2a-185">Fare clic su **Sfoglia** > **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="c2d2a-186">Selezionare il nome della macchina virtuale e quindi fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="c2d2a-187">Nel riquadro **Proprietà** osservare la casella **Nome di dominio** per ottenere il nome DNS.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="c2d2a-188">Ricavare il numero di porta per le connessioni SSH dalla casella **SSH** .</span><span class="sxs-lookup"><span data-stu-id="c2d2a-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="c2d2a-189">![Schermata che mostra il numero di porta della connessione SSH][8]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="c2d2a-190">Scaricare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="c2d2a-191">Dopo il download fare clic sul file eseguibile Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="c2d2a-192">Nella configurazione di PuTTY impostare le opzioni di base con il nome host e il numero di porta ottenuto dalle proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![Schermata che mostra le opzioni di configurazione di PuTTY relative a nome host e porta][9]

5. <span data-ttu-id="c2d2a-194">Nel riquadro a sinistra fare clic su **Connessione** > **SSH** > **Autenticazione** e quindi fare clic su **Sfoglia** per specificare il percorso del file privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="c2d2a-195">Il file PrivateKey contiene la chiave privata generata da PuTTYgen in precedenza nella sezione "Fase 1: creare un'immagine" di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="c2d2a-196">![Schermata che mostra la gerarchia di directory di connessione e il pulsante Sfoglia][10]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="c2d2a-197">Fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-197">Click **Open**.</span></span> <span data-ttu-id="c2d2a-198">Si potrebbe ricevere un avviso da una finestra di messaggio.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-198">You might be alerted by a message box.</span></span> <span data-ttu-id="c2d2a-199">Se il nome DNS e il numero di porta sono stati configurati correttamente, fare clic su **Yes**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="c2d2a-200">![Schermata che mostra la notifica][11]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="c2d2a-201">Viene chiesto di inserire il nome utente.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-201">You are prompted to enter your username.</span></span>  
![Schermata che mostra dove inserite il nome utente][12]

8. <span data-ttu-id="c2d2a-203">Inserire il nome utente utilizzato per creare la macchina virtuale nella sezione "Fase 1: creare un'immagine" di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="c2d2a-204">Verrà visualizzata una schermata simile alla seguente: </span><span class="sxs-lookup"><span data-stu-id="c2d2a-204">You will see something like the following:</span></span>  
![Schermata che mostra la conferma dell'autenticazione][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="c2d2a-206">Fase 3: installare il software</span><span class="sxs-lookup"><span data-stu-id="c2d2a-206">Phase 3: Install software</span></span>
<span data-ttu-id="c2d2a-207">In questa fase saranno installati l'ambiente di runtime Java, Tomcat7 e altri componenti di Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="c2d2a-208">Ambiente di runtime Java</span><span class="sxs-lookup"><span data-stu-id="c2d2a-208">Java runtime environment</span></span>
<span data-ttu-id="c2d2a-209">Tomcat è scritto in Java.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-209">Tomcat is written in Java.</span></span> <span data-ttu-id="c2d2a-210">Esistono due tipi di Java Development Kit (JDK): OpenJDK e Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="c2d2a-211">È possibile scegliere quello preferito.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="c2d2a-212">Il codice contenuto dai due JDK per le classi nell'API Java è praticamente identico, mentre il codice per la macchina virtuale è diverso.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="c2d2a-213">OpenJDK tende a usare librerie aperte mentre Oracle JDK tende a usare librerie chiuse.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="c2d2a-214">Oracle JDK dispone di più classi e include alcuni bug corretti, inoltre è più stabile di OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="c2d2a-215">Installare OpenJDK</span><span class="sxs-lookup"><span data-stu-id="c2d2a-215">Install OpenJDK</span></span>  

<span data-ttu-id="c2d2a-216">Usare il comando seguente per scaricare OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="c2d2a-217">Per creare una directory in cui includere i file di JDK:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="c2d2a-218">Per estrarre i file di JDK nella directory /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="c2d2a-219">Installare Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="c2d2a-219">Install Oracle JDK</span></span>


<span data-ttu-id="c2d2a-220">Usare il comando seguente per scaricare Oracle JDK dal sito Web di Oracle.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="c2d2a-221">Per creare una directory in cui includere i file di JDK:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="c2d2a-222">Per estrarre i file di JDK nella directory /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="c2d2a-223">Per impostare Oracle JDK come macchina virtuale Java predefinita:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="c2d2a-224">Verificare che l'installazione di Java sia riuscita</span><span class="sxs-lookup"><span data-stu-id="c2d2a-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="c2d2a-225">Per verificare se l'ambiente di runtime Java è stato installato correttamente, è possibile usare un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="c2d2a-226">Se è stato installato OpenJDK, si dovrebbe vedere un messaggio simile al seguente: ![installazione di OpenJDK riuscita][14]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="c2d2a-227">Se è stato installato Oracle JDK, si dovrebbe vedere un messaggio simile al seguente: ![installazione di Oracle JDK riuscita][15]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="c2d2a-228">Installare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-228">Install Tomcat7</span></span>
<span data-ttu-id="c2d2a-229">Usare il seguente comando per installare Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="c2d2a-230">Se non si usa Tomcat7, modificare il comando in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="c2d2a-231">Verificare che l'installazione di Tomcat7 sia riuscita</span><span class="sxs-lookup"><span data-stu-id="c2d2a-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="c2d2a-232">Per verificare se Tomcat7 è stato installato correttamente, passare al nome DNS del server Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="c2d2a-233">In questo articolo l'URL di esempio è http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="c2d2a-234">Se viene visualizzato un messaggio simile al seguente, Tomcat7 è stato installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="c2d2a-235">![Messaggio con l'avviso che l'installazione di Tomcat7 è riuscita][16]</span><span class="sxs-lookup"><span data-stu-id="c2d2a-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="c2d2a-236">Installare altri componenti di Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="c2d2a-237">Esistono altri componenti facoltativi di Tomcat che è possibile installare.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="c2d2a-238">Usare il comando **sudo apt-cache search tomcat7** per visualizzare tutti i componenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="c2d2a-239">Usare i seguenti comandi per installare alcuni utili componenti.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="c2d2a-240">Fase 4: configurare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="c2d2a-241">In questa fase si amministra Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="c2d2a-242">Avviare e arrestare Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="c2d2a-243">Il server Tomcat7 si avvia automaticamente durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="c2d2a-244">È possibile anche avviarlo con il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="c2d2a-245">Per arrestare Tomcat7：</span><span class="sxs-lookup"><span data-stu-id="c2d2a-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="c2d2a-246">Per visualizzare lo stato di Tomcat7：</span><span class="sxs-lookup"><span data-stu-id="c2d2a-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="c2d2a-247">Per riavviare i servizi Tomcat：</span><span class="sxs-lookup"><span data-stu-id="c2d2a-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="c2d2a-248">Amministrazione di Tomcat7</span><span class="sxs-lookup"><span data-stu-id="c2d2a-248">Tomcat7 administration</span></span>
<span data-ttu-id="c2d2a-249">È possibile modificare il file di configurazione utente di Tomcat per configurare le proprie credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="c2d2a-250">Usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="c2d2a-251">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-251">Here is an example:</span></span>  
![Schermata che mostra l'output del comando sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="c2d2a-253">Creare una password complessa per il nome utente dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="c2d2a-254">Dopo avere modificato questo file, è necessario riavviare i servizi Tomcat7 con il seguente comando per rendere effettive le modifiche:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="c2d2a-255">Aprire il browser e immettere l'URL **http://<your tomcat server DNS name>/manager/html**.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="c2d2a-256">Ad esempio, in questo articolo l'URL è http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="c2d2a-257">Dopo la connessione, si dovrebbe visualizzare una schermata simile alla seguente: </span><span class="sxs-lookup"><span data-stu-id="c2d2a-257">After connecting, you should see something similar to the following:</span></span>  
![Schermata di Tomcat Web Application Manager][18]

## <a name="common-issues"></a><span data-ttu-id="c2d2a-259">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="c2d2a-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="c2d2a-260">Impossibile accedere alla macchina virtuale con Tomcat e Moodle da Internet</span><span class="sxs-lookup"><span data-stu-id="c2d2a-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="c2d2a-261">Sintomo</span><span class="sxs-lookup"><span data-stu-id="c2d2a-261">Symptom</span></span>  
  <span data-ttu-id="c2d2a-262">Tomcat è in esecuzione ma non è possibile visualizzare la pagina predefinita di Tomcat con il browser.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="c2d2a-263">Possibile causa principale</span><span class="sxs-lookup"><span data-stu-id="c2d2a-263">Possible root cause</span></span>   

  * <span data-ttu-id="c2d2a-264">La porta di ascolto di Tomcat non corrisponde alla porta privata dell'endpoint della macchina virtuale per il traffico in Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="c2d2a-265">Controllare le impostazioni dell'endpoint della porta pubblica e privata e assicurarsi che la porta privata corrisponda alla porta di ascolto di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="c2d2a-266">Per istruzioni sulla configurazione degli endpoint per la macchina virtuale vedere la sezione di questo articolo "Fase 1: creare un'immagine".</span><span class="sxs-lookup"><span data-stu-id="c2d2a-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="c2d2a-267">Per determinare la porta di ascolto di Tomcat, aprire /etc/httpd/conf/httpd.conf (versione Red Hat) o /etc/tomcat7/server.xml (versione Debian).</span><span class="sxs-lookup"><span data-stu-id="c2d2a-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="c2d2a-268">Per impostazione predefinita la porta di ascolto di Tomcat è 8080.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="c2d2a-269">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="c2d2a-270">Se si usa una macchina virtuale come Debian o Ubuntu e si vuole modificare la porta di ascolto di Tomcat predefinita (ad esempio 8081), è necessario aprire la porta anche per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="c2d2a-271">Aprire innanzitutto il profilo:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="c2d2a-272">Rimuovere quindi i commenti dall’ultima riga e modificare “no” in “sì”.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="c2d2a-273">Il firewall ha disabilitato la porta di ascolto di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="c2d2a-274">È possibile visualizzare la pagina predefinita di Tomcat solo dall'host locale.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="c2d2a-275">Molto probabilmente il problema è che la porta su cui è in ascolto Tomcat è bloccata dal firewall.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="c2d2a-276">È possibile usare lo strumento w3m per passare alla pagina Web.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="c2d2a-277">I seguenti comandi consentono di installare w3m e di passare alla pagina predefinita di Tomcat:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="c2d2a-278">sudo yum install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="c2d2a-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="c2d2a-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="c2d2a-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="c2d2a-280">Soluzione</span><span class="sxs-lookup"><span data-stu-id="c2d2a-280">Solution</span></span>

  * <span data-ttu-id="c2d2a-281">Se la porta di ascolto di Tomcat non corrisponde alla porta privata dell'endpoint per il traffico nella macchina virtuale, è necessario modificare la porta privata dell'endpoint affinché corrisponda alla porta di ascolto di Tomcat.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="c2d2a-282">Se il problema è causato dal firewall o dagli iptable, aggiungere le seguenti righe a /etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="c2d2a-283">La seconda riga è necessaria solo per il traffico https:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="c2d2a-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="c2d2a-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="c2d2a-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="c2d2a-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="c2d2a-286">Assicurarsi che le righe precedenti siano posizionate sopra eventuali righe che limiterebbero globalmente l'accesso, come la seguente: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="c2d2a-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="c2d2a-287">Per ricaricare gli iptable, eseguire il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="c2d2a-288">Questa installazione è stata effettuata su CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="c2d2a-289">Autorizzazione negata quando si caricano i file di progetto in /var/lib/tomcat7/webapps/</span><span class="sxs-lookup"><span data-stu-id="c2d2a-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="c2d2a-290">Sintomo</span><span class="sxs-lookup"><span data-stu-id="c2d2a-290">Symptom</span></span>
  <span data-ttu-id="c2d2a-291">Quando si usa un client FTP sicuro (ad esempio FileZilla) per connettersi alla macchina virtuale e passare a /var/lib/tomcat7/webapps/ per pubblicare il sito, si ottiene un messaggio di errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="c2d2a-292">Possibile causa principale</span><span class="sxs-lookup"><span data-stu-id="c2d2a-292">Possible root cause</span></span>
  <span data-ttu-id="c2d2a-293">Non si dispone delle autorizzazioni di accesso alla cartella /var/lib/tomcat7/webapps.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="c2d2a-294">Soluzione</span><span class="sxs-lookup"><span data-stu-id="c2d2a-294">Solution</span></span>  
  <span data-ttu-id="c2d2a-295">È necessario ottenere l'autorizzazione dall'account radice.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-295">You need to get permission from the root account.</span></span> <span data-ttu-id="c2d2a-296">È possibile cambiare la proprietà di tale cartella dalla radice al nome utente usato per il provisioning della macchina.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="c2d2a-297">Di seguito è riportato un esempio con il nome dell'account azureuser:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="c2d2a-298">Usare l'opzione -R per applicare le autorizzazioni per tutti i file anche all'interno di una directory.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="c2d2a-299">Questo comando funziona anche per le directory.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-299">This command also works for directories.</span></span> <span data-ttu-id="c2d2a-300">L'opzione -R modifica le autorizzazioni per tutti i file e le directory all'interno della directory.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="c2d2a-301">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="c2d2a-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="c2d2a-302">Questo comando cambia la proprietà (sia utente che gruppo) per tutti i file e le directory che si trovano all'interno della directory stessa.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="c2d2a-303">Il comando seguente modifica l'autorizzazione solo per la directory della cartella.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="c2d2a-304">I file e cartelle all'interno della directory non vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="c2d2a-304">The files and folders inside the directory are not changed.</span></span>  

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
