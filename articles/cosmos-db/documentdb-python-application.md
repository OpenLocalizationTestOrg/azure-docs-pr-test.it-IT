---
title: esercitazione di applicazione web pallone aaaPython per Azure Cosmos DB | Documenti Microsoft
description: Esaminare un'esercitazione database sull'uso di Azure Cosmos DB toostore e accedere ai dati da un'applicazione web di Python pallone ospitato in Azure. Trovare soluzioni di sviluppo dell'applicazione.
keywords: Sviluppo di applicazioni, Python Flask, applicazione Web Python, sviluppo Web Python
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="9b8b5-105">Creare un'applicazione Web Python Flask con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9b8b5-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b8b5-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9b8b5-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="9b8b5-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="9b8b5-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="9b8b5-108">Java</span><span class="sxs-lookup"><span data-stu-id="9b8b5-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="9b8b5-109">Python</span><span class="sxs-lookup"><span data-stu-id="9b8b5-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="9b8b5-110">In questa esercitazione Mostra come toouse Azure Cosmos DB toostore e accedere ai dati da un Python web applicazione ospitata in Azure e si presuppongono di aver esperienza precedente usando Python e siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="9b8b5-111">In questa esercitazione del database vengono trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="9b8b5-112">Creazione e provisioning di un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="9b8b5-113">Creazione di un'applicazione Python Flask.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="9b8b5-114">Connessione tooand utilizzando Cosmos DB dall'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="9b8b5-115">Distribuzione hello tooAzure di applicazione web.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="9b8b5-116">Seguendo questa esercitazione, si creerà una semplice applicazione di voto che consente di toovote per un sondaggio.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Cattura di schermata dell'applicazione di voto hello creata da questa esercitazione database](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="9b8b5-118">Prerequisiti per l'esercitazione del database</span><span class="sxs-lookup"><span data-stu-id="9b8b5-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="9b8b5-119">Prima di seguire le istruzioni di hello in questo articolo, è necessario assicurarsi di aver installato quanto segue hello:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="9b8b5-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-120">An active Azure account.</span></span> <span data-ttu-id="9b8b5-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9b8b5-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="9b8b5-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="9b8b5-123">OR</span></span> 

    <span data-ttu-id="9b8b5-124">Un'installazione locale di hello [emulatore di Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="9b8b5-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="9b8b5-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="9b8b5-127">[Microsoft Azure SDK per Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="9b8b5-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9b8b5-129">Se si sta installando Python 2.7 hello per la prima volta, assicurarsi che nella schermata di Python personalizzare 2.7.13 hello, selezionare **aggiungere python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Cattura di schermata della schermata di Python personalizzare 2.7.11 hello, in cui è necessario tooselect Aggiungi python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="9b8b5-131">[Compilatore Microsoft Visual C++ per Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="9b8b5-132">Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9b8b5-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="9b8b5-133">Creare prima di tutto un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="9b8b5-134">Se è già un account o se si utilizza hello Azure Cosmos DB emulatore per questa esercitazione, è possibile ignorare troppo[passaggio 2: creare una nuova applicazione web Python pallone](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="9b8b5-135">È ora verrà illustrata la modalità messa a terra toocreate una nuova applicazione web di Python pallone da hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="9b8b5-136">Passaggio 2: Creare una nuova applicazione Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="9b8b5-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="9b8b5-137">In Visual Studio, su hello **File** menu, scegliere troppo**New**e quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="9b8b5-138">Hello **nuovo progetto** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="9b8b5-139">Nel riquadro sinistro hello espandere **modelli** e quindi **Python**, quindi fare clic su **Web**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="9b8b5-140">Selezionare **progetto Web pallone** nel riquadro centrale hello, quindi nell'hello **nome** digitare **esercitazione**e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="9b8b5-141">Tenere presente che i nomi di pacchetto di Python devono essere tutti in lettere minuscole, come descritto in hello [Guida di stile per il codice Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="9b8b5-142">Per tali nuovi tooPython pallone, è un framework di sviluppo di applicazioni web che consente di compilare applicazioni web in Python più velocemente.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Cattura di schermata della finestra Nuovo progetto hello in Visual Studio con Python evidenziato nella finestra di sinistra, Python pallone Web progetto selezionato in intermedio hello ed esercitazione nome hello nella casella Nome hello hello](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="9b8b5-144">In hello **Python Tools per Visual Studio** finestra, fare clic su **installare in un ambiente virtuale**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Cattura di schermata dell'esercitazione database hello - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="9b8b5-146">In hello **aggiungere ambiente virtuale** finestra, è possibile accettare le impostazioni predefinite hello e utilizzare Python 2.7 ambiente base hello PyDocumentDB supporta attualmente Python 3. x e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="9b8b5-147">Viene impostata l'ambiente virtuale di Python hello necessario per il progetto.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Cattura di schermata dell'esercitazione database hello - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="9b8b5-149">Visualizza finestra di output di Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quando ambiente hello è stato installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="9b8b5-150">Passaggio 3: Modificare un'applicazione web Python pallone hello</span><span class="sxs-lookup"><span data-stu-id="9b8b5-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="9b8b5-151">Aggiungere hello Python pallone pacchetti tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="9b8b5-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="9b8b5-152">Una volta configurato il progetto, è necessario tooadd hello necessario pallone pacchetti tooyour progetto, inclusi pydocumentdb, pacchetto di Python hello per DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="9b8b5-153">In Esplora soluzioni, aprire il file hello denominato **requirements.txt** e sostituire il contenuto di hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. <span data-ttu-id="9b8b5-154">Salvare hello **requirements.txt** file.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="9b8b5-155">In Esplora soluzioni fare clic con il pulsante destro del mouse su **env** e scegliere **Install from requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Cattura di schermata che mostra env (Python 2.7) selezionato con l'installazione da requirements.txt evidenziato nell'elenco di hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="9b8b5-157">Al termine dell'installazione, finestra di output di hello Visualizza seguente hello:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="9b8b5-158">In rari casi, è possibile visualizzare un errore nella finestra di output di hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="9b8b5-159">In tal caso, controllare se l'errore hello è toocleanup correlati.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="9b8b5-160">Talvolta pulizia hello ha esito negativo, ma sarà comunque possibile eseguire installazione di hello (scorrere verso l'alto tooverify finestra output di hello questo).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="9b8b5-161">È possibile verificare l'installazione da [ambiente virtuale di verifica hello](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="9b8b5-162">Se hello installazione non è riuscita ma hello verifica ha esito positivo, è toocontinue OK.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="9b8b5-163">Verificare l'ambiente virtuale hello</span><span class="sxs-lookup"><span data-stu-id="9b8b5-163">Verify hello virtual environment</span></span>
<span data-ttu-id="9b8b5-164">È importante verificare che tutto sia installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="9b8b5-165">Compilare la soluzione hello premendo **Ctrl**+**MAIUSC**+**B**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="9b8b5-166">Al termine della compilazione hello, avviare il sito Web di hello premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="9b8b5-167">Verrà avviato il server di sviluppo pallone hello e avvia il browser web.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="9b8b5-168">Dovrebbe essere hello dopo.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-168">You should see hello following page.</span></span>
   
    ![Hello Python pallone progetto web vuoto sviluppo visualizzato in un browser](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="9b8b5-170">Arrestare il debug del sito Web hello premendo **MAIUSC**+**F5** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="9b8b5-171">Creare definizioni di database, raccolta e documento</span><span class="sxs-lookup"><span data-stu-id="9b8b5-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="9b8b5-172">Ora viene creata l'applicazione di voto aggiungendo nuovi file e aggiornandone altri.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="9b8b5-173">In Esplora soluzioni fare doppio clic su hello **esercitazione** del progetto, fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="9b8b5-174">Selezionare **File Python vuoto** e nome file di hello **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="9b8b5-175">Aggiungere i seguenti file di codice toohello forms.py hello e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="9b8b5-176">Aggiungere tooviews.py importazioni hello richiesto</span><span class="sxs-lookup"><span data-stu-id="9b8b5-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="9b8b5-177">In Esplora soluzioni espandere hello **esercitazione** cartella e aprire hello **views.py** file.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="9b8b5-178">Aggiungere hello dopo l'importazione istruzioni toohello cima hello **views.py** file, quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="9b8b5-179">Questi importare Cosmos DB PythonSDK e hello pacchetti pallone.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="9b8b5-180">Creare il database, la raccolta e il documento</span><span class="sxs-lookup"><span data-stu-id="9b8b5-180">Create database, collection, and document</span></span>
* <span data-ttu-id="9b8b5-181">Ancora in **views.py**, aggiungere hello successivo toohello codice alla fine del file hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="9b8b5-182">Questo si occupa di creazione del database hello utilizzato dal modulo hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="9b8b5-183">Non eliminare il codice esistente in hello **views.py**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="9b8b5-184">Consente di accodare questo fine toohello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-184">Simply append this toohello end.</span></span>

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="9b8b5-185">Leggere il database, la raccolta e il documento e inviare il form</span><span class="sxs-lookup"><span data-stu-id="9b8b5-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="9b8b5-186">Ancora in **views.py**, aggiungere hello successivo toohello codice alla fine del file hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="9b8b5-187">Questo si occupa della configurazione di modulo hello, la lettura di documenti, raccolta e database hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="9b8b5-188">Non eliminare il codice esistente in hello **views.py**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="9b8b5-189">Consente di accodare questo fine toohello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-189">Simply append this toohello end.</span></span>

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a><span data-ttu-id="9b8b5-190">Creare hello file HTML</span><span class="sxs-lookup"><span data-stu-id="9b8b5-190">Create hello HTML files</span></span>
1. <span data-ttu-id="9b8b5-191">In Esplora soluzioni, in hello **esercitazione** cartella, a destra fare clic su hello **modelli** cartella, fare clic su **Aggiungi**, quindi fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="9b8b5-192">Selezionare **pagina HTML**e quindi nella casella digitare nome di hello **create.html**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="9b8b5-193">Ripetere i passaggi 1 e 2 toocreate due altri file HTML: results.html e vote.html.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="9b8b5-194">Aggiungere hello seguente codice troppo**create.html** in hello `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="9b8b5-195">Consente di visualizzare un messaggio che comunica l'avvenuta creazione di un nuovo database, di una raccolta e di un documento.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="9b8b5-196">Aggiungere hello seguente codice troppo**results.html** in hello `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="9b8b5-197">Visualizza risultati hello di polling hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-197">It displays hello results of hello poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. <span data-ttu-id="9b8b5-198">Aggiungere hello seguente codice troppo**vote.html** in hello `<body`> elemento.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="9b8b5-199">Visualizza il polling di hello e accetta hello voti.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="9b8b5-200">Registrazione voti hello, controllo hello viene passato tramite tooviews.py in cui verrà riconoscere hello voto cast e aggiungere il documento hello conseguenza.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="9b8b5-201">In hello **modelli** Sostituisci hello contenuto della cartella **index.html** con seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="9b8b5-202">Funge da hello pagina per l'applicazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="9b8b5-203">Aggiungere un file di configurazione e modificare hello \_ \_init\_\_. py.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="9b8b5-204">In Esplora soluzioni fare doppio clic su hello **esercitazione** del progetto, fare clic su **Aggiungi**, fare clic su **nuovo elemento**selezionare **File Python vuoto**e quindi file con nome hello **config.py**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="9b8b5-205">Questo file config è necessario per i moduli in Flask.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="9b8b5-206">È possibile utilizzarlo tooprovide anche una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="9b8b5-207">Tale chiave non sarà tuttavia necessaria per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="9b8b5-208">Aggiungere il seguente hello tooconfig.py di codice, è necessario valori hello tooalter di **DOCUMENTDB\_HOST** e **DOCUMENTDB\_chiave** nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="9b8b5-209">In hello [portale di Azure](https://portal.azure.com/), passare toohello **chiavi** pannello facendo **Sfoglia**, **gli account di Azure Cosmos DB**, fare doppio clic sul nome hello di hello toouse dell'account e quindi fare clic su hello **chiavi** pulsante hello **Essentials** area.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="9b8b5-210">In hello **chiavi** blade, hello copia **URI** valore e incollarlo in hello **config.py** file, come valore hello hello **DOCUMENTDB\_HOST**  proprietà.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="9b8b5-211">Nel portale di Azure in hello hello **chiavi** pannello hello copia valore hello **chiave primaria** o hello **chiave secondaria**e incollarlo in hello **config.py**  file, come valore hello hello **DOCUMENTDB\_chiave** proprietà.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="9b8b5-212">In hello  **\_ \_init\_\_py** file, aggiungere hello successiva riga.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="9b8b5-213">In modo che il contenuto del file hello hello è:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="9b8b5-214">Dopo avere aggiunto tutti i file hello, Esplora soluzioni dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9b8b5-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Cattura di schermata della finestra Esplora soluzioni di Visual Studio hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="9b8b5-216">Passaggio 4: Esecuzione dell'applicazione Web in locale</span><span class="sxs-lookup"><span data-stu-id="9b8b5-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="9b8b5-217">Compilare la soluzione hello premendo **Ctrl**+**MAIUSC**+**B**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="9b8b5-218">Al termine della compilazione hello, avviare il sito Web di hello premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="9b8b5-219">Esempio hello dovrebbe sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-219">You should see hello following on your screen.</span></span>
   
    ![Cattura di schermata della hello Python + Cosmos DB voto applicazione Azure visualizzata in un web browser](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="9b8b5-221">Fare clic su **creazione e la cancellazione hello voto Database** database hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Cattura di schermata della hello crea una pagina dell'applicazione web hello-informazioni sullo sviluppo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="9b8b5-223">Fare quindi clic su **Voto** e selezionare un'opzione.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-223">Then, click **Vote** and select your option.</span></span>
   
    ![Cattura di schermata dell'applicazione web hello una domanda voto poste](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="9b8b5-225">Per ogni voto che si esegue il cast, incrementa il numero appropriato di hello.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Cattura di schermata dei risultati della pagina di voto hello illustrato hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="9b8b5-227">Arrestare il debug di progetti hello premendo MAIUSC + F5.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="9b8b5-228">Passaggio 5: Distribuire hello web applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="9b8b5-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="9b8b5-229">Dopo aver creato un'applicazione completa hello funziona correttamente con DB Cosmos, verrà toodeploy questo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="9b8b5-230">Progetto hello pulsante destro del mouse in Esplora soluzioni (assicurarsi che non si è ancora in esecuzione, in locale) e selezionare **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Cattura di schermata dell'esercitazione hello selezionato in Esplora soluzioni, con l'opzione pubblica hello evidenziato](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="9b8b5-232">In hello **pubblica** nella finestra di dialogo **servizio App di Microsoft Azure**selezionare **Crea nuovo**, quindi fare clic su **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Cattura di schermata della finestra di hello pubblica sul Web con Microsoft Azure App Service evidenziato](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="9b8b5-234">In hello **Crea servizio App** finestra di dialogo immettere il nome di hello per le app web con il **sottoscrizione**, **gruppo di risorse**, e **piano di servizio App** , quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Cattura di schermata della finestra di hello finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="9b8b5-236">Dopo alcuni secondi, Visual Studio completerà la pubblicazione del servizio app e avvierà un browser in cui sarà possibile osservare il proprio lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Cattura di schermata della finestra di hello finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="9b8b5-238">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9b8b5-238">Troubleshooting</span></span>
<span data-ttu-id="9b8b5-239">Se si tratta di hello prima applicazione Python è stato eseguito nel computer, verificare che segue hello nella variabile di percorso sono inclusi cartelle (o percorsi di installazione equivalente hello):</span><span class="sxs-lookup"><span data-stu-id="9b8b5-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="9b8b5-240">Se si riceve un errore nella pagina del voto e si nome progetto diverso da **esercitazione**, assicurarsi che  **\_ \_init\_\_py** riferimenti hello Nome progetto corretto nella riga hello: `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b8b5-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b8b5-241">Next steps</span></span>
<span data-ttu-id="9b8b5-242">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-242">Congratulations!</span></span> <span data-ttu-id="9b8b5-243">Solo avere completato la prima applicazione web di Python usando DB Cosmos e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="9b8b5-244">Questo argomento viene aggiornato e migliorato spesso in base al feedback degli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="9b8b5-245">Una volta completati esercitazione hello utilizzando hello voto pulsanti hello superiore e inferiore di questa pagina ed essere tooinclude che commenti e suggerimenti su quali miglioramenti si desidera toosee apportate.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="9b8b5-246">Se desideri toocontact direttamente, ritieni libero tooinclude posta nei commenti.</span><span class="sxs-lookup"><span data-stu-id="9b8b5-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="9b8b5-247">applicazione web tooyour con funzionalità aggiuntive di tooadd, revisione hello API disponibili in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="9b8b5-248">Per ulteriori informazioni su Azure, Visual Studio e Python, vedere hello [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="9b8b5-249">Per ulteriori esercitazioni pallone Python, vedere [hello pallone Mega-esercitazione, Part i: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="9b8b5-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
