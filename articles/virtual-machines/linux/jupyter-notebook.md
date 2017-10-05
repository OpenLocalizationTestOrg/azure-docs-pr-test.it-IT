---
title: Creare un Jupyter/IPython Notebook | Microsoft Docs
description: Informazioni su come distribuire Jupyter/IPython Notebook in una macchina virtuale Linux o Windows creata con il modello di distribuzione del gestore delle risorse in Azure.
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b5940190822cd5c5b78ea0e8f5c8695608d351d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="cd43e-103">Creazione di una macchina virtuale di Azure, installazione di Jupyter ed esecuzione di Jupyter Notebook in Azure</span><span class="sxs-lookup"><span data-stu-id="cd43e-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="cd43e-104">Il [progetto Jupyter](http://jupyter.org), noto in precedenza come [progetto IPython](http://ipython.org), fornisce un insieme di strumenti per il calcolo scientifico usando potenti shell interattive che consentono di combinare l'esecuzione di codice con la creazione di un documento di calcolo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cd43e-104">The [Jupyter project](http://jupyter.org), formerly the [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with the creation of a live computational document.</span></span> <span data-ttu-id="cd43e-105">I file dei blocchi appunti possono contenere testo arbitrario, formule matematiche, codice di input, risultati, grafica, video e altri tipi di contenuti multimediali visualizzabili sui moderni Web browser.</span><span class="sxs-lookup"><span data-stu-id="cd43e-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="cd43e-106">Jupyter Notebook rappresenta la scelta ideale sia per gli utenti poco esperti di Python che desiderano apprenderne il funzionamento in un ambiente interattivo e divertente sia per quelli che si occupano di informatica avanzata in campo tecnico e parallelo.</span><span class="sxs-lookup"><span data-stu-id="cd43e-106">Whether you're absolutely new to Python and want to learn it in a fun, interactive environment or do some serious parallel/technical computing, the Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="cd43e-107">![Schermata](./media/jupyter-notebook/ipy-notebook-spectral.png) Uso dei pacchetti SciPy e Matplotlib per l'analisi della struttura di una registrazione audio.</span><span class="sxs-lookup"><span data-stu-id="cd43e-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages to analyze the structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="cd43e-108">Due modi di Jupyter: Azure Notebook o distribuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="cd43e-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="cd43e-109">Azure fornisce un servizio che è possibile utilizzare per [iniziare rapidamente a utilizzare Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd43e-109">Azure provides a service that you can use to [quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="cd43e-110">Usando Azure Notebook Service, è possibile ottenere facilmente accesso all'interfaccia accessibile tramite Web di Jupyter per risorse di calcolo scalabili, con la potenza di Python e delle numerose librerie correlate.</span><span class="sxs-lookup"><span data-stu-id="cd43e-110">By using the Azure Notebook Service, you can easily gain access to Jupyter's web-accessible interface to scalable computational resources with all the power of Python and its many libraries.</span></span>  <span data-ttu-id="cd43e-111">Poiché l'installazione viene gestita dal servizio, gli utenti possono accedere a queste risorse senza la necessità di amministrazione e configurazione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="cd43e-111">Since the installation is handled by the service, users can access these resources without the need for administration and configuration by the user.</span></span>

<span data-ttu-id="cd43e-112">Se il servizio notebook non funziona per lo scenario, continuare a leggere questo articolo che illustra come distribuire il Jupyter Notebook in Microsoft Azure utilizzando macchine virtuali (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="cd43e-112">If the notebook service does not work for your scenario please continue to read this article which will will show you how to deploy the Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="cd43e-113">Creazione e configurazione di una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="cd43e-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="cd43e-114">Il primo passaggio consiste nel creare una macchina virtuale eseguita in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd43e-114">The first step is to create a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="cd43e-115">La VM è un sistema operativo completo nel cloud e verrà utilizzata per l'esecuzione di Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="cd43e-115">This VM is a complete operating system in the cloud and will be used to run the Jupyter Notebook.</span></span> <span data-ttu-id="cd43e-116">Azure consente di eseguire macchine virtuali sia Linux che Windows, e in questo articolo verrà descritta la configurazione di Jupyter in entrambi i tipi.</span><span class="sxs-lookup"><span data-stu-id="cd43e-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover the setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="cd43e-117">Creare una VM Linux e aprire una porta per Jupyter</span><span class="sxs-lookup"><span data-stu-id="cd43e-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="cd43e-118">Seguire le istruzioni fornite [qui][portal-vm-linux] per creare una macchina virtuale della distribuzione *Ubuntu*.</span><span class="sxs-lookup"><span data-stu-id="cd43e-118">Follow the instructions given [here][portal-vm-linux] to create a virtual machine of the *Ubuntu* distribution.</span></span> <span data-ttu-id="cd43e-119">Questa esercitazione utilizza Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="cd43e-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="cd43e-120">Si presuppone che il nome utente sia *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="cd43e-120">We'll assume the user name *azureuser*.</span></span>

<span data-ttu-id="cd43e-121">Dopo aver distribuito la macchina virtuale è necessario aprire una regola di protezione nel gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="cd43e-121">After the virtual machine deploys we need to open up a security rule on the network security group.</span></span>  <span data-ttu-id="cd43e-122">Dal portale di Azure, passare a **Gruppi di sicurezza di rete** e aprire la scheda per il gruppo di sicurezza corrispondente alla VM.</span><span class="sxs-lookup"><span data-stu-id="cd43e-122">From the Azure portal, go to **Network Security Groups** and open the tab for the Security Group corresponding to your VM.</span></span> <span data-ttu-id="cd43e-123">È necessario aggiungere una regola di sicurezza in ingresso con le impostazioni seguenti: **TCP** per il protocollo, **\*** per la porta di origine (pubblica) e **9999** per la porta di destinazione (privata).</span><span class="sxs-lookup"><span data-stu-id="cd43e-123">You need to add an Inbound Security rule with the following settings: **TCP** for the protocol, **\*** for the source (public) port and **9999** for the destination (private) port.</span></span>

![Schermata](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="cd43e-125">Mentre ci si trova nel gruppo di sicurezza di rete, fare clic su **Interfacce di rete** e prendere nota dell’**Indirizzo IP pubblico**, poiché sarà necessario per connettersi alla VM nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="cd43e-125">While in your Network Security Group, click on **Network Interfaces** and note the **Public IP Address** as it will be needed to connect to your VM in the next step.</span></span>

## <a name="install-required-software-on-the-vm"></a><span data-ttu-id="cd43e-126">Installazione del software necessario nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cd43e-126">Install required software on the VM</span></span>
<span data-ttu-id="cd43e-127">Per eseguire Jupyter Notebook nella VM, è necessario installare prima Jupyter e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cd43e-127">To run the Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="cd43e-128">Connettersi alla VM Linux mediante ssh e la coppia nomeutente/password selezionata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="cd43e-128">Connect to your linux vm using ssh and the username/password pair you chose when you created the vm.</span></span> <span data-ttu-id="cd43e-129">In questa esercitazione verrà utilizzato PuTTY e ci si connetterà da Windows.</span><span class="sxs-lookup"><span data-stu-id="cd43e-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="cd43e-130">Installazione di Jupyter su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd43e-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="cd43e-131">Installare Anaconda, una famosa distribuzione python per le scienze dei dati, utilizzando uno dei collegamenti forniti da [Continuum Analytics](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="cd43e-131">Install Anaconda, a popular data science python distribution, using one of the links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="cd43e-132">Al momento della stesura di questo documento, i collegamenti riportati di seguito sono le versioni più aggiornate.</span><span class="sxs-lookup"><span data-stu-id="cd43e-132">As of the writing of this document, the below links are the most up to date versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="cd43e-133">Installazione di Anaconda per Linux</span><span class="sxs-lookup"><span data-stu-id="cd43e-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="cd43e-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="cd43e-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="cd43e-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="cd43e-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="cd43e-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cd43e-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="cd43e-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cd43e-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cd43e-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cd43e-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="cd43e-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cd43e-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="cd43e-140">Installazione di Anaconda3 2.3.0 a 64 bit su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd43e-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="cd43e-141">Ad esempio, in questo modo è possibile installare Anaconda su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cd43e-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter to the latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Schermata](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="cd43e-143">Configurazione di Jupyter e utilizzo di SSL</span><span class="sxs-lookup"><span data-stu-id="cd43e-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="cd43e-144">Dopo l'installazione, è necessario utilizzare alcuni minuti per configurare i file di configurazione per Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cd43e-144">After installing we need to take a moment to setup the configuration files for Jupyter.</span></span> <span data-ttu-id="cd43e-145">Se si verificano problemi relativi alla configurazione di Jupyter, può essere utile esaminare la [Documentazione di Jupyter per l'esecuzione di un Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="cd43e-145">If you experience troubles with configuring Jupyter it may be helpful to look at the [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="cd43e-146">Passare alla directory del profilo tramite `cd` per creare il certificato SSL e modificare il file di configurazione del profilo.</span><span class="sxs-lookup"><span data-stu-id="cd43e-146">Next we `cd` to the profile directory to create our SSL certificate and edit the profiles configuration file.</span></span>

<span data-ttu-id="cd43e-147">Utilizzare il comando seguente su Linux.</span><span class="sxs-lookup"><span data-stu-id="cd43e-147">On Linux use the following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="cd43e-148">Utilizzare il comando seguente per creare il certificato SSL (Linux e Windows).</span><span class="sxs-lookup"><span data-stu-id="cd43e-148">Use the following command to create the SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="cd43e-149">Si noti che, poiché verrà cercato un certificato SSL autofirmato, quando ci si connette al blocco appunti nel browser verrà visualizzato un avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="cd43e-149">Note that since we are creating a self-signed SSL certificate, when connecting to the notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="cd43e-150">Per l'utilizzo in produzione a lungo termine, è consigliabile utilizzare un certificato con una firma appropriata associato all'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="cd43e-150">For long-term production use, you will want to use a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="cd43e-151">Poiché la gestione dei certificati esula dall'ambito di questa dimostrazione, per il momento verrà utilizzato un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="cd43e-151">Since certificate management is beyond the scope of this demo, we will stick to a self-signed certificate for now.</span></span>

<span data-ttu-id="cd43e-152">Oltre a utilizzare un certificato, è anche necessario specificare una password per proteggere il blocco appunti dall'utilizzo non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="cd43e-152">In addition to using a certificate, you must also provide a password to protect your notebook from unauthorized use.</span></span>  <span data-ttu-id="cd43e-153">Per motivi di sicurezza, nel file di configurazione di Jupyter vengono utilizzate password crittografate, pertanto è necessario innanzitutto crittografare la password.</span><span class="sxs-lookup"><span data-stu-id="cd43e-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need to encrypt your password first.</span></span>  <span data-ttu-id="cd43e-154">In IPython è disponibile un'utilità per questo scopo. Al prompt dei comandi eseguire:</span><span class="sxs-lookup"><span data-stu-id="cd43e-154">IPython provides a utility to do so; at a command prompt run the following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="cd43e-155">Verrà richiesto di specificare e confermare una password, quindi stampare la password.</span><span class="sxs-lookup"><span data-stu-id="cd43e-155">This will prompt you for a password and confirmation, and will then print the password.</span></span> <span data-ttu-id="cd43e-156">Annotarla per il passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="cd43e-156">Note this for the following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided the rest for security)

<span data-ttu-id="cd43e-157">In seguito verrà modificato il file di configurazione del profilo, che corrisponde al file `jupyter_notebook_config.py` della directory corrente.</span><span class="sxs-lookup"><span data-stu-id="cd43e-157">Next, we will edit the profile's configuration file, which is the `jupyter_notebook_config.py` file in the directory you are in.</span></span>  <span data-ttu-id="cd43e-158">Si noti che questo file potrebbe non essere presente: in tal caso, crearlo.</span><span class="sxs-lookup"><span data-stu-id="cd43e-158">Note that this file may not exist -- just create it if that is the case.</span></span>  <span data-ttu-id="cd43e-159">Questo file contiene alcuni campi, tutti impostati come commento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cd43e-159">This file has a number of fields and by default all are commented out.</span></span>  <span data-ttu-id="cd43e-160">È possibile aprire questo file con qualsiasi editor di testo, assicurandosi che includa almeno il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="cd43e-160">You can open this file with any text editor of your liking, and you should ensure that it has at least the following content.</span></span> <span data-ttu-id="cd43e-161">**Assicurarsi di sostituire la password c.NotebookApp.password nella configurazione con sha1 dal passaggio precedente**.</span><span class="sxs-lookup"><span data-stu-id="cd43e-161">**Be sure to replace the c.NotebookApp.password in the config with the sha1 from the previous step**.</span></span>

    c = get_config()

    # You must give the path to the certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-the-jupyter-notebook"></a><span data-ttu-id="cd43e-162">Avviare il notebook Jupyter</span><span class="sxs-lookup"><span data-stu-id="cd43e-162">Run the Jupyter Notebook</span></span>
<span data-ttu-id="cd43e-163">A questo punto è possibile avviare Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="cd43e-163">At this point we are ready to start the Jupyter Notebook.</span></span> <span data-ttu-id="cd43e-164">A tale scopo, passare alla directory in cui si vogliono archiviare i blocchi appunti e avviare il server Jupyter Notebook con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cd43e-164">To do this, navigate to the directory you want to store notebooks in and start the Jupyter Notebook server with the following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="cd43e-165">A questo punto dovrebbe essere possibile accedere a Jupyter Notebook all'indirizzo `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="cd43e-165">You should now be able to access your Jupyter Notebook at the address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="cd43e-166">La prima volta che si accede al blocco appunti, nella pagina di accesso viene richiesto di immettere la password:</span><span class="sxs-lookup"><span data-stu-id="cd43e-166">When you first access your notebook, the login page asks for your password.</span></span> <span data-ttu-id="cd43e-167">Dopo l'accesso, verrà visualizzata la pagina "Jupyter Notebook Dashboard", ossia il centro di controllo per tutte le operazioni sui blocchi appunti.</span><span class="sxs-lookup"><span data-stu-id="cd43e-167">And once you log in, you will see the "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="cd43e-168">In questa pagina è possibile creare nuovi blocchi appunti e aprire quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="cd43e-168">From this page you can create new notebooks and open existing ones.</span></span>

![Schermata](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-the-jupyter-notebook"></a><span data-ttu-id="cd43e-170">Utilizzo di Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="cd43e-170">Using the Jupyter Notebook</span></span>
<span data-ttu-id="cd43e-171">Se si fa clic sul pulsante **Nuovo** , verrà visualizzata la seguente pagina di apertura.</span><span class="sxs-lookup"><span data-stu-id="cd43e-171">If you click the **New** button, you will see the following opening page.</span></span>

![Schermata](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="cd43e-173">L'area contrassegnata con `In []:` è l'area di input, in cui è possibile immettere qualsiasi codice Python valido che verrà eseguito premendo `Shift-Enter` oppure facendo clic sull'icona "Play", ossia il triangolo che punta a destra sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="cd43e-173">The area marked with an `In []:` prompt is the input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on the "Play" icon (the right-pointing triangle in the toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="cd43e-174">Un potente paradigma: documenti di calcolo in tempo reale con contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="cd43e-174">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="cd43e-175">Il blocco appunti dovrebbe risultare familiare a chiunque abbia usato Python e un elaboratore di testo, perché è una combinazione di entrambi: è possibile eseguire blocchi di codice Python, ma anche mantenere note e altro testo modificando lo stile di una cella da "Code" a "Markdown" tramite il menu a discesa della barra degli strumenti:</span><span class="sxs-lookup"><span data-stu-id="cd43e-175">The notebook itself should feel very natural to anyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing the style of a cell from "Code" to "Markdown" using the drop-down menu in the toolbar.</span></span>

<span data-ttu-id="cd43e-176">Jupyter è molto di più di un elaboratore di testo, in quanto consente di combinare calcolo e contenuti multimediali, ossia testo, grafica, video e qualsiasi altro contenuto visualizzabile in un moderno Web browser.</span><span class="sxs-lookup"><span data-stu-id="cd43e-176">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="cd43e-177">È possibile combinare, testo, codice, video e altro ancora!</span><span class="sxs-lookup"><span data-stu-id="cd43e-177">You can mix, text, code, videos and more!</span></span>

![Schermata](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="cd43e-179">Inoltre, con la potenza di molte eccellenti librerie di Python per il calcolo scientifico e tecnico, è possibile eseguire calcoli con la stessa facilità di un'analisi di rete complessa, tutto nello stesso ambiente:</span><span class="sxs-lookup"><span data-stu-id="cd43e-179">And with the power of Python's many excellent libraries for scientific and technical computing, in the following screenshot, a simple calculation can be performed with the same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="cd43e-180">Questo paradigma di combinare la potenza del moderno Web con il calcolo in tempo reale offre numerose possibilità ed è particolarmente indicato per il cloud. Il blocco appunti può essere utilizzato:</span><span class="sxs-lookup"><span data-stu-id="cd43e-180">This paradigm of mixing the power of the modern web with live computation offers many possibilities, and is ideally suited for the cloud; the Notebook can be used:</span></span>

* <span data-ttu-id="cd43e-181">Come blocco appunti computazionale per registrare il lavoro esplorativo su un problema.</span><span class="sxs-lookup"><span data-stu-id="cd43e-181">As a computational scratchpad to record exploratory work on a problem.</span></span>
* <span data-ttu-id="cd43e-182">Per condividere i risultati con i colleghi, sotto forma di calcolo in tempo reale o in formati stampabili (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="cd43e-182">To share results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="cd43e-183">Per distribuire e presentare materiale di formazione in tempo reale che implica calcoli, in modo che gli studenti possano sperimentare immediatamente con codice reale, modificarlo e rieseguirlo interattivamente.</span><span class="sxs-lookup"><span data-stu-id="cd43e-183">To distribute and present live teaching materials that involve computation, so students can immediately experiment with the real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="cd43e-184">Per fornire "documenti eseguibili" che presentano i risultati di una ricerca in modo da poter essere immediatamente riprodotti, convalidati e ampliati da altri.</span><span class="sxs-lookup"><span data-stu-id="cd43e-184">To provide "executable papers" that present the results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="cd43e-185">Come piattaforma per l'informatica collaborativa: più utenti possono accedere allo stesso server notebook per condividere una sessione di calcolo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cd43e-185">As a platform for collaborative computing: multiple users can log in to the same notebook server to share a live computational session.</span></span>

<span data-ttu-id="cd43e-186">Nel [repository][repository] di codice sorgente di IPython è disponibile un'intera directory con esempi di notebook che è possibile scaricare e provare nella propria VM Jupyter di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd43e-186">If you go to the IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="cd43e-187">È sufficiente scaricare i file `.ipynb` dal sito e caricarli nel dashboard della macchina virtuale di Azure dei blocchi appunti oppure scaricarli direttamente nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cd43e-187">Simply download the `.ipynb` files from the site and upload them onto the dashboard of your notebook Azure VM (or download them directly into the VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="cd43e-188">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="cd43e-188">Conclusion</span></span>
<span data-ttu-id="cd43e-189">Jupyter Notebook offre un'eccellente interfaccia per l'accesso interattivo alla potenza dell'ecosistema Python in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd43e-189">The Jupyter Notebook provides a powerful interface for accessing interactively the power of the Python ecosystem on Azure.</span></span>  <span data-ttu-id="cd43e-190">Rende possibile un'ampia gamma di casi di utilizzo, tra cui la semplice esplorazione di Python per apprenderne le funzionalità, l'analisi e la visualizzazione di dati, la simulazione e l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="cd43e-190">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="cd43e-191">I documenti Notebook risultanti contengono un record completo dei calcoli eseguiti e possono essere condivisi con altri utenti di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cd43e-191">The resulting Notebook documents contain a complete record of the computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="cd43e-192">È possibile utilizzare Jupyter Notebook come applicazione locale, ma si tratta di una soluzione particolarmente indicata per le distribuzioni cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="cd43e-192">The Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="cd43e-193">Le funzionalità di base di Jupyter sono anche disponibili all'interno di Visual Studio tramite [Python Tools per Visual Studio][Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="cd43e-193">The core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="cd43e-194">un plug-in open source reso disponibile da Microsoft che trasforma Visual Studio in un ambiente di sviluppo Python avanzato, con l'integrazione di un editor avanzato con IntelliSense, debug, profili ed elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="cd43e-194">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd43e-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd43e-195">Next steps</span></span>
<span data-ttu-id="cd43e-196">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="cd43e-196">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
