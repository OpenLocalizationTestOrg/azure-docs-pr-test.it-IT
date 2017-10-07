---
title: ruoli e utenti in Azure Analysis Services del database aaaManage | Documenti Microsoft
description: Informazioni su come toomanage database ruoli e utenti in un server Analysis Services in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Gestire ruoli del database e utenti

A livello di database modello hello, tutti gli utenti devono appartenere tooa ruolo. I ruoli definiscono gli utenti con determinate autorizzazioni per database modello hello. Qualsiasi utente o gruppo di protezione aggiunta tooa ruolo deve includere un account in un tenant di Azure AD in hello stessa sottoscrizione server hello.

Come definire i ruoli è diverso a seconda dello strumento hello che è utilizzato, ma è hello effetto hello stesso.

Le autorizzazioni di ruoli includono:
*  **Amministratore** -gli utenti hanno le autorizzazioni complete per il database di hello. I ruoli del database con autorizzazioni di amministratore sono diversi dagli amministratori di server.
*  **Processo** -gli utenti possono connettersi tooand eseguire operazioni di elaborazione nel database di hello e analizzare i dati del database modello.
*  **Lettura** -gli utenti possono usare un client applicazione tooconnect tooand analizzare i dati del database modello.

Quando si crea un progetto di modello tabulare, creare i ruoli e aggiungere utenti o gruppi di ruoli toothose tramite Gestione ruoli in SSDT. Quando è distribuito tooa server, utilizzare SQL Server Management Studio, [i cmdlet di PowerShell per Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx), o [linguaggio di Scripting del modello tabulare](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) o rimuovere ruoli e membri di un utente.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd o gestire ruoli e utenti in SSDT  
  
1.  In SSDT > **Esplora modelli tabulari** fare clic con il pulsante destro del mouse su **Ruoli**.  
  
2.  In **Gestione ruoli** fare clic su **Nuovo**.  
  
3.  Digitare un nome per il ruolo di hello.  
  
     Per impostazione predefinita, il nome di hello del ruolo predefinito di hello è numerato in modo incrementale per ogni nuovo ruolo. È consigliabile che si digita un nome che identifichi il tipo membro hello, ad esempio responsabili finanze o esperti di risorse umane.  
  
4.  Selezionare una di queste autorizzazioni hello:  
  
    |Autorizzazione|Descrizione|  
    |----------------|-----------------|  
    |**Nessuno**|I membri non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.|  
    |**Lettura**|I membri possono eseguire query dati (in base ai filtri di riga), ma non è possibile modificare lo schema del modello hello.|  
    |**Lettura ed elaborazione**|I membri possono eseguire una query dei dati (in base ai filtri a livello di riga) e l'esecuzione di operazioni elabora ed elabora tutto, ma non è possibile modificare lo schema del modello hello.|  
    |**Processo**|I membri possono eseguire operazioni Elabora ed Elabora tutto. Non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.|  
    |**Amministratore**|I membri possono modificare lo schema del modello hello e tutti i dati di query.|   
  
5.  Se il ruolo di hello sono creazione è di lettura o autorizzazione di lettura ed elaborazione, è possibile aggiungere filtri di riga tramite una formula DAX. Fare clic su hello **i filtri di riga** scheda, quindi selezionare una tabella, quindi fare clic su hello **filtro DAX** campo e quindi digitare una formula DAX.
  
6.  Fare clic su **Membri** > **Aggiungi esterno**.  
  
