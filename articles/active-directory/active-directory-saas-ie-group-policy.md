---
title: Distribuire l'estensione Pannello di accesso di Azure per Internet Explorer con un criterio di gruppo | Documentazione Microsoft
description: Come usare Criteri di gruppo per distribuire il componente aggiuntivo di Internet Explorer per il portale App personali.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b402ae326ab34ec71ad9de966e22be00045fee3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-deploy-the-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="2dd08-103">Come distribuire l'estensione Pannello di accesso per Internet Explorer con Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="2dd08-103">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="2dd08-104">Questa esercitazione illustra come usare Criteri di gruppo per installare l'estensione Pannello di accesso per Internet Explorer nei computer degli utenti in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="2dd08-104">This tutorial shows how to use group policy to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="2dd08-105">Questa estensione è necessaria per gli utenti di Internet Explorer che devono eseguire l'accesso ad app configurate con l' [accesso Single Sign-On basato su password](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2dd08-105">This extension is required for Internet Explorer users who need to sign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="2dd08-106">Si consiglia agli amministratori di automatizzare la distribuzione di questa estensione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-106">It is recommended that admins automate the deployment of this extension.</span></span> <span data-ttu-id="2dd08-107">In caso contrario, gli utenti devono scaricare e installare l'estensione in autonomia, un'operazione soggetta a errori e che richiede autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="2dd08-107">Otherwise, users have to download and install the extension themselves, which is prone to user error and requires administrator permissions.</span></span> <span data-ttu-id="2dd08-108">Questa esercitazione descrive un metodo per automatizzare le distribuzioni software tramite Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2dd08-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="2dd08-109">Altre informazioni su Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="2dd08-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="2dd08-110">L'estensione Pannello di accesso è disponibile per [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) e [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998). In entrambi i casi l'installazione non richiede autorizzazioni di amministratore.</span><span class="sxs-lookup"><span data-stu-id="2dd08-110">The Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions to install.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dd08-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2dd08-111">Prerequisites</span></span>
* <span data-ttu-id="2dd08-112">[Servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)è già stato configurato e i computer degli utenti sono stati aggiunti al dominio.</span><span class="sxs-lookup"><span data-stu-id="2dd08-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>
* <span data-ttu-id="2dd08-113">Per modificare l'oggetto Criteri di gruppo è necessaria l'autorizzazione "Modifica impostazione".</span><span class="sxs-lookup"><span data-stu-id="2dd08-113">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="2dd08-114">Questa autorizzazione è assegnata per impostazione predefinita ai membri dei gruppi di sicurezza seguenti: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="2dd08-114">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="2dd08-115">Altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="2dd08-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-the-distribution-point"></a><span data-ttu-id="2dd08-116">Passaggio 1: Creare il punto di distribuzione</span><span class="sxs-lookup"><span data-stu-id="2dd08-116">Step 1: Create the Distribution Point</span></span>
<span data-ttu-id="2dd08-117">Per prima cosa, salvare il pacchetto del programma di installazione in un percorso di rete a cui possono accedere i computer in cui si vuole installare l'estensione in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="2dd08-117">First, you must place the installer package on a network location that can be accessed by the machines that you wish to remotely install the extension on.</span></span> <span data-ttu-id="2dd08-118">A questo scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dd08-118">To do this, follow these steps:</span></span>

1. <span data-ttu-id="2dd08-119">Eseguire l'accesso al server come amministratore</span><span class="sxs-lookup"><span data-stu-id="2dd08-119">Log on to the server as an administrator</span></span>
2. <span data-ttu-id="2dd08-120">Nella finestra **Server Manager** passare a **Servizi file e archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-120">In the **Server Manager** window, go to **Files and Storage Services**.</span></span>
   
    ![Apertura di Servizi file e archiviazione](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="2dd08-122">Passare alla scheda **Condivisioni** . Fare clic su **Attività** > **Nuova condivisione...**</span><span class="sxs-lookup"><span data-stu-id="2dd08-122">Go to the **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Apertura di Servizi file e archiviazione](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="2dd08-124">Completare la **Creazione guidata nuova condivisione** e impostare le autorizzazioni per assicurarsi che i computer degli utenti possano accedervi.</span><span class="sxs-lookup"><span data-stu-id="2dd08-124">Complete the **New Share Wizard** and set permissions to ensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="2dd08-125">Altre informazioni sulle condivisioni.</span><span class="sxs-lookup"><span data-stu-id="2dd08-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="2dd08-126">Scaricare il pacchetto di Microsoft Windows Installer (file MSI) seguente: [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="2dd08-126">Download the following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="2dd08-127">Copiare il pacchetto del programma di installazione nel percorso desiderato nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-127">Copy the installer package to a desired location on the share.</span></span>
   
    ![Copiare il file MSI nella condivisione.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="2dd08-129">Verificare che i computer client possano accedere al pacchetto del programma di installazione dalla condivisione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-129">Verify that your client machines are able to access the installer package from the share.</span></span> 

## <a name="step-2-create-the-group-policy-object"></a><span data-ttu-id="2dd08-130">Passaggio 2: Creare l'oggetto Criteri di gruppo</span><span class="sxs-lookup"><span data-stu-id="2dd08-130">Step 2: Create the Group Policy Object</span></span>
1. <span data-ttu-id="2dd08-131">Accedere al server che ospita l'installazione di Servizi di dominio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2dd08-131">Log on to the server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="2dd08-132">In Server Manager passare a **Strumenti** > **Gestione Criteri di gruppo**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-132">In the Server Manager, go to **Tools** > **Group Policy Management**.</span></span>
   
    ![Passare a Strumenti > Gestione Criteri di gruppo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="2dd08-134">Nel riquadro sinistro della finestra **Gestione Criteri di gruppo** visualizzare la gerarchia della propria unità organizzativa e determinare il livello in base al quale verranno applicati i criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2dd08-134">In the left pane of the **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like to apply the group policy.</span></span> <span data-ttu-id="2dd08-135">Ad esempio, è possibile decidere di selezionare un'unità organizzativa di piccole dimensioni per eseguire la distribuzione per un numero limitato di utenti ai fini del test oppure scegliere un'unità organizzativa di primo livello per eseguire la distribuzione a livello dell'intera organizzazione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-135">For instance, you may decide to pick a small OU to deploy to a few users for testing, or you may pick a top-level OU to deploy to your entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2dd08-136">Per creare o modificare le unità organizzative, tornare a Server Manager e passare a **Strumenti** > **Utenti e computer di Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-136">If you would like to create or edit your Organization Units (OUs), switch back to the Server Manager and go to **Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="2dd08-137">Dopo aver selezionato un'unità organizzativa, fare clic con il pulsante destro del mouse su di essa e scegliere **Crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento...**</span><span class="sxs-lookup"><span data-stu-id="2dd08-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Creare un nuovo oggetto Criteri di gruppo](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="2dd08-139">Nella finestra **Nuovo oggetto Criteri di gruppo** digitare un nome per il nuovo oggetto Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="2dd08-139">In the **New GPO** prompt, type in a name for the new Group Policy Object.</span></span>
   
    ![Assegnare un nome al nuovo oggetto Criteri di gruppo](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="2dd08-141">Fare clic con il pulsante destro del mouse sull'oggetto Criteri di gruppo creato e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-141">Right-click the Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Modificare il nuovo oggetto Criteri di gruppo](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-the-installation-package"></a><span data-ttu-id="2dd08-143">Passaggio 3: Assegnare il pacchetto di installazione</span><span class="sxs-lookup"><span data-stu-id="2dd08-143">Step 3: Assign the Installation Package</span></span>
1. <span data-ttu-id="2dd08-144">Determinare se l'estensione dovrà essere distribuita in base a una **Configurazione computer** o una **Configurazione utente**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-144">Determine whether you would like to deploy the extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="2dd08-145">Con una [Configurazione computer](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), l'estensione viene installata nel computer indipendentemente dall'utente che vi accede.</span><span class="sxs-lookup"><span data-stu-id="2dd08-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), the extension is installed on the computer regardless of which users log on to it.</span></span> <span data-ttu-id="2dd08-146">Con una [Configurazione utente](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), l'estensione viene installata per l'utente, indipendentemente dal computer a cui accede.</span><span class="sxs-lookup"><span data-stu-id="2dd08-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have the extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="2dd08-147">Nel riquadro sinistro della finestra **Editor Gestione Criteri di gruppo** passare a uno dei percorsi di cartella seguenti, a seconda del tipo di configurazione scelto:</span><span class="sxs-lookup"><span data-stu-id="2dd08-147">In the left pane of the **Group Policy Management Editor** window, go to either of the following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="2dd08-148">Fare clic con il pulsante destro del mouse su **Installazione software** e quindi scegliere **Nuovo** > **Pacchetto...**</span><span class="sxs-lookup"><span data-stu-id="2dd08-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Creare un nuovo pacchetto di installazione software](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="2dd08-150">Passare alla cartella condivisa che contiene il pacchetto del programma di installazione scaricato nel [Passaggio 1: Creare il punto di distribuzione](#step-1-create-the-distribution-point), selezionare il file MSI e quindi fare clic su **Apri**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-150">Go to the shared folder that contains the installer package from [Step 1: Create the Distribution Point](#step-1-create-the-distribution-point), select the .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="2dd08-151">Se la condivisione si trova nello stesso server, verificare che l'accesso al file MSI avvenga tramite il percorso di rete e non tramite il percorso locale.</span><span class="sxs-lookup"><span data-stu-id="2dd08-151">If the share is located on this same server, verify that you are accessing the .msi through the network file path, rather than the local file path.</span></span>
   > 
   > 
   
    ![Selezionare il pacchetto di installazione dalla cartella condivisa.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="2dd08-153">Nella finestra **Installazione applicazione** selezionare **Assegnata** per il metodo di distribuzione in uso.</span><span class="sxs-lookup"><span data-stu-id="2dd08-153">In the **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="2dd08-154">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-154">Then click **OK**.</span></span>
   
    ![Selezionare Assegnata e quindi fare clic su OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="2dd08-156">L'estensione è stata distribuita nell'unità organizzativa selezionata.</span><span class="sxs-lookup"><span data-stu-id="2dd08-156">The extension is now deployed to the OU that you selected.</span></span> [<span data-ttu-id="2dd08-157">Altre informazioni su Criteri di gruppo Installazione software</span><span class="sxs-lookup"><span data-stu-id="2dd08-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-the-extension-for-internet-explorer"></a><span data-ttu-id="2dd08-158">Passaggio 4: Abilitare automaticamente l'estensione per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="2dd08-158">Step 4: Auto-Enable the Extension for Internet Explorer</span></span>
<span data-ttu-id="2dd08-159">Dopo aver eseguito il programma di installazione, è necessario abilitare in modo esplicito ogni estensione per Internet Explorer prima di poterla usare.</span><span class="sxs-lookup"><span data-stu-id="2dd08-159">In addition to running the installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="2dd08-160">Per abilitare l'estensione Pannello di accesso tramite Criteri di gruppo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dd08-160">Follow the steps below to enable the Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="2dd08-161">Nella finestra **Editor Gestione Criteri di gruppo** passare a uno dei percorsi di cartella seguenti, a seconda del tipo di configurazione scelto in [Passaggio 3: Assegnare il pacchetto di installazione](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="2dd08-161">In the **Group Policy Management Editor** window, go to either of the following paths, depending on which type of configuration you chose in [Step 3: Assign the Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="2dd08-162">Fare clic con il pulsante destro del mouse su **Elenco componenti aggiuntivi** e scegliere **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="2dd08-163">![Modifica dell'elenco componenti aggiuntivi.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="2dd08-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="2dd08-164">Nella finestra **Elenco componenti aggiuntivi** selezionare **Abilitati**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-164">In the **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="2dd08-165">Nella sezione **Opzioni** fare clic su **Mostra...**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-165">Then, under the **Options** section, click **Show...**.</span></span>
   
    ![Fare clic su Abilita e quindi su Mostra...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="2dd08-167">Nella finestra **Visualizzazione contenuto** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dd08-167">In the **Show Contents** window, perform the following steps:</span></span>
   
   1. <span data-ttu-id="2dd08-168">Per la prima colonna (campo **Nome valore**) copiare e incollare l'ID classe seguente: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="2dd08-168">For the first column (the **Value Name** field), copy and paste the following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="2dd08-169">Per la seconda colonna (campo **Valore**) copiare e incollare il valore seguente: `1`</span><span class="sxs-lookup"><span data-stu-id="2dd08-169">For the second column (the **Value** field), type in the following value: `1`</span></span>
   3. <span data-ttu-id="2dd08-170">Fare clic su **OK** per chiudere la finestra di dialogo **Visualizzazione contenuto**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-170">Click **OK** to close the **Show Contents** window.</span></span>
      
      ![Compilare i valori come specificato sopra.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="2dd08-172">Fare clic su **OK** per applicare le modifiche e chiudere la finestra **Elenco componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-172">Click **OK** to apply your changes and close the **Add-on List** window.</span></span>

<span data-ttu-id="2dd08-173">L'estensione dovrebbe ora essere abilitata per i computer nell'unità organizzativa selezionata.</span><span class="sxs-lookup"><span data-stu-id="2dd08-173">The extension should now be enabled for the machines in the selected OU.</span></span> [<span data-ttu-id="2dd08-174">Altre informazioni sull'uso di Criteri di gruppo per abilitare o disabilitare i componenti aggiuntivi di Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2dd08-174">Learn more about using group policy to enable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="2dd08-175">Passaggio 5 (facoltativo): disabilitare la richiesta "Memorizza password"</span><span class="sxs-lookup"><span data-stu-id="2dd08-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="2dd08-176">Quando gli utenti accedono a siti Web utilizzando l'estensione del Pannello di accesso, Internet Explorer potrebbe visualizzare la seguente richiesta "Si desidera memorizzare la password?"</span><span class="sxs-lookup"><span data-stu-id="2dd08-176">When users sign-in to websites using the Access Panel Extension, Internet Explorer may show the following prompt asking "Would you like to store your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="2dd08-177">Se si desidera impedire agli utenti la visualizzazione del messaggio, attenersi alla procedura seguente per impedire al completamento automatico di ricordare le password:</span><span class="sxs-lookup"><span data-stu-id="2dd08-177">If you wish to prevent your users from seeing this prompt, then follow the steps below to prevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="2dd08-178">Nella finestra **Editor Gestione criteri di gruppo** , passare al percorso elencato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2dd08-178">In the **Group Policy Management Editor** window, go to the path listed below.</span></span> <span data-ttu-id="2dd08-179">Questa impostazione di configurazione è disponibile solo in **Configurazione utente**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="2dd08-180">Individuare l'impostazione denominata **Attiva Completamento automatico per nomi utente e password nei moduli**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-180">Find the setting named **Turn on the auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2dd08-181">Le versioni precedenti di Active Directory possono elencare questa impostazione con il nome **Non consentire al completamento automatico di salvare le password**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-181">Previous versions of Active Directory may list this setting with the name **Do not allow auto-complete to save passwords**.</span></span> <span data-ttu-id="2dd08-182">La configurazione dell'impostazione differisce da quella descritta in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-182">The configuration for that setting differs from the setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Ricordarsi di controllarlo nelle Impostazioni utente.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="2dd08-184">Fare clic con il pulsante destro sull'impostazione precedente e selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-184">Right click the above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="2dd08-185">Nella finestra denominata **Attiva Completamento automatico per nomi utente e password nei moduli** selezionare **Disabilitato**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-185">In the window titled **Turn on the auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Selezionare Disabilita](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="2dd08-187">Fare clic su **OK** per applicare queste modifiche e chiudere la finestra.</span><span class="sxs-lookup"><span data-stu-id="2dd08-187">Click **OK** to apply these changes and close the window.</span></span>

<span data-ttu-id="2dd08-188">Gli utenti non saranno più in grado di archiviare le credenziali o di utilizzare il completamento automatico per accedere alle credenziali archiviate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2dd08-188">Users will no longer be able to store their credentials or use auto-complete to access previously stored credentials.</span></span> <span data-ttu-id="2dd08-189">Tuttavia, questo criterio consente agli utenti di continuare a utilizzare il completamento automatico per altri tipi di campi dei moduli, ad esempio i campi di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2dd08-189">However, this policy does allow users to continue to use auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="2dd08-190">Se questo criterio è abilitato dopo che gli utenti hanno scelto di memorizzare alcune credenziali, questo criterio *non* cancellerà le credenziali che sono già state archiviate.</span><span class="sxs-lookup"><span data-stu-id="2dd08-190">If this policy is enabled after users have chosen to store some credentials, this policy will *not* clear the credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-the-deployment"></a><span data-ttu-id="2dd08-191">Passaggio 6: Test della distribuzione</span><span class="sxs-lookup"><span data-stu-id="2dd08-191">Step 6: Testing the Deployment</span></span>
<span data-ttu-id="2dd08-192">Per verificare la corretta distribuzione dell'estensione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dd08-192">Follow the steps below to verify if the extension deployment was successful:</span></span>

1. <span data-ttu-id="2dd08-193">Se per la distribuzione è stata selezionata l'opzione **Configurazione computer**, accedere a un computer client appartenente all'unità organizzativa selezionata in [Passaggio 2: Creare l'oggetto Criteri di gruppo](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="2dd08-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs to the OU that you selected in [Step 2: Create the Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="2dd08-194">Se invece è stata selezionata l'opzione **Configurazione utente**, assicurarsi di eseguire l'accesso con un nome utente appartenente all'unità organizzativa.</span><span class="sxs-lookup"><span data-stu-id="2dd08-194">If you deployed using **User Configuration**, make sure to sign in as a user who belongs to that OU.</span></span>
2. <span data-ttu-id="2dd08-195">Potrebbero essere necessari più accessi prima che le modifiche a Criteri di gruppo risultino completamente aggiornate nel computer.</span><span class="sxs-lookup"><span data-stu-id="2dd08-195">It may take a couple sign ins for the group policy changes to fully update with this machine.</span></span> <span data-ttu-id="2dd08-196">Per forzare l'aggiornamento, aprire una finestra del **prompt dei comandi** ed eseguire il comando seguente: `gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="2dd08-196">To force the update, open a **Command Prompt** window and run the following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="2dd08-197">Per avviare l'installazione, è necessario riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="2dd08-197">You must restart the machine for the installation to take place.</span></span> <span data-ttu-id="2dd08-198">L'avvio potrebbe impiegare molto più tempo del normale mentre è in corso l'installazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="2dd08-198">Bootup may take significantly more time than usual while the extension installs.</span></span>
4. <span data-ttu-id="2dd08-199">Dopo aver riavviato, aprire **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="2dd08-200">Nell'angolo in alto a destra della finestra fare clic su **Strumenti** (l'icona a forma di ingranaggio) e quindi selezionare **Gestione componenti aggiuntivi**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-200">On the upper-right corner of the window, click **Tools** (the gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Passare a Strumenti > Gestione componenti aggiuntivi](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="2dd08-202">Nella finestra **Gestione componenti aggiuntivi** verificare che **Estensione Pannello di accesso** sia installata e che lo **Stato** sia impostato su **Abilitato**.</span><span class="sxs-lookup"><span data-stu-id="2dd08-202">In the **Manage Add-ons** window, verify that the **Access Panel Extension** has been installed and that its **Status** has been set to **Enabled**.</span></span>
   
    ![Verificare che l'estensione Pannello di accesso sia installata e abilitata.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="2dd08-204">Articoli correlati</span><span class="sxs-lookup"><span data-stu-id="2dd08-204">Related Articles</span></span>
* [<span data-ttu-id="2dd08-205">Indice di articoli per la gestione di applicazioni in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dd08-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="2dd08-206">Accesso alle applicazioni e Single Sign-On con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2dd08-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="2dd08-207">Risoluzione dei problemi dell’estensione del pannello di accesso per Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="2dd08-207">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

