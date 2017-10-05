---
title: Automatizzare l'installazione del servizio Mobility per Azure Site Recovery con gli strumenti di distribuzione software | Microsoft Docs
description: Questo articolo consente di automatizzare l'installazione del servizio Mobility con strumenti di distribuzione software come System Center Configuration Manager.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="aa250-103">Automatizzare l'installazione del servizio Mobility tramite strumenti di distribuzione software</span><span class="sxs-lookup"><span data-stu-id="aa250-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="aa250-104">In questo documento si presuppone l'utilizzo della versione **9.9.4510.1** o successiva.</span><span class="sxs-lookup"><span data-stu-id="aa250-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="aa250-105">In questo articolo viene descritto un esempio di come è possibile usare System Center Configuration Manager per distribuire il servizio Mobility di Azure Site Recovery nel data center.</span><span class="sxs-lookup"><span data-stu-id="aa250-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="aa250-106">L'uso di uno strumento di distribuzione software come Configuration Manager offre i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="aa250-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="aa250-107">Pianificazione della distribuzione di nuove installazioni e aggiornamenti durante la finestra di manutenzione pianificata per gli aggiornamenti software</span><span class="sxs-lookup"><span data-stu-id="aa250-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="aa250-108">Distribuzione a elevata scalabilità a centinaia di server simultaneamente</span><span class="sxs-lookup"><span data-stu-id="aa250-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="aa250-109">In questo articolo si usa System Center Configuration Manager 2012 R2 per illustrare l'attività di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa250-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="aa250-110">È anche possibile automatizzare l'installazione del servizio Mobility tramite [Automazione di Azure e la configurazione dello stato desiderato](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="aa250-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa250-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aa250-111">Prerequisites</span></span>
1. <span data-ttu-id="aa250-112">Uno strumento di distribuzione software come Configuration Manager già distribuito nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="aa250-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="aa250-113">Creare due [Raccolte dispositivi](https://technet.microsoft.com/library/gg682169.aspx), una per tutti i **server Windows** e una per tutti i **server Linux** da proteggere con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa250-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="aa250-114">Un server di configurazione già registrato con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa250-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="aa250-115">Una condivisione file di rete sicura (condivisione Server Message Block) che sia accessibile dal server di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="aa250-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="aa250-116">Distribuire il servizio Mobility nei computer che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="aa250-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="aa250-117">In questo articolo si presuppone che l'indirizzo IP del server di configurazione sia 192.168.3.121 e che la condivisione di file di rete sicura sia \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="aa250-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="aa250-118">Passaggio 1: preparare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="aa250-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="aa250-119">Creare una cartella nella condivisione di rete chiamandola **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="aa250-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="aa250-120">Accedere al server di configurazione e aprire un prompt dei comandi amministrativo.</span><span class="sxs-lookup"><span data-stu-id="aa250-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="aa250-121">Eseguire i comandi seguenti per generare un file passphrase:</span><span class="sxs-lookup"><span data-stu-id="aa250-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="aa250-122">Copiare il file **MobSvc.passphrase** nella cartella **MobSvcWindows** nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="aa250-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="aa250-123">Accedere al repository del programma di installazione nel server di configurazione eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aa250-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="aa250-124">Copiare **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** nella cartella **MobSvcWindows** nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="aa250-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="aa250-125">Copiare il codice seguente e salvarlo come **install.bat** nella cartella **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="aa250-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aa250-126">Sostituire i segnaposto [CSIP] nello script seguente con i valori effettivi dell'indirizzo IP del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa250-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="aa250-127">Passaggio 2: creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="aa250-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="aa250-128">Accedere alla console di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="aa250-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="aa250-129">Passare a **Raccolta software** > **Gestione applicazioni** > **Pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="aa250-130">Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="aa250-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="aa250-131">Indicare i valori per nome, descrizione, produttore, lingua e versione.</span><span class="sxs-lookup"><span data-stu-id="aa250-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="aa250-132">Selezionare la casella di controllo **Questo pacchetto contiene file di origine**.</span><span class="sxs-lookup"><span data-stu-id="aa250-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="aa250-133">Fare clic su **Sfoglia** e selezionare la condivisione di rete in cui è archiviato il programma di installazione (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="aa250-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="aa250-135">Nella pagina **Scegliere il tipo di programma da creare** selezionare **Programma standard** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="aa250-137">Nella pagina **Specificare le informazioni sul programma standard** indicare gli input seguenti e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="aa250-138">Gli altri input possono mantenere i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="aa250-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="aa250-139">**Nome parametro**</span><span class="sxs-lookup"><span data-stu-id="aa250-139">**Parameter name**</span></span> | <span data-ttu-id="aa250-140">**Valore**</span><span class="sxs-lookup"><span data-stu-id="aa250-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="aa250-141">Nome</span><span class="sxs-lookup"><span data-stu-id="aa250-141">Name</span></span> | <span data-ttu-id="aa250-142">Installare il servizio Mobility di Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="aa250-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="aa250-143">Riga di comando</span><span class="sxs-lookup"><span data-stu-id="aa250-143">Command line</span></span> | <span data-ttu-id="aa250-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="aa250-144">install.bat</span></span> |
  | <span data-ttu-id="aa250-145">Il programma può essere eseguito</span><span class="sxs-lookup"><span data-stu-id="aa250-145">Program can run</span></span> | <span data-ttu-id="aa250-146">anche se non ci sono utenti connessi</span><span class="sxs-lookup"><span data-stu-id="aa250-146">Whether or not a user is logged on</span></span> |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="aa250-148">Nella pagina successiva selezionare i sistemi operativi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="aa250-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="aa250-149">Il servizio Mobility può essere installato solo su Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="aa250-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="aa250-151">Fare clic su **Avanti** due volte per completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="aa250-152">Lo script supporta sia le nuove installazioni degli agenti del servizio Mobility che l'aggiornamento degli agenti già installati.</span><span class="sxs-lookup"><span data-stu-id="aa250-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="aa250-153">Passaggio 3: distribuire il pacchetto</span><span class="sxs-lookup"><span data-stu-id="aa250-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="aa250-154">Nella console di Configuration Manager fare clic con il pulsante destro del mouse sul pacchetto e selezionare **Distribuisci contenuto**.</span><span class="sxs-lookup"><span data-stu-id="aa250-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="aa250-155">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="aa250-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="aa250-156">Selezionare i **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** in cui copiare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="aa250-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="aa250-157">Completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-157">Complete the wizard.</span></span> <span data-ttu-id="aa250-158">Il pacchetto inizia la replica nei punti di distribuzione specificati.</span><span class="sxs-lookup"><span data-stu-id="aa250-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="aa250-159">Dopo aver completato la distribuzione del pacchetto, fare clic su quest'ultimo con il pulsante destro del mouse e selezionare **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="aa250-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="aa250-160">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="aa250-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="aa250-161">Selezionare la raccolta di dispositivi di Windows Server creata nella sezione dei prerequisiti come raccolta di destinazione per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa250-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="aa250-163">Nella pagina **Specificare la destinazione del contenuto** selezionare i **Punti di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="aa250-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="aa250-164">Nella pagina **Specificare le impostazioni per controllare la modalità di distribuzione del software** verificare che lo scopo sia **Obbligatorio**.</span><span class="sxs-lookup"><span data-stu-id="aa250-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="aa250-166">Specificare una pianificazione nella pagina **Specificare la pianificazione per questa distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="aa250-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="aa250-167">Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa250-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="aa250-168">Configurare le proprietà nella pagina **Punti di distribuzione** in base alle necessità del data center.</span><span class="sxs-lookup"><span data-stu-id="aa250-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="aa250-169">Completare quindi la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="aa250-170">Per evitare riavvii non necessari, pianificare l'installazione del pacchetto durante la finestra di manutenzione mensile o degli aggiornamenti software.</span><span class="sxs-lookup"><span data-stu-id="aa250-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="aa250-171">È possibile monitorare l'avanzamento della distribuzione tramite la console di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="aa250-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="aa250-172">Passare a **Monitoraggio** > **Distribuzioni** > *[nome pacchetto]*.</span><span class="sxs-lookup"><span data-stu-id="aa250-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Schermata dell'opzione di Configuration Manager per monitorare le distribuzioni](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="aa250-174">Distribuire il servizio Mobility nei computer che eseguono Linux</span><span class="sxs-lookup"><span data-stu-id="aa250-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="aa250-175">In questo articolo si presuppone che l'indirizzo IP del server di configurazione sia 192.168.3.121 e che la condivisione di file di rete sicura sia \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="aa250-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="aa250-176">Passaggio 1: preparare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="aa250-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="aa250-177">Creare una cartella nella condivisione di rete chiamandola **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="aa250-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="aa250-178">Accedere al server di configurazione e aprire un prompt dei comandi amministrativo.</span><span class="sxs-lookup"><span data-stu-id="aa250-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="aa250-179">Eseguire i comandi seguenti per generare un file passphrase:</span><span class="sxs-lookup"><span data-stu-id="aa250-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="aa250-180">Copiare il file **MobSvc.passphrase** nella cartella **MobSvcLinux** nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="aa250-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="aa250-181">Accedere al repository del programma di installazione nel server di configurazione eseguendo il comando:</span><span class="sxs-lookup"><span data-stu-id="aa250-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="aa250-182">Copiare i file seguenti nella cartella **MobSvcLinux** nella condivisione di rete:</span><span class="sxs-lookup"><span data-stu-id="aa250-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="aa250-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="aa250-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="aa250-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="aa250-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="aa250-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="aa250-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa250-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="aa250-189">Copiare il codice seguente e salvarlo come **install_linux.sh** nella cartella **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="aa250-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="aa250-190">Sostituire i segnaposto [CSIP] nello script seguente con i valori effettivi dell'indirizzo IP del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="aa250-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="aa250-191">Passaggio 2: creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="aa250-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="aa250-192">Accedere alla console di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="aa250-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="aa250-193">Passare a **Raccolta software** > **Gestione applicazioni** > **Pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="aa250-194">Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="aa250-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="aa250-195">Indicare i valori per nome, descrizione, produttore, lingua e versione.</span><span class="sxs-lookup"><span data-stu-id="aa250-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="aa250-196">Selezionare la casella di controllo **Questo pacchetto contiene file di origine**.</span><span class="sxs-lookup"><span data-stu-id="aa250-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="aa250-197">Fare clic su **Sfoglia** e selezionare la condivisione di rete in cui è archiviato il programma di installazione (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="aa250-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="aa250-199">Nella pagina **Scegliere il tipo di programma da creare** selezionare **Programma standard** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="aa250-201">Nella pagina **Specificare le informazioni sul programma standard** indicare gli input seguenti e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="aa250-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="aa250-202">Gli altri input possono mantenere i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="aa250-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="aa250-203">**Nome parametro**</span><span class="sxs-lookup"><span data-stu-id="aa250-203">**Parameter name**</span></span> | <span data-ttu-id="aa250-204">**Valore**</span><span class="sxs-lookup"><span data-stu-id="aa250-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="aa250-205">Nome</span><span class="sxs-lookup"><span data-stu-id="aa250-205">Name</span></span> | <span data-ttu-id="aa250-206">Installare il servizio Mobility di Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="aa250-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="aa250-207">Riga di comando</span><span class="sxs-lookup"><span data-stu-id="aa250-207">Command line</span></span> | <span data-ttu-id="aa250-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="aa250-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="aa250-209">Il programma può essere eseguito</span><span class="sxs-lookup"><span data-stu-id="aa250-209">Program can run</span></span> | <span data-ttu-id="aa250-210">anche se non ci sono utenti connessi</span><span class="sxs-lookup"><span data-stu-id="aa250-210">Whether or not a user is logged on</span></span> |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="aa250-212">Nella pagina successiva selezionare **Questo programma può essere eseguito in qualsiasi piattaforma**.</span><span class="sxs-lookup"><span data-stu-id="aa250-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="aa250-213">![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="aa250-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="aa250-214">Fare clic su **Avanti** due volte per completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="aa250-215">Lo script supporta sia le nuove installazioni degli agenti del servizio Mobility che l'aggiornamento degli agenti già installati.</span><span class="sxs-lookup"><span data-stu-id="aa250-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="aa250-216">Passaggio 3: distribuire il pacchetto</span><span class="sxs-lookup"><span data-stu-id="aa250-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="aa250-217">Nella console di Configuration Manager fare clic con il pulsante destro del mouse sul pacchetto e selezionare **Distribuisci contenuto**.</span><span class="sxs-lookup"><span data-stu-id="aa250-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="aa250-218">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="aa250-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="aa250-219">Selezionare i **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** in cui copiare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="aa250-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="aa250-220">Completare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-220">Complete the wizard.</span></span> <span data-ttu-id="aa250-221">Il pacchetto inizia la replica nei punti di distribuzione specificati.</span><span class="sxs-lookup"><span data-stu-id="aa250-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="aa250-222">Dopo aver completato la distribuzione del pacchetto, fare clic su quest'ultimo con il pulsante destro del mouse e selezionare **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="aa250-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="aa250-223">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="aa250-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="aa250-224">Selezionare la raccolta di dispositivi server Linux creata nella sezione dei prerequisiti come raccolta di destinazione per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="aa250-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="aa250-226">Nella pagina **Specificare la destinazione del contenuto** selezionare i **Punti di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="aa250-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="aa250-227">Nella pagina **Specificare le impostazioni per controllare la modalità di distribuzione del software** verificare che lo scopo sia **Obbligatorio**.</span><span class="sxs-lookup"><span data-stu-id="aa250-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="aa250-229">Specificare una pianificazione nella pagina **Specificare la pianificazione per questa distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="aa250-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="aa250-230">Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa250-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="aa250-231">Configurare le proprietà nella pagina **Punti di distribuzione** in base alle necessità del data center.</span><span class="sxs-lookup"><span data-stu-id="aa250-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="aa250-232">Completare quindi la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="aa250-232">Then complete the wizard.</span></span>

<span data-ttu-id="aa250-233">Il servizio Mobility viene installato nella raccolta di dispositivi server Linux in base alla pianificazione configurata.</span><span class="sxs-lookup"><span data-stu-id="aa250-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="aa250-234">Altri metodi per installare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="aa250-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="aa250-235">Di seguito sono riportate altre opzioni per l'installazione del servizio Mobility:</span><span class="sxs-lookup"><span data-stu-id="aa250-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="aa250-236">Installazione manuale tramite interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="aa250-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="aa250-237">Installazione manuale tramite la riga di comando</span><span class="sxs-lookup"><span data-stu-id="aa250-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="aa250-238">Installazione push tramite il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="aa250-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="aa250-239">Installazione automatica tramite Automazione di Azure e la configurazione dello stato desiderato</span><span class="sxs-lookup"><span data-stu-id="aa250-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="aa250-240">Disinstallare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="aa250-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="aa250-241">È possibile creare pacchetti di Configuration Manager per disinstallare il servizio Mobility.</span><span class="sxs-lookup"><span data-stu-id="aa250-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="aa250-242">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="aa250-242">Use the following script to do so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="aa250-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aa250-243">Next steps</span></span>
<span data-ttu-id="aa250-244">È ora possibile [abilitare la protezione](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="aa250-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
