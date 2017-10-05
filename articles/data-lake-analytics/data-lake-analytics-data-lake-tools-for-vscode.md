---
title: 'Strumenti Azure Data Lake: Usare Strumenti Azure Data Lake per Visual Studio Code | Microsoft Docs'
description: 'Informazioni su come usare gli Strumenti Azure Data Lake per Visual Studio Code per creare, testare ed eseguire gli script U-SQL. '
Keywords: VScode, Strumenti Azure Data Lake, Esecuzione locale, debug locale, Debug Locale, anteprima file di archiviazione, caricamento nel percorso di archiviazione
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="cbd13-104">Usare gli Strumenti Azure Data Lake per Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cbd13-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="cbd13-105">Informazioni su come usare gli Strumenti Azure Data Lake per Visual Studio Code (VS Code) per creare, testare ed eseguire gli script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="cbd13-106">Le informazioni sono disponibili anche nel video seguente:</span><span class="sxs-lookup"><span data-stu-id="cbd13-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="cbd13-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cbd13-107">Prerequisites</span></span>

<span data-ttu-id="cbd13-108">È possibile installare Strumenti Data Lake con le piattaforme supportate da VS Code.</span><span class="sxs-lookup"><span data-stu-id="cbd13-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="cbd13-109">Le piattaforme supportate includono Windows, Linux e MacOS.</span><span class="sxs-lookup"><span data-stu-id="cbd13-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="cbd13-110">Le diverse piattaforme hanno i seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="cbd13-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="cbd13-111">Windows</span><span class="sxs-lookup"><span data-stu-id="cbd13-111">Windows</span></span>

    - <span data-ttu-id="cbd13-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbd13-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="cbd13-113">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="cbd13-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="cbd13-114">Aggiungere il percorso java.exe al percorso della variabile di ambiente di sistema.</span><span class="sxs-lookup"><span data-stu-id="cbd13-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="cbd13-115">Per le istruzioni di configurazione vedere [Come impostare o modificare la variabile di sistema Path]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="cbd13-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="cbd13-116">Il percorso è simile a c:\Programmi\Java\jdk1.8.0_77\jre\bin.</span><span class="sxs-lookup"><span data-stu-id="cbd13-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="cbd13-117">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="cbd13-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="cbd13-118">Linux (è consigliabile scegliere Ubuntu 14.04 LTS)</span><span class="sxs-lookup"><span data-stu-id="cbd13-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="cbd13-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbd13-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="cbd13-120">Per installare il codice immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cbd13-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="cbd13-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="cbd13-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="cbd13-122">Per aggiornare l'origine pacchetto deb immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbd13-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="cbd13-123">Per installare Mono immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cbd13-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="cbd13-124">Mono 4.6 non è supportato.</span><span class="sxs-lookup"><span data-stu-id="cbd13-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="cbd13-125">Disinstallare completamente la versione 4.6 prima di installare la versione 4.2.x.</span><span class="sxs-lookup"><span data-stu-id="cbd13-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="cbd13-126">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="cbd13-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="cbd13-127">Per istruzioni sull'installazione, vedere la pagina con le [istruzioni di installazione di Linux a 64 bit per Java]( https://java.com/en/download/help/linux_x64_install.xml).</span><span class="sxs-lookup"><span data-stu-id="cbd13-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="cbd13-128">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="cbd13-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="cbd13-129">MacOS</span><span class="sxs-lookup"><span data-stu-id="cbd13-129">MacOS</span></span>

    - <span data-ttu-id="cbd13-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbd13-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="cbd13-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="cbd13-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="cbd13-132">[Aggiornamento 77 o successivo di Java SE Runtime Environment, versione 8](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="cbd13-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="cbd13-133">Per istruzioni sull'installazione, vedere la pagina con le [istruzioni di installazione di Linux a 64 bit per Java](https://java.com/en/download/help/mac_install.xml).</span><span class="sxs-lookup"><span data-stu-id="cbd13-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="cbd13-134">[Runtime di .NET Core SDK 1.0.3 o .NET Core 1.1](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="cbd13-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="cbd13-135">Installare gli strumenti di Data Lake</span><span class="sxs-lookup"><span data-stu-id="cbd13-135">Install Data Lake Tools</span></span>

<span data-ttu-id="cbd13-136">Dopo aver installato i prerequisiti, è possibile installare gli strumenti di Data Lake per VSCode.</span><span class="sxs-lookup"><span data-stu-id="cbd13-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="cbd13-137">**Per installare gli strumenti di Data Lake**</span><span class="sxs-lookup"><span data-stu-id="cbd13-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="cbd13-138">Aprire Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cbd13-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="cbd13-139">Selezionare CTRL+P e quindi immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cbd13-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="cbd13-140">È possibile visualizzare un elenco delle estensioni di codice di Visual Studio, tra cui</span><span class="sxs-lookup"><span data-stu-id="cbd13-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="cbd13-141">Una di queste è costituita da **Strumenti Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="cbd13-142">Selezionare **Installa** accanto a **Strumenti Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="cbd13-143">Dopo alcuni secondi il pulsante **Installa** diventa **Ricarica**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="cbd13-144">Fare clic su **Ricarica** per attivare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="cbd13-145">Selezionare **OK** per confermare.</span><span class="sxs-lookup"><span data-stu-id="cbd13-145">Select **OK** to confirm.</span></span> <span data-ttu-id="cbd13-146">È possibile visualizzare gli Strumenti Azure Data Lake nel riquadro **Estensioni**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="cbd13-147">![Riquadro Estensioni di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="cbd13-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="cbd13-148">Attivare Strumenti Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="cbd13-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="cbd13-149">Creare un nuovo file .usql o aprire un file .usql esistente per attivare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="cbd13-150">Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="cbd13-150">Connect to Azure</span></span>

<span data-ttu-id="cbd13-151">Prima di compilare ed eseguire gli script U-SQL in Data Lake Analytics, è necessario connettersi al proprio account di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="cbd13-152">**Connettersi ad Azure**</span><span class="sxs-lookup"><span data-stu-id="cbd13-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="cbd13-153">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="cbd13-154">Immettere **ADL: Login** (ADL: Accedi).</span><span class="sxs-lookup"><span data-stu-id="cbd13-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="cbd13-155">Le informazioni di accesso sono presenti nel riquadro **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="cbd13-156">![Riquadro comandi di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informazioni di accesso di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="cbd13-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="cbd13-157">Tenendo premuto CTRL fare clic sull'URL di accesso: https://aka.ms/devicelogin per aprire la pagina Web di accesso.</span><span class="sxs-lookup"><span data-stu-id="cbd13-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="cbd13-158">Immettere il codice **G567LX42V** nella casella di testo e quindi selezionare **Continua**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Codice di accesso da incollare di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="cbd13-160">Seguire le istruzioni per accedere dalla pagina Web.</span><span class="sxs-lookup"><span data-stu-id="cbd13-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="cbd13-161">Quando si è connessi viene visualizzato il nome di account di Azure sulla barra di stato nell'angolo inferiore sinistro della finestra **VS Code**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="cbd13-162">Se l'account ha due fattori abilitati, è consigliabile usare l'autenticazione telefonica anziché un PIN.</span><span class="sxs-lookup"><span data-stu-id="cbd13-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="cbd13-163">Per disconnettersi immettere il comando **ADL: Logout** (ADL: Disconnetti).</span><span class="sxs-lookup"><span data-stu-id="cbd13-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="cbd13-164">Elencare gli account di Data Lake Analytics personali</span><span class="sxs-lookup"><span data-stu-id="cbd13-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="cbd13-165">Per testare la connessione ottenere un elenco degli account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="cbd13-166">**Elencare gli account di Data Lake Analytics sotto una sottoscrizione di Azure**</span><span class="sxs-lookup"><span data-stu-id="cbd13-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="cbd13-167">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="cbd13-168">Immettere **ADL: List Accounts** (ADL: Elenca gli account).</span><span class="sxs-lookup"><span data-stu-id="cbd13-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="cbd13-169">L'account viene visualizzato nel riquadro **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="cbd13-170">Aprire lo script di esempio</span><span class="sxs-lookup"><span data-stu-id="cbd13-170">Open the sample script</span></span>
<span data-ttu-id="cbd13-171">Usare il riquadro comandi (CTRL+MAIUSC+P) e immettere **ADL: Open Sample Script** (ADL: Apri script di esempio).</span><span class="sxs-lookup"><span data-stu-id="cbd13-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="cbd13-172">Verrà quindi aperta un'altra istanza di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="cbd13-172">This opens another instance of this sample.</span></span> <span data-ttu-id="cbd13-173">Anche in questa istanza è possibile modificare, configurare e inviare lo script.</span><span class="sxs-lookup"><span data-stu-id="cbd13-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="cbd13-174">Uso di U-SQL</span><span class="sxs-lookup"><span data-stu-id="cbd13-174">Work with U-SQL</span></span>

<span data-ttu-id="cbd13-175">Per poter usare U-SQL è necessario aprire una cartella o un file U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="cbd13-176">**Aprire una cartella per il progetto U-SQL**</span><span class="sxs-lookup"><span data-stu-id="cbd13-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="cbd13-177">Da Visual Studio Code selezionare il menu **File** e quindi selezionare **Apri cartella**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="cbd13-178">Specificare una cartella e quindi scegliere **Seleziona cartella**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="cbd13-179">Selezionare il menu **File** e quindi scegliere **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="cbd13-180">Un file Untilted-1 viene aggiunto al progetto.</span><span class="sxs-lookup"><span data-stu-id="cbd13-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="cbd13-181">Immettere il codice seguente nel file Untitled-1:</span><span class="sxs-lookup"><span data-stu-id="cbd13-181">Enter the following code into the Untitled-1 file:</span></span>

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

    <span data-ttu-id="cbd13-182">Lo script crea un file departments.csv con alcuni dati inclusi nella cartella /output.</span><span class="sxs-lookup"><span data-stu-id="cbd13-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="cbd13-183">Salvare il file come **myUSQL.usql** nella cartella aperta.</span><span class="sxs-lookup"><span data-stu-id="cbd13-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="cbd13-184">Al progetto viene inoltre aggiunto il file di configurazione adltools_settings.json.</span><span class="sxs-lookup"><span data-stu-id="cbd13-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="cbd13-185">Aprire e configurare il file adltools_settings.json con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbd13-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="cbd13-186">Account: un account di Data Lake Analytics sotto la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="cbd13-187">Database: un database nel proprio account.</span><span class="sxs-lookup"><span data-stu-id="cbd13-187">Database: A database under your account.</span></span> <span data-ttu-id="cbd13-188">Il database predefinito è **master**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-188">The default is **master**.</span></span>
    - <span data-ttu-id="cbd13-189">Schema: uno schema nel database.</span><span class="sxs-lookup"><span data-stu-id="cbd13-189">Schema: A schema under your database.</span></span> <span data-ttu-id="cbd13-190">Lo schema è **dbo**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="cbd13-191">Impostazioni facoltative:</span><span class="sxs-lookup"><span data-stu-id="cbd13-191">Optional settings:</span></span>
        - <span data-ttu-id="cbd13-192">Priorità: L'intervallo di priorità va da 1 a 1000 dove la priorità più alta corrisponde al valore 1.</span><span class="sxs-lookup"><span data-stu-id="cbd13-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="cbd13-193">Il valore predefinito è **1000**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="cbd13-194">Parallelismo: l'intervallo di parallelismo va da 1 a 150.</span><span class="sxs-lookup"><span data-stu-id="cbd13-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="cbd13-195">Il valore predefinito è il parallelismo massimo consentito nell'account Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="cbd13-196">Se le impostazioni non sono valide, vengono applicati i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="cbd13-196">If the settings are invalid, the default values are used.</span></span>

    ![File di configurazione degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="cbd13-198">È necessario un account di calcolo di Data Lake Analytics per poter compilare ed eseguire i processi U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="cbd13-199">È necessario configurare l'account del computer prima di compilare ed eseguire i processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="cbd13-200">Dopo il salvataggio della configurazione, le informazioni di account, database e schema vengono visualizzate sulla barra di stato nella parte inferiore sinistra del file .usql corrispondente.</span><span class="sxs-lookup"><span data-stu-id="cbd13-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="cbd13-201">Rispetto all'apertura di un file, quando si apre una cartella è possibile:</span><span class="sxs-lookup"><span data-stu-id="cbd13-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="cbd13-202">Usare un file code-behind.</span><span class="sxs-lookup"><span data-stu-id="cbd13-202">Use a code-behind file.</span></span> <span data-ttu-id="cbd13-203">Code-behind non è supportato in modalità file unico.</span><span class="sxs-lookup"><span data-stu-id="cbd13-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="cbd13-204">Usare un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-204">Use a configuration file.</span></span> <span data-ttu-id="cbd13-205">Quando si apre una cartella, gli script nella cartella di lavoro condividono un singolo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="cbd13-206">La compilazione dello script U-SQL viene eseguita da remoto attraverso il servizio Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="cbd13-207">Quando si esegue il comando **compile**, lo script U-SQL viene inviato all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="cbd13-208">In seguito Visual Studio Code riceve il risultato della compilazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="cbd13-209">Per via della compilazione remota, Visual Studio Code richiede che vengano elencate le informazioni per connettersi all'account di Data Lake Analytics nel file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="cbd13-210">**Compilare uno script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="cbd13-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="cbd13-211">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="cbd13-212">Immettere **ADL: Compile Script**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="cbd13-213">I risultati di compilazione vengono visualizzati nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="cbd13-214">È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Compile Script** (ADL: Compila script) per eseguire la compilazione di un processo U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="cbd13-215">Il risultato della compilazione viene visualizzato nel riquadro **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="cbd13-216">**Inviare uno script U-SQL**</span><span class="sxs-lookup"><span data-stu-id="cbd13-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="cbd13-217">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="cbd13-218">Immettere **ADL: Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="cbd13-219">È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Invia processo**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="cbd13-220">Dopo aver inviato un processo U-SQL, i log di invio vengono visualizzati nella finestra **Output** in VS Code.</span><span class="sxs-lookup"><span data-stu-id="cbd13-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="cbd13-221">Se l'invio ha esito positivo, viene visualizzato anche l'URL del processo.</span><span class="sxs-lookup"><span data-stu-id="cbd13-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="cbd13-222">È possibile aprire l'URL del processo in un Web browser per monitorare lo stato del processo in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="cbd13-223">Per abilitare l'output dei dettagli del processo: impostare **jobInformationOutputPath** nel file **vs code for the u-sql_settings.json**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="cbd13-224">Usare un file code-behind</span><span class="sxs-lookup"><span data-stu-id="cbd13-224">Use a code-behind file</span></span>

<span data-ttu-id="cbd13-225">Un file code-behind è un file C# associato a uno script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="cbd13-226">È possibile definire uno script dedicato a UDO, UDA, UDT e UDFF nel file code-behind.</span><span class="sxs-lookup"><span data-stu-id="cbd13-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="cbd13-227">L'opzione UDO, UDA, UDT e UDF può essere usata direttamente nello script senza dover prima registrare l'assembly.</span><span class="sxs-lookup"><span data-stu-id="cbd13-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="cbd13-228">Il file code-behind viene inserito nella stessa cartella del suo file di script U-SQL associato.</span><span class="sxs-lookup"><span data-stu-id="cbd13-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="cbd13-229">Se lo script viene denominato xxx.usql, code-behind assume il nome xxx.usql.cs.</span><span class="sxs-lookup"><span data-stu-id="cbd13-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="cbd13-230">Se si elimina manualmente il file code-behind, viene disabilitata la funzionalità code-behind per lo script U-SQL associato.</span><span class="sxs-lookup"><span data-stu-id="cbd13-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="cbd13-231">Per altre informazioni sulla scrittura del codice cliente per lo script U-SQL, vedere [Scrivere e usare il codice personalizzato in U-SQL: funzioni definite dall'utente]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="cbd13-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="cbd13-232">Per supportare code-behind, è necessario aprire una cartella di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cbd13-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="cbd13-233">**Generare un file code-behind**</span><span class="sxs-lookup"><span data-stu-id="cbd13-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="cbd13-234">Aprire un file di origine.</span><span class="sxs-lookup"><span data-stu-id="cbd13-234">Open a source file.</span></span> 
2. <span data-ttu-id="cbd13-235">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="cbd13-236">Immettere **ADL: Generate Code Behind**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="cbd13-237">Viene creato un file code-behind nella stessa cartella.</span><span class="sxs-lookup"><span data-stu-id="cbd13-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="cbd13-238">È anche possibile fare clic con il pulsante destro del mouse su un file di script e selezionare **ADL: Generate Code Behind** (ADL: Genera code-behind).</span><span class="sxs-lookup"><span data-stu-id="cbd13-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="cbd13-239">La procedura di compilazione e invio di uno script U-SQL con code-behind è la stessa utilizzata per il file script U-SQL indipendente.</span><span class="sxs-lookup"><span data-stu-id="cbd13-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="cbd13-240">Le due schermate seguenti mostrano un file code-behind e il suo file di script U-SQL associato:</span><span class="sxs-lookup"><span data-stu-id="cbd13-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![File di script code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="cbd13-243">Usare gli assembly</span><span class="sxs-lookup"><span data-stu-id="cbd13-243">Use assemblies</span></span>

<span data-ttu-id="cbd13-244">Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="cbd13-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="cbd13-245">È possibile usare Strumenti Data Lake per registrare gli assembly di codice personalizzato nel catalogo di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="cbd13-246">**Registrare un assembly**</span><span class="sxs-lookup"><span data-stu-id="cbd13-246">**To register an assembly**</span></span>

<span data-ttu-id="cbd13-247">È possibile registrare l'assembly tramite i comandi **ADL: Register Assembly** (ADL: Registra assembly) o **ADL: Register Assembly through Configuration** (ADL: Regista assembly da configurazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="cbd13-248">**Per eseguire la registrazione mediante il comando ADL: Register Assembly** (ADL: Registra assembly)</span><span class="sxs-lookup"><span data-stu-id="cbd13-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="cbd13-249">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="cbd13-250">Immettere **ADL: Register Assembly** (ADL: Registra assembly).</span><span class="sxs-lookup"><span data-stu-id="cbd13-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="cbd13-251">Specificare il percorso dell'assembly locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="cbd13-252">Selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="cbd13-253">Selezionare un database.</span><span class="sxs-lookup"><span data-stu-id="cbd13-253">Select a database.</span></span>

<span data-ttu-id="cbd13-254">Risultati: il portale viene aperto nel browser e visualizza il processo di registrazione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="cbd13-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="cbd13-255">Un altro modo pratico per attivare il comando **ADL: Register Assembly** (ADL: Registra assembly) consiste nel fare clic con il pulsante destro del mouse sul file .dll in Esplora file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="cbd13-256">**Per eseguire la registrazione mediante il comando ADL: Register Assembly through Configuration** (ADL: Registra assembly da configurazione)</span><span class="sxs-lookup"><span data-stu-id="cbd13-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="cbd13-257">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="cbd13-258">Immettere **ADL: Register Assembly through Configuration** (ADL: Registra assembly da configurazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="cbd13-259">Specificare il percorso dell'assembly locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="cbd13-260">Verrà visualizzato il file JSON.</span><span class="sxs-lookup"><span data-stu-id="cbd13-260">The JSON file is displayed.</span></span> <span data-ttu-id="cbd13-261">Esaminare e modificare le dipendenze dell'assembly e i parametri delle risorse, se necessario.</span><span class="sxs-lookup"><span data-stu-id="cbd13-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="cbd13-262">Le istruzioni sono visualizzate nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="cbd13-263">Salvare (CTRL+S) il file JSON per procedere con la registrazione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="cbd13-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Code-behind di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="cbd13-265">Dipendenze dell'assembly: Strumenti Azure Data Lake rileva automaticamente se la DLL include dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cbd13-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="cbd13-266">Le dipendenze vengono visualizzate nel file JSON dopo che sono state rilevate.</span><span class="sxs-lookup"><span data-stu-id="cbd13-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="cbd13-267">Risorse: è possibile caricare le risorse DLL (ad esempio i file .txt, .png e .csv) come parte della registrazione dell'assembly.</span><span class="sxs-lookup"><span data-stu-id="cbd13-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="cbd13-268">Un altro modo pratico per attivare il comando **ADL: Register Assembly through Configuration** (ADL: Registra assembly da configurazione) consiste nel fare clic con il pulsante destro del mouse sul file .dll in Esplora file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="cbd13-269">Il codice U-SQL seguente illustra come chiamare un assembly.</span><span class="sxs-lookup"><span data-stu-id="cbd13-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="cbd13-270">Nell'esempio il nome dell'assembly è *test*.</span><span class="sxs-lookup"><span data-stu-id="cbd13-270">In the sample, the assembly name is *test*.</span></span>

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="cbd13-271">Accedere al catalogo di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cbd13-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="cbd13-272">Dopo essersi connessi ad Azure, è possibile seguire questa procedura per accedere al catalogo di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="cbd13-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="cbd13-273">**Per accedere ai metadati di Azure Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="cbd13-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="cbd13-274">Premere CTRL+MAIUSC+P e digitare **ADL: List Tables** (ADL: Elenca tabelle).</span><span class="sxs-lookup"><span data-stu-id="cbd13-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="cbd13-275">Selezionare uno degli account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="cbd13-276">Selezionare uno dei database di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="cbd13-277">Selezionare uno degli schemi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-277">Select one of the schemas.</span></span> <span data-ttu-id="cbd13-278">È possibile visualizzare l'elenco delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="cbd13-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="cbd13-279">Visualizzare i processi di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cbd13-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="cbd13-280">**Per visualizzare i processi di Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="cbd13-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="cbd13-281">Aprire il riquadro comandi (CTRL+MAIUSC+P) e selezionare **ADL: Show Job** (ADL: Mostra processo).</span><span class="sxs-lookup"><span data-stu-id="cbd13-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="cbd13-282">Selezionare un account di Data Lake Analytics o locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="cbd13-283">Attendere che venga visualizzato l'elenco dei processi per l'account.</span><span class="sxs-lookup"><span data-stu-id="cbd13-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="cbd13-284">Selezionare un processo nell'elenco. Strumenti Data Lake apre i dettagli del processo nel portale e mostra il file JobInfo in VSCode.</span><span class="sxs-lookup"><span data-stu-id="cbd13-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="cbd13-286">Integrazione di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cbd13-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="cbd13-287">È possibile usare i comandi correlati all'archiviazione di Azure Data Lake per:</span><span class="sxs-lookup"><span data-stu-id="cbd13-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="cbd13-288">Esplorare le risorse di archiviazione di Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="cbd13-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="cbd13-289">Visualizzare in anteprima il file di archiviazione di Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="cbd13-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="cbd13-290">Caricare il file direttamente nell'archiviazione di Azure Data Lake in VS Code.</span><span class="sxs-lookup"><span data-stu-id="cbd13-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="cbd13-291">Elencare il percorso di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cbd13-291">List the storage path</span></span> 
<span data-ttu-id="cbd13-292">È possibile elencare il percorso di archiviazione tramite il riquadro comandi o facendo clic con il pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="cbd13-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="cbd13-293">**Per elencare il percorso di archiviazione tramite il riquadro comandi**</span><span class="sxs-lookup"><span data-stu-id="cbd13-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="cbd13-294">Usare il riquadro comandi (CTRL+MAIUSC+P) e scegliere **ADL: List Storage Path** (ADL: Elenca percorso di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="cbd13-296">Selezionare il modo preferito per elencare il percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="cbd13-297">Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.</span><span class="sxs-lookup"><span data-stu-id="cbd13-297">This passage uses **Enter a path** as an example.</span></span>

    ![Un modo per elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="cbd13-299">VS Code mantiene l'ultimo percorso visitato in ogni account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="cbd13-300">Ad esempio /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="cbd13-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="cbd13-301">Sfogliare dal percorso radice: il percorso radice dell'elenco dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="cbd13-302">Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="cbd13-303">Selezionare un account dal percorso locale o un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Selezionare altro in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="cbd13-305">Selezionare **more** (altro) per elencare altri account di Data Lake Analytics e quindi selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="cbd13-307">Immettere un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-307">Enter an Azure storage path.</span></span> <span data-ttu-id="cbd13-308">Ad esempio /output.</span><span class="sxs-lookup"><span data-stu-id="cbd13-308">For example, /output.</span></span>

    ![Immettere un percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="cbd13-310">Risultati: il riquadro comandi elenca le informazioni sul percorso in base all'input.</span><span class="sxs-lookup"><span data-stu-id="cbd13-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Risultato dell'inserimento del percorso di archiviazione di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="cbd13-312">Un modo più pratico per elencare il percorso relativo consiste nell'usare il menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="cbd13-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="cbd13-313">**Per elencare il percorso di archiviazione facendo clic con il pulsante destro del mouse**</span><span class="sxs-lookup"><span data-stu-id="cbd13-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="cbd13-314">Fare clic con il pulsante destro del mouse sulla stringa del percorso e scegliere **List Storage Path** (Elenca percorso di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="cbd13-316">Il percorso relativo selezionato viene visualizzato nel riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-316">The selected relative path appears in the command palette.</span></span>

   ![Percorso relativo selezionato in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="cbd13-318">Selezionare un account dal percorso locale o un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="cbd13-320">Risultati: il riquadro comandi elenca le cartelle e i file per il percorso corrente.</span><span class="sxs-lookup"><span data-stu-id="cbd13-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Elenco del percorso corrente in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="cbd13-322">Visualizzare in anteprima il file di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cbd13-322">Preview the storage file</span></span>
<span data-ttu-id="cbd13-323">È possibile visualizzare in anteprima il file di archiviazione tramite il riquadro comandi o facendo clic con il pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="cbd13-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="cbd13-324">**Per visualizzare in anteprima il file di archiviazione tramite il riquadro comandi**</span><span class="sxs-lookup"><span data-stu-id="cbd13-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="cbd13-325">Usare il riquadro comandi (CTRL+MAIUSC+P) e immettere **ADL: Preview Storage File** (ADL: anteprima file di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Anteprima dei file di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="cbd13-327">Selezionare un account dal percorso locale o un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Elencare l'account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="cbd13-329">Selezionare **more** (altro) per elencare altri account di Data Lake Analytics e quindi selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="cbd13-331">Immettere un file o un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="cbd13-332">Ad esempio /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="cbd13-332">For example, /output/SearchLog.txt.</span></span>

       ![Immissione di un file o percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="cbd13-334">Risultati: il riquadro comandi elenca le informazioni sul percorso in base all'input.</span><span class="sxs-lookup"><span data-stu-id="cbd13-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="cbd13-336">**Per elencare il percorso di archiviazione facendo clic con il pulsante destro del mouse**</span><span class="sxs-lookup"><span data-stu-id="cbd13-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="cbd13-337">Per visualizzare in anteprima un file, fare clic con il pulsante destro del mouse sul percorso del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-337">To preview a file, right-click the file path.</span></span>

   ![Menu di scelta rapida di Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="cbd13-339">Selezionare un account dal percorso locale o un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Selezionare un account in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="cbd13-341">Risultati: VS Code mostra il risultato dell'anteprima del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Risultato del file di anteprima in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="cbd13-343">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="cbd13-343">Upload a file</span></span> 

<span data-ttu-id="cbd13-344">È possibile caricare i file immettendo i comandi **ADL: Carica file** o **ADL: Upload File through Configuration** (ADL: Carica file da configurazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="cbd13-345">**Per caricare i file mediante il comando ADL: Carica file**</span><span class="sxs-lookup"><span data-stu-id="cbd13-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="cbd13-346">Premere CTRL+MAIUSC+P per aprire il riquadro comandi o fare clic con il pulsante destro del mouse sull'editor di script e immettere **Carica file**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="cbd13-347">Per caricare il file immettere un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-347">To upload the file, enter a local path.</span></span>

    ![Inserimento di un percorso locale in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="cbd13-349">Selezionare uno dei modi per elencare il percorso di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cbd13-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="cbd13-350">Questo passaggio usa **Enter a path** (Immetti un percorso) come esempio.</span><span class="sxs-lookup"><span data-stu-id="cbd13-350">This passage uses **Enter a path** as an example.</span></span>

    ![Elencare il percorso di archiviazione in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="cbd13-352">VS Code mantiene l'ultimo percorso visitato in ogni account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="cbd13-353">Ad esempio /tt/ss.</span><span class="sxs-lookup"><span data-stu-id="cbd13-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="cbd13-354">Sfogliare dal percorso radice: il percorso radice dell'elenco dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="cbd13-355">Immettere un percorso: elencare un percorso specificato dall'account di Data Lake Analytics selezionato o un percorso locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="cbd13-356">Selezionare un account dal percorso locale o un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Archiviazione dal menu di scelta rapida in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="cbd13-358">Immettere un percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-358">Enter an Azure storage path.</span></span> <span data-ttu-id="cbd13-359">Ad esempio /output.</span><span class="sxs-lookup"><span data-stu-id="cbd13-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="cbd13-360">Individuare il percorso di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-360">Find your Azure storage path.</span></span> <span data-ttu-id="cbd13-361">Selezionare **Choose current folder** (Scegli cartella corrente).</span><span class="sxs-lookup"><span data-stu-id="cbd13-361">Select **Choose current folder**.</span></span>

    ![Selezionare una cartella in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="cbd13-363">Risultati: la finestra **Output** mostra lo stato di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="cbd13-365">**Per caricare i file mediante il comando ADL: Upload File through Configuration (ADL: Carica file da configurazione)**</span><span class="sxs-lookup"><span data-stu-id="cbd13-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="cbd13-366">Premere CTRL+MAIUSC+P per aprire il riquadro comandi o fare clic con il pulsante destro del mouse sull'editor di script, quindi immettere **Upload File through Configuration** (Carica file da configurazione).</span><span class="sxs-lookup"><span data-stu-id="cbd13-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="cbd13-367">VS Code visualizza un file JSON.</span><span class="sxs-lookup"><span data-stu-id="cbd13-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="cbd13-368">È possibile immettere i percorsi di file e caricare più file contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="cbd13-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="cbd13-369">Le istruzioni sono visualizzate nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="cbd13-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="cbd13-370">Salvare (CTRL+S) il file JSON per procedere con il caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Percorso del file in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="cbd13-372">Risultati: la finestra **Output** mostra lo stato di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Stato di caricamento in Strumenti Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="cbd13-374">Un altro modo per caricare file da archiviare è fare clic con il pulsante destro del mouse sul percorso completo del file o sul percorso relativo del file nell'editor di script.</span><span class="sxs-lookup"><span data-stu-id="cbd13-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="cbd13-375">Immettere il percorso del file locale e quindi selezionare l'account.</span><span class="sxs-lookup"><span data-stu-id="cbd13-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="cbd13-376">La finestra **Output** mostra lo stato di caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="cbd13-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="cbd13-377">Aprire Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="cbd13-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="cbd13-378">È possibile aprire **Azure Storage Explorer** immettendo il comando **ADL: Open Web Azure Storage Explorer** (ADL: Apri Web Azure Storage Explorer) o selezionando la voce dal menu di scelta rapida visualizzato facendo clic con il pulsante destro del mouse.</span><span class="sxs-lookup"><span data-stu-id="cbd13-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="cbd13-379">**Per aprire Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="cbd13-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="cbd13-380">Premere CTRL+MAIUSC+P per aprire il riquadro comandi.</span><span class="sxs-lookup"><span data-stu-id="cbd13-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="cbd13-381">Immettere **Open Web Azure Storage Explorer** (Apri Web Azure Storage Explorer) o fare clic con il pulsante destro del mouse su un percorso relativo o un percorso completo nell'editor di script e quindi scegliere **Open Web Azure Storage Explorer** (Apri Web Azure Storage Explorer).</span><span class="sxs-lookup"><span data-stu-id="cbd13-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="cbd13-382">Selezionare un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="cbd13-383">Strumenti Data Lake apre il percorso di archiviazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cbd13-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="cbd13-384">È possibile trovare il percorso e visualizzare in anteprima il file dal Web.</span><span class="sxs-lookup"><span data-stu-id="cbd13-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="cbd13-385">Esecuzione e debug locale per utenti Windows</span><span class="sxs-lookup"><span data-stu-id="cbd13-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="cbd13-386">L'esecuzione locale di U-SQL verifica i dati locali e convalida lo script localmente prima che il codice venga pubblicato in Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="cbd13-387">La funzionalità di debug locale consente di completare le seguenti operazioni prima che il codice venga inviato a Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="cbd13-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="cbd13-388">Eseguire il debug del code-behind di C#.</span><span class="sxs-lookup"><span data-stu-id="cbd13-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="cbd13-389">Eseguire il codice passo per passo.</span><span class="sxs-lookup"><span data-stu-id="cbd13-389">Step through the code.</span></span> 
- <span data-ttu-id="cbd13-390">Convalidare lo script in locale.</span><span class="sxs-lookup"><span data-stu-id="cbd13-390">Validate your script locally.</span></span>

<span data-ttu-id="cbd13-391">Per istruzioni sull'esecuzione e il debug locali, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="cbd13-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="cbd13-392">Funzionalità aggiuntive</span><span class="sxs-lookup"><span data-stu-id="cbd13-392">Additional features</span></span>

<span data-ttu-id="cbd13-393">Strumenti Data Lake per VS Code supporta le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbd13-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="cbd13-394">Completamento automatico di IntelliSense: vengono visualizzati suggerimenti in finestre popup intorno agli elementi, ad esempio parole chiave, metodi e variabili.</span><span class="sxs-lookup"><span data-stu-id="cbd13-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="cbd13-395">Le icone differenti rappresentano tipi di oggetti diversi:</span><span class="sxs-lookup"><span data-stu-id="cbd13-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="cbd13-396">Tipo di dati Scala</span><span class="sxs-lookup"><span data-stu-id="cbd13-396">Scala data type</span></span>
    - <span data-ttu-id="cbd13-397">Tipo di dati complesso</span><span class="sxs-lookup"><span data-stu-id="cbd13-397">Complex data type</span></span>
    - <span data-ttu-id="cbd13-398">UDT integrati</span><span class="sxs-lookup"><span data-stu-id="cbd13-398">Built-in UDTs</span></span>
    - <span data-ttu-id="cbd13-399">Raccolta e classi .NET</span><span class="sxs-lookup"><span data-stu-id="cbd13-399">.NET collection and classes</span></span>
    - <span data-ttu-id="cbd13-400">Espressioni C#</span><span class="sxs-lookup"><span data-stu-id="cbd13-400">C# expressions</span></span>
    - <span data-ttu-id="cbd13-401">UDF, UDO e UDAAG di C# integrati</span><span class="sxs-lookup"><span data-stu-id="cbd13-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="cbd13-402">Funzioni di U-SQL</span><span class="sxs-lookup"><span data-stu-id="cbd13-402">U-SQL functions</span></span>
    - <span data-ttu-id="cbd13-403">Funzione di windowing di U-SQL</span><span class="sxs-lookup"><span data-stu-id="cbd13-403">U-SQL windowing function</span></span>
 
    ![Tipi di oggetto IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="cbd13-405">Completamento automatico IntelliSense per i metadati di Data Lake Analytics: Strumanti Data Lake scarica le informazioni di metadati di Data Lake Analytics localmente.</span><span class="sxs-lookup"><span data-stu-id="cbd13-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="cbd13-406">La funzionalità IntelliSense popola automaticamente gli oggetti, tra cui database, schemi, tabelle, visualizzazione, funzione con valori di tabella, procedure e assembly C#, dai metadati di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="cbd13-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Metadati IntelliSense degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="cbd13-408">Indicatore di errore di IntelliSense: Strumenti Data Lake sottolinea gli errori di modifica per U-SQL e C#.</span><span class="sxs-lookup"><span data-stu-id="cbd13-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="cbd13-409">Evidenziazione della sintassi: Strumenti Data Lake usa colori diversi per distinguere gli elementi, ad esempio variabili, parole chiave, tipo di dati e funzioni.</span><span class="sxs-lookup"><span data-stu-id="cbd13-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Sintassi in evidenza degli strumenti di Data Lake per Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="cbd13-411">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbd13-411">Next steps</span></span>

- <span data-ttu-id="cbd13-412">Per l'esecuzione e il debug locali di U-SQL con Visual Studio Code, vedere [Esecuzione locale e debug locale di U-SQL con Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="cbd13-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="cbd13-413">Per informazioni introduttive su Data Lake Analytics, vedere [Esercitazione: Introduzione a Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbd13-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="cbd13-414">Per informazioni sull'uso degli strumenti di Data Lake per Visual Studio, vedere [Esercitazione: Sviluppare script U-SQL tramite Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cbd13-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="cbd13-415">Per informazioni sullo sviluppo di assembly, vedere [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md) (Sviluppare assembly U-SQL per i processi di Azure Data Lake Analytics).</span><span class="sxs-lookup"><span data-stu-id="cbd13-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



