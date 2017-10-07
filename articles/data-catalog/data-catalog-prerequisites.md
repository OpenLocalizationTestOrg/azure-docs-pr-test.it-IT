---
title: prerequisiti di catalogo dati aaaAzure | Documenti Microsoft
description: "Informazioni sui prerequisiti di hello che è necessario tooget avviato con Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Prerequisiti del Catalogo dati di Azure

È necessario tootake cure alcuni aspetti prima di configurare Azure Data Catalog. che però non richiedono molto tempo.

## <a name="azure-subscription"></a>Sottoscrizione di Azure
tooset catalogo dati, è necessario essere proprietario di hello o Comproprietario di una sottoscrizione di Azure.

Le sottoscrizioni di Azure consentono di organizzare toocloud-service di accedere alle risorse, ad esempio catalogo dati. Le sottoscrizioni consentono anche di controllare come l'utilizzo delle risorse viene segnalato, fatturato e pagato. Ogni sottoscrizione può avere un metodo di fatturazione e pagamento distinto e avere così sottoscrizioni e piani diversi per reparto, progetto, ufficio locale e così via. Ogni servizio cloud appartiene tooa sottoscrizione ed è necessario toohave una sottoscrizione prima di impostare il catalogo dati. vedere, più toolearn [gestire account, sottoscrizioni e ruoli amministrativi](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset catalogo dati, è necessario essere connessi con un account utente di Azure Active Directory (Azure AD).

Azure AD fornisce un modo semplice per le identità di business toomanage e l'accesso, sia nel cloud hello e locali. Gli utenti possono utilizzare un singolo account aziendale o dell'istituto di istruzione per il cloud tooany single sign-in e applicazione web locale. Catalogo dati utilizza Azure AD tooauthenticate Accedi. vedere, più toolearn [che cos'è Azure Active Directory?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Utilizzando hello [portale di Azure](http://portal.azure.com/), è possibile accedere con un account Microsoft personale o di Azure Active Directory di lavoro o scuola account. tooset catalogo dati utilizzando sia hello portale di Azure o hello [portale catalogo dati](http://www.azuredatacatalog.com), è necessario accedere con un account di Azure Active Directory, non un account personale.
>
>

## <a name="active-directory-policy-configuration"></a>Configurazione dei criteri di Azure Active Directory
Si potrebbe verificarsi una situazione in cui è possibile accedere al portale di catalogo dati toohello, ma quando si tenta di toosign nello strumento di registrazione origine dati toohello, che si verifichi un messaggio di errore che impedisce l'accesso. Il comportamento di questo problema potrebbe verificarsi solo quando si è nella rete aziendale hello o potrebbe verificarsi solo quando si connette da una rete aziendale esterna hello.

strumento di registrazione di origine dati Hello utilizza l'autenticazione basata su form toovalidate le credenziali dell'utente in Active Directory. toohelp che accedi correttamente, un amministratore di Active Directory deve abilitare autenticazione basata su form in hello criteri di autenticazione globali.

In Criteri di autenticazione globali hello, metodi di autenticazione possono essere abilitate separatamente per la rete intranet ed extranet connessioni, come illustrato nella seguente schermata hello. Se l'autenticazione basata su form non è abilitato per la rete hello da cui si esegue la connessione, potrebbero verificarsi errori di accesso.

 ![Criteri di autenticazione globali di Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).
