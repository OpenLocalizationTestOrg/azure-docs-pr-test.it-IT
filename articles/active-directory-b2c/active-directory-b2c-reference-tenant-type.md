---
title: "Azure Active Directory B2C: aree di disponibilità e residenza dei dati | Microsoft Docs"
description: Un argomento sui tipi di hello di tenant di Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: aree di disponibilità e residenza dei dati
La residenza in dati e la disponibilità di area sono due concetti molto diversi che si applicano in modo diverso tooAzure AD B2C dal resto hello di Azure. In questo articolo verrà illustrano hello differenze tra questi due concetti e confrontare come si applica tooAzure e Azure Active Directory B2C.

## <a name="summary"></a>Riepilogo
Azure Active Directory B2C è **in genere disponibile in tutto il mondo** con l'opzione hello **residenza dati negli Stati Uniti o in Europa**.

## <a name="concepts"></a>Concetti
* **Disponibilità area** toowhere di fa riferimento un servizio è disponibile per l'utilizzo.
* **La residenza in dati** fa riferimento toowhere utente vengono archiviati.

## <a name="region-availability"></a>Aree di disponibilità
Azure Active Directory B2C è disponibile in tutto il mondo tramite hello cloud pubblico di Azure. 

Questo comportamento è diverso dal modello hello maggior parte degli altri eseguire servizi di Azure cui associare la disponibilità a residenza in dati. È possibile visualizzare esempi di questo tipo in entrambi Azure [prodotti disponibili per regione](https://azure.microsoft.com/regions/services/) pagina e hello [calcolatore dei costi di Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Residenza dei dati
Azure AD B2C archivia i dati utente negli Stati Uniti o in Europa.

La residenza dei dati viene determinata in base al paese e/o all'area geografica che viene selezionato durante [la creazione di un tenant Azure AD B2C](active-directory-b2c-get-started.md).

![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Dati si trovano negli Stati Uniti hello per hello seguente paesi/aree geografiche.

> Stati Uniti, Canada, Costa Rica, Repubblica dominicana, El Salvador, Guatemala, Messico, Panama, Portorico e Trinidad e Tobago

Dati si trovano in Europa per hello paesi seguenti:

> Algeria, Austria, Azerbaigian, Bahrain, Belarus, Belgio, Bulgaria, Croazia, Cipro, Repubblica ceca, Danimarca, Egitto, Estonia, Finlandia, Francia, Germania, Grecia, Ungheria, Islanda, Irlanda, Israele, Italia, Giordania, Kazakhstan, Kenya, Kuwait, Lettonia, Libano, Liechtenstein, Lituania, Lussemburgo, Ex Repubblica Jugoslava di Macedonia, Malta, Montenegro, Marocco, Paesi Bassi, Nigeria, Norvegia , Oman, Pakistan, Polonia, Portogallo, Qatar, Romania, Russia, Arabia Saudita, Serbia, Slovacchia, Slovenia, Sud Africa, Spagna, Svezia, Svizzera, Tunisia, Turchia, Ucraina, Emirati Arabi Uniti e Regno Unito.

Hello rimanenti paesi sono nel processo di hello dall'elenco toohello aggiunta.  Per il momento, è possibile utilizzare ancora Azure Active Directory B2C scegliendo hello paesi/aree precedente.

> Afghanistan, Argentina, Australia, Brasile, Cile, Colombia, Ecuador, Regione amministrativa speciale di Hong Kong, India, Indonesia, Iraq, Giappone, Corea, Malaysia, Nuova Zelanda, Paraguay, Perù, Filippine, Singapore, Sri Lanka, Taiwan, Thailandia, Uruguay e Venezuela.

## <a name="preview-tenant"></a>Tenant di anteprima
Se è stato creato un tenant B2C durante il periodo di anteprima di Azure AD B2C, è probabile che **Tipo di tenant** sia **Tenant di anteprima**. In caso di hello, è necessario utilizzare il tenant solo per scopi di sviluppo e test e non per le applicazioni di produzione.

> [!IMPORTANT]
> Non è un percorso di migrazione da un'anteprima tenant B2C di B2C tenant tooa scala di produzione. Si noti che si verificano problemi quando si elimina un tenant di anteprima B2C e ricreare il tenant B2C una scala di produzione hello stesso nome di dominio. Disporre di toocreate un tenant B2C scala di produzione con un nome di dominio diverso.


![Screenshot di un tenant di anteprima](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
