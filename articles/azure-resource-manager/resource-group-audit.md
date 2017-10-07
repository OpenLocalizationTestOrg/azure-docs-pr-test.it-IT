---
title: "attività di Azure aaaView registra risorse toomonitor | Documenti Microsoft"
description: "Utilizzare hello attività registra errori e tooreview azioni dell'utente. Mostra il portale di Azure, PowerShell, l'interfaccia della riga di comando di Azure e REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Visualizza attività registra le azioni tooaudit sulle risorse
Con i log attività è possibile determinare:

* le operazioni eseguite sulle risorse hello nella sottoscrizione
* che ha avviato l'operazione di hello (anche se le operazioni avviate da un servizio back-end non restituiscono un utente come chiamante hello)
* Quando si è verificato il funzionamento di hello
* stato Hello dell'operazione di hello
* i valori Hello altre proprietà che potrebbero facilitare la ricerca operazione hello

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

È possibile recuperare informazioni dal log attività hello tramite il portale di hello, PowerShell, CLI di Azure, l'API REST di Insights o [libreria .NET di Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>di Microsoft Azure
1. Selezionare i log di attività hello tooview tramite il portale di hello **monitoraggio**.
   
    ![Selezionare i log di attività](./media/resource-group-audit/select-monitor.png)

   O, nel log attività di hello tooautomatically filtro per una determinata risorsa o un gruppo di risorse, seleziona **log attività** da tale pannello della risorsa. Si noti che log attività hello vengono filtrati automaticamente dalla risorsa hello selezionato.
   
    ![filtrare in base alla risorsa](./media/resource-group-audit/filtered-by-resource.png)
2. In hello **Log attività** pannello viene visualizzato un riepilogo delle operazioni recenti.
   
    ![visualizzare le azioni](./media/resource-group-audit/audit-summary.png)
3. numero di hello toorestrict di operazioni visualizzata, selezionare condizioni diverse. Ad esempio, hello seguente immagine Mostra hello **Timespan** e **evento avviato da** campi modificati azioni di hello tooview da un particolare utente o applicazione per hello mese scorso. Selezionare **applica** risultati hello tooview della query.
   
    ![impostare le opzioni di filtro](./media/resource-group-audit/set-filter.png)

4. Se è necessario query hello toorun in un secondo momento, selezionare **salvare** e assegnare un nome di query hello.
   
    ![Salvare la query](./media/resource-group-audit/save-query.png)
5. tooquickly eseguire una query, è possibile selezionare una delle query incorporato hello, ad esempio distribuzioni non riuscite.

    ![Selezionare la query](./media/resource-group-audit/select-quick-query.png)

   la query selezionata Hello imposta automaticamente i valori di filtro hello necessario.

    ![Visualizzare gli errori di distribuzione](./media/resource-group-audit/view-failed-deployment.png)   

6. Selezionare una delle operazioni di hello toosee un riepilogo dell'evento hello.

    ![Visualizzare l'operazione](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. le voci di log tooretrieve, eseguire hello **Get AzureRmLog** comando. Fornire parametri aggiuntivi toofilter hello elenco voci. Se non si specifica un'ora di inizio e fine, vengono restituite le voci per hello ultima ora. Ad esempio, eseguire le operazioni di hello tooretrieve per un gruppo di risorse durante l'ultima ora hello:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Hello di esempio seguente viene illustrato come attività hello toouse log tooresearch operazioni eseguite durante un tempo specificato. date di inizio e fine Hello vengono specificate in un formato di Data.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    In alternativa, è possibile utilizzare funzioni toospecify hello data intervallo di date, ad esempio hello ultimi 14 giorni.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. In base all'ora di inizio hello specificate, i comandi precedenti hello possono restituire un lungo elenco di operazioni per il gruppo di risorse hello. È possibile filtrare i risultati di hello per ciò che si sta cercando, fornendo i criteri di ricerca. Se si sta tentando di tooresearch come un'app web è stata arrestata, ad esempio, è possibile eseguire hello comando seguente:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    In questo esempio indica che è stata eseguita un'azione di arresto da someone@contoso.com. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. È possibile esaminare le azioni di hello intraprese da un particolare utente, anche per un gruppo di risorse che non esiste più.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. È possibile filtrare le operazioni non riuscite.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. È possibile concentrarsi su un errore esaminando il messaggio di stato hello per tale voce.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Che restituisce:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
* le voci del registro tooretrieve eseguire hello **gruppo azure log Mostra** comando.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>API REST
le operazioni REST Hello per l'utilizzo di log attività hello fanno parte di hello [API REST di Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx). tooretrieve attività log eventi, vedere [elenco eventi di gestione di hello in una sottoscrizione](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Passaggi successivi
* Log attività Azure è utilizzabile con Power BI toogain maggiori informazioni relative sulle azioni di hello nella sottoscrizione. Vedere [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Visualizzare e analizzare i log attività di Azure in Power BI e altri strumenti).
* toolearn sull'impostazione di criteri di sicurezza, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).
* toolearn sui comandi hello per la visualizzazione delle operazioni di distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).
* toolearn tooprevent eliminazioni su una risorsa per tutti gli utenti, vedere [bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).

