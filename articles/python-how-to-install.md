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
# <a name="installing-python-and-hello-sdk"></a>L'installazione di Python e hello SDK
Python è facile tooset backup in Windows e preinstallata sul Mac, Linux, e [Bash per Windows](https://msdn.microsoft.com/commandline/wsl/about). In questa guida vengono illustrate le procedure per installare il programma e per predisporre il computer per l'utilizzo con Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>Che cos'è in hello Python Azure SDK?
Hello Azure SDK per Python include i componenti che consentono di toodevelop, distribuiscono e gestire le applicazioni di Python per Azure. In particolare, hello Azure SDK per Python include seguente hello:

* **Librerie di gestione**. Queste librerie di classe offre un'interfaccia di gestione delle risorse di Azure, come ad esempio gli account di archiviazione e le macchine virtuali.
* **Librerie di runtime**. Queste librerie di classe offrono un'interfaccia per accedere alle funzionalità di Azure, ad esempio l'archiviazione e il bus di servizio.

## <a name="which-python-and-which-version-toouse"></a>Quali Python e quali toouse versione
Sono disponibili diverse versioni di interpreti Python, ad esempio:

* CPython - interprete Python standard e utilizzate più di frequente di hello
* PyPy - tooCPython implementazione alternativa rapida, conforme
* IronPython: interprete Python eseguito in .NET/CLR
* Jython - interprete Python in esecuzione nella macchina virtuale Java hello

**CPython** sono testati e supportati per hello Python Azure SDK versione 2.7 o 3.3 + e PyPy 5.4.0.

## <a name="where-tooget-python"></a>Dove tooget Python?
Esistono diversi modi tooget CPython:

* Direttamente da [www.python.org][www.python.org]
* Da un distributore attendibile, ad esempio [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] o [www.activestate.com][www.activestate.com]
* Compilandolo da codice sorgente.

A meno che non si dispone di una specifica esigenza, si consiglia di hello prime due opzioni.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Installazione dell'SDK in Windows, Linux e MacOS (solo per le librerie client)
Se si dispone già di Python installato, è possibile utilizzare pip tooinstall un'aggregazione di tutte le librerie client hello nel esistente Python 2.7 o ambiente Python 3.3 +. Ciò Scarica i pacchetti hello da hello [indice del pacchetto Python] [ Python Package Index] (PyPI).

Tale operazione potrebbe richiedere i diritti di amministratore:

* Linux e MacOS, utilizzare hello `sudo` comando: `sudo pip install azure-mgmt-compute`.
* Windows: aprire il prompt dei comandi PowerShell come amministratore

È possibile installare singolarmente ogni libreria per ciascun servizio di Azure:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Pacchetti di anteprima possono essere installati usando hello `--pre` flag:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

È inoltre possibile installare un set di librerie di Azure in un'unica riga utilizzando hello `azure` meta pacchetto. Poiché non tutti i pacchetti in questo pacchetto di metadati vengono pubblicati come stabile ancora, hello `azure` meta pacchetto è ancora in anteprima.
Tuttavia, i pacchetti di base hello, ottica/completezza di qualità di codice possono essere considerati "stabili" in questo momento

* La definizione ufficiale avverrà in sincronia con le altre lingue il prima possibile.
  Fino ad allora non si prevedono altre modifiche sostanziali.

Poiché si tratta di una versione di anteprima, è necessario toouse hello `--pre` flag:

```console
   $ pip install --pre azure
```

o direttamente

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Altri pacchetti
Hello [indice del pacchetto Python] [ Python Package Index] (PyPI) è una selezione avanzata delle librerie di Python.  Se si sceglie tooinstall una distribuzione, è necessario già la maggior parte delle hello interessanti bits per vari scenari da web sviluppo tooTechnical Computing.

## <a name="python-tools-for-visual-studio"></a>Python Tools per Visual Studio
[Python Tools per Visual Studio][Python Tools per Visual Studio] (PTVS) è un plug-in OSS/gratuito di Microsoft che trasforma VS in un ambiente IDE Python completo:

![how-to-install-python-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

Anche se è facoltativo, l'uso di PTVS è consigliabile in quanto offre il supporto per la soluzione o il progetto Python e Web, oltre a funzionalità di debug, definizione dei profili, finestra interattiva, modifica di modelli e IntelliSense.

PTVS rende facile toodeploy tooMicrosoft, Azure, con supporto per la distribuzione troppo[servizi Cloud](cloud-services/cloud-services-python-ptvs.md) e [siti Web](app-service-web/web-sites-python-ptvs-django-mysql.md).

PTVS funziona con la versione di Visual Studio 2013, 2015 o 2017 attualmente installata.  Per la documentazione, il download e le discussioni, vedere [Python Tools per Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Scenari di Python per Azure in Linux e MacOS
Per Linux o MacOS, ecco gli scenari principali di Azure supportati:

1. Utilizzo di servizi di Azure tramite le librerie client hello per Python
2. Esecuzione dell'app in una macchina virtuale Linux
3. Lo sviluppo e la pubblicazione di siti Web tooAzure tramite Git

primo scenario Hello consente le app web avanzati tooauthor usufruire di hello funzionalità PaaS di Azure, ad esempio [nell'archiviazione blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [coda archiviazione](storage/queues/storage-python-how-to-use-queue-storage.md), [archivio tabelle](cosmos-db/table-storage-how-to-use-python.md) via via Pythonic wrapper per hello API REST di Azure. Il funzionamento è identico in Windows, Mac e Linux.  È inoltre possibile usare queste librerie client dal computer di sviluppo locale oppure da una macchina virtuale Linux in esecuzione su Azure.

Scenario di VM hello, avviare una VM Linux di propria scelta (Ubuntu, CentOS, Suse) e si desidera/gestire esecuzione.  Ad esempio, è possibile eseguire [IPython] [ IPython] REPL/notebook nel punto del browser tooa Linux o VM in esecuzione più processi di Windows hello motore IPython in Azure e computer Mac/Windows/Linux.

Per informazioni su come tooset di una VM Linux, vedere hello [creare una macchina virtuale che esegue Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) esercitazione.

Mediante la distribuzione Git, è possibile sviluppare un'applicazione web di Python e pubblicarlo tooan sito Web di Azure da qualsiasi sistema operativo.  Quando si esegue il push tooAzure del repository, viene creato automaticamente un ambiente virtuale e pip installa i pacchetti necessari.

Per ulteriori informazioni sullo sviluppo e la pubblicazione di siti Web di Azure, vedere le esercitazioni di hello per [la creazione di siti Web con Django](app-service-web/web-sites-python-create-deploy-django-app.md), [la creazione di siti Web con Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), e [la creazione di siti Web con Pallone](app-service-web/web-sites-python-create-deploy-flask-app.md). Per informazioni generali sull'uso di qualsiasi framework compatibile con WSGI, vedere [Configurazione di Python con Siti Web di Azure](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Risorse e software aggiuntivi:
* [Azure SDK per Python ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [Azure SDK per Python GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Esempi ufficiali di Azure per Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Distribuzione Python per l'analisi di una sequenza di valori][Continuum Analytics Python Distribution]
* [Distribuzione Python di Enthought][Enthought Python Distribution]
* [Distribuzione Python di ActiveState][ActiveState Python Distribution]
* [Serie di librerie scientifiche SciPy per Python][SciPy - A suite of Scientific Python libraries]
* [Serie di librerie numeriche NumPy per Python][NumPy - A numerics library for Python]
* [Progetto Django: framework/CMS Web avanzato][Django Project - A mature web framework/CMS]
* [IPython: REPL/Notebook avanzato per Python][IPython - an advanced REPL/Notebook for Python]
* [Python Tools per Visual Studio su GitHub][Python Tools for Visual Studio on GitHub]
* [Centro per sviluppatori Python](/develop/python/)

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
