---
title: aaa "abilitare HTTPS in un dominio personalizzato CDN di Azure | Documenti di Microsoft"
description: Informazioni su come tooenable HTTPS nell'endpoint rete CDN di Azure con un dominio personalizzato.
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Abilitare HTTPS in un dominio personalizzato della rete CDN di Azure

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Supporto HTTPS per i domini personalizzati rete CDN di Azure consente toodeliver contenuto protetto tramite SSL utilizzando la propria sicurezza di hello tooimprove nome dominio dei dati in transito. Hello end-to-end del flusso di lavoro tooenable HTTPS per il dominio personalizzato è semplificata tramite un solo clic abilitazione, la gestione dei certificati completato e tutti i dati con senza alcun costo aggiuntivo.

È critico tooensure sulla privacy di hello e l'integrità dei dati di tutti i dati sensibili di applicazioni web in transito. Utilizzando il protocollo HTTPS garantisce che i dati sensibili vengono crittografati quando vengono inviate in hello hello internet. Assicura attendibilità, autenticazione e protezione delle applicazioni Web da attacchi. La rete CDN di Azure supporta attualmente il protocollo HTTPS su un endpoint della rete CDN. Ad esempio, se si crea un endpoint CDN dalla rete CDN di Azure, ad esempio https://contoso.azureedge.net, il protocollo HTTPS è abilitato per impostazione predefinita. A questo punto, con la funzionalità HTTPS per il dominio personalizzato è possibile anche abilitare la distribuzione sicura per un dominio personalizzato, ad esempio https://www.contoso.com. 

Alcuni degli attributi della chiave hello di funzionalità HTTPS sono:

- Assenza di costi aggiuntivi: non sono previsti costi per l'acquisizione o il rinnovo di certificati o per il traffico HTTPS. Si paga solo per GB in uscita dalla rete CDN hello.

- Abilitazione della semplice: il provisioning di un clic è disponibile da hello [portale di Azure](https://portal.azure.com). È inoltre possibile utilizzare API REST o altre funzionalità di hello tooenable strumenti per sviluppatori.

- Gestione completa dei certificati: tutta la fase di approvvigionamento e gestione di certificati viene gestita automaticamente. I certificati vengono automaticamente il provisioning e rinnovato tooexpiration precedente. Questo rimuove completamente rischi hello dell'interruzione del servizio a causa della scadenza di un certificato.

>[!NOTE] 
>Supporta HTTPS tooenabling precedente, è necessario avere già stabilito un [dominio personalizzato CDN Azure](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Passaggio 1: Abilitare la funzionalità di hello 

1. In hello [portale di Azure](https://portal.azure.com), Sfoglia Verizon tooyour standard o premium profilo CDN.

2. Nell'elenco di hello degli endpoint, fare clic sull'endpoint hello contenente il dominio personalizzato.

3. Fare clic su dominio di hello personalizzato per il quale si desidera tooenable HTTPS.

    ![Pannello Endpoint](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Fare clic su **su** tooenable HTTPS e salvare la modifica hello.

    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Passaggio 2: convalida del dominio

>[!IMPORTANT] 
>Prima che la funzionalità HTTPS sia attiva nel dominio personalizzato, è necessario completare la convalida del dominio. Si dispone di 6 business giorni tooapprove hello dominio. La richiesta verrà annullata se non si riceve l'approvazione entro 6 giorni lavorativi.  

Dopo aver abilitato HTTPS nel dominio personalizzato, il provider del certificato HTTPS DigiCert convaliderà la proprietà del dominio, contattare la persona hello per il dominio, in base alle informazioni di persona WHOIS, tramite posta elettronica (per impostazione predefinita) o telefono. DigiCert anche invierà hello verifica posta elettronica toohello sotto indirizzi. Se le informazioni sui registranti WHOIS sono private, assicurarsi di poterle approvare direttamente da uno di questi indirizzi.

>admin@<your-domain-name.com> administrator@<your-domain-name.com>  
>webmaster@<your-domain-name.com>  
>hostmaster@<your-domain-name.com>  
>postmaster@<your-domain-name.com>


Alla ricezione di posta elettronica hello, sono disponibili due opzioni di verifica:

1. È possibile approvare tutte le future ordini tramite hello stesso account per hello stesso dominio radice, ad esempio consoto.com. Questo è un approccio consigliato se si intende tooadd ulteriori domini personalizzati in futuro per hello hello nello stesso dominio radice.
 
2. È possibile approvare solo nome host specifico hello utilizzato in questa richiesta. Le richieste successive richiederanno un'approvazione aggiuntiva.

    Posta elettronica di esempio:
    
    ![Finestra di dialogo HTTPS personalizzato](./media/cdn-custom-ssl/domain-validation-email-example.png)

Dopo l'approvazione, DigiCert verrà aggiunto il certificato di SAN toohello nome dominio personalizzato. il certificato Hello sarà valido per un anno e venga automaticamente rinnovato prima della scadenza.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Passaggio 3: Attendere per la propagazione di hello quindi iniziare a usare le funzionalità

Al termine della convalida di nome di dominio hello richiederà too6 8 ore per hello dominio personalizzato HTTPS funzionalità toobe attivo. Una volta completato il processo di hello, lo stato di "HTTPS personalizzati" hello in hello portale di Azure verrà impostato troppo "Enabled". La funzionalità HTTPS con il dominio personalizzato è ora pronta per l'uso.

## <a name="frequently-asked-questions"></a>Domande frequenti

1. *Chi è il provider certificate hello e viene utilizzato il tipo di certificato?*

    Viene usato il certificato dei nomi alternativi soggetto (SAN) fornito da DigiCert. Un certificato SAN può proteggere più nomi di dominio completi con un certificato.

2. *È possibile usare il certificato dedicato personale?*
    
    Non attualmente, ma è on hello Guida di orientamento.

3. *Cosa accade se non si riceve posta elettronica di verifica dominio hello da DigiCert?*

    Se non si riceve un messaggio di posta elettronica entro 24 ore, contattare Microsoft.

4. *L'uso di un certificato SAN è meno sicuro rispetto a un certificato dedicato?*
    
    Un certificato SAN segue hello standard di crittografia e protezione stesso come un certificato dedicato. Tutti i certificati SSL emessi usano l'algoritmo SHA-256 per la protezione avanzata di server.

5. *È possibile usare la funzionalità HTTPS del dominio personalizzato con la rete CDN di Azure fornita da Akamai?*

    Attualmente questa funzionalità è disponibile solo con la rete CDN di Azure fornita da Verizon. Stiamo lavorando sul supporto di questa funzionalità con la rete CDN Azure da Akamai nei prossimi mesi hello.


## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come tooset backup un [dominio personalizzato per l'endpoint rete CDN di Azure](./cdn-map-content-to-custom-domain.md)


