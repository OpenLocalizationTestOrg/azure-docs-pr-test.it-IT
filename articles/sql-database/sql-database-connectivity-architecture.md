---
title: "architettura di connettività di Database SQL aaaAzure | Documenti Microsoft"
description: "Questo documento illustra hello Azure SQLDB connettività architettura da Azure o da all'esterno di Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Architettura della connettività del database SQL di Azure 

In questo articolo illustra l'architettura di connettività di Database SQL di Azure hello e viene spiegato come diversi componenti hello funzionano toodirect traffico tooyour istanza Database SQL di Azure. Questi componenti di connettività di Database SQL di Azure di funzione toohello il traffico di rete toodirect il database di Azure con i client che si connettono da all'interno di Azure e con i client che si connettono dall'esterno di Azure. In questo articolo fornisce anche toochange esempi di script come si verifica la connettività e considerazioni hello relative impostazioni di connettività toochanging hello predefinito. Se dopo aver letto questo articolo sorgono domande, contattare Dhruv all'indirizzo dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Architettura della connettività

Hello seguente diagramma fornisce una panoramica generale di hello architettura di connettività di Database SQL di Azure. 

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/architecture-overview.png)


Hello passaggi seguenti descrivono come una connessione viene stabilita tooan database SQL di Azure tramite hello Database SQL di Azure software carico-bilanciamento e il gateway di Database SQL di Azure hello.

- I client all'interno di Azure o all'esterno di Azure connettersi toohello SLB, che ha un indirizzo IP pubblico e in ascolto sulla porta 1433.
- Hello SLB indirizza il gateway di traffico toohello Database SQL di Azure.
- gateway Hello reindirizza hello traffico toohello proxy corretto middleware.
- middleware proxy Hello reindirizza il database SQL di Azure appropriato di hello traffico toohello.

> [!IMPORTANT]
> Ognuno di questi componenti è distribuiti di tipo denial of protection service (DDoS) incorporato in rete hello e il livello di applicazione hello.
>

## <a name="connectivity-from-within-azure"></a>Connettività dall'interno di Azure

Se ci si connette dall'interno di Azure, il criterio di connessione predefinito per le connessioni è **reindirizzamento**. Un criterio di **reindirizzare** significa che le connessioni al termine della sessione TCP hello database SQL di Azure toohello stabilita, sessione client hello è quindi reindirizzati toohello proxy middleware con un IP virtuale di destinazione toohello modifica da che di hello Azure SQL Database gateway toothat di hello proxy middleware. Successivamente, tutti i pacchetti successivi del flusso direttamente tramite il middleware proxy hello, ignorando il gateway di Database SQL di Azure hello. Hello seguente diagramma illustra il flusso del traffico.

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Connettività dall'esterno di Azure

Se ci si connette dall'esterno di Azure, le connessioni usano un criterio di connessione **proxy** per impostazione predefinita. Un criterio di **Proxy** significa che sessione TCP hello viene stabilita tramite il gateway di Database SQL di Azure hello e tutti i pacchetti successivi flusso tramite hello gateway. Hello seguente diagramma illustra il flusso del traffico.