8.  In **Aggiungi membro esterno** immettere gli utenti o i gruppi nel tenant di Azure AD dall'indirizzo e-mail. Dopo avere fatto clic su OK e avere chiuso Gestione ruoli, i ruoli e i membri del ruolo vengono visualizzati in Esplora modelli tabulari. 
 
     ![Ruoli e utenti in Esplora modelli tabulari](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Distribuire il server Azure Analysis Services tooyour.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd o gestire ruoli e utenti in SQL Server Management Studio
tooadd ruoli e utenti tooa distribuita database modello, è necessario essere connessi toohello server come un amministratore del Server o già in un ruolo del database con autorizzazioni di amministratore.

1. In Esplora oggetti fare clic con il pulsante destro del mouse su **Ruoli** > **Nuovo ruolo**.

2. In **Crea ruolo** immettere il nome di un ruolo e una descrizione.

3. Selezionare un'autorizzazione.
   |Autorizzazione|Descrizione|  
   |----------------|-----------------|  
   |**Controllo completo (amministratore)**|I membri possono modificare schema del modello hello, elaborare ed eseguire query su tutti i dati.| 
   |**Elabora database**|I membri possono eseguire operazioni Elabora ed Elabora tutto. Non è possibile modificare lo schema del modello hello e non è possibile eseguire query sui dati.|  
   |**Lettura**|I membri possono eseguire query dati (in base ai filtri di riga), ma non è possibile modificare lo schema del modello hello.|  
  
4. Fare clic su **Appartenenza**, quindi immettere un utente o un gruppo nel tenant di Azure AD dall'indirizzo e-mail.

     ![Add user](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Se il ruolo di hello che si sta creando dispone dell'autorizzazione di lettura, è possibile aggiungere filtri di riga tramite una formula DAX. Fare clic su **i filtri di riga**, selezionare una tabella e quindi digitare una formula DAX in hello **filtro DAX** campo. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd ruoli e utenti usando uno script TMSL
È possibile eseguire uno script TMSL nella finestra XMLA di hello in SQL Server Management Studio o PowerShell. Hello utilizzare [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) comando e hello [ruoli](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) oggetto.

**Script di esempio del linguaggio di scripting del modello tabulare**

In questo esempio, un utente esterno B2B e un gruppo vengono aggiunti ruolo analista toohello con autorizzazioni di lettura per il database SalesBI hello. Entrambi hello utente esterno e gruppo deve trovarsi nello stesso tenant di Azure AD.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd ruoli e utenti tramite PowerShell
Hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) modulo fornisce database specifici di attività Gestione cmdlet e hello generiche cmdlet Invoke-ASCmd che accetta un query Tabular Model Scripting Language (TMSL) o uno script. Hello seguendo i cmdlet utilizzato per gestire utenti e ruoli del database.
  
|Cmdlet|Descrizione|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Aggiungere un ruolo del database membro tooa.| 
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Rimuove un membro da un ruolo del database.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Esegue uno script TMSL.|

## <a name="row-filters"></a>Filtri di riga  
I filtri di riga definiscono le righe di una tabella su cui i membri di uno specifico ruolo possono eseguire query. Vengono definiti per ogni tabella in un modello usando formule DAX.  
  
I filtri di riga possono essere definiti solo per i ruoli con le autorizzazioni Lettura e Lettura ed elaborazione. Per impostazione predefinita, se un filtro di riga non è definito per una determinata tabella, i membri possono eseguire una query tutte le righe nella tabella hello a meno che non applicato il filtro incrociato da un'altra tabella.
  
 I filtri di riga richiedono una formula DAX, che deve restituire tooa valore TRUE o FALSE, le righe di hello toodefine che i membri di tale particolare ruolo possono eseguire query. Impossibile recuperare le righe non incluse nella formula DAX hello. Ad esempio, hello tabella Customers con hello espressione i filtri di riga, seguente *= clienti [Paese] = 'USA'*, i membri del ruolo Sales hello è possono visualizzare solo i clienti in hello USA.  
  
I filtri di riga applicano toohello specificato righe e le righe correlate. Quando una tabella dispone di più relazioni, filtri si applicano la protezione per relazione hello che è attiva. I filtri di riga vengono intersecati con altri filtri di riga definiti per le tabelle correlate, ad esempio:  
  
|Table|Espressione DAX|  
|-----------|--------------------|  
|Region|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|Transazioni|=Transactions[Year]=2016|  
  
 effetto Hello è i membri possono eseguire una query le righe di dati in cui hello cliente si trova negli Stati Uniti hello, categoria di prodotto hello è quella delle biciclette e anno hello è 2016. Gli utenti non è possibile eseguire una query transazioni di fuori di Stati Uniti hello, transazioni che non sono biciclette o le transazioni non 2016 a meno che non sono membri di un altro ruolo che garantisce tali autorizzazioni.
  
 È possibile utilizzare il filtro di hello, *=FALSE()*, righe di tooall toodeny accesso per un'intera tabella.

## <a name="next-steps"></a>Passaggi successivi
  [Gestire gli amministratori di server](analysis-services-server-admins.md)   
  [Gestire Azure Analysis Services con PowerShell](analysis-services-powershell.md)  
  [Riferimento al Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

