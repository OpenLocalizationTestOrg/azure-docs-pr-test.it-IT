---
title: un Gateway di applicazione di Azure - modelli aaaCreate | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate un gateway applicazione Azure utilizzando il modello di gestione risorse di Azure hello
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Creare un gateway applicazione utilizzando il modello di gestione risorse di Azure hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [PowerShell per Azure classico](application-gateway-create-gateway.md)
> * [Modello di Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfaccia della riga di comando di Azure](application-gateway-create-gateway-cli.md)

Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7. Fornisce il failover e il routing delle prestazioni delle richieste HTTP tra server diversi, che si trovino in locale o cloud hello. Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre. toofind un elenco completo delle funzionalità supportate, visitare [Panoramica di Gateway applicazione](application-gateway-introduction.md)

In questo articolo viene illustrato il download e modifica di un modello di gestione risorse di Azure esistente da GitHub e la distribuzione modello hello da GitHub, PowerShell e hello CLI di Azure.

Se si distribuiscono semplicemente il modello di Azure Resource Manager hello direttamente da GitHub senza apportare modifiche, è possibile ignorare toodeploy un modello da GitHub.

## <a name="scenario"></a>Scenario

In questo scenario si apprenderà come:

* Creare un gateway applicazione con web application firewall.
* Creare una rete virtuale denominata VirtualNetwork1 con un blocco CIDR riservato 10.0.0.0/16.
* Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.
* Configurare due indirizzi IP back-end configurato in precedenza per i server web hello si desidera bilanciare il traffico in hello tooload. In questo esempio di modello, hello IP back-end sono 10.0.1.10 e 10.0.1.11.

> [!NOTE]
> Tali impostazioni sono parametri di hello per questo modello. modello di hello toocustomize, è possibile modificare le regole, i listener di hello, SSL e altre opzioni nel file azuredeploy.json hello.

