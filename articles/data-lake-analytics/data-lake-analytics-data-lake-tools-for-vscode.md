---
title: 'Strumenti Azure Data Lake: Usare Strumenti Azure Data Lake per Visual Studio Code | Microsoft Docs'
description: 'Informazioni su come toouse Azure Data Lake Tools per Visual Studio Code toocreate, testare ed eseguire gli script U-SQL. '
Keywords: Percorso di toostorage di caricamento di VScode, strumenti di Azure Data Lake, esecuzione, file di archiviazione locale di debug, eseguire il Debug locale, anteprima locale
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="057b5-104">Usare gli Strumenti Azure Data Lake per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="057b5-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="057b5-105">Informazioni su come toouse Azure Data Lake Tools per Visual Studio Code (codice di Visual Studio) toocreate, testare ed eseguire gli script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="057b5-106">informazioni di Hello sono anche incluso in hello video seguente:</span><span class="sxs-lookup"><span data-stu-id="057b5-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="057b5-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="057b5-107">Prerequisites</span></span>

<span data-ttu-id="057b5-108">Data Lake Tools può essere installato su piattaforme hello supportate dal codice di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="057b5-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="057b5-109">piattaforme supportata Hello includono Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="057b5-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="057b5-110">diverse piattaforme Hello hanno hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="057b5-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="057b5-111">Windows</span><span class="sxs-lookup"><span data-stu-id="057b5-111">Windows</span></span>

    - <span data-ttu-id="057b5-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="057b5-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="057b5-113">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="057b5-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="057b5-114">Aggiungere hello java.exe toohello sistema ambiente variabile percorso.</span><span class="sxs-lookup"><span data-stu-id="057b5-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="057b5-115">Per istruzioni sulla configurazione, vedere [come impostare o modificare una variabile di sistema Path hello?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="057b5-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="057b5-116">percorso di Hello è tooC:\Program Files\Java\jdk1.8.0_77\jre\bin simile.</span><span class="sxs-lookup"><span data-stu-id="057b5-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="057b5-117">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="057b5-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="057b5-118">Linux (è consigliabile scegliere Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="057b5-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="057b5-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="057b5-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="057b5-120">tooinstall hello codice, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="057b5-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="057b5-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="057b5-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="057b5-122">pacchetto di deb hello tooupdate del codice sorgente, immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="057b5-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="057b5-123">tooinstall Mono, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="057b5-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="057b5-124">Mono 4.6 non è supportato.</span><span class="sxs-lookup"><span data-stu-id="057b5-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="057b5-125">Disinstallare completamente la versione 4.6 prima di installare la versione 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="057b5-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="057b5-126">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="057b5-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="057b5-127">Per istruzioni sull'installazione, vedere hello [Linux a 64 bit di istruzioni di installazione per Java]( https://java.com/en/download/help/linux_x64_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="057b5-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="057b5-128">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="057b5-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="057b5-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="057b5-129">MacOS</span></span>

    - <span data-ttu-id="057b5-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="057b5-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="057b5-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="057b5-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="057b5-132">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="057b5-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="057b5-133">Per istruzioni sull'installazione, vedere hello [Linux a 64 bit di istruzioni di installazione per Java](https://java.com/en/download/help/mac_install.xml) pagina.</span><span class="sxs-lookup"><span data-stu-id="057b5-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="057b5-134">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="057b5-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="057b5-135">Installare gli strumenti di Data Lake</span><span class="sxs-lookup"><span data-stu-id="057b5-135">Install Data Lake Tools</span></span>

<span data-ttu-id="057b5-136">Dopo aver installato i prerequisiti di hello, è possibile installare Data Lake Tools per Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="057b5-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="057b5-137">**tooinstall Data Lake Tools**</span><span class="sxs-lookup"><span data-stu-id="057b5-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="057b5-138">Aprire Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="057b5-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="057b5-139">Selezionare Ctrl + P e quindi immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="057b5-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="057b5-140">È possibile visualizzare un elenco delle estensioni di codice di Visual Studio, tra cui</span><span class="sxs-lookup"><span data-stu-id="057b5-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="057b5-141">Una di queste è costituita da **Strumenti Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="057b5-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="057b5-142">Selezionare **installare** Avanti troppo**Azure Data Lake Tools**.</span><span class="sxs-lookup"><span data-stu-id="057b5-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="057b5-143">Dopo alcuni secondi, hello **installare** pulsante verrà modificato troppo**Ricarica**.</span><span class="sxs-lookup"><span data-stu-id="057b5-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="057b5-144">Selezionare **Ricarica** estensione hello tooactivate.</span><span class="sxs-lookup"><span data-stu-id="057b5-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="057b5-145">Selezionare **OK** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="057b5-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="057b5-146">È possibile visualizzare gli strumenti di Azure Data Lake nella hello **estensioni** riquadro.</span><span class="sxs-lookup"><span data-stu-id="057b5-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="057b5-147">![Riquadro Estensioni di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="057b5-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="057b5-148">Attivare Strumenti Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="057b5-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="057b5-149">Creare un nuovo file .usql o aprire esistente .usql tooactivate hello estensione di file.</span><span class="sxs-lookup"><span data-stu-id="057b5-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="057b5-150">Connettersi tooAzure</span><span class="sxs-lookup"><span data-stu-id="057b5-150">Connect tooAzure</span></span>

<span data-ttu-id="057b5-151">Prima di è possibile compilare ed eseguire gli script U-SQL in Data Lake Analitica, è necessario connettersi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="057b5-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="057b5-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="057b5-153">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="057b5-154">Immettere **ADL: Login** (ADL: Accedi).</span><span class="sxs-lookup"><span data-stu-id="057b5-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="057b5-155">informazioni di accesso Hello viene visualizzato in hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="057b5-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="057b5-156">![Riquadro comandi di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informazioni di accesso di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="057b5-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="057b5-157">Selezionare Ctrl + clic sull'URL di account di accesso hello: pagina Web di accesso https://aka.ms/devicelogin tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="057b5-158">Immettere il codice hello **G567LX42V** nella casella di testo hello e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="057b5-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Codice di accesso da incollare di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="057b5-160">Seguire toosign istruzioni hello dalla pagina Web hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="057b5-161">Quando si è connessi, il nome dell'account di Azure viene visualizzato sulla barra di stato hello nell'angolo inferiore sinistro hello di hello **Visual Studio Code** finestra.</span><span class="sxs-lookup"><span data-stu-id="057b5-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="057b5-162">Se l'account ha due fattori abilitati, è consigliabile usare l'autenticazione telefonica anziché un PIN.</span><span class="sxs-lookup"><span data-stu-id="057b5-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="057b5-163">toosign, immettere il comando hello **ADL: disconnessione**.</span><span class="sxs-lookup"><span data-stu-id="057b5-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="057b5-164">Elencare gli account di Data Lake Analytics personali</span><span class="sxs-lookup"><span data-stu-id="057b5-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="057b5-165">connessione di hello tootest, ottenere un elenco di account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="057b5-166">**toolist hello Data Lake Analitica gli account utilizzati per la sottoscrizione di Azure**</span><span class="sxs-lookup"><span data-stu-id="057b5-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="057b5-167">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="057b5-168">Immettere **ADL: List Accounts** (ADL: Elenca gli account).</span><span class="sxs-lookup"><span data-stu-id="057b5-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="057b5-169">gli account Hello appaiano nel hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="057b5-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="057b5-170">Script di esempio hello aperto</span><span class="sxs-lookup"><span data-stu-id="057b5-170">Open hello sample script</span></span>
<span data-ttu-id="057b5-171">Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: aprire uno Script di esempio**.</span><span class="sxs-lookup"><span data-stu-id="057b5-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="057b5-172">Verrà quindi aperta un'altra istanza di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="057b5-172">This opens another instance of this sample.</span></span> <span data-ttu-id="057b5-173">Anche in questa istanza è possibile modificare, configurare e inviare lo script.</span><span class="sxs-lookup"><span data-stu-id="057b5-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="057b5-174">Uso di U-SQL</span><span class="sxs-lookup"><span data-stu-id="057b5-174">Work with U-SQL</span></span>

<span data-ttu-id="057b5-175">È necessario aprire un file U-SQL o una cartella toowork con U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="057b5-176">**tooopen una cartella per il progetto U-SQL**</span><span class="sxs-lookup"><span data-stu-id="057b5-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="057b5-177">Il codice di Visual Studio, selezionare hello **File** menu e quindi selezionare **Apri cartella**.</span><span class="sxs-lookup"><span data-stu-id="057b5-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="057b5-178">Specificare una cartella e quindi scegliere **Seleziona cartella**.</span><span class="sxs-lookup"><span data-stu-id="057b5-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="057b5-179">Seleziona hello **File** menu e quindi selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="057b5-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="057b5-180">Un file senza titolo 1 viene aggiunto il progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="057b5-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="057b5-181">Immettere hello seguente codice nel file hello senza titolo 1:</span><span class="sxs-lookup"><span data-stu-id="057b5-181">Enter hello following code into hello Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="057b5-182">script Hello crea un file departments.csv con alcuni dati inclusi nella cartella /output hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="057b5-183">Salvare il file hello come **myUSQL.usql** hello aprire cartella.</span><span class="sxs-lookup"><span data-stu-id="057b5-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="057b5-184">Un file di configurazione adltools_settings.json aggiunto anche toohello progetto.</span><span class="sxs-lookup"><span data-stu-id="057b5-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="057b5-185">Aprire e configurare adltools_settings.json con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="057b5-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="057b5-186">Account: un account di Data Lake Analytics sotto la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="057b5-187">Database: un database nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="057b5-187">Database: A database under your account.</span></span> <span data-ttu-id="057b5-188">valore predefinito di Hello è **master**.</span><span class="sxs-lookup"><span data-stu-id="057b5-188">hello default is **master**.</span></span>
    - <span data-ttu-id="057b5-189">Schema: uno schema nel database.</span><span class="sxs-lookup"><span data-stu-id="057b5-189">Schema: A schema under your database.</span></span> <span data-ttu-id="057b5-190">valore predefinito di Hello è **dbo**.</span><span class="sxs-lookup"><span data-stu-id="057b5-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="057b5-191">Impostazioni facoltative:</span><span class="sxs-lookup"><span data-stu-id="057b5-191">Optional settings:</span></span>
        - <span data-ttu-id="057b5-192">Priorità: intervallo di priorità hello è 1 too1000 con 1 come priorità più alta hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="057b5-193">valore predefinito di Hello è **1000**.</span><span class="sxs-lookup"><span data-stu-id="057b5-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="057b5-194">Parallelismo: intervallo di parallelismo hello è compreso tra 1 too150.</span><span class="sxs-lookup"><span data-stu-id="057b5-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="057b5-195">valore predefinito di Hello è parallelismo di hello massimo consentito nell'account di Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="057b5-196">Se le impostazioni di hello non sono validi, vengono utilizzati i valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-196">If hello settings are invalid, hello default values are used.</span></span>

    ![File di configurazione degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="057b5-198">Un calcolo account Data Lake Analitica è necessario toocompile ed eseguire processi U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="057b5-199">È necessario configurare l'account computer hello prima di compilare ed eseguire i processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="057b5-200">Dopo aver salvata la configurazione hello, sulla barra di stato hello nell'angolo inferiore sinistro di hello del file .usql corrispondente hello hello informazioni di schema, database e account.</span><span class="sxs-lookup"><span data-stu-id="057b5-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="057b5-201">Confrontati tooopening un file, quando si apre una cartella in cui che è possibile:</span><span class="sxs-lookup"><span data-stu-id="057b5-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="057b5-202">Usare un file code-behind.</span><span class="sxs-lookup"><span data-stu-id="057b5-202">Use a code-behind file.</span></span> <span data-ttu-id="057b5-203">Codice non è supportato in modalità solo file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="057b5-204">Usare un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="057b5-204">Use a configuration file.</span></span> <span data-ttu-id="057b5-205">Quando si apre una cartella, gli script hello nella cartella di lavoro hello condividono un singolo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="057b5-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="057b5-206">Hello script U-SQL viene compilato in modalità remota tramite il servizio Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="057b5-207">Quando si esegue hello **compilare** comando inviato account Data Lake Analitica tooyour hello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="057b5-208">Successivamente, codice di Visual Studio riceve il risultato della compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="057b5-209">A causa di compilazione remoto toohello, codice di Visual Studio richiede informazioni hello tooconnect tooyour Data Lake Analitica account nel file di configurazione hello elencati.</span><span class="sxs-lookup"><span data-stu-id="057b5-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="057b5-210">**script toocompile U-SQL**</span><span class="sxs-lookup"><span data-stu-id="057b5-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="057b5-211">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="057b5-212">Immettere **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="057b5-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="057b5-213">Hello compilazione risultati vengono visualizzati in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="057b5-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="057b5-214">È possibile anche fare doppio clic su un file di script e quindi selezionare **ADL: compilare Script** processo toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="057b5-215">viene visualizzato il risultato della compilazione Hello in hello **Output** riquadro.</span><span class="sxs-lookup"><span data-stu-id="057b5-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="057b5-216">**script toosubmit U-SQL**</span><span class="sxs-lookup"><span data-stu-id="057b5-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="057b5-217">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="057b5-218">Immettere **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="057b5-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="057b5-219">È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Invia processo**.</span><span class="sxs-lookup"><span data-stu-id="057b5-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="057b5-220">Dopo aver inviato un processo U-SQL, i log di invio di hello vengono visualizzati in hello **Output** finestra in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="057b5-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="057b5-221">Se l'invio di hello ha esito positivo, viene visualizzato anche hello processo URL.</span><span class="sxs-lookup"><span data-stu-id="057b5-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="057b5-222">È possibile aprire URL processo hello in uno stato di processo in tempo reale di web browser tootrack hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="057b5-223">output di hello tooenable dettagli processo hello, impostare **jobInformationOutputPath** in hello **codice di Visual Studio per hello u-sql_settings.json** file.</span><span class="sxs-lookup"><span data-stu-id="057b5-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="057b5-224">Usare un file code-behind</span><span class="sxs-lookup"><span data-stu-id="057b5-224">Use a code-behind file</span></span>

<span data-ttu-id="057b5-225">Un file code-behind è un file C# associato a uno script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="057b5-226">È possibile definire un tooUDO script dedicato, aggregazione definita dall'utente, tipo definito dall'utente e funzioni definite dall'utente nel file code-behind hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="057b5-227">Hello UDO, aggregazione definita dall'utente, tipo definito dall'utente e la funzione definita dall'utente è utilizzabile direttamente nello script di hello senza registrare assembly hello prima.</span><span class="sxs-lookup"><span data-stu-id="057b5-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="057b5-228">Hello file code-behind viene inserito in hello stessa cartella del relativo file di script U-SQL peering.</span><span class="sxs-lookup"><span data-stu-id="057b5-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="057b5-229">Se lo script di hello è denominato xxx.usql, denominato codice hello come xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="057b5-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="057b5-230">Se si elimina manualmente file code-behind hello, funzionalità code-behind hello è disabilitata per lo script U-SQL associato.</span><span class="sxs-lookup"><span data-stu-id="057b5-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="057b5-231">Per altre informazioni sulla scrittura del codice cliente per lo script U-SQL, vedere [Scrivere e usare il codice personalizzato in U-SQL: funzioni definite dall'utente]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="057b5-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="057b5-232">codice toosupport, è necessario aprire una cartella di lavoro.</span><span class="sxs-lookup"><span data-stu-id="057b5-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="057b5-233">**un file code-behind toogenerate**</span><span class="sxs-lookup"><span data-stu-id="057b5-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="057b5-234">Aprire un file di origine.</span><span class="sxs-lookup"><span data-stu-id="057b5-234">Open a source file.</span></span> 
2. <span data-ttu-id="057b5-235">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="057b5-236">Immettere **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="057b5-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="057b5-237">Viene creato un file code-behind in hello stessa cartella.</span><span class="sxs-lookup"><span data-stu-id="057b5-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="057b5-238">È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Generate Code Behind** (ADL: Genera code-behind).</span><span class="sxs-lookup"><span data-stu-id="057b5-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="057b5-239">toocompile e inviare uno script U-SQL con un file code-behind è hello uguale al file di script con la versione autonoma di hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="057b5-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="057b5-240">Hello due schermate seguenti Mostra un file code-behind e il relativo file di script U-SQL associato:</span><span class="sxs-lookup"><span data-stu-id="057b5-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![File di script code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="057b5-243">Usare gli assembly</span><span class="sxs-lookup"><span data-stu-id="057b5-243">Use assemblies</span></span>

<span data-ttu-id="057b5-244">Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="057b5-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="057b5-245">È possibile utilizzare gli assembly di codice personalizzato tooregister Data Lake Tools nel catalogo dati Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="057b5-246">**tooregister un assembly**</span><span class="sxs-lookup"><span data-stu-id="057b5-246">**tooregister an assembly**</span></span>

<span data-ttu-id="057b5-247">È possibile registrare l'assembly hello tramite hello **ADL: registrare Assembly** o **ADL: registrare Assembly tramite la configurazione** comandi.</span><span class="sxs-lookup"><span data-stu-id="057b5-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="057b5-248">**tooregister tramite hello ADL: comando registra Assembly**</span><span class="sxs-lookup"><span data-stu-id="057b5-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="057b5-249">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="057b5-250">Immettere **ADL: Register Assembly** (ADL: Registra assembly).</span><span class="sxs-lookup"><span data-stu-id="057b5-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="057b5-251">Specificare il percorso di assembly locale hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="057b5-252">Selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="057b5-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="057b5-253">Selezionare un database.</span><span class="sxs-lookup"><span data-stu-id="057b5-253">Select a database.</span></span>

<span data-ttu-id="057b5-254">Risultati: portale hello viene aperto in un browser e Visualizza processo di registrazione assembly hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="057b5-255">Un altro hello di tootrigger pratica **ADL: registrare Assembly** comando è file con estensione DLL di hello tooright clic in Esplora File.</span><span class="sxs-lookup"><span data-stu-id="057b5-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="057b5-256">**tooregister hello tuttavia ADL: registrare Assembly tramite il comando di configurazione**</span><span class="sxs-lookup"><span data-stu-id="057b5-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="057b5-257">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="057b5-258">Immettere **ADL: Register Assembly through Configuration** (ADL: Registra assembly da configurazione).</span><span class="sxs-lookup"><span data-stu-id="057b5-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="057b5-259">Specificare il percorso di assembly locale hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="057b5-260">file JSON Hello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="057b5-260">hello JSON file is displayed.</span></span> <span data-ttu-id="057b5-261">Esaminare e modificare le dipendenze dell'assembly hello e i parametri delle risorse, se necessario.</span><span class="sxs-lookup"><span data-stu-id="057b5-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="057b5-262">Le istruzioni vengono visualizzate in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="057b5-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="057b5-263">tooproceed toohello registrazione dell'assembly, salvare file JSON di hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="057b5-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="057b5-265">Le dipendenze dell'assembly: rileva automaticamente gli strumenti di Azure Data Lake hello DLL se dispone di tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="057b5-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="057b5-266">dipendenze di Hello vengono visualizzate nel file JSON hello dopo che vengono rilevati.</span><span class="sxs-lookup"><span data-stu-id="057b5-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="057b5-267">Risorse: È possibile caricare le risorse DLL (ad esempio, txt, PNG e CSV) come parte della registrazione dell'assembly hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="057b5-268">Hello di tootrigger un altro modo **ADL: registrare Assembly tramite la configurazione** è file. dll di hello tooright clic in Esplora File.</span><span class="sxs-lookup"><span data-stu-id="057b5-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="057b5-269">Hello codice U-SQL seguente viene illustrato come toocall un assembly.</span><span class="sxs-lookup"><span data-stu-id="057b5-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="057b5-270">Nell'esempio hello è il nome dell'assembly hello *test*.</span><span class="sxs-lookup"><span data-stu-id="057b5-270">In hello sample, hello assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="057b5-271">Catalogo dati Lake Analitica hello di accesso</span><span class="sxs-lookup"><span data-stu-id="057b5-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="057b5-272">Dopo avere stabilito la connessione tooAzure, è possibile utilizzare hello catalog di passaggi tooaccess hello U-SQL seguente.</span><span class="sxs-lookup"><span data-stu-id="057b5-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="057b5-273">**metadati di Azure Data Lake Analitica hello tooaccess**</span><span class="sxs-lookup"><span data-stu-id="057b5-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="057b5-274">Premere CTRL+MAIUSC+P e digitare **ADL: List Tables** (ADL: Elenca tabelle).</span><span class="sxs-lookup"><span data-stu-id="057b5-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="057b5-275">Selezionare uno degli account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="057b5-276">Selezionare uno dei database di Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="057b5-277">Selezionare uno degli schemi di hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-277">Select one of hello schemas.</span></span> <span data-ttu-id="057b5-278">È possibile visualizzare l'elenco di hello delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="057b5-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="057b5-279">Visualizzare i processi di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="057b5-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="057b5-280">**processi di Data Lake Analitica tooview**</span><span class="sxs-lookup"><span data-stu-id="057b5-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="057b5-281">Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e selezionare **ADL: processo mostra**.</span><span class="sxs-lookup"><span data-stu-id="057b5-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="057b5-282">Selezionare un account di Data Lake Analytics o locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="057b5-283">Attendere per l'elenco di processi hello tooappear account hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="057b5-284">Selezionare un processo dall'elenco di processi, Data Lake Tools apre i dettagli dei processi hello nel portale di Azure hello e visualizza i file di JobInfo hello in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="057b5-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="057b5-286">Integrazione di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="057b5-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="057b5-287">È possibile usare i comandi correlati all'archiviazione di Azure Data Lake per:</span><span class="sxs-lookup"><span data-stu-id="057b5-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="057b5-288">Esplorare le risorse di archiviazione di Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="057b5-289">File di archiviazione di Azure Data Lake hello di anteprima.</span><span class="sxs-lookup"><span data-stu-id="057b5-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="057b5-290">Caricare hello direttamente file tooAzure Lake archiviazione dei dati in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="057b5-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="057b5-291">Percorso di archiviazione hello elenco</span><span class="sxs-lookup"><span data-stu-id="057b5-291">List hello storage path</span></span> 
<span data-ttu-id="057b5-292">È possibile elencare percorso di archiviazione hello tramite tavolozza comando hello o pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="057b5-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="057b5-293">**percorso di archiviazione di hello toolist tramite tavolozza comando hello**</span><span class="sxs-lookup"><span data-stu-id="057b5-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="057b5-294">Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: percorso di archiviazione elenco**.</span><span class="sxs-lookup"><span data-stu-id="057b5-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="057b5-296">Selezionare il modo migliore per elencare il percorso di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="057b5-297">Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.</span><span class="sxs-lookup"><span data-stu-id="057b5-297">This passage uses **Enter a path** as an example.</span></span>

    ![Data Lake Tools per Visual Studio Code percorso di archiviazione hello toolist unidirezionale](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="057b5-299">Codice di Visual Studio consente di mantenere percorso visitato ultimo hello ogni account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="057b5-300">Ad esempio /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="057b5-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="057b5-301">Browser dal percorso radice: percorso radice di elenco hello dall'account Data Lake Analitica selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="057b5-302">Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="057b5-303">Selezionare un account dal percorso locale hello o un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Selezionare altro in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="057b5-305">Selezionare **più** toolist ulteriori account Data Lake Analitica e quindi selezionare un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="057b5-307">Immettere un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-307">Enter an Azure storage path.</span></span> <span data-ttu-id="057b5-308">Ad esempio /output.</span><span class="sxs-lookup"><span data-stu-id="057b5-308">For example, /output.</span></span>

    ![Immettere un percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="057b5-310">Risultati: tavolozza di hello comando Visualizza le informazioni di percorso hello in base ai valori immessi.</span><span class="sxs-lookup"><span data-stu-id="057b5-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Risultato dell'inserimento del percorso di archiviazione di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="057b5-312">Un modo più pratico percorso relativo di toolist hello è tramite hello fare clic sul menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="057b5-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="057b5-313">**percorso di archiviazione hello toolist tramite mouse**</span><span class="sxs-lookup"><span data-stu-id="057b5-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="057b5-314">Fare doppio clic su hello percorso stringa tooselect **il percorso di archiviazione elenco**.</span><span class="sxs-lookup"><span data-stu-id="057b5-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="057b5-316">percorso relativo di Hello selezionato viene visualizzato nel riquadro comandi hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-316">hello selected relative path appears in hello command palette.</span></span>

   ![Percorso relativo selezionato in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="057b5-318">Selezionare un account dal percorso locale hello o un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="057b5-320">Risultati: riquadro comandi hello Elenca hello cartelle e file per il percorso corrente hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Data Lake Tools per elenco di codice di Visual Studio dal percorso corrente hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="057b5-322">File di archiviazione hello anteprima</span><span class="sxs-lookup"><span data-stu-id="057b5-322">Preview hello storage file</span></span>
<span data-ttu-id="057b5-323">È possibile visualizzare l'anteprima di file di archiviazione hello tramite tavolozza comando hello o pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="057b5-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="057b5-324">**file di archiviazione hello toopreview tramite tavolozza comando hello**</span><span class="sxs-lookup"><span data-stu-id="057b5-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="057b5-325">Aprire il riquadro comandi hello (Ctrl + MAIUSC + P) e immettere **ADL: File di archiviazione di anteprima**.</span><span class="sxs-lookup"><span data-stu-id="057b5-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Anteprima dei file di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="057b5-327">Selezionare un account dal percorso locale hello o un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Elencare l'account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="057b5-329">Selezionare **più** toolist ulteriori account Data Lake Analitica e quindi selezionare un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="057b5-331">Immettere un file o un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="057b5-332">Ad esempio /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="057b5-332">For example, /output/SearchLog.txt.</span></span>

       ![Immissione di un file o percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="057b5-334">Risultati: tavolozza di hello comando Visualizza le informazioni di percorso hello in base ai valori immessi.</span><span class="sxs-lookup"><span data-stu-id="057b5-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="057b5-336">**percorso di archiviazione hello toolist tramite mouse**</span><span class="sxs-lookup"><span data-stu-id="057b5-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="057b5-337">toopreview un file, fare clic sul percorso del file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-337">toopreview a file, right-click hello file path.</span></span>

   ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="057b5-339">Selezionare un account dal percorso locale hello o un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="057b5-341">Risultati: Codice di Visual Studio visualizza i risultati di anteprima hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="057b5-343">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="057b5-343">Upload a file</span></span> 

<span data-ttu-id="057b5-344">È possibile caricare file immettendo i comandi di hello **ADL: carica File** o **ADL: carica File tramite la configurazione**.</span><span class="sxs-lookup"><span data-stu-id="057b5-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="057b5-345">**file tooupload hello tuttavia ADL: il comando Carica File**</span><span class="sxs-lookup"><span data-stu-id="057b5-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="057b5-346">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza o editor di script hello e quindi immettere **carica File**.</span><span class="sxs-lookup"><span data-stu-id="057b5-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="057b5-347">hello tooupload file, immettere un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-347">tooupload hello file, enter a local path.</span></span>

    ![Inserimento di un percorso locale in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="057b5-349">Selezionare uno dei modi hello del percorso di archiviazione hello elenco.</span><span class="sxs-lookup"><span data-stu-id="057b5-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="057b5-350">Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.</span><span class="sxs-lookup"><span data-stu-id="057b5-350">This passage uses **Enter a path** as an example.</span></span>

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="057b5-352">Codice di Visual Studio consente di mantenere percorso visitato ultimo hello ogni account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="057b5-353">Ad esempio /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="057b5-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="057b5-354">Browser dal percorso radice: percorso radice di elenco hello dall'account Data Lake Analitica selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="057b5-355">Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="057b5-356">Selezionare un account dal percorso locale hello o un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Archiviazione dal menu di scelta rapida in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="057b5-358">Immettere un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-358">Enter an Azure storage path.</span></span> <span data-ttu-id="057b5-359">Ad esempio /output.</span><span class="sxs-lookup"><span data-stu-id="057b5-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="057b5-360">Individuare il percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-360">Find your Azure storage path.</span></span> <span data-ttu-id="057b5-361">Selezionare **Choose current folder** (Scegli cartella corrente).</span><span class="sxs-lookup"><span data-stu-id="057b5-361">Select **Choose current folder**.</span></span>

    ![Selezionare una cartella in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="057b5-363">Risultati: hello **Output** finestra viene visualizzato lo stato di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="057b5-365">**file tooupload hello tuttavia ADL: caricare File tramite il comando di configurazione**</span><span class="sxs-lookup"><span data-stu-id="057b5-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="057b5-366">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza o editor di script hello e quindi immettere **carica File tramite la configurazione**.</span><span class="sxs-lookup"><span data-stu-id="057b5-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="057b5-367">VS Code visualizza un file JSON.</span><span class="sxs-lookup"><span data-stu-id="057b5-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="057b5-368">È possibile immettere i percorsi di file e caricare più file hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="057b5-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="057b5-369">Le istruzioni vengono visualizzate in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="057b5-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="057b5-370">file di hello il tooproceed tooupload, salvare file JSON di hello (Ctrl + S).</span><span class="sxs-lookup"><span data-stu-id="057b5-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Percorso del file in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="057b5-372">Risultati: hello **Output** finestra viene visualizzato lo stato di caricamento file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="057b5-374">Menu di scelta rapida nel percorso completo del file hello o percorso del file hello nell'editor di script hello un'altra tooupload modo consiste nell'utilizzare un toostorage file hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="057b5-375">Immettere il percorso di file locale hello e quindi selezionare account hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="057b5-376">Hello **Output** finestra Visualizza lo stato di caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="057b5-377">Aprire Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="057b5-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="057b5-378">È possibile aprire **Azure Storage Explorer** immettendo il comando hello **ADL: aprire Web Azure Storage Explorer** o selezionarlo dal menu di scelta rapida hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="057b5-379">**tooopen Esplora archivi Azure**</span><span class="sxs-lookup"><span data-stu-id="057b5-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="057b5-380">Selezionare Ctrl + MAIUSC + P tooopen hello comando tavolozza.</span><span class="sxs-lookup"><span data-stu-id="057b5-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="057b5-381">Immettere **aprire Esplora risorse di archiviazione Azure Web** o fare clic su un percorso relativo o il percorso completo di hello nell'editor di script hello e quindi selezionare **aprire Esplora risorse di archiviazione Azure Web**.</span><span class="sxs-lookup"><span data-stu-id="057b5-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="057b5-382">Selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="057b5-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="057b5-383">Data Lake Tools consente di aprire il percorso di archiviazione di Azure hello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="057b5-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="057b5-384">È possibile trovare i file di hello di percorso e anteprima hello dal web hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="057b5-385">Esecuzione e debug locale per utenti Windows</span><span class="sxs-lookup"><span data-stu-id="057b5-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="057b5-386">Esecuzione locale U-SQL verifica i dati locali e di convalidare lo script in locale, prima che il codice venga pubblicato tooData Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="057b5-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="057b5-387">Hello consente di funzionalità di debug locale è toocomplete hello seguenti attività prima che il codice venga inviata Analitica tooData Lake:</span><span class="sxs-lookup"><span data-stu-id="057b5-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="057b5-388">Eseguire il debug del code-behind di C#.</span><span class="sxs-lookup"><span data-stu-id="057b5-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="057b5-389">Esaminare il codice hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-389">Step through hello code.</span></span> 
- <span data-ttu-id="057b5-390">Convalidare lo script in locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-390">Validate your script locally.</span></span>

<span data-ttu-id="057b5-391">Per istruzioni sull'esecuzione e il debug locali, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="057b5-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="057b5-392">Funzionalità aggiuntive</span><span class="sxs-lookup"><span data-stu-id="057b5-392">Additional features</span></span>

<span data-ttu-id="057b5-393">Data Lake Tools per Visual Studio Code supporta hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="057b5-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="057b5-394">Completamento automatico di IntelliSense: vengono visualizzati suggerimenti in finestre popup intorno agli elementi, ad esempio parole chiave, metodi e variabili.</span><span class="sxs-lookup"><span data-stu-id="057b5-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="057b5-395">Icone diverse rappresentano diversi tipi di oggetti hello:</span><span class="sxs-lookup"><span data-stu-id="057b5-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="057b5-396">Tipo di dati Scala</span><span class="sxs-lookup"><span data-stu-id="057b5-396">Scala data type</span></span>
    - <span data-ttu-id="057b5-397">Tipo di dati complesso</span><span class="sxs-lookup"><span data-stu-id="057b5-397">Complex data type</span></span>
    - <span data-ttu-id="057b5-398">UDT integrati</span><span class="sxs-lookup"><span data-stu-id="057b5-398">Built-in UDTs</span></span>
    - <span data-ttu-id="057b5-399">Raccolta e classi .NET</span><span class="sxs-lookup"><span data-stu-id="057b5-399">.NET collection and classes</span></span>
    - <span data-ttu-id="057b5-400">Espressioni C#</span><span class="sxs-lookup"><span data-stu-id="057b5-400">C# expressions</span></span>
    - <span data-ttu-id="057b5-401">UDF, UDO e UDAAG di C# integrati</span><span class="sxs-lookup"><span data-stu-id="057b5-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="057b5-402">Funzioni di U-SQL</span><span class="sxs-lookup"><span data-stu-id="057b5-402">U-SQL functions</span></span>
    - <span data-ttu-id="057b5-403">Funzione di windowing di U-SQL</span><span class="sxs-lookup"><span data-stu-id="057b5-403">U-SQL windowing function</span></span>
 
    ![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="057b5-405">IntelliSense, completamento automatico sui metadati Data Lake Analitica: Data Lake Tools Scarica hello Data Lake Analitica informazioni sui metadati in locale.</span><span class="sxs-lookup"><span data-stu-id="057b5-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="057b5-406">funzionalità IntelliSense Hello popola automaticamente gli oggetti, inclusi database hello, schema, tabella, vista, funzione con valori di tabella, procedure e gli assembly c#, dai metadati Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="057b5-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Metadati IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="057b5-408">Indicatore di errore di IntelliSense: Data Lake Tools sottolinea hello U-SQL e c# per l'elaborazione degli errori.</span><span class="sxs-lookup"><span data-stu-id="057b5-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="057b5-409">Caratteristiche salienti di sintassi: Data Lake Tools Usa elementi toodifferentiate colori diversi, ad esempio variabili, le parole chiave, il tipo di dati e funzioni.</span><span class="sxs-lookup"><span data-stu-id="057b5-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Sintassi in evidenza degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="057b5-411">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="057b5-411">Next steps</span></span>

- <span data-ttu-id="057b5-412">Per l'esecuzione e il debug locali di U-SQL con Visual Studio Code, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="057b5-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="057b5-413">Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="057b5-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="057b5-414">Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="057b5-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="057b5-415">Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="057b5-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



