---
title: "installazione del servizio di mobilità per Azure Site Recovery usando gli strumenti di distribuzione software aaaAutomate | Documenti Microsoft"
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
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="28a09-103">Automatizzare l'installazione del servizio Mobility tramite strumenti di distribuzione software</span><span class="sxs-lookup"><span data-stu-id="28a09-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="28a09-104">In questo documento si presuppone l'utilizzo della versione **9.9.4510.1** o successiva.</span><span class="sxs-lookup"><span data-stu-id="28a09-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="28a09-105">In questo articolo si fornisce un esempio di utilizzo di System Center Configuration Manager toodeploy hello servizio di mobilità di Azure Site Recovery nel Data Center.</span><span class="sxs-lookup"><span data-stu-id="28a09-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="28a09-106">Utilizzando uno strumento di distribuzione software come Configuration Manager ha hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="28a09-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="28a09-107">Pianificazione della distribuzione di nuove installazioni e aggiornamenti durante la finestra di manutenzione pianificata per gli aggiornamenti software</span><span class="sxs-lookup"><span data-stu-id="28a09-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="28a09-108">Scalabilità toohundreds di distribuzione di server contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="28a09-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="28a09-109">In questo articolo usa l'attività di distribuzione di System Center Configuration Manager 2012 R2 toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="28a09-110">È anche possibile automatizzare l'installazione del servizio Mobility tramite [Automazione di Azure e la configurazione dello stato desiderato](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="28a09-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28a09-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="28a09-111">Prerequisites</span></span>
1. <span data-ttu-id="28a09-112">Uno strumento di distribuzione software come Configuration Manager già distribuito nell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="28a09-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="28a09-113">Creare due [raccolte dispositivi](https://technet.microsoft.com/library/gg682169.aspx), uno per tutti i **server Windows**e un altro per tutti i **server Linux**, che si desidera tooprotect tramite il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="28a09-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="28a09-114">Un server di configurazione già registrato con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="28a09-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="28a09-115">Condivisione file di rete sicura (condivisione di Server Message Block) accessibile dal server di Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="28a09-116">Distribuire il servizio Mobility nei computer che eseguono Windows</span><span class="sxs-lookup"><span data-stu-id="28a09-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="28a09-117">In questo articolo presuppone che l'indirizzo IP hello hello del server di configurazione è 192.168.3.121, e tale condivisione di file di rete sicura hello \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="28a09-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="28a09-118">Passaggio 1: preparare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="28a09-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="28a09-119">Creare una cartella nella condivisione di rete hello e denominarlo **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="28a09-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="28a09-120">Accedi a server di configurazione tooyour e aprire un prompt dei comandi amministrativo.</span><span class="sxs-lookup"><span data-stu-id="28a09-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="28a09-121">Eseguire hello seguenti comandi toogenerate un file della passphrase:</span><span class="sxs-lookup"><span data-stu-id="28a09-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="28a09-122">Hello copia **MobSvc.passphrase** file hello **MobSvcWindows** cartella nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="28a09-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="28a09-123">Sfoglia toohello repository di programma di installazione nel server di configurazione hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="28a09-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="28a09-124">Hello copia  **Microsoft ASR\_UA\_*versione*\_Windows\_GA\_*data* \_ Release.exe** toohello **MobSvcWindows** cartella nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="28a09-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="28a09-125">Copiare hello seguente di codice e salvarlo come **install.bat** in hello **MobSvcWindows** cartella.</span><span class="sxs-lookup"><span data-stu-id="28a09-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28a09-126">Sostituire i segnaposto hello [CSIP] in questo script con i valori effettivi hello dell'indirizzo IP di hello del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="28a09-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="28a09-127">Passaggio 2: creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="28a09-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="28a09-128">Accedi tooyour console di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="28a09-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="28a09-129">Sfoglia troppo**libreria Software** > **Application Management** > **pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="28a09-130">Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="28a09-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="28a09-131">Fornire valori per hello nome, descrizione, produttore, lingua e versione.</span><span class="sxs-lookup"><span data-stu-id="28a09-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="28a09-132">Seleziona hello **questo pacchetto contiene file di origine** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="28a09-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="28a09-133">Fare clic su **Sfoglia**e condivisione di rete selezionare hello in cui è archiviato installer hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="28a09-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="28a09-135">In hello **scegliere hello programma il tipo che si desidera toocreate** selezionare **programma Standard**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="28a09-137">In hello **specificare le informazioni sul programma standard** pagina specificare hello seguendo gli input e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="28a09-138">(hello altri input possono utilizzare i valori predefiniti.)</span><span class="sxs-lookup"><span data-stu-id="28a09-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="28a09-139">**Nome parametro**</span><span class="sxs-lookup"><span data-stu-id="28a09-139">**Parameter name**</span></span> | <span data-ttu-id="28a09-140">**Valore**</span><span class="sxs-lookup"><span data-stu-id="28a09-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="28a09-141">Nome</span><span class="sxs-lookup"><span data-stu-id="28a09-141">Name</span></span> | <span data-ttu-id="28a09-142">Installare il servizio Mobility di Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="28a09-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="28a09-143">Riga di comando</span><span class="sxs-lookup"><span data-stu-id="28a09-143">Command line</span></span> | <span data-ttu-id="28a09-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="28a09-144">install.bat</span></span> |
  | <span data-ttu-id="28a09-145">Il programma può essere eseguito</span><span class="sxs-lookup"><span data-stu-id="28a09-145">Program can run</span></span> | <span data-ttu-id="28a09-146">anche se non ci sono utenti connessi</span><span class="sxs-lookup"><span data-stu-id="28a09-146">Whether or not a user is logged on</span></span> |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="28a09-148">Nella pagina successiva di hello, selezionare i sistemi operativi di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="28a09-149">Il servizio Mobility può essere installato solo su Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="28a09-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="28a09-151">procedura guidata hello toocomplete, fare clic su **Avanti** due volte.</span><span class="sxs-lookup"><span data-stu-id="28a09-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="28a09-152">script di Hello supporta entrambe le nuove installazioni di agenti di servizio di mobilità e aggiorna tooagents che sono già installati.</span><span class="sxs-lookup"><span data-stu-id="28a09-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="28a09-153">Passaggio 3: Distribuire il pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="28a09-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="28a09-154">Nella console di Configuration Manager hello, il pacchetto e scegliere **Distribuisci contenuto**.</span><span class="sxs-lookup"><span data-stu-id="28a09-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="28a09-155">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="28a09-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="28a09-156">Seleziona hello  **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  su toowhich devono essere copiati i pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="28a09-157">Creazione guidata hello completo.</span><span class="sxs-lookup"><span data-stu-id="28a09-157">Complete hello wizard.</span></span> <span data-ttu-id="28a09-158">pacchetto Hello quindi avvia la replica toohello specifica i punti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="28a09-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="28a09-159">Dopo la distribuzione del pacchetto di hello, pacchetto hello e scegliere **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="28a09-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="28a09-160">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="28a09-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="28a09-161">Selezionare hello raccolta di dispositivi di Windows Server che è stato creato nella sezione Prerequisiti hello come raccolta di destinazione hello per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="28a09-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="28a09-163">In hello **specifica destinazione di contenuto hello** pagina, selezionare il **punti di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="28a09-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="28a09-164">In hello **toocontrol le impostazioni di specificare la modalità di distribuzione del software** pagina, assicurarsi che sia scopo hello **necessari**.</span><span class="sxs-lookup"><span data-stu-id="28a09-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="28a09-166">In hello **specificare la pianificazione per questa distribuzione hello** , specificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="28a09-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="28a09-167">Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="28a09-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="28a09-168">In hello **punti di distribuzione** pagina, configurare le proprietà di hello in base alle esigenze toohello del centro dati.</span><span class="sxs-lookup"><span data-stu-id="28a09-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="28a09-169">Quindi completare la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="28a09-170">riavvio di tooavoid non necessari, pianificare l'installazione del pacchetto hello durante la finestra di manutenzione mensile o una finestra degli aggiornamenti software.</span><span class="sxs-lookup"><span data-stu-id="28a09-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="28a09-171">È possibile monitorare l'avanzamento della distribuzione hello utilizzando la console di Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="28a09-172">Andare troppo**monitoraggio** > **distribuzioni** > *[nome pacchetto]*.</span><span class="sxs-lookup"><span data-stu-id="28a09-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Distribuzioni di toomonitor opzione schermata di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="28a09-174">Distribuire il servizio Mobility nei computer che eseguono Linux</span><span class="sxs-lookup"><span data-stu-id="28a09-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="28a09-175">In questo articolo presuppone che l'indirizzo IP hello hello del server di configurazione è 192.168.3.121, e tale condivisione di file di rete sicura hello \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="28a09-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="28a09-176">Passaggio 1: preparare la distribuzione</span><span class="sxs-lookup"><span data-stu-id="28a09-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="28a09-177">Creare una cartella nella condivisione di rete hello e denominarla come **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="28a09-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="28a09-178">Accedi a server di configurazione tooyour e aprire un prompt dei comandi amministrativo.</span><span class="sxs-lookup"><span data-stu-id="28a09-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="28a09-179">Eseguire hello seguenti comandi toogenerate un file della passphrase:</span><span class="sxs-lookup"><span data-stu-id="28a09-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="28a09-180">Hello copia **MobSvc.passphrase** file hello **MobSvcLinux** cartella nella condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="28a09-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="28a09-181">Sfoglia toohello repository di programma di installazione nel server di configurazione hello eseguendo il comando hello:</span><span class="sxs-lookup"><span data-stu-id="28a09-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="28a09-182">Esempio hello copia file toohello **MobSvcLinux** cartella nella condivisione di rete:</span><span class="sxs-lookup"><span data-stu-id="28a09-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="28a09-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="28a09-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="28a09-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="28a09-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="28a09-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="28a09-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="28a09-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="28a09-189">Copiare hello seguente di codice e salvarlo come **install_linux.sh** in hello **MobSvcLinux** cartella.</span><span class="sxs-lookup"><span data-stu-id="28a09-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="28a09-190">Sostituire i segnaposto hello [CSIP] in questo script con i valori effettivi hello dell'indirizzo IP di hello del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="28a09-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="28a09-191">Passaggio 2: creare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="28a09-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="28a09-192">Accedi tooyour console di Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="28a09-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="28a09-193">Sfoglia troppo**libreria Software** > **Application Management** > **pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="28a09-194">Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="28a09-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="28a09-195">Fornire valori per hello nome, descrizione, produttore, lingua e versione.</span><span class="sxs-lookup"><span data-stu-id="28a09-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="28a09-196">Seleziona hello **questo pacchetto contiene file di origine** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="28a09-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="28a09-197">Fare clic su **Sfoglia**e condivisione di rete selezionare hello in cui è archiviato installer hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="28a09-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="28a09-199">In hello **scegliere hello programma il tipo che si desidera toocreate** selezionare **programma Standard**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="28a09-201">In hello **specificare le informazioni sul programma standard** pagina specificare hello seguendo gli input e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="28a09-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="28a09-202">(hello altri input possono utilizzare i valori predefiniti.)</span><span class="sxs-lookup"><span data-stu-id="28a09-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="28a09-203">**Nome parametro**</span><span class="sxs-lookup"><span data-stu-id="28a09-203">**Parameter name**</span></span> | <span data-ttu-id="28a09-204">**Valore**</span><span class="sxs-lookup"><span data-stu-id="28a09-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="28a09-205">Nome</span><span class="sxs-lookup"><span data-stu-id="28a09-205">Name</span></span> | <span data-ttu-id="28a09-206">Installare il servizio Mobility di Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="28a09-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="28a09-207">Riga di comando</span><span class="sxs-lookup"><span data-stu-id="28a09-207">Command line</span></span> | <span data-ttu-id="28a09-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="28a09-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="28a09-209">Il programma può essere eseguito</span><span class="sxs-lookup"><span data-stu-id="28a09-209">Program can run</span></span> | <span data-ttu-id="28a09-210">anche se non ci sono utenti connessi</span><span class="sxs-lookup"><span data-stu-id="28a09-210">Whether or not a user is logged on</span></span> |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="28a09-212">Nella pagina successiva di hello, selezionare **questo programma può essere eseguito su qualsiasi piattaforma**.</span><span class="sxs-lookup"><span data-stu-id="28a09-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="28a09-213">![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="28a09-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="28a09-214">procedura guidata hello toocomplete, fare clic su **Avanti** due volte.</span><span class="sxs-lookup"><span data-stu-id="28a09-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="28a09-215">script di Hello supporta entrambe le nuove installazioni di agenti di servizio di mobilità e aggiorna tooagents che sono già installati.</span><span class="sxs-lookup"><span data-stu-id="28a09-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="28a09-216">Passaggio 3: Distribuire il pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="28a09-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="28a09-217">Nella console di Configuration Manager hello, il pacchetto e scegliere **Distribuisci contenuto**.</span><span class="sxs-lookup"><span data-stu-id="28a09-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="28a09-218">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="28a09-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="28a09-219">Seleziona hello  **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  su toowhich devono essere copiati i pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="28a09-220">Creazione guidata hello completo.</span><span class="sxs-lookup"><span data-stu-id="28a09-220">Complete hello wizard.</span></span> <span data-ttu-id="28a09-221">pacchetto Hello quindi avvia la replica toohello specifica i punti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="28a09-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="28a09-222">Dopo la distribuzione del pacchetto di hello, pacchetto hello e scegliere **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="28a09-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="28a09-223">![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="28a09-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="28a09-224">Selezionare hello raccolta dispositivi Linux Server è stato creato nella sezione Prerequisiti hello come raccolta di destinazione hello per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="28a09-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="28a09-226">In hello **specifica destinazione di contenuto hello** pagina, selezionare il **punti di distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="28a09-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="28a09-227">In hello **toocontrol le impostazioni di specificare la modalità di distribuzione del software** pagina, assicurarsi che sia scopo hello **necessari**.</span><span class="sxs-lookup"><span data-stu-id="28a09-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="28a09-229">In hello **specificare la pianificazione per questa distribuzione hello** , specificare una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="28a09-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="28a09-230">Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="28a09-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="28a09-231">In hello **punti di distribuzione** pagina, configurare le proprietà di hello in base alle esigenze toohello del centro dati.</span><span class="sxs-lookup"><span data-stu-id="28a09-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="28a09-232">Quindi completare la procedura guidata hello.</span><span class="sxs-lookup"><span data-stu-id="28a09-232">Then complete hello wizard.</span></span>

