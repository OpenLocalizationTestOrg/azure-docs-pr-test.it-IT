---
title: Outlook per Azure RemoteApp aaaUsing | Documenti Microsoft
description: Informazioni su come tooconfigure e utilizzare Outlook in Azure RemoteApp | Microsoft Azure
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Uso di Microsoft Outlook in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Azure RemoteApp supporta Microsoft Outlook O365. Altre informazioni sul [funzionamento di Office in Azure RemoteApp](remoteapp-officesubscription.md). Per l'uso di Outlook in Azure RemoteApp è opportuno adottare alcune impostazioni consigliate.

## <a name="cached-mode"></a>Modalità cache
La modalità cache è una configurazione consigliata per l'uso di Outlook in Azure RemoteApp. Quando si configura un toouse account Outlook 2013 modalità cache, Outlook 2013 funziona da una copia locale della cassetta postale di Microsoft Exchange dell'utente di hello archiviati in un file di dati offline (file OST) nel computer dell'utente hello, insieme a hello Rubrica non in linea (RUBRICA OFFLINE). cassetta postale memorizzati nella cache di Hello e Rubrica non in linea vengono aggiornate periodicamente da hello servizio Office 365. Altre informazioni sui [le differenze tra la modalità online e memorizzati nella cache di hello](https://technet.microsoft.com/library/jj683103.aspx).

Hello utente può selezionare **modalità cache** o **modalità Online** durante l'installazione di account o modificando le impostazioni dell'account hello. È inoltre possibile distribuire una modalità o altri hello utilizzando hello Office strumento personalizzazione () o criteri di gruppo.  

Vedere le [istruzioni dettagliate su come abilitare la modalità cache](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Search
In Azure RemoteApp, l'uso della ricerca all'interno di Outlook presenta alcune limitazioni. Azure RemoteApp utilizza le sessioni utente di tooaccommodate macchine virtuali in pool. L'indicizzazione di ricerca dipende dall'ID macchina hello, che è diverso per le macchine virtuali diverse. È possibile che ogni volta che un utente accede a RemoteApp di Azure, sono diretto tooa nuova macchina virtuale. Che comporterebbe, se si abilita ricerca locale, l'indicizzatore di hello verrà eseguito ogni volta che cambia di ID di macchina hello (quando l'utente hello è in una macchina virtuale di diversa). A seconda delle dimensioni di hello di hello. File OST, indicizzatore hello potrebbe richiedere un toocomplete molto tempo e usare le risorse necessarie per le altre app. La ricerca, quindi, può risultare lenta o non dare alcun risultato. Utilizzando un profilo di account in modalità Online potrebbe risolvere il problema, ma le prestazioni complessive risentirebbero a causa di mancanza di toohello di una cache locale (vedere hello collegamento sopra per ulteriori informazioni sulla differenza tra la modalità online e memorizzati nella cache di hello). Purtroppo, in Outlook 2013 non è possibile disabilitare la ricerca locale/indicizzata e abilitare la ricerca online per impostazione predefinita.

