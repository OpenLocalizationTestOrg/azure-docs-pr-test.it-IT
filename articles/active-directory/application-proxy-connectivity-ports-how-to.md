---
title: aaaHow tooopen hello le porte del firewall necessarie per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: Scoprire quali tooopen porte per toowork Proxy dell'applicazione hello Azure AD correttamente
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Come tooopen hello porte del firewall necessarie per un'applicazione Proxy dell'applicazione

toosee un elenco completo delle porte necessarie hello e la funzione hello di ciascuna porta, vedere sezione Prerequisiti hello hello [documentazione del Proxy di applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Si noti che il Proxy di applicazione usa solo le porte in uscita.

È inoltre possibile verificare se è aperta tutti hello necessarie porte da aprire hello [strumento di Test porte connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) dalla rete locale. La presenza di più segni di spunta verdi indica una maggiore resilienza. 

## <a name="app-proxy-regions"></a>Aree del proxy dell'applicazione

Stiamo lavorando in un modo toolet si conosce quali di queste aree deve toobe verde per l'utente. Per il momento, assicurarsi che tutte siano verdi. Anche l'area Stati Uniti centrali è necessaria indipendentemente dall'area in cui ci si trova.

toomake che hello strumento offre hello risultati corretti, assicurarsi di:

-   Aprire lo strumento hello in un browser dal server hello in cui è stato installato connettore hello.

-   Verificare che qualsiasi tooyour applicabile proxy o firewall connettore vengono anche applicate toothis pagina. Questa operazione può essere eseguita in Internet Explorer passando troppo**impostazioni**  - &gt; **Opzioni Internet**  - &gt; **connessioni**  - &gt; **Impostazioni Lan**. In questa pagina viene visualizzato il campo di hello "Usa un Proxy Server per il LAN". Selezionare questa casella e inserire l'indirizzo del proxy hello nel campo "Address" hello.

## <a name="next-steps"></a>Passaggi successivi
[Comprendere i connettori del proxy applicazione Azure AD](application-proxy-understand-connectors.md)
