---
title: "Servizio di mobilità (VMware o fisici tooAzure) aaaInstall | Documenti Microsoft"
description: "Informazioni su come tooinstall hello servizio di mobilità agente tooprotect computer locale."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Installare il servizio di mobilità (VMware o fisici tooAzure)
Servizio di mobilità di Azure Site Recovery acquisisce scritture di dati in un computer e quindi li inoltra toohello server di elaborazione. Distribuire il servizio di mobilità tooevery (VMware VM o server fisico) che si desidera tooreplicate tooAzure. È possibile distribuire server toohello servizio di mobilità che si desidera tooprotect utilizzando hello dei seguenti metodi:


* [Installare il Servizio Mobility con strumenti di distribuzione software come System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Installare il Servizio Mobility tramite Automazione di Azure e la configurazione dello stato desiderato (Automation DSC)](site-recovery-automate-mobility-service-install.md)
* [Installare manualmente il servizio Mobility tramite l'interfaccia utente grafica di hello (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Installare manualmente il Servizio Mobility tramite un prompt di comando](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Installare il Servizio Mobility tramite installazione push da Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> A partire dalla versione 9.7.0.0, nelle macchine virtuali di Windows (VM), programma di installazione del servizio di mobilità hello viene installato anche hello più recente disponibile [agente VM di Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Quando un computer viene eseguito il failover tooAzure, computer hello soddisfa hello agente prerequisito di installazione per l'utilizzo di qualsiasi estensione della macchina virtuale.

## <a name="prerequisites"></a>Prerequisiti
Completare questa procedura per i prerequisiti prima di iniziare a installare manualmente il Servizio Mobility nel server:
1. Accedi a server di configurazione tooyour e quindi aprire una finestra del prompt dei comandi come amministratore.
2. Cambiare cartella bin di hello directory toohello e quindi creare un file passphrase:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. File dell'archivio hello passphrase in un luogo sicuro. Utilizzare file hello durante l'installazione del servizio di mobilità hello.
4. Installazione di servizi di mobilità per tutti i sistemi operativi supportati sono nella cartella %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Programma di installazione del servizio Mobility per il mapping del sistema operativo

| Nome del modello del file del programma di installazione| Sistema operativo |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 bit) </br> Windows Server 2012 (64 bit) </br> Windows Server 2012 R2 (64 bit) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (solo a 64 bit) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (solo a 64 bit) </br> CentOS 7.0, 7.1, 7.2 (solo a 64 bit)</br> CentOs 7.3 (solo per la migrazione) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (solo a 64 bit)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (solo a 64 bit)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (solo a 64 bit)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (solo a 64 bit)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Installare manualmente il servizio Mobility tramite interfaccia utente grafica hello

>[!IMPORTANT]
> Se si utilizza un **Server di configurazione** tooreplicate **macchine virtuali IaaS di Azure** da una sottoscrizione di Azure/area geografica, tooanother quindi **usare l'installazione da riga di comando basata su hello**  (metodo)

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Installare manualmente il Servizio Mobility tramite un prompt di comando

### <a name="command-line-installation-on-a-windows-computer"></a>Installazione dalla riga di comando in un computer Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Installazione dalla riga di comando in un computer Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Installare il Servizio Mobility tramite installazione push da Azure Site Recovery
toodo un'installazione push del servizio di mobilità tramite il ripristino del sito, tutti i computer di destinazione devono soddisfare i seguenti prerequisiti hello.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Dopo aver installato il servizio di mobilità, nel portale di Azure hello selezionare hello **replicare** toostart pulsante proteggere queste macchine virtuali.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Disinstallare il servizio Mobility in un computer Windows Server
Utilizzare uno dei seguenti metodi toouninstall servizio di mobilità in un computer Server di Windows hello.

### <a name="uninstall-by-using-hello-gui"></a>Disinstallare utilizzando l'interfaccia utente grafica hello
1. Nel Pannello di controllo, selezionare **Programmi**.
2. Selezionare **Microsoft Azure Site Recovery Mobility Service/Master Target server** (Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master) e fare clic su **Disinstalla**.

### <a name="uninstall-at-a-command-prompt"></a>Disinstallare dal prompt dei comandi
1. Aprire una finestra del Prompt dei comandi come amministratore.
2. toouninstall servizio di mobilità, eseguire hello comando seguente:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Disinstallare il servizio Mobility in computer Linux
1. Sul server Linux, accedere come utente **Root**.
2. In un terminal, andare troppo/utente/locale/ripristino automatico di sistema.
3. toouninstall servizio di mobilità, eseguire hello comando seguente:

```
uninstall.sh -Y
```