![Scenario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Scaricare e comprendere il modello di Azure Resource Manager hello

È possibile scaricare hello esistente Azure Resource Manager modello toocreate una rete virtuale e due subnet da GitHub, apportare le modifiche potrebbe essere necessario e riutilizzarlo. toodo in tal caso, utilizzare hello alla procedura seguente:

1. Passare troppo[crea applicazioni Gateway con firewall applicazione web abilitata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Fare clic su **azuredeploy.json**, quindi fare clic su **RAW**.
1. Salvare una cartella locale di hello file tooa nel computer.
1. Se si ha familiarità con i modelli di gestione risorse di Azure, ignorare toostep 7.
1. Aprire il file hello salvato ed esaminare il contenuto di hello in **parametri** nella riga
1. La sezione parameters del modello di Gestione risorse di Azure è un segnaposto per i valori che possono essere inseriti durante la distribuzione.

  | Parametro | Descrizione |
  | --- | --- |
  | **subnetPrefix** |Blocco CIDR per la subnet del gateway applicazione hello. |
  | **applicationGatewaySize** | Dimensioni del gateway applicazione hello.  WAF consente solo gateway di medie e grandi dimensioni. |
  | **backendIpaddress1** |Indirizzo IP del server web prima di hello. |
  | **backendIpaddress2** |Indirizzo IP del server web secondo hello. |
  | **wafEnabled** | Impostazione toodetermine se WAF è abilitata.|
  | **wafMode** | Modalità di hello web application firewall.  Le opzioni disponibili sono **prevention** (prevenzione) e **detection** (rilevamento).|
  | **wafRuleSetType** | Tipo di set di regole per WAF.  Attualmente OWASP è hello supportata solo l'opzione. |
  | **wafRuleSetVersion** |Versione del set di regole. OWASP CRS 2.2.9 e 3.0 sono attualmente opzioni hello è supportato. |

1. Controllare il contenuto hello **risorse** e notifica hello le proprietà seguenti:

   * **type**. Tipo di risorsa viene creato dal modello hello. In questo caso, è di tipo hello `Microsoft.Network/applicationGateways`, che rappresenta un gateway applicazione.
   * **name**. Nome per la risorsa hello. Avviso hello utilizzo di `[parameters('applicationGatewayName')]`, significa che tale nome hello viene fornito come input dall'utente o da un file dei parametri durante la distribuzione.
   * **properties**. Elenco di proprietà per la risorsa hello. Il modello utilizza la rete virtuale hello e indirizzo IP pubblico durante la creazione del gateway applicazione.

   > [!NOTE]
   > Per altre informazioni sui modelli, visitare la pagina [Resource Manager templates reference (Riferimenti ai modelli di Resource Manager)](/templates/)

1. Passare troppo[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Fare clic su **azuredeploy-parameters.json** e quindi su **RAW**.
1. Salvare una cartella locale di hello file tooa nel computer.
1. Aprire il file hello che è stato salvato e modificare i valori hello per i parametri di hello. Utilizzare hello gateway applicazione hello toodeploy valori nello scenario descritto di seguito.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Salvare il file hello. È possibile testare i modelli di parametro e JSON hello utilizzando strumenti di convalida JSON online come [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Distribuire il modello di gestione risorse di Azure hello tramite PowerShell

Se non si è mai usato PowerShell di Azure, visitare: [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire toosign istruzioni hello in Azure e selezionare la sottoscrizione.

1. Account di accesso tooPowerShell

    ```powershell
    Login-AzureRmAccount
    ```

1. Controllare le sottoscrizioni di hello per account hello.

    ```powershell
    Get-AzureRmSubscription
    ```

    Si è tooauthenticate richiesta con le credenziali.

1. Scegliere quali di toouse le sottoscrizioni di Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Se necessario, creare un gruppo di risorse utilizzando hello **New AzureResourceGroup** cmdlet. Nell'esempio seguente di hello, si crea un gruppo di risorse denominato AppgatewayRG nel percorso di Stati Uniti orientali.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Eseguire hello **New AzureRmResourceGroupDeployment** cmdlet toodeploy hello nuova rete virtuale tramite hello che precede i file di modello e sui parametri è stato scaricato e modificato.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Distribuire il modello di gestione risorse di Azure hello utilizzando hello CLI di Azure

modello di gestione risorse di Azure hello toodeploy scaricato tramite l'interfaccia CLI di Azure, seguire hello alla procedura seguente:

1. Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](/cli/azure/install-azure-cli) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.

1. Se necessario, hello esecuzione `az group create` comando toocreate un gruppo di risorse, come illustrato nel seguente frammento di codice hello. Notare l'output di hello del comando hello. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (o --nome)**. Nome per il nuovo gruppo di risorse hello. Per questo scenario, *appgatewayRG*.
    
    **-l (o --location)**. Area di Azure in cui viene creato il nuovo gruppo di risorse hello. Per questo scenario, *westus*.

1. Eseguire hello `az group deployment create` cmdlet toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato nel precedente passaggio hello. elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Distribuire il modello di gestione risorse di Azure hello utilizzando fare clic su da distribuire

Fare clic su per la distribuzione è un altro modo toouse modelli di gestione risorse di Azure. Si tratta di modelli di toouse un modo semplice con hello portale di Azure.

1. Andare troppo[creare un gateway applicazione con firewall applicazione web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Fare clic su **distribuire tooAzure**.

    ![Distribuire tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Compilare i parametri di hello per il modello di distribuzione hello nel portale di hello e fare clic su **OK**.

    ![parameters](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Selezionare **accetto le condizioni indicate in precedenza toohello** e fare clic su **acquisto**.

1. Nel Pannello di distribuzione personalizzata hello, fare clic su **crea**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Fornisce gestione modelli di certificato dati tooResource

Quando si usa SSL con un modello, certificato hello deve toobe fornito in una stringa base64 anziché in fase di caricamento. stringa base64 pfx o CER tooa tooconvert utilizzare uno dei seguenti comandi hello. Hello seguenti comandi convertono hello certificato tooa stringa base64, che può essere fornita toohello modello. Hello è previsto output è una stringa che può essere archiviata in una variabile e incollata nel modello di hello.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, completare una delle hello alla procedura seguente:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooconfigure offload SSL, visitare: [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).

Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, visitare: [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

