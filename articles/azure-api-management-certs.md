---
title: aaaUpload un certificato API di gestione di Azure | Documenti Microsoft
description: Informazioni su come il convertitore tooupload API di gestione del certificato per hello portale classico di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Caricare un certificato di gestione dell'API di gestione di Azure
I certificati di gestione consentono tooauthenticate con modello di distribuzione classica hello fornita da Azure. Molti programmi e strumenti (ad esempio Visual Studio o hello Azure SDK) di utilizzare questi configurazione tooautomate dei certificati e la distribuzione dei vari servizi di Azure. 

> [!WARNING]
> Fare attenzione. Questi tipi di certificati consentono di qualsiasi utente che esegue l'autenticazione con le sottoscrizioni di hello toomanage sono associate.
>
>

Se servono altre informazioni sui certificati di Azure, compresa la creazione di un certificato autofirmato, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

È inoltre possibile utilizzare [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate codice client per scopi di automazione.

## <a name="upload-a-management-certificate"></a>Creare un certificato di gestione
Una volta che si disponga di un certificato di gestione creato (file con estensione cer con solo una chiave pubblica hello) è possibile caricarlo nel portale di hello. Quando è disponibile nel portale di hello certificato di hello, chiunque disponga di un certificato corrispondente (chiave privata) può connettersi tramite hello API di gestione e accesso hello risorse per la sottoscrizione associata hello.

1. Accedi toohello [portale di Azure](http://portal.azure.com).
2. Fare clic su **più servizi** elenco di servizi di Azure hello inferiore, quindi selezionare **sottoscrizioni** in hello _generale_ gruppo del servizio.

    ![Menu Sottoscrizioni](./media/azure-api-management-certs/subscriptions_menu.png)

3. Assicurarsi che tooselect hello corretto sottoscrizione che si desidera tooassociate con certificato hello.     
4. Dopo aver selezionato la sottoscrizione corretta hello, premere **i certificati di gestione** in hello _impostazioni_ gruppo.

    ![Impostazioni](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Hello premere **caricare** pulsante.

    ![Caricamento nella pagina Certificati](./media/azure-api-management-certs/certificates_page.png)
6. Compila informazioni di finestra di dialogo hello e premere **caricare**.

    ![Impostazioni](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un certificato di gestione associato a una sottoscrizione, è possibile (dopo aver installato hello corrispondente certificato in locale) a livello di programmazione connettersi toohello [API REST del modello di distribuzione classica](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizzare Hello varie risorse di Azure che sono anche associate alla sottoscrizione.
