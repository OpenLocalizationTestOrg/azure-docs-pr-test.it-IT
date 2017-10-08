---
title: aaaUsing PowerShell toomanage Traffic Manager in Azure | Documenti Microsoft
description: Uso di PowerShell per Gestione traffico con Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Utilizzo di PowerShell toomanage Traffic Manager

Gestione risorse di Azure è l'interfaccia di gestione Preferiti hello per servizi di Azure. I profili di Gestione traffico di Azure possono ora essere gestiti usando le API e gli strumenti basati su Azure Resource Manager.

## <a name="resource-model"></a>Modello di risorsa

Gestione traffico di Azure viene configurato utilizzando una serie di impostazioni denominate "profilo di Gestione traffico". Il profilo contiene le impostazioni DNS, le impostazioni del routing del traffico, le impostazioni di monitoraggio degli endpoint e viene indirizzato un elenco di traffico toowhich gli endpoint del servizio.

Ogni profilo di Gestione traffico è rappresentato da una risorsa di tipo "TrafficManagerProfiles". A livello di API REST di hello, hello URI per ogni profilo è il seguente:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configurazione di Azure PowerShell

In queste istruzioni viene usato Microsoft Azure PowerShell. Hello articolo seguente viene illustrato come tooinstall e configurare Azure PowerShell.

* [Come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)

esempi di Hello in questo articolo presuppongono che sia disponibile un gruppo di risorse esistente. È possibile creare un gruppo di risorse utilizzando hello comando seguente:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager richiede che tutti i gruppi di risorse specifichino un percorso, Questo percorso viene utilizzato come valore predefinito di hello per le risorse create in tale gruppo di risorse. Tuttavia, poiché le risorse di profilo di gestione traffico globale e non regionali, scelta hello del percorso del gruppo di risorse ha alcun impatto su Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Creazione di un profilo di Gestione traffico

toocreate un profilo di Traffic Manager, utilizzare hello `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Hello nella tabella seguente vengono descritti i parametri di hello:

| . | Descrizione |
| --- | --- |
| Nome |nome della risorsa Hello hello risorse profilo di Traffic Manager. I profili in hello stesso gruppo di risorse deve avere nomi univoci. Questo nome è separato dal nome DNS hello per le query DNS. |
| ResourceGroupName |nome Hello di hello gruppo contenitore hello profilo risorsa. |
| TrafficRoutingMethod |Specifica hello routing del traffico utilizzato toodetermine endpoint a cui viene restituito in risposta a una query DNS. I valori possibili sono "Performance", "'Weighted" e "Priority". |
| RelativeDnsName |Specifica porzione hostname di hello del nome DNS hello fornito da questo profilo di Traffic Manager. Questo valore viene combinato con il nome di dominio DNS hello utilizzato da Gestione traffico di Azure tooform hello Nome dominio completo (FQDN) del profilo di hello. Ad esempio, impostare il valore di hello del 'contoso' diventa 'contoso.trafficmanager.net'. |
| TTL |Specifica hello DNS Time-to-Live (TTL), in secondi. Questa durata TTL indica ai resolver DNS locali hello e i client DNS tempo delle risposte DNS toocache per questo profilo di Traffic Manager. |
| MonitorProtocol |Specifica l'integrità dell'endpoint toomonitor toouse protocollo hello. I valori possibili sono "HTTP" e "HTTPS". |
| MonitorPort |Specifica la porta TCP hello toomonitor integrità dell'endpoint. |
| MonitorPath |Specifica nome di dominio dell'endpoint di hello percorso relativo toohello utilizzato tooprobe per lo stato di endpoint. |

Hello cmdlet crea un profilo di Traffic Manager in Azure e restituisce un corrispondente tooPowerShell oggetto profilo. A questo punto, hello profilo non contiene alcun endpoint. Per ulteriori informazioni sull'aggiunta del profilo di Traffic Manager tooa endpoint, vedere [aggiunta di endpoint di gestione traffico](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Visualizzazione di un profilo di Gestione traffico

tooretrieve un oggetto profilo di gestione traffico esistente, utilizzare hello `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Questo cmdlet restituisce un oggetto profilo di Gestione traffico.

