---
ms.assetid: 
title: ambienti di sicurezza separati insieme di credenziali chiave aaaAzure | Documenti Microsoft
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Scenari di sicurezza di Azure Key Vault e confini geografici

Azure Key Vault è un servizio multi-tenant e usa un pool di moduli di protezione Hardware (HSM) in ogni posizione di Azure. 

Tutti i moduli di protezione hardware in Azure posizioni hello stessa area geografica condividono hello stesso limite di crittografia (ambiente di sicurezza Thales). Stati Uniti orientali e condividere Stati Uniti occidentali, ad esempio, hello stesso ambiente di sicurezza perché appartengono località geografica toohello Stati Uniti. Analogamente, tutte le posizioni di Azure nella condivisione Giappone hello world protezione stesso e tutte le posizioni di Azure in Australia, India e così via. 

## <a name="backup-and-restore-behavior"></a>Comportamento di backup e ripristino

Un backup di una chiave da un insieme di credenziali chiave in una località di Azure può essere ripristinato tooa insieme di credenziali delle chiavi in un altro percorso di Azure, purché entrambe queste condizioni sono vere:

- Entrambi hello Azure percorsi appartengono toohello stessa area geografica
- Entrambi gli insiemi di credenziali chiave hello appartengono toohello stessa sottoscrizione di Azure

Ad esempio, un backup eseguito da una specifica sottoscrizione di una chiave in un insieme di credenziali chiave India occidentale, può essere solo insieme di credenziali chiave tooanother ripristinato in hello stessa sottoscrizione e posizione geografica. India occidentale, India centrale o India meridionale.

## <a name="regions-and-products"></a>Aree e prodotti

- [Aree di Azure](https://azure.microsoft.com/regions/)
- [Prodotti Microsoft in base all'area](https://azure.microsoft.com/regions/services/)

Le aree sono mappate toosecurity mondi, visualizzati come intestazioni principale nelle tabelle di hello:

Prodotti hello dall'articolo area, ad esempio, hello **Americas** scheda contiene est US, Stati Uniti centrali, Stati Uniti OCCIDENTALI tutti i mapping toohello Americas area. 

>[!NOTE]
>Un'eccezione è che il Dipartimento della difesa Stati Uniti orientali e il Dipartimento della difesa Stati Uniti centrali hanno i propri scenari di sicurezza. 

Analogamente, sul hello **Europe** scheda, Europa settentrionale ed Europa occidentale eseguono entrambi il mapping area Europa toohello. Hello stesso vale anche nel hello **Asia-Pacifico** scheda.



