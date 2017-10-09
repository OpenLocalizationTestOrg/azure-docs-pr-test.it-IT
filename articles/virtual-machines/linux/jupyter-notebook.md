---
title: aaaCreate un Notebook Jupyter/IPython | Documenti Microsoft
description: Informazioni su come creata i toodeploy hello Notebook Jupyter/IPython in una macchina virtuale Linux con modello di distribuzione Gestione risorse hello in Azure.
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
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="cab10-103">Creazione di una macchina virtuale di Azure, installazione di Jupyter ed esecuzione di Jupyter Notebook in Azure</span><span class="sxs-lookup"><span data-stu-id="cab10-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="cab10-104">Hello [Jupyter progetto](http://jupyter.org), precedentemente hello [IPython progetto](http://ipython.org), fornisce una raccolta di strumenti per l'elaborazione scientifica utilizzando una potente shell interattiva che combinano l'esecuzione del codice con la creazione di hello di un documento di calcolo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cab10-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="cab10-105">I file dei blocchi appunti possono contenere testo arbitrario, formule matematiche, codice di input, risultati, grafica, video e altri tipi di contenuti multimediali visualizzabili sui moderni Web browser.</span><span class="sxs-lookup"><span data-stu-id="cab10-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="cab10-106">Se si sta tooPython assolutamente nuovo e si desidera toolearn in una divertente, ambiente interattivo o eseguire alcune grave parallelo o tecnico computing, hello server Jupyter Notebook rappresenta un'ottima scelta.</span><span class="sxs-lookup"><span data-stu-id="cab10-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="cab10-107">![Schermata di](./media/jupyter-notebook/ipy-notebook-spectral.png) SciPy usando Matplotlib pacchetti tooanalyze hello struttura e di una registrazione audio.</span><span class="sxs-lookup"><span data-stu-id="cab10-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="cab10-108">Due modi di Jupyter: Azure Notebook o distribuzione personalizzata</span><span class="sxs-lookup"><span data-stu-id="cab10-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="cab10-109">Azure fornisce un servizio che è possibile utilizzare anche[iniziare rapidamente a utilizzare Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="cab10-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="cab10-110">Utilizzando hello Azure Notebook servizio, è possibile ottenere facilmente interfaccia web accessibile del tooJupyter accesso alle risorse di calcolo scalabile con tutta la potenza di hello di Python e le relative librerie molti.</span><span class="sxs-lookup"><span data-stu-id="cab10-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="cab10-111">Poiché l'installazione di hello viene gestita dal servizio hello, gli utenti possono accedere a queste risorse senza necessità di hello di amministrazione e configurazione utente hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="cab10-112">Se il servizio di notebook hello non funziona per lo scenario continuare tooread in questo articolo in cui verrà sono visualizzate come toodeploy hello server Jupyter Notebook in Microsoft Azure, utilizzando macchine virtuali Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="cab10-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="cab10-113">Creazione e configurazione di una macchina virtuale in Azure</span><span class="sxs-lookup"><span data-stu-id="cab10-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="cab10-114">primo passaggio Hello è toocreate una macchina virtuale (VM) in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="cab10-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="cab10-115">Questa macchina virtuale è un sistema operativo completo nel cloud hello e verrà utilizzata per eseguire hello server Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="cab10-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="cab10-116">È in grado di eseguire le macchine virtuali Linux e Windows Azure e illustra l'installazione di hello del server Jupyter su entrambi i tipi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cab10-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="cab10-117">Creare una VM Linux e aprire una porta per Jupyter</span><span class="sxs-lookup"><span data-stu-id="cab10-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="cab10-118">Seguire le istruzioni di hello data [qui] [ portal-vm-linux] toocreate una macchina virtuale di hello *Ubuntu* distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cab10-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="cab10-119">Questa esercitazione utilizza Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="cab10-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="cab10-120">Si presupporrà che il nome di utente hello *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="cab10-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="cab10-121">Dopo la distribuzione di macchina virtuale hello è necessario tooopen una regola di protezione nel gruppo di sicurezza di rete hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="cab10-122">Dal portale di Azure hello, andare troppo**gruppi di sicurezza di rete** scheda hello open per hello tooyour corrispondente di gruppo di protezione VM e.</span><span class="sxs-lookup"><span data-stu-id="cab10-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="cab10-123">È necessario tooadd una regola di sicurezza in ingresso con hello seguenti impostazioni: **TCP** per il protocollo hello  **\***  per la porta di origine (pubblico) hello e **9999** per porta di destinazione (privato) Hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Schermata](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="cab10-125">Mentre nel gruppo di sicurezza di rete, fare clic su **interfacce di rete** e hello nota **indirizzo IP pubblico** poiché sarà necessario tooconnect tooyour VM nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="cab10-126">Installare il software necessario in hello VM</span><span class="sxs-lookup"><span data-stu-id="cab10-126">Install required software on hello VM</span></span>
<span data-ttu-id="cab10-127">toorun hello server Jupyter Notebook la macchina virtuale, sarà necessario installare innanzitutto Jupyter e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cab10-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="cab10-128">Connettere la macchina virtuale linux tooyour tramite ssh e coppia di nome utente/password hello scelto al momento della creazione hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cab10-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="cab10-129">In questa esercitazione verrà utilizzato PuTTY e ci si connetterà da Windows.</span><span class="sxs-lookup"><span data-stu-id="cab10-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="cab10-130">Installazione di Jupyter su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cab10-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="cab10-131">Installare Anaconda, una distribuzione di python di analisi scientifica dei dati comuni, utilizzando uno dei collegamenti hello forniti da [Continuum Analitica](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="cab10-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="cab10-132">A partire dalla scrittura hello di questo documento, hello collegamenti riportati di seguito sono hello più backup toodate versioni.</span><span class="sxs-lookup"><span data-stu-id="cab10-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="cab10-133">Installazione di Anaconda per Linux</span><span class="sxs-lookup"><span data-stu-id="cab10-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="cab10-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="cab10-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="cab10-135">Python 2.7</span><span class="sxs-lookup"><span data-stu-id="cab10-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="cab10-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cab10-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="cab10-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cab10-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cab10-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cab10-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="cab10-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span><span class="sxs-lookup"><span data-stu-id="cab10-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="cab10-140">Installazione di Anaconda3 2.3.0 a 64 bit su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cab10-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="cab10-141">Ad esempio, in questo modo è possibile installare Anaconda su Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cab10-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Schermata](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="cab10-143">Configurazione di Jupyter e utilizzo di SSL</span><span class="sxs-lookup"><span data-stu-id="cab10-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="cab10-144">Dopo l'installazione è necessario tootake un file di configurazione attualmente hello toosetup per Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cab10-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="cab10-145">Se si verificano dei problemi relativi alla configurazione Jupyter potrebbe essere utile toolook in hello [Jupyter documentazione per l'esecuzione di un Server Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="cab10-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="cab10-146">Avanti è `cd` toohello profilo toocreate directory il certificato SSL e modificare i file di configurazione di profili di hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="cab10-147">In Linux usare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cab10-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="cab10-148">Utilizzare hello successivo comando toocreate hello certificato SSL (Linux e Windows).</span><span class="sxs-lookup"><span data-stu-id="cab10-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="cab10-149">Si noti che poiché viene creato un certificato SSL autofirmato, quando ci si connette toohello notebook nel browser verrà visualizzato un avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="cab10-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="cab10-150">Per la produzione a lungo termine, sarà necessario toouse un certificato firmato correttamente associato all'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="cab10-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="cab10-151">Poiché la gestione dei certificati esula dall'ambito hello di questa dimostrazione, si verrà soffermeremo certificato autofirmato tooa per ora.</span><span class="sxs-lookup"><span data-stu-id="cab10-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="cab10-152">Inoltre toousing un certificato, è necessario fornire anche un tooprotect password notebook da usi non autorizzati.</span><span class="sxs-lookup"><span data-stu-id="cab10-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="cab10-153">Per motivi di sicurezza Jupyter password crittografate nel file di configurazione, pertanto sarà necessario tooencrypt la password viene utilizzata prima.</span><span class="sxs-lookup"><span data-stu-id="cab10-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="cab10-154">IPython fornisce un toodo utilità. a un prompt dei comandi eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cab10-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="cab10-155">Questo richiederà una password e conferma e verrà quindi password hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="cab10-156">Annotare questo per hello riportata dopo il passaggio.</span><span class="sxs-lookup"><span data-stu-id="cab10-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="cab10-157">Successivamente, è necessario modificare i file di configurazione del profilo di hello, ovvero il `jupyter_notebook_config.py` file nella directory hello in.</span><span class="sxs-lookup"><span data-stu-id="cab10-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="cab10-158">Si noti che questo file non esiste, crearla solo se è questo caso hello.</span><span class="sxs-lookup"><span data-stu-id="cab10-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="cab10-159">Questo file contiene alcuni campi, tutti impostati come commento per impostazione predefinita.  È possibile aprire questo file con qualsiasi editor di testo di base alle proprie esigenze, e accertarsi che ha almeno hello in seguito il contenuto.</span><span class="sxs-lookup"><span data-stu-id="cab10-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="cab10-160">**Essere c.NotebookApp.password di hello tooreplace che nella configurazione di hello con sha1 hello dal passaggio precedente hello**.</span><span class="sxs-lookup"><span data-stu-id="cab10-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="cab10-161">Eseguire hello server Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="cab10-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="cab10-162">A questo punto siamo toostart pronto hello server Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="cab10-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="cab10-163">toodo, passare toohello directory desiderato notebook toostore e avviare hello server Jupyter Notebook con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cab10-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="cab10-164">Dovrebbe ora essere in grado di tooaccess Jupyter Notebook all'indirizzo hello `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="cab10-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="cab10-165">Quando si accede a notebook, pagina di accesso hello richiede la password.</span><span class="sxs-lookup"><span data-stu-id="cab10-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="cab10-166">E quando si accede, verrà visualizzato hello "Jupyter Notebook Dashboard", ovvero il centro ontrollo per tutte le operazioni di blocco note.</span><span class="sxs-lookup"><span data-stu-id="cab10-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="cab10-167">In questa pagina è possibile creare nuovi blocchi appunti e aprire quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="cab10-167">From this page you can create new notebooks and open existing ones.</span></span>

![Schermata](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="cab10-169">Utilizzo di hello server Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="cab10-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="cab10-170">Se si fa clic hello **New** pulsante, verrà visualizzato hello seguente pagina di apertura.</span><span class="sxs-lookup"><span data-stu-id="cab10-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Schermata](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="cab10-172">area Hello contrassegnati con un `In []:` prompt dei comandi è l'area di input hello, qui è possibile digitare qualsiasi codice Python valido e verrà eseguito quando si raggiunge `Shift-Enter` o fare clic sull'icona "Play" hello (hello verso destra triangolo nella barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="cab10-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="cab10-173">Un potente paradigma: documenti di calcolo in tempo reale con contenuti multimediali</span><span class="sxs-lookup"><span data-stu-id="cab10-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="cab10-174">blocco appunti Hello stesso dovrebbero risultare tooanyone molto naturale che ha utilizzato Python e un elaboratore di testo, perché è in qualche modo una combinazione di entrambi: è possibile eseguire i blocchi di codice Python, ma è anche possibile mantenere le note e altro testo modificando troppo stile hello di una cella da "Code" "Ma rkdown"utilizzando il menu di scelta rapida hello nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="cab10-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="cab10-175">Jupyter è molto di più di un elaboratore di testo, in quanto consente di combinare calcolo e contenuti multimediali, ossia testo, grafica, video e qualsiasi altro contenuto visualizzabile in un moderno Web browser.</span><span class="sxs-lookup"><span data-stu-id="cab10-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="cab10-176">È possibile combinare, testo, codice, video e altro ancora!</span><span class="sxs-lookup"><span data-stu-id="cab10-176">You can mix, text, code, videos and more!</span></span>

![Schermata](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="cab10-178">E con la potenza di molte librerie eccellente di Python per il calcolo di scientifici e tecnici, nella seguente schermata hello hello un calcolo semplice può essere eseguito con hello stesso semplificano come un'analisi di rete complessi, in un ambiente.</span><span class="sxs-lookup"><span data-stu-id="cab10-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="cab10-179">Questo paradigma di combinazione di risparmio energia hello Web moderna hello con calcolo in tempo reale offre molte possibilità ed è idealmente appropriato per il cloud hello. è possibile utilizzare Hello Notebook:</span><span class="sxs-lookup"><span data-stu-id="cab10-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="cab10-180">Toorecord un calcolo area dettatura esplorativo collaborare su un problema.</span><span class="sxs-lookup"><span data-stu-id="cab10-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="cab10-181">tooshare risultati con i colleghi, nel modulo di calcolo 'in tempo reale' o in copia cartacea formati (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="cab10-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="cab10-182">toodistribute e presente in tempo reale per insegnanti materiali che implicano il calcolo, in modo studenti sperimentare immediatamente codice effettivo hello, modificarlo ed eseguirla di nuovo in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="cab10-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="cab10-183">tooprovide "paper eseguibile" per visualizzare i risultati hello della ricerca in modo che può essere riprodotta immediatamente, convalidato ed esteso da altri utenti.</span><span class="sxs-lookup"><span data-stu-id="cab10-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="cab10-184">Come piattaforma per il calcolo collaborazione: più utenti possono accedere toothe stesso server notebook tooshare una sessione di calcolo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cab10-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="cab10-185">Se si passa il codice sorgente IPython toohello [repository][repository], si noterà un'intera directory con gli esempi di notebook che è possibile scaricare e quindi provare a utilizzare la propria macchina virtuale Jupyter di Azure.</span><span class="sxs-lookup"><span data-stu-id="cab10-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="cab10-186">Basta scaricare hello `.ipynb` file hello del sito e caricarle in dashboard hello del blocco note macchina virtuale di Azure (o scaricarli direttamente in hello VM).</span><span class="sxs-lookup"><span data-stu-id="cab10-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="cab10-187">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="cab10-187">Conclusion</span></span>
<span data-ttu-id="cab10-188">Hello Server Jupyter Notebook fornisce un'interfaccia potente per accedere in modo interattivo power hello dell'ecosistema di hello Python in Azure.</span><span class="sxs-lookup"><span data-stu-id="cab10-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="cab10-189">Rende possibile un'ampia gamma di casi di utilizzo, tra cui la semplice esplorazione di Python per apprenderne le funzionalità, l'analisi e la visualizzazione di dati, la simulazione e l'elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="cab10-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="cab10-190">documenti Notebook risultanti Hello contengono un record completo dei calcoli hello che vengono eseguiti e possono essere condivisi con altri utenti Jupyter.</span><span class="sxs-lookup"><span data-stu-id="cab10-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="cab10-191">Hello Server Jupyter Notebook può essere utilizzato come un'applicazione locale, ma è ideale per le distribuzioni di cloud in Azure</span><span class="sxs-lookup"><span data-stu-id="cab10-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="cab10-192">funzionalità di base di Hello di Jupyter sono inoltre disponibili all'interno di Visual Studio tramite il [Python Tools per Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="cab10-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="cab10-193">un plug-in open source reso disponibile da Microsoft che trasforma Visual Studio in un ambiente di sviluppo Python avanzato, con l'integrazione di un editor avanzato con IntelliSense, debug, profili ed elaborazione parallela.</span><span class="sxs-lookup"><span data-stu-id="cab10-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab10-194">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cab10-194">Next steps</span></span>
<span data-ttu-id="cab10-195">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="cab10-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
