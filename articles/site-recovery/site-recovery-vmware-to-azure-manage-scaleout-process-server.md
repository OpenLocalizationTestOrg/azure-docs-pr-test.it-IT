---
title: " Gestire un server di elaborazione con scalabilità orizzontale in Azure Site Recovery | Microsoft Docs"
description: "Questo articolo viene descritto come tooset configurare e gestire un Server di elaborazione di scalabilità orizzontale in Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Gestire un server di elaborazione con scalabilità orizzontale

Server di scalabilità orizzontale processo agisce come un coordinatore per il trasferimento di dati tra servizi di ripristino del sito di hello e l'infrastruttura locale. Questo articolo descrive come impostare, configurare e gestire i server di elaborazione con scalabilità orizzontale.

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello sono hello consigliato tooset necessarie di configurazione di rete di un Server di scalabilità orizzontale processo hardware e software.

> [!NOTE]
> [Pianificazione della capacità](site-recovery-capacity-planner.md) è tooensure un passaggio importante distribuire hello processo Server di scalabilità orizzontale con una configurazione adatta i requisiti di carico. Altre informazioni sulle [caratteristiche di scalabilità per un server di elaborazione con scalabilità orizzontale](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Download del software Server di scalabilità orizzontale processo hello
1. Accedere toohello tooyour Azure portal e passare credenziali di servizi di ripristino.
2. Sfoglia troppo**infrastruttura di Site Recovery** > **server di configurazione** (in VMware per la & macchine fisiche).
3. Selezionare il toodrill di server di configurazione verso il basso nella pagina dei dettagli del server di configurazione hello.
4. Fare clic su hello **+ Server di elaborazione** pulsante.
5. In hello **server di elaborazione aggiungere** selezionare **distribuzione una scalabilità orizzontale di un processo Server on-premise** opzione hello **specificare dove toodeploy il server di elaborazione** elenco a discesa.

  ![Pagina di aggiunta server](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Fare clic su hello **hello Download installazione unificata di Microsoft Azure Site Recovery** collegamento toodownload hello più recente di installazione di Server di elaborazione hello scalabilità orizzontale.

  > [!WARNING]
  Hello la versione del Server di scalabilità orizzontale processo deve essere uguale tooor inferiore alla versione di hello del Server di configurazione in esecuzione nell'ambiente. Compatibilità di versione tooensure un modo semplice è toouse hello stessi bit di installazione che è utilizzato recentemente tooinstall/aggiornare il Server di configurazione.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dall'interfaccia utente grafica
Se hai tooscale orizzontalmente la distribuzione oltre 200 macchine di origine, oppure un totale giornaliero di varianza del tasso di più di 2 TB, è necessario volume di traffico hello toohandle server processo aggiuntivo.

Controllare hello [consigli per i server di elaborazione di dimensioni](#size-recommendations-for-the-process-server), quindi seguire queste istruzioni tooset dei server di elaborazione hello. Dopo aver configurato il server di hello, eseguire la migrazione toouse macchine di origine è.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Installazione e registrazione di un server di elaborazione con scalabilità orizzontale dalla riga di comando

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Esempio di utilizzo
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Argomenti della riga di comando del programma di installazione del server di elaborazione con scalabilità orizzontale.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Creare un file di configurazione delle impostazioni del proxy
Il parametro ProxySettingsFilePath prende un file come input. Creare file utilizzando hello seguente formattare e passarlo come parametro di input ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modifica delle impostazioni proxy per il server di elaborazione con scalabilità orizzontale
1. Accedere al server di elaborazione con scalabilità orizzontale.
2. Aprire una finestra di prompt dei comandi di PowerShell per amministratore.
3. Eseguire hello comando seguente
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Quindi cerca nella directory toohello **%PROGRAMDATA%\ASR\Agent** e hello esecuzione comando seguente
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Nuova registrazione di un server di elaborazione con scalabilità orizzontale
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Quindi aprire un prompt dei comandi come amministratore.
* Sfogliare la directory toohello **%PROGRAMDATA%\ASR\Agent** ed eseguire il comando hello

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Aggiornamento di un server di elaborazione con scalabilità orizzontale
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Rimozione di un server di elaborazione con scalabilità orizzontale
1. Assicurarsi che:
  - Mostra lo stato della connessione del Server di configurazione come **connesso** in hello portale di Azure
  - Server di elaborazione è comunque possibile toocommunicate con il server di configurazione di hello.
2. Accedere come amministratore server di elaborazione toohello
3. Scegliere Pannello di controllo > Programma > Disinstallare programmi
4. Disinstallare i programmi di hello in sequenza hello fornito seguente:
  * Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery
  * Dipendenze del server di configurazione di Microsoft Azure Site Recovery
  * Agente di Servizi di ripristino di Microsoft Azure

Può richiedere fino too15 minuti per tooreflect l'eliminazione di Server di elaborazione hello in hello portale di Azure.

  > [!NOTE]
  Se il server di elaborazione di hello è Impossibile toocommunicate con hello del Server di configurazione (stato di connessione nel portale è disconnesso), è necessario toofollow hello seguendo i passaggi toopurge da hello del Server di configurazione.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Annullamento della registrazione di un server di elaborazione con scalabilità orizzontale disconnesso da un server di configurazione

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Requisiti per il ridimensionamento di un server di elaborazione con scalabilità orizzontale

| **Server di elaborazione aggiuntivo** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti** |
| --- | --- | --- | --- |
|4 vCPU (2 socket * 2 core a 2,5 GHz), 8 GB di memoria |300 GB |250 GB o inferiore |Replicare un massimo di 85 computer. |
|8 vCPU (2 socket * 4 core a 2,5 GHz), 12 GB di memoria |600 GB |250 GB too1 TB |Replicare tra 85 e 150 computer. |
|12 vCPU (2 socket * 6 core a 2,5 GHz), 24 GB di memoria |1 TB |1 TB too2 TB |Replicare tra 150 e 225 computer. |