## <a name="update-a-traffic-manager-profile"></a>Aggiornare un profilo di Gestione traffico

La modifica dei profili di Gestione traffico prevede un processo in 3 passaggi:

1. Recuperare hello profilo utilizzando `Get-AzureRmTrafficManagerProfile` oppure utilizzare il profilo di hello restituito da `New-AzureRmTrafficManagerProfile`.
2. Modificare il profilo di hello. È possibile aggiungere e rimuovere endpoint o modificare i parametri dell'endpoint o del profilo. Queste modifiche sono operazioni offline. Si sta modificando solo oggetto locale di hello in memoria che rappresenta il profilo di hello.
3. Salvare le modifiche utilizzando hello `Set-AzureRmTrafficManagerProfile` cmdlet.

Tutte le proprietà di profilo possono essere modificate, ad eccezione RelativeDnsName del profilo hello. toochange hello RelativeDnsName, è necessario eliminare profilo e un nuovo profilo con un nuovo nome.

Hello di esempio seguente viene illustrato come toochange hello durata (TTL) del profilo:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Sono disponibili tre tipi di endpoint di Gestione traffico:

1. I servizi **Endpoint di Azure** sono ospitati hosting in Azure
2. I servizi **Endpoint esterni** sono ospitati all'esterno di Azure
3. **Annidati endpoint** gerarchie utilizzate tooconstruct annidati di profili di gestione traffico. Gli endpoint annidati consentono configurazioni avanzate del routing del traffico per applicazioni complesse.

In tutti e tre i casi è possibile aggiungere gli endpoint in due modi:

1. Usando il processo in 3 passaggi descritto in precedenza. Il vantaggio di Hello di questo metodo è che possono essere apportate molte modifiche di endpoint in un singolo aggiornamento.
2. Utilizzo di cmdlet New-AzureRmTrafficManagerEndpoint hello. Questo cmdlet aggiunge un profilo di Traffic Manager endpoint tooan esistente in un'unica operazione.

## <a name="adding-azure-endpoints"></a>Aggiunta di endpoint di Azure

Gli endpoint di Azure fanno riferimento ai servizi ospitati in Azure. Sono attualmente supportati due tipi di endpoint di Azure:

1. App Web di Azure 
2. PublicIpAddress le risorse di Azure (che possono essere collegato tooa bilanciamento del carico o una scheda di rete di macchina virtuale). Hello PublicIpAddress deve avere un nome DNS assegnato toobe utilizzato in Traffic Manager.

In ogni caso:

* servizio Hello viene specificato utilizzando il parametro 'ID risorsa di destinazione' hello di `Add-AzureRmTrafficManagerEndpointConfig` o `New-AzureRmTrafficManagerEndpoint`.
* Hello 'Target' e 'EndpointLocation' impliciti di hello ID risorsa di destinazione.
* Hello 'Peso' è facoltativo. I pesi vengono usati solo se il profilo di hello è metodo di routing del traffico toouse configurato hello 'Weighted'. In caso contrario, vengono ignorate. Se specificato, il valore di hello deve essere un numero compreso tra 1 e 1000. valore predefinito di Hello è '1'.
* Hello specificando 'Priority' è facoltativo. Le priorità vengono utilizzate solo se il profilo di hello è metodo di routing del traffico configurate toouse hello 'Priority'. In caso contrario, vengono ignorate. I valori validi sono da 1 too1000 con i valori più bassi, che indica una priorità più alta. Se si specifica questo valore per un endpoint, sarà necessario specificarlo per tutti gli endpoint. Se omesso, vengono applicati i valori predefiniti a partire da '1' in ordine di hello sono elencati gli endpoint hello.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Esempio 1: Aggiunta di endpoint di App Web usando `Add-AzureRmTrafficManagerEndpointConfig`

