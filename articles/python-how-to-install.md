---
title: Installare Python e l'SDK - Azure
description: Informazioni su come installare Python e l'SDK da usare con Azure.
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="6258f-103">Installazione di Python e dell'SDK</span><span class="sxs-lookup"><span data-stu-id="6258f-103">Installing Python and the SDK</span></span>
<span data-ttu-id="6258f-104">Python è semplice da installare in Windows e viene fornito preinstallato in Mac, Linux e [Bash per Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="6258f-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="6258f-105">In questa guida vengono illustrate le procedure per installare il programma e per predisporre il computer per l'utilizzo con Azure.</span><span class="sxs-lookup"><span data-stu-id="6258f-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="6258f-106">Descrizione di Python Azure SDK</span><span class="sxs-lookup"><span data-stu-id="6258f-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="6258f-107">Azure SDK per Python include componenti che consentono di sviluppare, distribuire e gestire applicazioni Python per Azure.</span><span class="sxs-lookup"><span data-stu-id="6258f-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="6258f-108">In particolare, Azure SDK per Python include i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6258f-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="6258f-109">**Librerie di gestione**.</span><span class="sxs-lookup"><span data-stu-id="6258f-109">**Management libraries**.</span></span> <span data-ttu-id="6258f-110">Queste librerie di classe offre un'interfaccia di gestione delle risorse di Azure, come ad esempio gli account di archiviazione e le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6258f-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="6258f-111">**Librerie di runtime**.</span><span class="sxs-lookup"><span data-stu-id="6258f-111">**Runtime libraries**.</span></span> <span data-ttu-id="6258f-112">Queste librerie di classe offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio l'archiviazione e il bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="6258f-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="6258f-113">Tipo e versione di Python da utilizzare</span><span class="sxs-lookup"><span data-stu-id="6258f-113">Which Python and which version to use</span></span>
<span data-ttu-id="6258f-114">Sono disponibili diverse versioni di interpreti Python, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6258f-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="6258f-115">CPython: l'interprete Python standard e più comunemente usato</span><span class="sxs-lookup"><span data-stu-id="6258f-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="6258f-116">PyPy - implementazione alternativa rapida e conforme a CPython</span><span class="sxs-lookup"><span data-stu-id="6258f-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="6258f-117">IronPython: interprete Python eseguito in .NET/CLR</span><span class="sxs-lookup"><span data-stu-id="6258f-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="6258f-118">Jython: interprete Python eseguito sulla macchina virtuale Java</span><span class="sxs-lookup"><span data-stu-id="6258f-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="6258f-119">**CPython** le versioni v2.7 o v3.3+ e PyPy 5.4.0 vengono testate e supportate per Python Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="6258f-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="6258f-120">Dove è possibile reperire Python</span><span class="sxs-lookup"><span data-stu-id="6258f-120">Where to get Python?</span></span>
<span data-ttu-id="6258f-121">È possibile ottenere CPython in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="6258f-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="6258f-122">Direttamente da [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="6258f-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="6258f-123">Da un distributore attendibile, ad esempio [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] o [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="6258f-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="6258f-124">Compilandolo da codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="6258f-124">Build from source!</span></span>

<span data-ttu-id="6258f-125">Salvo esigenze specifiche, si consiglia di scegliere le prime due opzioni.</span><span class="sxs-lookup"><span data-stu-id="6258f-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="6258f-126">Installazione dell'SDK in Windows, Linux e MacOS (solo per le librerie client)</span><span class="sxs-lookup"><span data-stu-id="6258f-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="6258f-127">Se si dispone già di Python installato, è possibile utilizzare pip per installare un bundle di tutte le librerie client nell'ambiente Python 3.3 + o Python 2.7.esistenti.</span><span class="sxs-lookup"><span data-stu-id="6258f-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="6258f-128">I pacchetti verranno scaricati da [Python Package Index][Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="6258f-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="6258f-129">Tale operazione potrebbe richiedere i diritti di amministratore:</span><span class="sxs-lookup"><span data-stu-id="6258f-129">You may need administrator rights:</span></span>

* <span data-ttu-id="6258f-130">Per Linux e MacOS utilizzare il comando `sudo`: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="6258f-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="6258f-131">Windows: aprire il prompt dei comandi PowerShell come amministratore</span><span class="sxs-lookup"><span data-stu-id="6258f-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="6258f-132">È possibile installare singolarmente ogni libreria per ciascun servizio di Azure:</span><span class="sxs-lookup"><span data-stu-id="6258f-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="6258f-133">I pacchetti di anteprima possono essere installati mediante il flag `--pre` :</span><span class="sxs-lookup"><span data-stu-id="6258f-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="6258f-134">È inoltre possibile installare un set di librerie di Azure in una singola riga utilizzando il meta pacchetto `azure` .</span><span class="sxs-lookup"><span data-stu-id="6258f-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="6258f-135">Poiché non tutti i pacchetti presenti in questo meta pacchetto sono già stati pubblicati come stabili, il meta pacchetto `azure` è ancora in anteprima.</span><span class="sxs-lookup"><span data-stu-id="6258f-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="6258f-136">Tuttavia, al momento i pacchetti principali possono essere considerati come stabili dal punto di vista della qualità e della completezza</span><span class="sxs-lookup"><span data-stu-id="6258f-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="6258f-137">La definizione ufficiale avverrà in sincronia con le altre lingue il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="6258f-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="6258f-138">Fino ad allora non si prevedono altre modifiche sostanziali.</span><span class="sxs-lookup"><span data-stu-id="6258f-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="6258f-139">Trattandosi di una versione in anteprima, è necessario utilizzare il flag `--pre` :</span><span class="sxs-lookup"><span data-stu-id="6258f-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="6258f-140">o direttamente</span><span class="sxs-lookup"><span data-stu-id="6258f-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="6258f-141">Altri pacchetti</span><span class="sxs-lookup"><span data-stu-id="6258f-141">Getting More Packages</span></span>
<span data-ttu-id="6258f-142">[Python Package Index][Python Package Index] (PyPI) è una selezione completa di librerie Python.</span><span class="sxs-lookup"><span data-stu-id="6258f-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="6258f-143">Se si è scelto di installare una distribuzione, si disporrà già della maggior parte dei componenti interessanti per vari scenari, dallo sviluppo Web all'informatica tecnica.</span><span class="sxs-lookup"><span data-stu-id="6258f-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="6258f-144">Python Tools per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6258f-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="6258f-145">[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) è un plug-in OSS/gratuito di Microsoft che trasforma VS in un ambiente IDE Python completo:</span><span class="sxs-lookup"><span data-stu-id="6258f-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="6258f-147">Anche se è facoltativo, l'uso di PTVS è consigliabile in quanto offre il supporto per la soluzione o il progetto Python e Web, oltre a funzionalità di debug, definizione dei profili, finestra interattiva, modifica di modelli e IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="6258f-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="6258f-148">PTVS semplifica, inoltre, la distribuzione in Microsoft Azure e supporta la distribuzione in [Servizi cloud](cloud-services/cloud-services-python-ptvs.md) e [Siti Web](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="6258f-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="6258f-149">PTVS funziona con la versione di Visual Studio 2013, 2015 o 2017 attualmente installata.</span><span class="sxs-lookup"><span data-stu-id="6258f-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="6258f-150">Per la documentazione, il download e le discussioni, vedere [Python Tools per Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="6258f-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="6258f-151">Scenari di Python per Azure in Linux e MacOS</span><span class="sxs-lookup"><span data-stu-id="6258f-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="6258f-152">Per Linux o MacOS, ecco gli scenari principali di Azure supportati:</span><span class="sxs-lookup"><span data-stu-id="6258f-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="6258f-153">Uso di Servizi di Azure mediante le librerie client per Python</span><span class="sxs-lookup"><span data-stu-id="6258f-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="6258f-154">Esecuzione dell'app in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="6258f-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="6258f-155">Sviluppo e pubblicazione nei siti Web di Azure tramite Git</span><span class="sxs-lookup"><span data-stu-id="6258f-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="6258f-156">Il primo scenario consente di creare App Web avanzate che sfruttano le funzionalità PaaS di Azure, come l'[archiviazione BLOB](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), l'[archiviazione code](storage/queues/storage-python-how-to-use-queue-storage.md), l'[archiviazione tabelle](cosmos-db/table-storage-how-to-use-python.md) e così via, tramite wrapper di Python per le API REST di Azure.</span><span class="sxs-lookup"><span data-stu-id="6258f-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="6258f-157">Il funzionamento è identico in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="6258f-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="6258f-158">È inoltre possibile usare queste librerie client dal computer di sviluppo locale oppure da una macchina virtuale Linux in esecuzione su Azure.</span><span class="sxs-lookup"><span data-stu-id="6258f-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="6258f-159">Per lo scenario della macchina virtuale, avviare una VM Linux a scelta (Ubuntu, CentOS, Suse) ed eseguire o gestire i componenti desiderati.</span><span class="sxs-lookup"><span data-stu-id="6258f-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="6258f-160">È possibile ad esempio eseguire [IPython][IPython] REPL/Notebook nel computer Windows/Mac/Linux e puntare il browser a una VM multi-processore Linux o Max che esegue il motore IPython in Azure.</span><span class="sxs-lookup"><span data-stu-id="6258f-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="6258f-161">Per informazioni sulla procedura di configurazione di una VM Linux, vedere l'esercitazione [Creare una macchina virtuale che esegue Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6258f-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="6258f-162">Usando la distribuzione GIT, è possibile sviluppare un'applicazione Web di Python e pubblicarla in un sito Web di Azure da qualsiasi sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="6258f-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="6258f-163">Quando si effettua il push del repository in Azure, viene creato automaticamente un ambiente virtuale e tramite pip vengono installati i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="6258f-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="6258f-164">Per altre informazioni su sviluppo e pubblicazione di siti Web di Azure, vedere le esercitazioni [Creazione di siti Web con Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creazione di siti Web con Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md) e [Creazione di siti Web con Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="6258f-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="6258f-165">Per informazioni generali sull'uso di qualsiasi framework compatibile con WSGI, vedere [Configurazione di Python con Siti Web di Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6258f-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="6258f-166">Risorse e software aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="6258f-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="6258f-167">Azure SDK per Python ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="6258f-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="6258f-168">Azure SDK per Python GitHub</span><span class="sxs-lookup"><span data-stu-id="6258f-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="6258f-169">Esempi ufficiali di Azure per Python</span><span class="sxs-lookup"><span data-stu-id="6258f-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="6258f-170">[Distribuzione Python per l'analisi di una sequenza di valori][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6258f-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="6258f-171">[Distribuzione Python di Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6258f-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="6258f-172">[Distribuzione Python di ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="6258f-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="6258f-173">[Serie di librerie scientifiche SciPy per Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="6258f-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="6258f-174">[Serie di librerie numeriche NumPy per Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="6258f-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="6258f-175">[Progetto Django: framework/CMS Web avanzato][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="6258f-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="6258f-176">[IPython: REPL/Notebook avanzato per Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="6258f-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="6258f-177">[Python Tools per Visual Studio su GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="6258f-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="6258f-178">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="6258f-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
