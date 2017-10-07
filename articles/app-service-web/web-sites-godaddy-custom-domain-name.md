---
title: aaaConfigure un nome di dominio personalizzato in Azure App Service (GoDaddy)
description: Informazioni su come assegnare un nome toouse un dominio di GoDaddy con le app Web di Azure
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Configurare un nome di dominio personalizzato nel servizio app di Azure (acquistato direttamente da GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Se si hanno acquistato dominio tramite l'App Web di servizio App di Azure, vedere toohello passaggio finale della [acquistare dominio per le app Web](custom-dns-web-site-buydomains-web-app.md).

Questo articolo contiene istruzioni generiche sull'uso di un nome di dominio personalizzato acquistato direttamente da [GoDaddy](https://godaddy.com) con [App Web del servizio app](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Informazioni sui record DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Aggiunta di un record DNS per il dominio personalizzato
tooassociate il dominio personalizzato con un'app web nel servizio App, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite gli strumenti forniti da GoDaddy. Utilizzare i seguenti strumenti DNS hello toolocate di passaggi per GoDaddy.com hello

1. Accesso account tooyour con GoDaddy.com e selezionare **Account personale** e quindi **Manage my domains**. Menu di scelta rapida selezionare hello hello nome di dominio che si desidera toouse con l'app web di Azure e si seleziona **Manage DNS**.
   
    ![pagina del domino personalizzato per GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Da hello **i dettagli del dominio** pagina, scorrere toohello **File di zona DNS** scheda. Si tratta di sezione hello utilizzata per aggiungere e modificare i record DNS per il nome di dominio.
   
    ![Scheda DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Selezionare **Aggiungi Record** tooadd un record esistente.
   
    troppo**modifica** un record esistente, selezionare hello penna e carta accanto icona record hello.
   
   > [!NOTE]
   > Prima di aggiungere nuovi record, tenere presente che GoDaddy ha già creato i record DNS per i sottodomini più diffusi (denominati **Host** nell'editor), ad esempio **email**, **files**, **mail** e altri ancora. Se nome hello desiderato toouse già esiste, modificare record di hello esistente anziché crearne uno nuovo.
   > 
   > 
3. Quando si aggiunge un record, è necessario innanzitutto selezionare tipo di record di hello.
   
    ![select record type](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Successivamente, è necessario fornire hello **Host** (hello dominio personalizzato o sottodominio) e l'oggetto a cui **punta a**.
   
    ![add zone record](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Quando si aggiunge un **record (host)** -è necessario impostare hello **Host** campo tooeither  **@**  (rappresenta il nome di dominio radice, ad esempio  **Contoso.com**,) * (un carattere jolly per la corrispondenza più sottodomini,) o un sottodominio di hello desiderato toouse (ad esempio, **www**.) È necessario impostare hello **punta a** campo indirizzo IP toohello dell'app web di Azure.
   * Quando si aggiunge un **record CNAME (alias)** -è necessario impostare hello **Host** sottodominio del toohello campo desiderato toouse. ad esempio **www**. È necessario impostare hello **punta a** campo toohello **. azurewebsites.net** nome di dominio dell'applicazione web di Azure. Ad esempio, **contoso.azurewebsites.net**.
4. Fare clic su **Aggiungi utente**.
5. Selezionare **TXT** come tipo di record hello, quindi specificare un **Host** valore  **@**  e **punta a** valore  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Questo record TXT viene usato da Azure toovalidate che si è proprietari di dominio hello descritto da hello un record TXT primo record o hello. Dopo aver mappato toohello app web nel portale di Azure hello dominio hello, questa voce di record TXT può essere rimossi.
   > 
   > 
6. Quando si hanno completato l'aggiunta o la modifica di record, fare clic su **fine** toosave modifiche.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Abilitare il nome di dominio hello in app web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