<span data-ttu-id="28a09-233">Servizio di mobilità viene installato e su hello raccolta di dispositivi Server Linux, in base toohello pianificazione configurata.</span><span class="sxs-lookup"><span data-stu-id="28a09-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="28a09-234">Altri tooinstall metodi del servizio di mobilità</span><span class="sxs-lookup"><span data-stu-id="28a09-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="28a09-235">Di seguito sono riportate altre opzioni per l'installazione del servizio Mobility:</span><span class="sxs-lookup"><span data-stu-id="28a09-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="28a09-236">Installazione manuale tramite interfaccia utente grafica</span><span class="sxs-lookup"><span data-stu-id="28a09-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="28a09-237">Installazione manuale tramite la riga di comando</span><span class="sxs-lookup"><span data-stu-id="28a09-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="28a09-238">Installazione push tramite il server di configurazione</span><span class="sxs-lookup"><span data-stu-id="28a09-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="28a09-239">Installazione automatica tramite Automazione di Azure e la configurazione dello stato desiderato</span><span class="sxs-lookup"><span data-stu-id="28a09-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="28a09-240">Disinstallare il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="28a09-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="28a09-241">È possibile creare pacchetti di Configuration Manager toouninstall servizio di mobilità.</span><span class="sxs-lookup"><span data-stu-id="28a09-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="28a09-242">Utilizzare hello lo script seguente viene toodo pertanto:</span><span class="sxs-lookup"><span data-stu-id="28a09-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="28a09-243">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28a09-243">Next steps</span></span>
<span data-ttu-id="28a09-244">Si è pronti a questo punto troppo[abilitare la protezione](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="28a09-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
