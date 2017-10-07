---
title: aaaSizing informazioni per una rete virtuale in Azure RemoteApp | Documenti Microsoft
description: Informazioni sui requisiti di indirizzo IP di hello per Azure RemoteApp in esecuzione con una rete virtuale
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informazioni sul ridimensionamento di una rete virtuale in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Quando si usa Azure RemoteApp con una rete virtuale (VNET), RemoteApp Usa gli indirizzi IP in subnet hello. In base alla scala di hello del servizio di RemoteApp, è necessario che la subnet disponga di indirizzi IP sufficienti per le macchine virtuali RemoteApp tooensure. Queste indicazioni di ridimensionamento non sono complete se si osserva in che modo RemoteApp esegue dinamicamente lo spin-up e lo spin-down delle macchine virtuali all'interno di una raccolta, tuttavia consentono di stimare l'intervallo di subnet. Ciò è particolarmente importante perché, dopo un servizio di RemoteApp è posizionato in una rete virtuale, non è possibile aumentare la dimensione della subnet hello senza rimuovere RemoteApp.

Per ogni raccolta RemoteApp che si desidera toorun alla capacità massima, è necessario 100 gli indirizzi IP disponibili. Ad esempio, se si dispone di una raccolta RemoteApp nel piano Standard hello e si desidera toohave hello massimo 500 utenti, è necessario 100 indirizzi IP per la raccolta. Analogamente, è necessario 100 indirizzi IP per una raccolta RemoteApp nel piano base hello dotato di 800 utenti. Se si prevede di toohave un numero di utenti (minore di hello massima), è possibile ridurre gli indirizzi IP hello necessari per ogni raccolta. requisiti relativi alla dimensione minima subnet Hello sono 30 indirizzi IP (/ 27).

Estrarre hello dopo che la rete virtuale sia configurata con informazioni toomake e funziona correttamente:

* [Eseguire la migrazione da un tooan di rete virtuale personale rete virtuale di Azure](remoteapp-migratevnet.md)
* [Convalidare hello toouse di rete virtuale di Azure con Azure RemoteApp](remoteapp-vnet.md)

