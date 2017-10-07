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
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Automatizzare l'installazione del servizio Mobility tramite strumenti di distribuzione software

>[!IMPORTANT]
In questo documento si presuppone l'utilizzo della versione **9.9.4510.1** o successiva.

In questo articolo si fornisce un esempio di utilizzo di System Center Configuration Manager toodeploy hello servizio di mobilità di Azure Site Recovery nel Data Center. Utilizzando uno strumento di distribuzione software come Configuration Manager ha hello seguenti vantaggi:
* Pianificazione della distribuzione di nuove installazioni e aggiornamenti durante la finestra di manutenzione pianificata per gli aggiornamenti software
* Scalabilità toohundreds di distribuzione di server contemporaneamente


> [!NOTE]
> In questo articolo usa l'attività di distribuzione di System Center Configuration Manager 2012 R2 toodemonstrate hello. È anche possibile automatizzare l'installazione del servizio Mobility tramite [Automazione di Azure e la configurazione dello stato desiderato](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Prerequisiti
1. Uno strumento di distribuzione software come Configuration Manager già distribuito nell'ambiente.
  Creare due [raccolte dispositivi](https://technet.microsoft.com/library/gg682169.aspx), uno per tutti i **server Windows**e un altro per tutti i **server Linux**, che si desidera tooprotect tramite il ripristino del sito.
3. Un server di configurazione già registrato con Site Recovery.
4. Condivisione file di rete sicura (condivisione di Server Message Block) accessibile dal server di Configuration Manager hello.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Distribuire il servizio Mobility nei computer che eseguono Windows
> [!NOTE]
> In questo articolo presuppone che l'indirizzo IP hello hello del server di configurazione è 192.168.3.121, e tale condivisione di file di rete sicura hello \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Passaggio 1: preparare la distribuzione
1. Creare una cartella nella condivisione di rete hello e denominarlo **MobSvcWindows**.
2. Accedi a server di configurazione tooyour e aprire un prompt dei comandi amministrativo.
3. Eseguire hello seguenti comandi toogenerate un file della passphrase:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hello copia **MobSvc.passphrase** file hello **MobSvcWindows** cartella nella condivisione di rete.
5. Sfoglia toohello repository di programma di installazione nel server di configurazione hello eseguendo hello comando seguente:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Hello copia  **Microsoft ASR\_UA\_*versione*\_Windows\_GA\_*data* \_ Release.exe** toohello **MobSvcWindows** cartella nella condivisione di rete.
7. Copiare hello seguente di codice e salvarlo come **install.bat** in hello **MobSvcWindows** cartella.

   > [!NOTE]
   > Sostituire i segnaposto hello [CSIP] in questo script con i valori effettivi hello dell'indirizzo IP di hello del server di configurazione.

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

### <a name="step-2-create-a-package"></a>Passaggio 2: creare un pacchetto

1. Accedi tooyour console di Configuration Manager.
2. Sfoglia troppo**libreria Software** > **Application Management** > **pacchetti**.
3. Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.
4. Fornire valori per hello nome, descrizione, produttore, lingua e versione.
5. Seleziona hello **questo pacchetto contiene file di origine** casella di controllo.
6. Fare clic su **Sfoglia**e condivisione di rete selezionare hello in cui è archiviato installer hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. In hello **scegliere hello programma il tipo che si desidera toocreate** selezionare **programma Standard**, fare clic su **Avanti**.

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. In hello **specificare le informazioni sul programma standard** pagina specificare hello seguendo gli input e fare clic su **Avanti**. (hello altri input possono utilizzare i valori predefiniti.)

  | **Nome parametro** | **Valore** |
  |--|--|
  | Nome | Installare il servizio Mobility di Microsoft Azure (Windows) |
  | Riga di comando | install.bat |
  | Il programma può essere eseguito | anche se non ci sono utenti connessi |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. Nella pagina successiva di hello, selezionare i sistemi operativi di destinazione hello. Il servizio Mobility può essere installato solo su Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. procedura guidata hello toocomplete, fare clic su **Avanti** due volte.


> [!NOTE]
> script di Hello supporta entrambe le nuove installazioni di agenti di servizio di mobilità e aggiorna tooagents che sono già installati.

### <a name="step-3-deploy-hello-package"></a>Passaggio 3: Distribuire il pacchetto di hello
1. Nella console di Configuration Manager hello, il pacchetto e scegliere **Distribuisci contenuto**.
  ![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Seleziona hello  **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  su toowhich devono essere copiati i pacchetti hello.
3. Creazione guidata hello completo. pacchetto Hello quindi avvia la replica toohello specifica i punti di distribuzione.
4. Dopo la distribuzione del pacchetto di hello, pacchetto hello e scegliere **Distribuisci**.
  ![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Selezionare hello raccolta di dispositivi di Windows Server che è stato creato nella sezione Prerequisiti hello come raccolta di destinazione hello per la distribuzione.

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. In hello **specifica destinazione di contenuto hello** pagina, selezionare il **punti di distribuzione**.
7. In hello **toocontrol le impostazioni di specificare la modalità di distribuzione del software** pagina, assicurarsi che sia scopo hello **necessari**.

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. In hello **specificare la pianificazione per questa distribuzione hello** , specificare una pianificazione. Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).
9. In hello **punti di distribuzione** pagina, configurare le proprietà di hello in base alle esigenze toohello del centro dati. Quindi completare la procedura guidata hello.

> [!TIP]
> riavvio di tooavoid non necessari, pianificare l'installazione del pacchetto hello durante la finestra di manutenzione mensile o una finestra degli aggiornamenti software.

È possibile monitorare l'avanzamento della distribuzione hello utilizzando la console di Configuration Manager hello. Andare troppo**monitoraggio** > **distribuzioni** > *[nome pacchetto]*.

  ![Distribuzioni di toomonitor opzione schermata di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Distribuire il servizio Mobility nei computer che eseguono Linux
> [!NOTE]
> In questo articolo presuppone che l'indirizzo IP hello hello del server di configurazione è 192.168.3.121, e tale condivisione di file di rete sicura hello \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Passaggio 1: preparare la distribuzione
1. Creare una cartella nella condivisione di rete hello e denominarla come **MobSvcLinux**.
2. Accedi a server di configurazione tooyour e aprire un prompt dei comandi amministrativo.
3. Eseguire hello seguenti comandi toogenerate un file della passphrase:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Hello copia **MobSvc.passphrase** file hello **MobSvcLinux** cartella nella condivisione di rete.
5. Sfoglia toohello repository di programma di installazione nel server di configurazione hello eseguendo il comando hello:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Esempio hello copia file toohello **MobSvcLinux** cartella nella condivisione di rete:
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. Copiare hello seguente di codice e salvarlo come **install_linux.sh** in hello **MobSvcLinux** cartella.
   > [!NOTE]
   > Sostituire i segnaposto hello [CSIP] in questo script con i valori effettivi hello dell'indirizzo IP di hello del server di configurazione.

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

### <a name="step-2-create-a-package"></a>Passaggio 2: creare un pacchetto

1. Accedi tooyour console di Configuration Manager.
2. Sfoglia troppo**libreria Software** > **Application Management** > **pacchetti**.
3. Fare clic con il pulsante destro del mouse su **Pacchetti** e selezionare **Crea pacchetto**.
4. Fornire valori per hello nome, descrizione, produttore, lingua e versione.
5. Seleziona hello **questo pacchetto contiene file di origine** casella di controllo.
6. Fare clic su **Sfoglia**e condivisione di rete selezionare hello in cui è archiviato installer hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. In hello **scegliere hello programma il tipo che si desidera toocreate** selezionare **programma Standard**, fare clic su **Avanti**.

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. In hello **specificare le informazioni sul programma standard** pagina specificare hello seguendo gli input e fare clic su **Avanti**. (hello altri input possono utilizzare i valori predefiniti.)

    | **Nome parametro** | **Valore** |
  |--|--|
  | Nome | Installare il servizio Mobility di Microsoft Azure (Linux) |
  | Riga di comando | ./install_linux.sh |
  | Il programma può essere eseguito | anche se non ci sono utenti connessi |

  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. Nella pagina successiva di hello, selezionare **questo programma può essere eseguito su qualsiasi piattaforma**.
  ![Schermata di Creazione guidata pacchetto e programma](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. procedura guidata hello toocomplete, fare clic su **Avanti** due volte.

> [!NOTE]
> script di Hello supporta entrambe le nuove installazioni di agenti di servizio di mobilità e aggiorna tooagents che sono già installati.

### <a name="step-3-deploy-hello-package"></a>Passaggio 3: Distribuire il pacchetto di hello
1. Nella console di Configuration Manager hello, il pacchetto e scegliere **Distribuisci contenuto**.
  ![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Seleziona hello  **[punti di distribuzione](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  su toowhich devono essere copiati i pacchetti hello.
3. Creazione guidata hello completo. pacchetto Hello quindi avvia la replica toohello specifica i punti di distribuzione.
4. Dopo la distribuzione del pacchetto di hello, pacchetto hello e scegliere **Distribuisci**.
  ![Schermata della console di Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Selezionare hello raccolta dispositivi Linux Server è stato creato nella sezione Prerequisiti hello come raccolta di destinazione hello per la distribuzione.

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. In hello **specifica destinazione di contenuto hello** pagina, selezionare il **punti di distribuzione**.
7. In hello **toocontrol le impostazioni di specificare la modalità di distribuzione del software** pagina, assicurarsi che sia scopo hello **necessari**.

  ![Schermata della Distribuzione guidata del software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. In hello **specificare la pianificazione per questa distribuzione hello** , specificare una pianificazione. Per altre informazioni, vedere la sezione relativa alla [pianificazione dei pacchetti](https://technet.microsoft.com/library/gg682178.aspx).
9. In hello **punti di distribuzione** pagina, configurare le proprietà di hello in base alle esigenze toohello del centro dati. Quindi completare la procedura guidata hello.

Servizio di mobilità viene installato e su hello raccolta di dispositivi Server Linux, in base toohello pianificazione configurata.

## <a name="other-methods-tooinstall-mobility-service"></a>Altri tooinstall metodi del servizio di mobilità
Di seguito sono riportate altre opzioni per l'installazione del servizio Mobility:
* [Installazione manuale tramite interfaccia utente grafica](http://aka.ms/mobsvcmanualinstall)
* [Installazione manuale tramite la riga di comando](http://aka.ms/mobsvcmanualinstallcli)
* [Installazione push tramite il server di configurazione](http://aka.ms/pushinstall)
* [Installazione automatica tramite Automazione di Azure e la configurazione dello stato desiderato](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Disinstallare il servizio Mobility
È possibile creare pacchetti di Configuration Manager toouninstall servizio di mobilità. Utilizzare hello lo script seguente viene toodo pertanto:

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

## <a name="next-steps"></a>Passaggi successivi
Si è pronti a questo punto troppo[abilitare la protezione](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) per le macchine virtuali.
