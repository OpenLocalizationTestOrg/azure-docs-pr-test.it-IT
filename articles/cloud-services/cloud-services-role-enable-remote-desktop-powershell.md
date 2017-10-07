---
title: aaaEnable connessione Desktop remoto per un ruolo in servizi Cloud di Azure tramite PowerShell
description: Tooconfigure cloud di azure tramite le connessioni desktop remoto di PowerShell tooallow applicazione del servizio
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Abilitare una connessione Desktop remoto per un ruolo in Servizi cloud di Azure con PowerShell
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portale di Azure classico](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Desktop remoto consente desktop hello tooaccess di un ruolo in esecuzione in Azure. È possibile utilizzare un tootroubleshoot connessione Desktop remoto e diagnosticare i problemi dell'applicazione mentre è in esecuzione.

Questo articolo viene descritto come tooenable desktop remoto i ruoli dei servizi Cloud tramite PowerShell. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per prerequisiti hello necessari per questo articolo. PowerShell Usa hello estensione Desktop remoto, pertanto è possibile abilitare Desktop remoto dopo la distribuzione di un'applicazione hello.

## <a name="configure-remote-desktop-from-powershell"></a>Configurare Remote Desktop da PowerShell
Hello [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet consente tooenable Desktop remoto su tutti i ruoli di distribuzione del servizio cloud o di ruoli specificati. Hello cmdlet consente di specificare hello nome utente e Password per utente desktop remoto hello tramite hello *credenziali* parametro che accetta un oggetto PSCredential.

Se si usa PowerShell in modo interattivo, è possibile impostare facilmente oggetto PSCredential hello dal chiamante hello [Ottieni credenziali](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

```
$remoteusercredentials = Get-Credential
```

Questo comando Visualizza una finestra di dialogo che consente di tooenter hello nome utente e password per l'utente remoto hello in modo sicuro.

Poiché consente di PowerShell in scenari di automazione, è possibile anche impostare hello **PSCredential** oggetto in modo che non richiede l'intervento dell'utente. In primo luogo, è necessario tooset una password sicura. Iniziare con specificando una password in testo normale convertire la stringa sicura tooa utilizzando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). È quindi necessario tooconvert questa stringa protetta in una stringa standard crittografata usando [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx). Ora è possibile salvare questo file tooa stringa standard crittografata utilizzando [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).

È anche possibile creare un file di password di protezione in modo che non è tootype password hello ogni volta. Inoltre, un file della password di protezione è preferibile a un file di testo normale. Utilizzare hello PowerShell toocreate un file di password di protezione seguenti:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> Quando si imposta la password di hello, assicurarsi che siano soddisfatti hello [i requisiti di complessità](https://technet.microsoft.com/library/cc786468.aspx).
>
>

oggetto credenziale di hello toocreate dal file di password sicura hello, è necessario leggere il contenuto del file hello e convertirli tooa indietro secure stringa utilizzando [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Hello [Set AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet accetta inoltre un *scadenza* parametro che specifica un **DateTime** utente hello scadenza account. Ad esempio, è possibile impostare hello account tooexpire pochi giorni dalla data e ora correnti di hello.

In questo esempio di PowerShell viene illustrato come tooset hello estensione Desktop remoto in un servizio cloud:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
È anche possibile specificare lo slot di distribuzione hello e i ruoli che si desidera includere tooenable desktop remoto. Se questi parametri vengono omessi, hello cmdlet Abilita desktop remoto su tutti i ruoli di hello **produzione** slot di distribuzione.

Hello estensione Desktop remoto è associata a una distribuzione. Se si crea una nuova distribuzione per il servizio di hello, è necessario tooenable desktop remoto nella distribuzione. Se si desidera comunque toohave desktop remoto abilitato, è necessario considerare l'integrazione di script di PowerShell hello nel flusso di lavoro di distribuzione.

## <a name="remote-desktop-into-a-role-instance"></a>Desktop remoto in un'istanza del ruolo
Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet è desktop tooremote utilizzato in un'istanza del ruolo specifico del servizio cloud. È possibile utilizzare hello *LocalPath* hello toodownload di parametro RDP file localmente. Oppure è possibile utilizzare hello *avviare* tooaccess di finestra di dialogo connessione Desktop remoto di parametro toodirectly avvio hello hello istanza del ruolo del servizio cloud.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Verificare se l'estensione di Desktop remoto è attivata in un servizio
Hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet Visualizza che desktop remoto è abilitato o disabilitato su una distribuzione del servizio. cmdlet di Hello restituisce hello username per utente desktop remoto hello e i ruoli di hello abilitata per l'estensione di desktop remoto hello. Per impostazione predefinita, in questo caso nello slot di distribuzione hello ed è possibile scegliere hello toouse invece slot di staging.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Rimuovere l'estensione di Desktop remoto da un servizio
Estensione di desktop remoto hello in una distribuzione è già stato abilitato, se necessario tooupdate hello impostazioni desktop remoto, è necessario rimuovere prima estensione hello. E abilitarlo di nuovo con nuove impostazioni hello. Ad esempio, se si desidera tooset una nuova password per l'account utente remoto hello o hello account scaduto. Questa operazione è necessaria per le distribuzioni esistenti che presentano hello estensione desktop remoto abilitato. Per nuove distribuzioni, è possibile applicare estensione hello semplicemente direttamente.

tooremove hello remote desktop estensione dalla distribuzione hello, è possibile utilizzare hello [Remove AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet. È anche possibile specificare lo slot di distribuzione hello e il ruolo da cui si desidera l'estensione di desktop remoto di tooremove hello.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> configurazione dell'estensione hello remove toocompletely, è necessario chiamare hello *rimuovere* cmdlet con hello **UninstallConfiguration** parametro.
>
> Hello **UninstallConfiguration** parametro consente di disinstallare qualsiasi configurazione dell'estensione che è applicato toohello servizio. Ogni configurazione dell'estensione è associata a una configurazione del servizio hello. Chiamare il metodo hello *rimuovere* cmdlet senza **UninstallConfiguration** disassocia hello <mark>distribuzione</mark> dalla configurazione dell'estensione hello, in modo efficace rimuovendo estensione Hello. Configurazione dell'estensione hello rimane tuttavia associato hello servizio.
>
>

## <a name="additional-resources"></a>Risorse aggiuntive

[Come servizi Cloud tooConfigure](cloud-services-how-to-configure.md)
[domande frequenti - servizi Cloud Desktop remoto](cloud-services-faq.md)
