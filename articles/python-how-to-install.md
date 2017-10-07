---
title: aaaInstall Python e hello SDK - Azure
description: Informazioni su come tooinstall Python e hello SDK toouse con Azure.
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="d8265-103">L'installazione di Python e hello SDK</span><span class="sxs-lookup"><span data-stu-id="d8265-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="d8265-104">Python è facile tooset backup in Windows e preinstallata sul Mac, Linux, e [Bash per Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="d8265-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="d8265-105">In questa guida vengono illustrate le procedure per installare il programma e per predisporre il computer per l'utilizzo con Azure.</span><span class="sxs-lookup"><span data-stu-id="d8265-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="d8265-106">Che cos'è in hello Python Azure SDK?</span><span class="sxs-lookup"><span data-stu-id="d8265-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="d8265-107">Hello Azure SDK per Python include i componenti che consentono di toodevelop, distribuiscono e gestire le applicazioni di Python per Azure.</span><span class="sxs-lookup"><span data-stu-id="d8265-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="d8265-108">In particolare, hello Azure SDK per Python include seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d8265-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="d8265-109">**Librerie di gestione**.</span><span class="sxs-lookup"><span data-stu-id="d8265-109">**Management libraries**.</span></span> <span data-ttu-id="d8265-110">Queste librerie di classe offre un'interfaccia di gestione delle risorse di Azure, come ad esempio gli account di archiviazione e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d8265-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="d8265-111">**Librerie di runtime**.</span><span class="sxs-lookup"><span data-stu-id="d8265-111">**Runtime libraries**.</span></span> <span data-ttu-id="d8265-112">Queste librerie di classe offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio l'archiviazione e il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="d8265-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="d8265-113">Quali Python e quali toouse versione</span><span class="sxs-lookup"><span data-stu-id="d8265-113">Which Python and which version toouse</span></span>
<span data-ttu-id="d8265-114">Sono disponibili diverse versioni di interpreti Python, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d8265-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="d8265-115">CPython - interprete Python standard e utilizzate più di frequente di hello</span><span class="sxs-lookup"><span data-stu-id="d8265-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="d8265-116">PyPy - tooCPython implementazione alternativa rapida, conforme</span><span class="sxs-lookup"><span data-stu-id="d8265-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="d8265-117">IronPython: interprete Python eseguito in .NET/CLR</span><span class="sxs-lookup"><span data-stu-id="d8265-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="d8265-118">Jython - interprete Python in esecuzione nella macchina virtuale Java hello</span><span class="sxs-lookup"><span data-stu-id="d8265-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="d8265-119">**CPython** sono testati e supportati per hello Python Azure SDK versione 2.7 o 3.3 + e PyPy 5.4.0.</span><span class="sxs-lookup"><span data-stu-id="d8265-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="d8265-120">Dove tooget Python?</span><span class="sxs-lookup"><span data-stu-id="d8265-120">Where tooget Python?</span></span>
<span data-ttu-id="d8265-121">Esistono diversi modi tooget CPython:</span><span class="sxs-lookup"><span data-stu-id="d8265-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="d8265-122">Direttamente da [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="d8265-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="d8265-123">Da un distributore attendibile, ad esempio [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] o [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="d8265-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="d8265-124">Compilandolo da codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="d8265-124">Build from source!</span></span>

<span data-ttu-id="d8265-125">A meno che non si dispone di una specifica esigenza, si consiglia di hello prime due opzioni.</span><span class="sxs-lookup"><span data-stu-id="d8265-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="d8265-126">Installazione dell'SDK in Windows, Linux e MacOS (solo per le librerie client)</span><span class="sxs-lookup"><span data-stu-id="d8265-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="d8265-127">Se si dispone già di Python installato, è possibile utilizzare pip tooinstall un'aggregazione di tutte le librerie client hello nel esistente Python 2.7 o ambiente Python 3.3 +.</span><span class="sxs-lookup"><span data-stu-id="d8265-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="d8265-128">Ciò Scarica i pacchetti hello da hello [indice del pacchetto Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="d8265-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="d8265-129">Tale operazione potrebbe richiedere i diritti di amministratore:</span><span class="sxs-lookup"><span data-stu-id="d8265-129">You may need administrator rights:</span></span>

* <span data-ttu-id="d8265-130">Linux e MacOS, utilizzare hello `sudo` comando: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="d8265-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="d8265-131">Windows: aprire il prompt dei comandi PowerShell come amministratore</span><span class="sxs-lookup"><span data-stu-id="d8265-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="d8265-132">È possibile installare singolarmente ogni libreria per ciascun servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="d8265-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="d8265-133">Pacchetti di anteprima possono essere installati usando hello `--pre` flag:</span><span class="sxs-lookup"><span data-stu-id="d8265-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="d8265-134">È inoltre possibile installare un set di librerie di Azure in un'unica riga utilizzando hello `azure` meta pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d8265-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="d8265-135">Poiché non tutti i pacchetti in questo pacchetto di metadati vengono pubblicati come stabile ancora, hello `azure` meta pacchetto è ancora in anteprima.</span><span class="sxs-lookup"><span data-stu-id="d8265-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="d8265-136">Tuttavia, i pacchetti di base hello, ottica/completezza di qualità di codice possono essere considerati "stabili" in questo momento</span><span class="sxs-lookup"><span data-stu-id="d8265-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="d8265-137">La definizione ufficiale avverrà in sincronia con le altre lingue il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="d8265-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="d8265-138">Fino ad allora non si prevedono altre modifiche sostanziali.</span><span class="sxs-lookup"><span data-stu-id="d8265-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="d8265-139">Poiché si tratta di una versione di anteprima, è necessario toouse hello `--pre` flag:</span><span class="sxs-lookup"><span data-stu-id="d8265-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="d8265-140">o direttamente</span><span class="sxs-lookup"><span data-stu-id="d8265-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="d8265-141">Altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="d8265-141">Getting More Packages</span></span>
<span data-ttu-id="d8265-142">Hello [indice del pacchetto Python] [ Python Package Index] (PyPI) è una selezione avanzata delle librerie di Python.</span><span class="sxs-lookup"><span data-stu-id="d8265-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="d8265-143">Se si sceglie tooinstall una distribuzione, è necessario già la maggior parte delle hello interessanti bits per vari scenari da web sviluppo tooTechnical Computing.</span><span class="sxs-lookup"><span data-stu-id="d8265-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="d8265-144">Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8265-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="d8265-145">[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) è un plug-in OSS/gratuito di Microsoft che trasforma VS in un ambiente IDE Python completo:</span><span class="sxs-lookup"><span data-stu-id="d8265-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="d8265-147">Anche se è facoltativo, l'uso di PTVS è consigliabile in quanto offre il supporto per la soluzione o il progetto Python e Web, oltre a funzionalità di debug, definizione dei profili, finestra interattiva, modifica di modelli e IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="d8265-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="d8265-148">PTVS rende facile toodeploy tooMicrosoft, Azure, con supporto per la distribuzione troppo[servizi Cloud](cloud-services/cloud-services-python-ptvs.md) e [siti Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="d8265-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="d8265-149">PTVS funziona con la versione di Visual Studio 2013, 2015 o 2017 attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="d8265-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="d8265-150">Per la documentazione, il download e le discussioni, vedere [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="d8265-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="d8265-151">Scenari di Python per Azure in Linux e MacOS</span><span class="sxs-lookup"><span data-stu-id="d8265-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="d8265-152">Per Linux o MacOS, ecco gli scenari principali di Azure supportati:</span><span class="sxs-lookup"><span data-stu-id="d8265-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="d8265-153">Utilizzo di servizi di Azure tramite le librerie client hello per Python</span><span class="sxs-lookup"><span data-stu-id="d8265-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="d8265-154">Esecuzione dell'app in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="d8265-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="d8265-155">Lo sviluppo e la pubblicazione di siti Web tooAzure tramite Git</span><span class="sxs-lookup"><span data-stu-id="d8265-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="d8265-156">primo scenario Hello consente le app web avanzati tooauthor usufruire di hello funzionalità PaaS di Azure, ad esempio [nell'archiviazione blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [coda archiviazione](storage/queues/storage-python-how-to-use-queue-storage.md), [archivio tabelle](cosmos-db/table-storage-how-to-use-python.md) via via Pythonic wrapper per hello API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="d8265-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="d8265-157">Il funzionamento è identico in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="d8265-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="d8265-158">È inoltre possibile usare queste librerie client dal computer di sviluppo locale oppure da una macchina virtuale Linux in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="d8265-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="d8265-159">Scenario di VM hello, avviare una VM Linux di propria scelta (Ubuntu, CentOS, Suse) e si desidera/gestire esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d8265-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="d8265-160">Ad esempio, è possibile eseguire [IPython] [ IPython] REPL/notebook nel punto del browser tooa Linux o VM in esecuzione più processi di Windows hello motore IPython in Azure e computer Mac/Windows/Linux.</span><span class="sxs-lookup"><span data-stu-id="d8265-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="d8265-161">Per informazioni su come tooset di una VM Linux, vedere hello [creare una macchina virtuale che esegue Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d8265-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="d8265-162">Mediante la distribuzione Git, è possibile sviluppare un'applicazione web di Python e pubblicarlo tooan sito Web di Azure da qualsiasi sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d8265-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="d8265-163">Quando si esegue il push tooAzure del repository, viene creato automaticamente un ambiente virtuale e pip installa i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="d8265-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="d8265-164">Per ulteriori informazioni sullo sviluppo e la pubblicazione di siti Web di Azure, vedere le esercitazioni di hello per [la creazione di siti Web con Django](app-service-web/web-sites-python-create-deploy-django-app.md), [la creazione di siti Web con Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), e [la creazione di siti Web con Pallone](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8265-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="d8265-165">Per informazioni generali sull'uso di qualsiasi framework compatibile con WSGI, vedere [Configurazione di Python con Siti Web di Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d8265-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="d8265-166">Risorse e software aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="d8265-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="d8265-167">Azure SDK per Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="d8265-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="d8265-168">Azure SDK per Python GitHub</span><span class="sxs-lookup"><span data-stu-id="d8265-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="d8265-169">Esempi ufficiali di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="d8265-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="d8265-170">[Distribuzione Python per l'analisi di una sequenza di valori][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="d8265-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="d8265-171">[Distribuzione Python di Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="d8265-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="d8265-172">[Distribuzione Python di ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="d8265-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="d8265-173">[Serie di librerie scientifiche SciPy per Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="d8265-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="d8265-174">[Serie di librerie numeriche NumPy per Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="d8265-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="d8265-175">[Progetto Django: framework/CMS Web avanzato][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="d8265-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="d8265-176">[IPython: REPL/Notebook avanzato per Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="d8265-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="d8265-177">[Python Tools per Visual Studio su GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="d8265-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="d8265-178">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="d8265-178">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Python Tools per Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
