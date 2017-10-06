---
title: " Gestire un server di configurazione in Azure Site Recovery | Microsoft Docs"
description: Questo articolo viene descritto come tooset e gestire un Server di configurazione.
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Gestire un server di configurazione

Configurazione Server funziona come un coordinatore tra servizi di ripristino del sito di hello e l'infrastruttura locale. Questo articolo descrive come è possibile impostare, configurare e gestire hello del Server di configurazione.

## <a name="prerequisites"></a>Prerequisiti
di seguito Hello sono hello minimo hardware, software e tooset necessarie di configurazione di rete di un Server di configurazione.

> [!NOTE]
> [Pianificazione della capacità](site-recovery-capacity-planner.md) è tooensure un passaggio importante distribuire hello Server di configurazione con una configurazione adatta i requisiti di carico. Per altre informazioni, vedere la sezione [Requisiti di dimensione per un server di configurazione](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Download del software Server di configurazione hello
1. Accedere toohello tooyour Azure portal e passare credenziali di servizi di ripristino.
2. Sfoglia troppo**infrastruttura di Site Recovery** > **server di configurazione** (in VMware per la & macchine fisiche).

  ![Pagina di aggiunta server](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Fare clic su hello **+ server** pulsante.
4. In hello **Aggiungi Server** pagina, fare clic su chiave di registrazione hello toodownload pulsante Download hello. Questa chiave è necessaria durante hello del Server di configurazione installazione tooregister con il servizio di Azure Site Recovery.
5. Fare clic su hello **hello Download installazione unificata di Microsoft Azure Site Recovery** collegamento toodownload hello ultima versione di hello del Server di configurazione.

  ![Pagina di download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  La versione più recente di hello del Server di configurazione può essere scaricata direttamente da [pagina di download di Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Installazione e registrazione di un server di configurazione dall'interfaccia utente grafica
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Installazione e registrazione di un server di configurazione dalla riga di comando

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Esempio di utilizzo
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Argomenti della riga di comando del programma di installazione del server di configurazione.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Creare un file di credenziali di MySql
Il parametro MySQLCredsFilePath prende un file come input. Creare file hello utilizzando hello seguente formattare e passarlo come parametro di input MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Creare un file di configurazione delle impostazioni del proxy
Il parametro ProxySettingsFilePath prende un file come input. Creare file hello utilizzando hello seguente formattare e passarlo come parametro di input ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modifica delle impostazioni del proxy per il server di configurazione
1. Account di accesso tooyour Server di configurazione.
2. Avviare cspsconfigtool.exe hello utilizzando il collegamento di hello nel.
3. Fare clic su hello **registrazione insieme credenziali** scheda.
4. Scaricare un nuovo file di registrazione dell'insieme di credenziali dal portale hello e fornirlo come input toohello strumento.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Fornire dettagli hello del nuovo Server Proxy e fare clic su hello **registrare** pulsante.
6. Aprire una finestra di prompt dei comandi di PowerShell per amministratore.
7. Eseguire hello comando seguente
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Se dispone di server di scalabilità orizzontale processo collegato toothis Server di configurazione, è necessario troppo[correggere le impostazioni del proxy hello in tutti i server di scalabilità orizzontale processo hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) nella distribuzione.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Registrare un Server di configurazione con hello stesso archivio di servizi di ripristino
  1. Account di accesso tooyour Server di configurazione.
  2. Avvia cspsconfigtool.exe hello utilizzando il collegamento di hello sul desktop.
  3. Fare clic su hello **registrazione insieme credenziali** scheda.
  4. Scaricare un nuovo file di registrazione dal portale hello e fornirlo come input toohello strumento.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Fornire i dettagli del Server Proxy hello e fare clic su hello **registrare** pulsante.  
  6. Aprire una finestra di prompt dei comandi di PowerShell per amministratore.
  7. Eseguire hello comando seguente

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Se dispone di server di scalabilità orizzontale processo collegato toothis Server di configurazione, è necessario troppo[registrare nuovamente tutti i server di scalabilità orizzontale processo hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) nella distribuzione.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Registrazione di un server di configurazione con un insieme di credenziali di Servizi di ripristino diverso.
1. Account di accesso tooyour Server di configurazione.
2. da un prompt dei comandi di amministratore, eseguire il comando di hello

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Avviare cspsconfigtool.exe hello utilizzando il collegamento di hello nel.
4. Fare clic su hello **registrazione insieme credenziali** scheda.
5. Scaricare un nuovo file di registrazione dal portale hello e fornirlo come input toohello strumento.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Fornire i dettagli del Server Proxy hello e fare clic su hello **registrare** pulsante.  
7. Aprire una finestra di prompt dei comandi di PowerShell per amministratore.
8. Eseguire hello comando seguente
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Rimozione delle autorizzazioni per un server di configurazione
Verificare i seguenti hello prima di iniziare rimuovere il Server di configurazione.
1. Disabilitare la protezione di tutte le macchine virtuali in questo server di configurazione.
2. Annullare l'associazione di tutti i criteri di replica dal Server di configurazione hello.
3. Eliminare tutti gli host del server/vSphere vCenter toohello associato Server di configurazione.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Eliminare hello del Server di configurazione dal portale di Azure
1. Nel portale di Azure, passare troppo**infrastruttura di Site Recovery** > **server di configurazione** dal menu di hello insieme di credenziali.
2. Fare clic su Server di configurazione che si desidera toodecommission hello.
3. Nella pagina dettagli del Server di configurazione hello, fare clic sul pulsante Elimina hello.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Fare clic su **Sì** tooconfirm l'eliminazione di hello del server di hello.

  >[!WARNING]
  Se si dispone di macchine virtuali, criteri di replica o vCenter server/vSphere host associato a questo Server di configurazione, è possibile eliminare il server di hello. Eliminare queste entità prima di provare l'insieme di credenziali toodelete hello.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Disinstallare il software di Server di configurazione hello e le relative dipendenze
  > [!TIP]
  Se si prevede di nuovo tooreuse hello configurazione Server con Azure Site Recovery, quindi è possibile ignorare toostep 4 direttamente

1. Accedere come amministratore toohello Server di configurazione.
2. Scegliere Pannello di controllo > Programma > Disinstallare programmi
3. Disinstallare programmi hello in hello seguente sequenza:
  * Agente di Servizi di ripristino di Microsoft Azure
  * Servizio Mobility di Microsoft Azure Site Recovery/server di destinazione master
  * Provider di Microsoft Azure Site Recovery
  * Server di elaborazione/Server di configurazione di Microsoft Azure Site Recovery
  * Dipendenze del server di configurazione di Microsoft Azure Site Recovery
  * MySQL Server 5.5
4. Eseguire hello comando dal seguente e prompt dei comandi come amministratore.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Rinnovare i certificati SSL (Server Secure Socket Layer) di configurazione
Hello del Server di configurazione è un server Web incorporato, che coordina le attività di hello di hello servizio di mobilità, i server di elaborazione e i server di destinazione Master connessi toohello Server di configurazione. server Web del Server di configurazione Hello utilizza un tooauthenticate certificato SSL dei client. Questo certificato ha una scadenza di tre anni e può essere rinnovato in qualsiasi momento usando hello seguente metodo:

> [!WARNING]
La scadenza del certificato può avvenire solo nella versione 9.4.XXXX.X o versione successiva. Aggiornare tutti i componenti di Azure Site Recovery hello (Server di configurazione, Server di elaborazione, Server di destinazione Master, servizio di mobilità) prima di iniziare del flusso di lavoro di hello rinnovare i certificati.

1. In hello portale di Azure, passare tooyour insieme di credenziali > infrastruttura di Site Recovery > Server di configurazione.
2. Fare clic su hello del Server di configurazione per il quale è necessario toorenew hello certificato SSL per.
3. In hello integrità del Server di configurazione, è possibile visualizzare la data di scadenza hello per hello certificato SSL.
4. Rinnova certificato di hello facendo hello **rinnovare i certificati** azione, come illustrato nella seguente immagine hello:

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Avviso di scadenza del certificato SSL

> [!NOTE]
Hello validità del certificato SSL per tutte le installazioni che si sono verificati prima di maggio 2016 è stata impostata tooone anno. si è avviato visualizzare notifiche di scadenza certificato viene visualizzato nel portale di Azure hello.

1. Se il certificato SSL del Server di configurazione hello verrà tooexpire in hello due mesi successivi, il servizio di hello avvia la notifica agli utenti tramite il portale di Azure hello & posta elettronica (è necessario toobe sottoscritto tooAzure Site Recovery notifiche). Iniziare a vedere un banner di notifica nella pagina delle risorse dell'insieme di credenziali di hello.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Fare clic su hello banner tooget ulteriori informazioni sulla scadenza del certificato hello.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Se al posto del pulsante **Renew Now** (Rinnova ora) viene visualizzato un pulsante **Upgrade Now** (Aggiorna ora). Questo significa che sono disponibili alcuni componenti nell'ambiente che non sono ancora stato aggiornato too9.4.xxxx.x o versioni successive.

## <a name="sizing-requirements-for-a-configuration-server"></a>Requisiti di dimensione per un server di configurazione

| **CPU** | **Memoria** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 socket * 4 core a 2,5 GHz) |16 GB |300 GB |500 GB o inferiore |Replicare meno di 100 computer. |
| 12 vCPU (2 socket * 6 core a 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Replicare tra 100 e 150 computer. |
| 16 vCPU (2 socket * 8 core a 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Replicare tra 150 e 200 computer. |

  >[!TIP]
  Se la varianza dei dati giornaliera supera i 2 TB o tooreplicate si prevede più di 200 macchine virtuali, è consigliabile toodeploy processo aggiuntivo server tooload saldo hello il traffico di replica. Altre informazioni su come server di toodeploy il processo di scalabilità orizzontale.


## <a name="common-issues"></a>Problemi comuni
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
