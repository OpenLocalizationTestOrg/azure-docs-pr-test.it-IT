---
title: aaaHow tooview correlati asset di dati in Azure Data Catalog | Documenti Microsoft
description: Questo articolo spiega come tooview correlati asset di dati di un asset di dati selezionato in Azure Data Catalog.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Correlazione asset di dati in Azure Data Catalog tooview?
Azure Data Catalog consente tooview dati asset correlati tooa selezionato dati asset e visualizzare le relazioni tra loro. 

## <a name="supported-data-sources"></a>Origini dati supportate 
Quando si registra l'asset di dati da hello seguenti origini dati, Azure Data Catalog registra automaticamente i metadati relativi a relazioni di join tra gli asset di dati hello selezionato. 

- SQL Server
- Database SQL di Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Visualizzare gli asset di dati correlati
tooview asset di dati che sono set di dati correlati tooa selezionato, utilizzare hello **relazioni** scheda come illustrato nella seguente immagine hello: 

![Azure Data Catalog - Visualizzare gli asset di dati correlati](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

In questo esempio sono presenti due relazioni per hello selezionato **ProductSubcategory** asset di dati: 

- Colonna ProductSubcategoryID della tabella Product hello ha una relazione di chiave esterna con ProductSubcategoryID colonna della tabella ProductSubcategory hello selezionato. 
- ProductCategoryID colonna della tabella ProductSubCategory hello ha una relazione di chiave esterna con ProductCategoryID colonna della tabella ProductCategory hello selezionato.

> [!NOTE]
> Si noti la direzione hello della freccia hello nella visualizzazione ad albero di relazioni hello.  

toosee ulteriori dettagli, ad esempio nome completo di hello della colonna hello, spostare il mouse di hello su e viene visualizzato un toohello simile popup seguente immagine: 

![Azure Data Catalog - Elemento popup della relazione](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relazioni tra gli asset che sono già stati registrati, registrare nuovamente tali risorse.

## <a name="next-steps"></a>Passaggi successivi
- [Come asset di dati toomanage](data-catalog-how-to-manage.md)