![panoramica dell'architettura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Indirizzi IP del gateway del database SQL di Azure

database di SQL Azure tooconnect tooan da risorse locali, è necessario gateway di Database SQL di Azure toohello di traffico di tooallow rete in uscita per l'area di Azure. Le connessioni passano solo tramite il gateway di hello quando ci si connette in modalità Proxy, che è l'impostazione predefinita di hello durante la connessione da risorse locali.

Nella seguente sono elencati nella tabella Hello hello IP primario e secondario del gateway di Database SQL di Azure hello per tutte le aree dati. Per alcune aree sono disponibili due indirizzi IP. In queste aree, indirizzo IP primario hello è l'indirizzo IP corrente hello del gateway hello e secondo indirizzo IP di hello è un indirizzo IP di failover. indirizzo failover Hello è toowhich indirizzo hello è possibile spostare l'elevata disponibilità server tookeep hello del servizio. Per queste aree, è consigliabile consentire tooboth in uscita gli indirizzi IP hello. secondo indirizzo IP di Hello è di proprietà di Microsoft e non è in ascolto su alcun servizio fino a quando non viene attivato da connessioni tooaccept Database SQL di Azure.

| Nome area | Indirizzo IP primario | Indirizzo IP secondario |
| --- | --- |--- |
| Australia orientale | 191.238.66.109 | 13.75.149.87 |
| Australia sud-orientale | 191.239.192.109 | 13.73.109.251 |
| Brasile meridionale | 104.41.11.5 | |    
| Canada centrale | 40.85.224.249 | |    
| Canada orientale | 40.86.226.166 | |
| Stati Uniti centrali | 23.99.160.139 | 13.67.215.62 |
| Asia orientale | 191.234.2.139 | 52.175.33.150 |
| Stati Uniti orientali 1 | 191.238.6.43 | 40.121.158.30 |
| Stati Uniti orientali 2 | 191.239.224.107 | 40.79.84.180 |
| India centrale | 104.211.96.159  | |   
| India meridionale | 104.211.224.146  | |
| India occidentale | 104.211.160.80 | |
| Giappone orientale | 191.237.240.43 | 13.78.61.196 |
| Giappone occidentale | 191.238.68.11 | 104.214.148.156 |
| Corea centrale | 52.231.32.42 | |
| Corea meridionale | 52.231.200.86 |  |
| Stati Uniti centro-settentrionali | 23.98.55.75 | 23.96.178.199 |
| Europa settentrionale | 191.235.193.75 | 40.113.93.91 |
| Stati Uniti centro-meridionali | 23.98.162.75 | 13.66.62.124 |
| Asia sudorientale | 23.100.117.95 | 104.43.15.0 |
| Regno Unito settentrionale | 13.87.97.210 | |
| Regno Unito meridionale 1 | 51.140.184.11 | |    
| Regno Unito meridionale 2 | 13.87.34.7 | |
| Regno Unito occidentale | 51.141.8.11  | |
| Stati Uniti centro-occidentali | 13.78.145.25 | |
| Europa occidentale | 191.237.232.75 | 40.68.37.158 |
| Stati Uniti occidentali 1 | 23.99.34.75 | 104.42.238.205 |
| Stati Uniti occidentali 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Modificare il criterio di connessione del database SQL di Azure

hello toochange criteri di connessione di Database SQL di Azure per un server di Database SQL di Azure, utilizzare hello [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Se il criterio di connessione è stato impostato troppo**Proxy**, tutto il flusso dei pacchetti tramite il gateway di Database SQL di Azure hello di rete. Per questa impostazione, è necessario IP del gateway tooallow tooonly in uscita hello Database SQL di Azure. L'uso dell'impostazione **proxy** ha una latenza maggiore rispetto all'impostazione **reindirizzamento**. 
- Se i criteri di connessione sono l'impostazione **reindirizzare**, tutti i pacchetti di rete direttamente flusso toohello middleware proxy. Per questa impostazione, è necessario tooallow in uscita toomultiple gli indirizzi IP. 

## <a name="script-toochange-connection-settings"></a>Impostazioni di connessione toochange script

> [!IMPORTANT]
> Questo script richiede hello [modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Hello lo script di PowerShell seguente viene illustrato come toochange hello criteri di connessione.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come toochange hello criteri di connessione di Database SQL di Azure per un server di Database SQL di Azure, vedere [Create o criteri di connessione Server di aggiornamento tramite API REST di hello](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Per informazioni sul comportamento della connessione al database SQL di Azure per i client che usano ADO.NET 4.5 o versione successiva, vedere [Porte successive alla 1433 per ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Per una panoramica generale sullo sviluppo di applicazioni, vedere [Panoramica dello sviluppo di applicazioni del database SQL](sql-database-develop-overview.md).
