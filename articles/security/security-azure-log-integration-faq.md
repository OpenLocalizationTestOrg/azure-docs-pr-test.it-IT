---
title: domande frequenti sull'integrazione di Log aaaAzure | Documenti Microsoft
description: Questo articolo contiene le risponde alle domande sull'integrazione dei log di Azure.
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Domande frequenti sull'integrazione dei log di Azure
Questo articolo contiene le risponde alle domande frequenti sull'integrazione dei log di Azure. 

Integrazione di Log di Azure è un servizio di sistema operativo Windows che è possibile utilizzare i registri non elaborato toointegrate dalle risorse di Azure in locale sicurezza informazioni ed eventi (SIEM) sistemi di gestione dei. Questa integrazione fornisce un dashboard unificato per tutte le attività, locale o nel cloud hello. È possibile aggregare, correlare, analizzare e inviare avvisi per gli eventi di sicurezza associati alle applicazioni.

## <a name="is-hello-azure-log-integration-software-free"></a>È disponibile il software di integrazione di Log di Azure hello?
Sì. Non è previsto alcun addebito per hello software di integrazione di Log di Azure.

## <a name="where-is-azure-log-integration-available"></a>Dove è disponibile l'integrazione dei log di Azure?

Attualmente è disponibile nell'area commerciale di Azure e in Azure per enti pubblici e non è disponibile in Cina né in Germania.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Come è possibile visualizzare gli account di archiviazione hello da cui integrazione di Log di Azure effettua il pull di registri di macchina virtuale di Azure?
Eseguire il comando hello **elenco origine azlog**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Come individuare quale hello sottoscrizione Azure Integration Log i registri sono da

In caso di hello dei registri di controllo che vengono inseriti in hello **AzureResourcemanagerJson** directory, l'ID sottoscrizione hello è nel nome del file di log hello. Ciò vale anche per i log di hello **AzureSecurityCenterJson** cartella. ad esempio:

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Registri di controllo di Azure Active Directory includono l'ID tenant hello come parte del nome hello.

ID sottoscrizione hello come parte del nome di hello non includono i log di diagnostica che vengono letti da un hub eventi. Includono invece soprannome hello specificato come parte della creazione di hello di origine di hub eventi hello. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Come è possibile aggiornare la configurazione del proxy hello?
Se l'impostazione proxy non consente l'accesso di archiviazione di Azure direttamente, aprire hello **AZLOG. FILE EXE. CONFIGURAZIONE** file **c:\Program Files\Microsoft Azure Log integrazione**. Hello tooinclude file di aggiornamento hello **defaultProxy** sezione con l'indirizzo del proxy hello dell'organizzazione. Al termine dell'aggiornamento di hello, arrestare e avviare il servizio hello tramite comandi hello **net stop azlog** e **net start azlog**.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>È possibile vedere informazioni sulla sottoscrizione hello negli eventi di Windows?
Aggiungere nome descrittivo toohello ID sottoscrizione hello durante l'aggiunta di origine hello:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
evento Hello XML ha hello metadati, inclusi ID sottoscrizione hello seguente:

![XML dell'evento][1]

## <a name="error-messages"></a>messaggi di errore
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Quando si esegue il comando hello **azlog createazureid**, perché viene visualizzato il seguente errore hello?
Error:

  *Non è stato possibile toocreate applicazione AAD - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Non consentito', messaggio = 'dispone di privilegi sufficienti operazione hello toocomplete'.*

Hello **azlog createazureid** comando tenta di un'entità servizio in tutti i tenant di Azure AD hello per le sottoscrizioni hello hello accesso di Azure ha accesso a toocreate. Se l'account di accesso di Azure è solo un utente guest nel tenant di Azure AD, il comando di hello non riesce con "operazione di hello toocomplete di privilegi sufficienti." Chiedere tenant hello tooadd amministratore account come utente nel tenant di hello.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Quando si esegue il comando hello **azlog autorizzare**, perché viene visualizzato il seguente errore hello?
Error:

  *Avviso di creazione di assegnazione di ruolo - AuthorizationFailed: client hello janedo@microsoft.com' con l'oggetto 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' id non è stata autorizzazione tooperform azione 'Microsoft.Authorization/roleAssignments/write' sull'ambito ' / le sottoscrizioni / 70d 95299-d689-4c 97-b971-0d8ff0000000'.*

Hello **azlog autorizzare** comando Assegna hello ruolo dell'entità servizio di Azure AD toohello lettore (creata con **azlog createazureid**) sottoscrizioni toohello fornito. Se hello accesso di Azure non è un CO-amministratore o un proprietario della sottoscrizione di hello, operazione non riesce con un messaggio di errore "Autorizzazione non riuscita". Azure Role-Based Access controllo (RBAC) di CO-amministratore o il proprietario è necessario toocomplete questa azione.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Dove trovare definizione hello delle proprietà di hello nel log di controllo hello?
Vedere:

* [Operazioni di controllo con Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)
* [Elenco eventi di gestione di hello in una sottoscrizione in hello API REST di monitoraggio di Azure](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Dove sono disponibili altre informazioni sugli avvisi del Centro sicurezza di Azure?
Vedere [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Come è possibile scegliere quali informazioni raccogliere con la diagnostica delle VM?
Per ulteriori informazioni su come tooget, modificare e impostare la configurazione di diagnostica Azure hello, vedere [tooenable PowerShell utilizzare diagnostica Azure in una macchina virtuale che esegue Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hello seguente esempio ottiene una configurazione di diagnostica di Azure hello:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Hello di esempio seguente modifica una configurazione di diagnostica Azure hello. In questa configurazione, solo l'evento ID 4624 e l'evento ID 4625 vengono raccolti dal registro eventi di sicurezza hello. Microsoft Antimalware per gli eventi di Azure vengono raccolti dal registro eventi di sistema hello. Per informazioni dettagliate sull'utilizzo di hello delle espressioni XPath, vedere [utilizzo degli eventi](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Hello esempio seguente imposta la configurazione di diagnostica Azure hello:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Dopo aver apportato modifiche, controllare tooensure account di archiviazione hello che hello corretto gli eventi vengono raccolti.

Se si dispone di eventuali problemi durante l'installazione di hello e configurazione, aprire un [richiesta di supporto](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Selezionare **Log integrazione** come servizio hello per il quale si richiede supporto.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>È possibile utilizzare i log di integrazione di Azure Log toointegrate Watcher di rete in my SIEM?

Azure Network Watcher genera grandi quantità di informazioni di registrazione. Questi log non sono adatti toobe inviati tooa SIEM. destinazione Hello è supportato solo per i log di controllo di rete è un account di archiviazione. Integrazione di Log di Azure non supporta la lettura di questi registri e rendendoli disponibile tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
