---
title: stringhe di filtro aaaConstructing per Progettazione tabelle hello | Documenti Microsoft
description: Creazione di stringhe di filtro per Progettazione tabelle hello
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Creazione di stringhe di filtro per hello Progettazione tabelle
## <a name="overview"></a>Panoramica
toofilter dati in una tabella di Azure che viene visualizzato in Visual Studio di hello **Progettazione tabelle**, si costruisce una stringa di filtro e immetterla nel campo filtro hello. sintassi della stringa di filtro Hello è definita da WCF Data Services hello ed è simile tooa clausola SQL WHERE, ma viene inviata toohello servizio tabella tramite una richiesta HTTP. Hello **Progettazione tabelle** handle hello codifica appropriata, quindi toofilter su un valore di proprietà desiderato, è necessario immettere solo nome della proprietà hello, operatore di confronto, valore dei criteri, e, facoltativamente, il filtro operatore booleano hello campo. Non è necessaria l'opzione query hello $filter tooinclude come se si costruisce una tabella di hello tooquery URL tramite hello [riferimento all'API REST di servizi di archiviazione](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Hello WCF Data Services si basa su hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Per informazioni dettagliate sull'opzione di query di sistema di filtro hello (**$filter**), vedere hello [specifica di convenzioni URI OData](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Operatori di confronto
Hello seguenti operatori logici sono supportati per tutti i tipi di proprietà:

| Operatore logico | Descrizione | Stringa di filtro di esempio |
| --- | --- | --- |
| eq |Uguale |Città eq "Redmond" |
| gt |Maggiore di |Prezzo gt 20 |
| ge |Maggiore o uguale troppo|Prezzo ge 10 |
| lt |Minore di |Prezzo lt 20 |
| le |Minore o uguale |Prezzo le 100 |
| ne |Diverso |Città ne "Londra" |
| e |e |Prezzo le 200 and Prezzo gt 3,5 |
| oppure |oppure |Prezzo le 3,5 or Prezzo gt 200 |
| not |not |not isAvailable |

Quando si crea una stringa di filtro, hello regole seguenti sono importanti:

* Utilizzare gli operatori logici di hello toocompare tooa valore della proprietà. Si noti che non è possibile toocompare tooa dinamica valore della proprietà; un lato dell'espressione hello deve essere una costante.
* Tutte le parti della stringa di filtro hello maiuscole e minuscole.
* valore costante Hello deve essere di hello del tipo di dati stesso come proprietà hello affinché hello filtro tooreturn valido risultati. Per ulteriori informazioni sui tipi di proprietà supportati, vedere [hello comprensione modello di dati del servizio tabelle](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Applicazione di filtri alle proprietà della stringa
Quando si filtra le proprietà della stringa, racchiudere la costante di stringa hello tra virgolette singole.

Hello seguendo i filtri di esempio hello **PartitionKey** e **RowKey** proprietà; chiave ulteriore proprietà anche possibile aggiungere la stringa di filtro toohello:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Anche se non è necessario, è possibile racchiudere ogni espressione di filtro tra parentesi:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Si noti che hello del servizio tabelle non supporta query con caratteri jolly non sono supportate sia in Progettazione tabelle hello. Tuttavia, è possibile eseguire utilizzando gli operatori di confronto sul prefisso desiderato hello di corrispondenza dei prefissi. Hello esempio seguente vengono restituite le entità con una proprietà LastName che inizia con la lettera hello 'A':

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Applicazione di filtri alle proprietà numeriche
toofilter su un numero intero o un numero a virgola mobile, specificare il numero di hello senza virgolette.

Questo esempio restituisce tutte le entità con una proprietà Age il cui valore è maggiore di 30:

    Age gt 30

Questo esempio vengono restituite tutte le entità con una proprietà AmountDue il cui valore è minore o uguale a too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Applicazione di filtri alle proprietà booleane
toofilter su un valore booleano, specificare **true** o **false** senza virgolette.

Hello esempio seguente restituisce tutte le entità in cui hello proprietà IsActive è impostata troppo**true**:

    IsActive eq true

È anche possibile scrivere questa espressione di filtro senza operatore logico hello. Nell'esempio seguente di hello, hello servizio tabella restituirà anche tutte le entità in cui IsActive è **true**:

    IsActive

tutte le entità in cui IsActive è false, è possibile utilizzare hello non tooreturn operatore:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Applicazione di filtri alle proprietà DateTime
toofilter su un valore DateTime, specificare hello **datetime** (parola chiave), seguita dalla costante data/ora hello tra virgolette singole. costante di data/ora Hello deve essere in formato UTC combinato, come descritto [la formattazione dei valori di proprietà DateTime](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Hello di esempio seguente restituisce le entità in proprietà CustomerSince hello è uguale tooJuly 10, 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
