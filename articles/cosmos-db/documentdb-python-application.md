---
title: Esercitazione per un'applicazione Web Python Flask per Azure Cosmos DB | Microsoft Docs
description: Esaminare un'esercitazione del database sull'utilizzo di Azure Cosmos DB per archiviare e accedere ai dati da un'applicazione web Python Flask ospitata in Azure. Trovare soluzioni di sviluppo dell'applicazione.
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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="1a3a2-105">Creare un'applicazione Web Python Flask con Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a3a2-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a3a2-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1a3a2-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="1a3a2-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="1a3a2-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="1a3a2-108">Java</span><span class="sxs-lookup"><span data-stu-id="1a3a2-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="1a3a2-109">Python</span><span class="sxs-lookup"><span data-stu-id="1a3a2-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="1a3a2-110">Questa esercitazione mostra come usare Azure Cosmos DB per archiviare e accedere ai dati forniti da un'applicazione Web Python ospitata in Azure e presuppone che si siano già usati Python e Siti Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="1a3a2-111">In questa esercitazione del database vengono trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="1a3a2-112">Creazione e provisioning di un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="1a3a2-113">Creazione di un'applicazione Python Flask.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="1a3a2-114">Connettersi e usare Azure Cosmos DB dall'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="1a3a2-115">Distribuzione dell'applicazione Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="1a3a2-116">Seguendo questa esercitazione, si creerà una semplice applicazione di voto che consente di votare per un sondaggio.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Screenshot dell'applicazione di voto creata in questa esercitazione del database](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="1a3a2-118">Prerequisiti per l'esercitazione del database</span><span class="sxs-lookup"><span data-stu-id="1a3a2-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="1a3a2-119">Prima di seguire le istruzioni di questo articolo, verificare che siano disponibili i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="1a3a2-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-120">An active Azure account.</span></span> <span data-ttu-id="1a3a2-121">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1a3a2-122">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="1a3a2-123">OPPURE</span><span class="sxs-lookup"><span data-stu-id="1a3a2-123">OR</span></span> 

    <span data-ttu-id="1a3a2-124">Un'installazione locale dell'[emulatore Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="1a3a2-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="1a3a2-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="1a3a2-127">[Microsoft Azure SDK per Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="1a3a2-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1a3a2-129">Se si installa Python 2.7 per la prima volta, nella schermata Customize Python 2.7.13 (Personalizza Python 2.7.13) assicurarsi di selezionare **Add python.exe to Path** (Aggiungi python.exe a percorso).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Schermata Customize Python 2.7.11, in cui è necessario selezionare Add python.exe to Path](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="1a3a2-131">[Compilatore Microsoft Visual C++ per Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="1a3a2-132">Passaggio 1: Creare un account del database di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a3a2-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="1a3a2-133">Creare prima di tutto un account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="1a3a2-134">Se si ha già un account o si usa l'emulatore Azure Cosmos DB per questa esercitazione, è possibile andare al [Passaggio 2: Creare una nuova applicazione Web Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="1a3a2-135">Verrà ora illustrata in dettaglio la procedura per creare un'applicazione Web Python Flask completamente nuova.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="1a3a2-136">Passaggio 2: Creare una nuova applicazione Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="1a3a2-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="1a3a2-137">Scegliere **Nuovo** dal menu **File** di Visual Studio e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="1a3a2-138">Verrà visualizzata la finestra di dialogo **Nuovo progetto** .</span><span class="sxs-lookup"><span data-stu-id="1a3a2-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="1a3a2-139">Nel riquadro sinistro espandere **Modelli** e quindi **Python**, quindi fare clic su **Web**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="1a3a2-140">Selezionare **Flask Web Project** (Progetto Web Flask) nel riquadro centrale, quindi digitare **tutorial** (esercitazione) nella casella **Nome** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="1a3a2-141">Tenere presente che i nomi di pacchetto Python devono essere tutti in lettere minuscole, come descritto nella [guida di stile per il codice Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="1a3a2-142">Se è la prima volta che si usa Python Flask, si tratta di un framework di sviluppo di applicazioni Web che consente di creare applicazioni Web in Python più velocemente.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Schermata della finestra Nuovo progetto in Visual Studio con Python selezionato a sinistra, progetto web Flask selezionato nella parte centrale ed esercitazioni sul nome nella casella nome](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="1a3a2-144">Nella finestra **Python Tools for Visual Studio** selezionare **Install into a virtual environment** (Installa in un ambiente virtuale).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Schermata dell'esercitazione del database - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="1a3a2-146">Nella finestra **Add Virtual Environment** (Aggiungi ambiente virtuale) è possibile accettare le impostazioni predefinite e usare Python 2.7 come ambiente di base, perché PyDocumentDB attualmente non supporta Python 3.x, quindi fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="1a3a2-147">Questo permette di configurare l'ambiente virtuale Python per il progetto.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Schermata dell'esercitazione del database - Python Tools per la finestra di Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="1a3a2-149">Se l'installazione dell'ambiente riesce, nella finestra di output verrà visualizzato il messaggio `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` .</span><span class="sxs-lookup"><span data-stu-id="1a3a2-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="1a3a2-150">Passaggio 3: Modificare l'applicazione Web Python Flask</span><span class="sxs-lookup"><span data-stu-id="1a3a2-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="1a3a2-151">Aggiungere i pacchetti Python Flask al progetto</span><span class="sxs-lookup"><span data-stu-id="1a3a2-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="1a3a2-152">Dopo la configurazione del progetto sarà necessario aggiungere i pacchetti Flask necessari per il progetto, compreso pydocumentdb, il pacchetto python per DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="1a3a2-153">In Esplora soluzioni aprire il file denominato **requirements.txt** e sostituire il contenuto esistente con quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="1a3a2-154">Salvare il file **requirements.txt** .</span><span class="sxs-lookup"><span data-stu-id="1a3a2-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="1a3a2-155">In Esplora soluzioni fare clic con il pulsante destro del mouse su **env** e scegliere **Install from requirements.txt**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Schermata che mostra env (Python 2.7) selezionata con l'installazione da requirements.txt evidenziato nell'elenco](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="1a3a2-157">Al termine dell'installazione, la finestra di output visualizza quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="1a3a2-158">In rari casi è possibile che venga visualizzato un errore nella finestra di output.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="1a3a2-159">In un'eventualità di questo tipo, verificare se l'errore è correlato alla pulizia.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="1a3a2-160">Talvolta la pulizia può avere esito negativo, ma l'installazione viene comunque completata correttamente (scorrere verso l'alto nella finestra di output per verificarlo).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="1a3a2-161">È possibile controllare l'installazione [verificando l'ambiente virtuale](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="1a3a2-162">Se l'installazione non è riuscita, ma la verifica ha esito positivo, è possibile continuare.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="1a3a2-163">Verifica dell'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="1a3a2-163">Verify the virtual environment</span></span>
<span data-ttu-id="1a3a2-164">È importante verificare che tutto sia installato correttamente.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="1a3a2-165">Premere **CTRL**+**MAIUSC**+**B** per compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="1a3a2-166">Al termine della compilazione, avviare il sito Web premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="1a3a2-167">Verranno avviati il server di sviluppo Flask e il Web browser.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="1a3a2-168">Dovrebbe essere visualizzata la pagina seguente:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-168">You should see the following page.</span></span>
   
    ![Il progetto di sviluppo web Python Flask vuoto visualizzato in un browser](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="1a3a2-170">Per arrestare il debug del sito Web, premere **MAIUSC**+**F5**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="1a3a2-171">Creare definizioni di database, raccolta e documento</span><span class="sxs-lookup"><span data-stu-id="1a3a2-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="1a3a2-172">Ora viene creata l'applicazione di voto aggiungendo nuovi file e aggiornandone altri.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="1a3a2-173">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **tutorial**, (esercitazione) quindi scegliere **Aggiungi** e infine **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="1a3a2-174">Selezionare **Empty Python File** (File di Python vuoto) e denominare il file **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="1a3a2-175">Aggiungere il codice seguente al file forms.py e quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="1a3a2-176">Aggiungere le importazioni necessarie a views.py</span><span class="sxs-lookup"><span data-stu-id="1a3a2-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="1a3a2-177">In Esplora soluzioni espandere la cartella **tutorial** (esercitazione) e aprire il file **views.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="1a3a2-178">Aggiungere le istruzioni import seguenti all'inizio del file **views.py** e quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="1a3a2-179">Queste importano i pacchetti PythonSDK e Flask di Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="1a3a2-180">Creare il database, la raccolta e il documento</span><span class="sxs-lookup"><span data-stu-id="1a3a2-180">Create database, collection, and document</span></span>
* <span data-ttu-id="1a3a2-181">Ancora in **views.py**aggiungere il codice seguente alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="1a3a2-182">Verrà creato il database usato dal form.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="1a3a2-183">Non eliminare nessuna porzione del codice esistente dal file **views.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="1a3a2-184">Aggiungere semplicemente la parte nuova alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-184">Simply append this to the end.</span></span>

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="1a3a2-185">Leggere il database, la raccolta e il documento e inviare il form</span><span class="sxs-lookup"><span data-stu-id="1a3a2-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="1a3a2-186">Ancora in **views.py**aggiungere il codice seguente alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="1a3a2-187">Verrà configurato il form e verranno letti il database, la raccolta e il documento.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="1a3a2-188">Non eliminare nessuna porzione del codice esistente dal file **views.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="1a3a2-189">Aggiungere semplicemente la parte nuova alla fine del file.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-189">Simply append this to the end.</span></span>

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

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
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


### <a name="create-the-html-files"></a><span data-ttu-id="1a3a2-190">Creare i file HTML</span><span class="sxs-lookup"><span data-stu-id="1a3a2-190">Create the HTML files</span></span>
1. <span data-ttu-id="1a3a2-191">Nella cartella **tutorial** (esercitazione) in Esplora soluzioni fare clic con il pulsante destro del mouse sulla cartella **modelli**, scegliere **Aggiungi** e infine **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="1a3a2-192">Selezionare **Pagina HTML** e nella casella del nome digitare **create.html**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="1a3a2-193">Ripetere i passaggi 1 e 2 per creare altri due file HTML: results.html e vote.html.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="1a3a2-194">Aggiungere il codice seguente al file **create.html** in the `<body>` .</span><span class="sxs-lookup"><span data-stu-id="1a3a2-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="1a3a2-195">Consente di visualizzare un messaggio che comunica l'avvenuta creazione di un nuovo database, di una raccolta e di un documento.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="1a3a2-196">Aggiungere il codice seguente al file **results.html** nell'elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="1a3a2-197">Consente di visualizzare i risultati del sondaggio.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-197">It displays the results of the poll.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
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
6. <span data-ttu-id="1a3a2-198">Aggiungere il codice seguente al file **vote.html** nell'elemento `<body`>.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="1a3a2-199">Consente di visualizzare il sondaggio e di accettare i voti.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="1a3a2-200">Alla registrazione dei voti il controllo viene passato a views.py che riconoscerà il voto espresso e ne effettuerà l'aggiunta al documento.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. <span data-ttu-id="1a3a2-201">Nella cartella **modelli** sostituire il contenuto del file **index.html** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="1a3a2-202">Questo fungerà da pagina di destinazione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="1a3a2-203">Aggiungere un file di configurazione e modificare \_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="1a3a2-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="1a3a2-204">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **tutorial** (esercitazione), scegliere **Aggiungi**, **Nuovo elemento** e infine **Empty Python File** (File di Python vuoto), quindi denominare il file **config.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="1a3a2-205">Questo file config è necessario per i moduli in Flask.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="1a3a2-206">È possibile usarlo anche per fornire una chiave privata.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="1a3a2-207">Tale chiave non sarà tuttavia necessaria per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="1a3a2-208">Aggiungere il codice seguente al file config.py. Nel passaggio successivo sarà necessario modificare i valori di **DOCUMENTDB\_HOST** e **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="1a3a2-209">Nel [portale di Azure](https://portal.azure.com/) passare al pannello **Chiavi** facendo clic su **Esplora** e quindi su **Account Azure Cosmos DB**, fare doppio clic sul nome dell'account da usare e quindi fare clic sul pulsante **Chiavi** nell'area **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="1a3a2-210">Nel pannello **Chiavi** copiare il valore **URI** e incollarlo nel file **config.py** come valore della proprietà **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="1a3a2-211">Tornare al portale di Azure. Nel pannello **Chiavi** copiare il valore della **Chiave primaria** o della **Chiave secondaria** e incollarlo nel file **config.py** come valore della proprietà **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="1a3a2-212">Aggiungere la riga seguente al file **\_\_init\_\_.py**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="1a3a2-213">Il contenuto del file deve essere analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="1a3a2-214">Dopo aver aggiunto tutti i file, l'aspetto di Esplora soluzioni dovrebbe risultare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Schermata della finestra Esplora soluzioni di Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="1a3a2-216">Passaggio 4: Esecuzione dell'applicazione Web in locale</span><span class="sxs-lookup"><span data-stu-id="1a3a2-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="1a3a2-217">Premere **CTRL**+**MAIUSC**+**B** per compilare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="1a3a2-218">Al termine della compilazione, avviare il sito Web premendo **F5**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="1a3a2-219">Dovrebbe venire visualizzata la schermata seguente.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-219">You should see the following on your screen.</span></span>
   
    ![Screenshot di Python e dell'applicazione per votazione di Azure Cosmos DB visualizzati in un Web browser](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="1a3a2-221">Fare clic su **Create/Clear the Voting Database** per generare il database.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Schermata della pagina di creazione dell'applicazione web - informazioni dettagliate sullo sviluppo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="1a3a2-223">Fare quindi clic su **Voto** e selezionare un'opzione.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-223">Then, click **Vote** and select your option.</span></span>
   
    ![Schermata dell'applicazione Web con una domanda relativa al voto](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="1a3a2-225">Ogni voto espresso va a incrementare il contatore appropriato.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Schermata dei risultati della pagina voto visualizzata](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="1a3a2-227">Per arrestare il debug del sito Web, premere MAIUSC+F5.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="1a3a2-228">Passaggio 5: Distribuire l'applicazione Web in Azure</span><span class="sxs-lookup"><span data-stu-id="1a3a2-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="1a3a2-229">Ora che l'applicazione completa funziona correttamente su Cosmos DB, è possibile distribuirla in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="1a3a2-230">Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, assicurarsi che il progetto non sia ancora in esecuzione localmente e quindi selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Schermata dell'esercitazione selezionata in Esplora soluzioni, con l'opzione Pubblica evidenziata](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="1a3a2-232">Nella finestra di dialogo **Pubblica** selezionare **Servizio app di Microsoft Azure**, selezionare **Crea nuovo** e quindi fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Screenshot della finestra Pubblica sul Web con Servizio app di Microsoft Azure evidenziato](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="1a3a2-234">Nella finestra di dialogo **Crea servizio app** immettere il nome dell'app Web, specificando anche **Sottoscrizione**, **Gruppo di risorse** e **Piano di Servizio app**, quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Screenshot della finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="1a3a2-236">Dopo alcuni secondi, Visual Studio completerà la pubblicazione del servizio app e avvierà un browser in cui sarà possibile osservare il proprio lavoro in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Screenshot della finestra App Web di Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="1a3a2-238">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1a3a2-238">Troubleshooting</span></span>
<span data-ttu-id="1a3a2-239">Se si tratta della prima app Python eseguita nel computer, assicurarsi che le cartelle seguenti o i percorsi di installazione equivalenti siano inclusi nella variabile PATH:</span><span class="sxs-lookup"><span data-stu-id="1a3a2-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="1a3a2-240">Se si riceve un errore nella pagina di voto e il progetto ha un nome diverso da **tutorial** (esercitazione), assicurarsi che **\_\_init\_\_.py** faccia riferimento al nome di progetto corretto nella riga `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a3a2-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a3a2-241">Next steps</span></span>
<span data-ttu-id="1a3a2-242">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-242">Congratulations!</span></span> <span data-ttu-id="1a3a2-243">È stata appena creata la prima applicazione Web Python con Cosmos DB, che è stata quindi pubblicata in Azure.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="1a3a2-244">Questo argomento viene aggiornato e migliorato spesso in base al feedback degli utenti.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="1a3a2-245">Dopo aver completato l'esercitazione, utilizzare i pulsanti per la votazione nella parte superiore e inferiore della pagina e assicurarsi di includere il feedback sui miglioramenti che si desidera vedere.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="1a3a2-246">Se si desidera contattarci, è possibile includere l'indirizzo di posta elettronica nel commento per il follow-up.</span><span class="sxs-lookup"><span data-stu-id="1a3a2-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="1a3a2-247">Per aggiungere altre funzionalità all'applicazione Web, esaminare le API disponibili in [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="1a3a2-248">Per altre informazioni su Azure, Visual Studio e Python, vedere il [centro per sviluppatori di Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="1a3a2-249">Per altre esercitazioni su Python Flask, vedere [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world)(Esercitazione su Flask, parte I: Hello, World!).</span><span class="sxs-lookup"><span data-stu-id="1a3a2-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