In questo esempio, creare un profilo di gestione traffico e aggiungere due endpoint di App Web utilizzando hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Esempio 2: Aggiunta di un endpoint publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`

In questo esempio, una risorsa di indirizzo IP pubblica viene aggiunto il profilo di gestione traffico toohello. indirizzo IP pubblico Hello deve avere un nome DNS configurato e può essere associata una scheda NIC di bilanciamento del carico macchina virtuale o tooa toohello.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Aggiunta di endpoint esterni

Il traffico di gestione utilizza gli endpoint esterni toodirect traffico tooservices ospitato all'esterno di Azure. Come con gli endpoint di Azure, gli endpoint esterni possono essere aggiunti usando `Add-AzureRmTrafficManagerEndpointConfig` seguito da `Set-AzureRmTrafficManagerProfile` o `New-AzureRMTrafficManagerEndpoint`.

Quando si specificano endpoint esterni:

* nome di dominio di Hello endpoint deve essere specificata utilizzando il parametro 'Target' hello
* Se viene utilizzato il metodo di routing del traffico "Prestazioni" hello, hello 'EndpointLocation' è obbligatorio. In caso contrario, è facoltativo. il valore di Hello deve essere un [nome dell'area di Azure valido](https://azure.microsoft.com/regions/).
* Hello 'Peso' e 'Priority' sono facoltativi.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Esempio 1: Aggiunta di endpoint esterni usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

In questo esempio è creare un profilo di Traffic Manager, aggiungere due endpoint esterni e commit delle modifiche hello.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Esempio 2: Aggiunta di endpoint esterni usando `New-AzureRmTrafficManagerEndpoint`

In questo esempio, si aggiunge un profilo esistente di endpoint esterni tooan. profilo Hello è specificato utilizzando i nomi di gruppi di profili e risorse hello.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Aggiunta di endpoint 'annidati'

Ciascun profilo di Gestione traffico specifica un solo metodo di routing del traffico. Esistono tuttavia scenari che richiedono più sofisticato il routing del traffico di routing hello fornito da un unico profilo di Traffic Manager. È possibile nidificare i vantaggi di gestione traffico profili toocombine hello di più di un metodo di routing del traffico. Profili nidificati consentono toooverride hello predefinito Traffic Manager comportamento toosupport maggiori e le distribuzioni di applicazioni più complesse. Per esempi più dettagliati, vedere [Profili annidati di Gestione traffico](traffic-manager-nested-profiles.md).

Gli endpoint annidati sono configurati nel profilo padre hello, utilizzando un tipo di endpoint specifico, 'NestedEndpoints'. Quando si specificano endpoint annidati:

* endpoint Hello deve essere specificata utilizzando il parametro 'ID risorsa di destinazione' hello
* Se viene utilizzato il metodo di routing del traffico "Prestazioni" hello, hello 'EndpointLocation' è obbligatorio. In caso contrario, è facoltativo. il valore di Hello deve essere un [nome dell'area di Azure valido](http://azure.microsoft.com/regions/).
* Hello 'Peso' e 'Priority' sono facoltativi, come endpoint di Azure.
* parametro 'MinChildEndpoints' Hello è facoltativo. valore predefinito di Hello è '1'. Se hello degli endpoint disponibile scende sotto questa soglia, profilo padre hello considera profilo figlio hello 'danneggiato' e la trasferisce traffico toohello altri endpoint nel profilo padre hello.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Esempio 1: Aggiunta di endpoint annidati usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

In questo esempio, è creare padre e figlio di Traffic Manager nuovi profili Aggiungi figlio hello come padre toohello endpoint annidati e commit delle modifiche di hello.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Per brevità, in questo esempio, non è stato aggiunto qualsiasi altro endpoint toohello padre o figlio profilo.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Esempio 2: Aggiunta di endpoint annidati usando `New-AzureRmTrafficManagerEndpoint`

In questo esempio è aggiungere un profilo figlio esistente come un profilo padre esistente tooan endpoint annidati. profilo Hello è specificato utilizzando i nomi di gruppi di profili e risorse hello.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Aggiornare un endpoint di Gestione traffico

Esistono due modi tooupdate un endpoint di gestione traffico esistente:

1. Profilo di Traffic Manager hello tramite `Get-AzureRmTrafficManagerProfile`, aggiornare le proprietà endpoint hello nel profilo hello e salvare le modifiche di hello utilizzando `Set-AzureRmTrafficManagerProfile`. Questo metodo presenta il vantaggio di hello di essere in grado di tooupdate più di un endpoint in un'unica operazione.
2. Ottenere l'endpoint di gestione traffico hello utilizzando `Get-AzureRmTrafficManagerEndpoint`, aggiornare le proprietà endpoint hello e salvare le modifiche di hello utilizzando `Set-AzureRmTrafficManagerEndpoint`. Questo metodo è più semplice, poiché non richiede l'indicizzazione in una matrice di endpoint hello nel profilo hello.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Esempio 1: Aggiornamento di endpoint usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`

