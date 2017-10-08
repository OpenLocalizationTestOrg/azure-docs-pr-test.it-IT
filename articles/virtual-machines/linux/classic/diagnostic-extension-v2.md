---
title: una VM Linux con un'estensione VM aaaMonitoring | Documenti Microsoft
description: Informazioni su come toouse hello estensione diagnostica per Linux toomonitor hello dati sulle prestazioni e diagnostica di una VM Linux di Azure.
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Utilizzare hello estensione diagnostica per Linux toomonitor hello dati sulle prestazioni e diagnostica di una VM Linux

Questo documento descrive versione 2.3 di hello estensione diagnostica per Linux.

> [!IMPORTANT]
> Questa versione è deprecata e la sua pubblicazione potrebbe essere annullata a partire dal 30 giugno 2018. È stata sostituita dalla versione 3.0. Per ulteriori informazioni, vedere hello [documentazione per la versione 3.0 di hello estensione diagnostica per Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Introduzione

(**Nota**: hello estensione diagnostica per Linux è open source in [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) in cui le informazioni più recenti hello sull'estensione hello prima pubblicazione. Potrebbe essere necessario hello toocheck [pagina GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) prima.)

Estensione diagnostica per Linux Hello consente un hello monitoraggio utente macchine virtuali Linux in esecuzione in Microsoft Azure. Dispone di hello seguenti funzionalità:

* Raccoglie e carica informazioni sulle prestazioni di sistema hello dalla tabella di archiviazione dell'utente di hello VM Linux toohello, incluse informazioni di diagnostica e syslog.
* Consente la metrica utenti toocustomize hello dati che verrà raccolti e caricata.
* Consente agli utenti tooupload log specificato file tooa designato archiviazione tabella.

Nella versione corrente di hello 2.3, i dati di hello includono:

* Tutti i log Rsyslog Linux, inclusi i log di sistema, sicurezza e applicazioni.
* Tutti i dati di sistema specificata in [sito soluzioni piattaforma incrociata di System Center hello](https://scx.codeplex.com/wikipage?title=xplatproviders).
* I file di log specificati dall'utente.

Questa estensione funziona con hello classic e modelli di distribuzione di gestione risorse.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Versione corrente dell'estensione hello e rimozione di versioni precedenti

Hello la versione più recente dell'estensione hello è **2.3**, e **le versioni precedenti (2.0, 2.1 e 2.2) verranno deprecate e non pubblicate dalla fine dell'anno (2017)**. Se è stato installato con l'aggiornamento automatico di versione secondaria disabilitata hello estensione diagnostica di Linux, è consigliabile disinstallare l'estensione hello e reinstallarlo con l'aggiornamento di versione secondaria automatico abilitato. In classico (ASM) di macchine virtuali, è possibile ottenere specificando '2.*' come versione di hello, se si sta installando l'estensione hello tramite Azure XPLAT CLI o Powershell. Nelle macchine virtuali ARM, è possibile ottenere questo includendo ' "autoUpgradeMinorVersion": true' nel modello di distribuzione VM hello. Qualsiasi nuova installazione dell'estensione di hello, inoltre, deve avere una versione secondaria di hello automatica aggiornare l'opzione è attivata.

## <a name="enable-hello-extension"></a>Abilitare l'estensione hello

È possibile abilitare questa estensione utilizzando hello [portale di Azure](https://portal.azure.com/#), Azure PowerShell o script CLI di Azure.

tooview e configurare il sistema hello e seguono i dati sulle prestazioni direttamente dal portale di Azure hello, [questi passaggi nel blog di Azure hello](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Questo articolo è incentrato sulla tooenable e configurare l'estensione hello utilizzando i comandi CLI di Azure. In questo modo tooread e visualizzare i dati hello direttamente dalla tabella di archiviazione hello.

Si noti che i metodi di configurazione hello descritte di seguito non funzioneranno per hello portale di Azure. tooview e configurare i dati di sistema e delle prestazioni hello direttamente dal portale di Azure hello, hello estensione deve essere abilitata tramite il portale di hello.

## <a name="prerequisites"></a>Prerequisiti

* **Agente Linux di Azure 2.0.6 o versione successiva**.

  Si noti che la maggior parte delle immagini della raccolta Linux di macchine virtuali di Azure include la versione 2.0.6 o successive. È possibile eseguire **WAAgent-versione** tooconfirm quale versione è installata nella macchina virtuale hello. Se hello macchina virtuale è in esecuzione una versione precedente a 2.0.6, è possibile seguire [queste istruzioni in GitHub](https://github.com/Azure/WALinuxAgent "istruzioni") tooupdate è.
* **Interfaccia della riga di comando di Azure**. Seguire [queste linee guida per l'installazione di CLI](../../../cli-install-nodejs.md) tooset ambiente Azure CLI hello nel computer. Dopo aver installato CLI di Azure, è possibile utilizzare hello **azure** comando l'interfaccia della riga di comando (Bash Terminal comandi o il prompt dei comandi) tooaccess hello CLI di Azure. ad esempio:

  * Eseguire **azure vm extension set --help** per informazioni della Guida dettagliate.
  * Eseguire **accesso di azure** toosign in tooAzure.
  * Eseguire **elenco di macchine virtuali di azure** toolist tutti hello macchine virtuali che presentano in Azure.
* Oggetto dati di hello toostore account di archiviazione. È necessario un nome di account di archiviazione creato in precedenza e un archivio di tooyour accesso tooupload chiave hello dati.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Utilizzare hello tooenable di comando CLI di Azure hello estensione diagnostica per Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Scenario 1. Abilitare l'estensione hello hello set di dati predefinito

Nella versione 2.3 o versioni successive, hello predefinito dati verranno raccolti includono:

* Tutte le informazioni Rsyslog (inclusi i log di sistema, sicurezza e applicazioni).  
* Un set principale di dati di sistema di base. Si noti che i set di dati completo hello sono descritta in hello [sito soluzioni piattaforma incrociata di System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Se si desidera tooenable dati aggiuntivi, continuare con i passaggi di hello in scenari di 2 e 3.

Passaggio 1. Creare un file denominato Privateconfig con hello seguente contenuto:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Passaggio 2. Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Scenario 2. Personalizzare le metriche di monitoraggio delle prestazioni di hello

In questa sezione viene descritto come toocustomize hello prestazioni e la tabella di dati di diagnostica.

Passaggio 1. Creare un file denominato Privateconfig con contenuto hello descritto nello Scenario 1. Creare anche un file denominato PublicConfig.json. Specificare i dati di particolare hello desiderati toocollect.

Per tutte supportate dei provider e le variabili, fare riferimento a hello [sito soluzioni piattaforma incrociata di System Center](https://scx.codeplex.com/wikipage?title=xplatproviders). È possibile avere più query e archiviarli in più tabelle aggiungendo più script toohello di query.

Per impostazione predefinita, hello Rsyslog dati verrà sempre raccolti.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Passaggio 2. Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Scenario 3. Caricamento dei propri file di log

In questa sezione viene descritto come toocollect e il caricamento dei log specifici file tooyour account di archiviazione. È necessario toospecify entrambi hello percorso tooyour log hello nome del file e della tabella hello in cui si desidera toostore il log. È possibile creare più file di log aggiungendo più script toohello voci di file o tabella.

Passaggio 1. Creare un file denominato Privateconfig con contenuto hello descritto nello Scenario 1. Quindi creare un altro file denominato PublicConfig.json con hello seguente contenuto:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Passaggio 2. Eseguire `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Si noti che con questa impostazione su versioni estensione hello too2.3 precedenti, tutti i log scritti troppo`/var/log/mysql.err` potrebbero essere duplicati troppo`/var/log/syslog` (o `/var/log/messages` a seconda della distribuzione di Linux hello) nonché. Se si desidera tooavoid il duplicato di registrazione, è possibile escludere la registrazione di `local6` funzionalità Registra nella configurazione rsyslog. Distribuzione di Linux hello dipende, ma in un sistema, Ubuntu 14.04 toomodify file hello è `/etc/rsyslog.d/50-default.conf` è possibile sostituire la riga hello `*.*;auth,authpriv.none -/var/log/syslog` troppo`*.*;auth,authpriv,local6.none -/var/log/syslog`. Il problema viene risolto nella versione hotfix più recente di hello di 2.3 (2.3.9007), pertanto se si dispone di estensione hello versione 2.3, il problema non dovrebbe verificarsi. Se continua a non anche dopo il riavvio della macchina virtuale, contattare Microsoft e contribuire a risolvere il motivo per cui hello hotfix più recente non viene installato automaticamente.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Scenario 4. Estensione hello di raccogliere i registri di arresto

In questa sezione viene descritto come estensione di hello toostop dalla raccolta di log. Si noti che hello processo dell'agente di monitoraggio sarà ancora in esecuzione anche con la riconfigurazione. Se si desidera hello toostop completamente il processo dell'agente di monitoraggio, è possibile farlo tramite la disabilitazione di estensione hello. estensione di hello toodisable comando Hello è `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Passaggio 1. Creare un file denominato Privateconfig con contenuto hello descritto nello Scenario 1. Creare un altro file denominato PublicConfig.json con hello seguente contenuto:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Passaggio 2. Eseguire **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

## <a name="review-your-data"></a>Esaminare i dati

Hello dati sulle prestazioni e diagnostica vengono archiviati in una tabella di archiviazione di Azure. Revisione [come toouse archiviazione tabelle di Azure da Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn come tabella di dati hello tooaccess nel servizio di archiviazione hello utilizzando gli script di CLI di Azure.

Inoltre, è possibile utilizzare dati di hello tooaccess strumenti dell'interfaccia utente descritti di seguito:

1. Esplora server di Visual Studio. Passare tooyour account di archiviazione. Dopo l'esecuzione di hello VM per circa cinque minuti, si noterà tabelle predefinite hello quattro: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog". Fare doppio clic su dati hello tooview nomi della tabella hello.
1. [Esplora archivi di Azure](https://azurestorageexplorer.codeplex.com/ "Esplora archivi di Azure").

![immagine](./media/diagnostic-extension/no1.png)

Se è stata abilitata fileCfg o perfCfg (come descritto in scenari di 2 e 3), è possibile utilizzare i dati non predefinita di tooview Esplora Server Visual Studio e Azure Storage Explorer.

## <a name="known-issues"></a>Problemi noti

* Hello Rsyslog informazioni e file di log specificato dal cliente è accessibile solo tramite script.