In questo esempio viene modificata la priorità di hello in due endpoint all'interno di un profilo esistente.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Esempio 2: Aggiornamento di un endpoint usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`

In questo esempio è modificare il peso di hello di un singolo endpoint in un profilo esistente.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Abilitazione e disabilitazione di endpoint e profili

Gestione traffico consente singoli endpoint toobe abilitati e disabilitati, oltre a consentire l'abilitazione e disabilitazione dei profili interi.
Queste modifiche possono essere apportate dalle risorse hello ottenimento o l'aggiornamento o l'impostazione di endpoint o un profilo. toostreamline queste operazioni comuni, sono anche supportate tramite cmdlet dedicati.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Esempio 1: Abilitazione e disabilitazione di un profilo di Gestione traffico

Utilizzare un profilo di Traffic Manager, tooenable `Enable-AzureRmTrafficManagerProfile`. è possibile specificare il profilo di Hello utilizzando un oggetto profilo. Hello oggetto profilo può essere passato tramite la pipeline hello o utilizzando hello '-TrafficManagerProfile' parametro. In questo esempio, si specifica il profilo di hello dal nome del gruppo di risorse e profilo di hello.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable un profilo di gestione traffico:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

cmdlet Disable-AzureRmTrafficManagerProfile Hello chiesta la conferma. Questo messaggio può essere soppresso mediante hello '-Force' parametro.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Esempio 2: Abilitazione e disabilitazione di un endpoint di Gestione traffico

tooenable un endpoint di Traffic Manager, utilizzare `Enable-AzureRmTrafficManagerEndpoint`. Esistono due endpoint di hello toospecify modi

1. Utilizzando un oggetto TrafficManagerEndpoint passato tramite la pipeline hello o hello '-TrafficManagerEndpoint' parametro
2. Utilizzando il nome dell'endpoint hello, tipo di endpoint, nome del profilo e nome del gruppo di risorse:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Analogamente, toodisable un endpoint di gestione traffico:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Come con `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet chiesta la conferma. Questo messaggio può essere soppresso mediante hello '-Force' parametro.

## <a name="delete-a-traffic-manager-endpoint"></a>Eliminare un endpoint di Gestione traffico

tooremove singoli endpoint, utilizzare hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Il cmdlet richiede una conferma. Questo messaggio può essere soppresso mediante hello '-Force' parametro.

## <a name="delete-a-traffic-manager-profile"></a>Eliminare un profilo di Gestione traffico

toodelete un profilo di Traffic Manager, utilizzare hello `Remove-AzureRmTrafficManagerProfile` specificando nomi di gruppi di profili e risorse hello:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Il cmdlet richiede una conferma. Questo messaggio può essere soppresso mediante hello '-Force' parametro.

Hello profilo toobe eliminato è possibile specificare anche utilizzando un oggetto profilo:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Questa sequenza può anche essere inoltrata tramite pipe:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Passaggi successivi

[Monitoraggio di Gestione traffico](traffic-manager-monitoring.md)

[Considerazioni sulle prestazioni di gestione traffico](traffic-manager-performance-considerations.md)
