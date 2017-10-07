---
title: aaaAdd SSL certificato app di Azure App Service tooyour | Documenti Microsoft
description: Informazioni su come tooadd SSL certificato tooyour app del servizio App.
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Acquistare e configurare un certificato SSL per il servizio app di Azure

In questa esercitazione, si intende proteggere l'app Web tramite l'acquisto di un certificato SSL per il  **[servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)**, archiviandolo in modo sicuro nell'[ Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associandolo a un dominio personalizzato.

## <a name="step-1---log-in-tooazure"></a>Passaggio 1 - Log in tooAzure

Accedi toohello portale di Azure all'indirizzo http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Passaggio 2: eseguire un ordine per un certificato SSL

È possibile inserire un ordine di certificato SSL creando un nuovo [certificato di servizio App](https://portal.azure.com/#create/Microsoft.SSL) In hello **portale di Azure**.

![Creazione del certificato](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Immettere un nome **nome** per il SSL di certificato e immettere hello **nome di dominio**

> [!NOTE]
> Si tratta di una delle parti principali di hello del processo di acquisto hello. Verificare che tooenter correggere il nome host (dominio personalizzato) che si desidera tooprotect con questo certificato. **NON** aggiungere il nome Host hello con WWW. 
>

Selezionare la **Sottoscrizione**, il **Gruppo di risorse** e lo **SKU del certificato**

> [!WARNING]
> Certificati di servizio App possono essere usati solo da altri servizi di App all'interno di hello stessa sottoscrizione.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Passaggio 3: Archivia certificato hello nell'insieme di credenziali chiave di Azure

> [!NOTE]
> Il [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) è un servizio di Azure che consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud.
>

Una volta hello acquisto di certificati SSL, è necessario tooopen [i certificati di servizio App](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) pannello della risorsa.

![inserire un'immagine di toostore pronto in KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Si noterà che lo stato di certificato **"Rilascio in sospeso"** vi sono alcuni altri passaggi toocomplete è necessario prima di iniziare a usare questo certificato.

Fare clic su **configurazione dei certificati** all'interno di pannello delle proprietà del certificato e fare clic su **passaggio 1: archivio** toostore questo certificato nell'insieme di credenziali chiave di Azure.

Da **lo stato dell'insieme di credenziali chiave** pannello, fare clic su **Repository dell'insieme di credenziali chiave** toochoose un toostore insieme di credenziali chiave esistente questo certificato **o creare nuovo insieme di credenziali chiave** toocreate nuova chiave dell'insieme di credenziali all'interno delle stesso gruppo di risorse e di sottoscrizione.

> [!NOTE]
> L' Azure Key Vault prevede addebiti minimi per l'archiviazione di questo certificato.
> Per altre informazioni, vedere **[Prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Dopo aver selezionato hello Repository dell'insieme di credenziali chiave toostore questo certificato, hello **archivio** opzione deve visualizzare l'esito positivo.

![inserimento immagine per la riuscita dell'archiviazione in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Passaggio 4: verificare hello proprietario del dominio

> [!NOTE]
> Esistono 3 tipi di verifica del dominio supportati da Certificati del servizio app: Domain, Mail, Manual Verification. Questi sono spiegati in dettaglio nell'hello [avanzate sezione](#advanced).

Da hello stesso **configurazione dei certificati** blade utilizzata nel passaggio 3, fare clic su **passaggio 2: verificare**.

**Verifica del dominio** si tratta di processo più semplice hello **solo se** è  **[acquistato il dominio personalizzato da servizio App di Azure.](custom-dns-web-site-buydomains-web-app.md)**
Fare clic su **verificare** pulsante toocomplete questo passaggio.

![inserimento immagine della verifica del dominio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Dopo aver fatto clic **verificare**, utilizzare hello **aggiornamento** pulsante finché hello **verificare** opzione deve visualizzare l'esito positivo.

![inserimento immagine per la riuscita della verifica in un Key Vault](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Passaggio 5: assegnare tooApp certificato del servizio App

> [!NOTE]
> Prima di eseguire i passaggi di hello in questa sezione, è necessario aver associato un nome di dominio personalizzato con l'app. Per altre informazioni, vedere **[Configurare un nome di dominio personalizzato nel servizio app di Azure.](app-service-web-tutorial-custom-domain.md)**
>

In hello  **[portale di Azure](https://portal.azure.com/)**, fare clic su hello **servizio App** opzione a sinistra di hello della pagina hello.

Fare clic sul nome hello di toowhich l'app si desidera tooassign questo certificato.

In hello **impostazioni**, fare clic su **i certificati SSL**.

Fare clic su **Importa certificato di servizio App** e certificato selezionare hello appena acquistato.

![inserimento immagine dell'importazione del certificato](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

In hello **associazioni ssl** sezione fare clic su **aggiungere associazioni**, utilizzare hello elenchi a discesa tooselect hello dominio nome toosecure con SSL e hello toouse certificato. È inoltre possibile selezionare se toouse  **[indicazione nome Server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o SSL basato su IP.

![inserimento immagine di associazioni SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Fare clic su **aggiungere un Binding** toosave hello modifiche e abilitare SSL.

> [!NOTE]
> Se si seleziona **SSL basato su IP** e il dominio personalizzato viene configurato usando un record A, è necessario eseguire passaggi aggiuntivi hello. Questi sono spiegati in dettaglio nell'hello [avanzate sezione](#Advanced).

A questo punto, si deve essere in grado di toovisit l'app utilizzando `HTTPS://` anziché `HTTP://` tooverify che hello certificato è stato configurato correttamente.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Passaggio 6: attività di gestione

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Avanzate

### <a name="verifying-domain-ownership"></a>Verifica della la proprietà del dominio

Esistono altri due tipi di verifica del dominio supportati da Certificati del servizio app: Mail e Manual Verification.

#### <a name="mail-verification"></a>Verifica tramite posta elettronica

Messaggio di verifica è stata inviata toohello che indirizzi di posta elettronica associato al dominio personalizzato.
passaggio di verifica tramite posta elettronica hello toocomplete, aprire il messaggio hello e fare clic sul collegamento di verifica hello.

![inserimento immagine della verifica dell'indirizzo di posta elettronica](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Se è necessario posta elettronica di verifica hello tooresend, fare clic su hello **invia di nuovo messaggio** pulsante.

#### <a name="manual-verification"></a>Verifica manuale

> [!IMPORTANT]
> Verifica della pagina Web HTML (funziona solo con lo SKU del certificato standard)
>

1. Creare un file HTML denominato **"starfield.html"**

1. Contenuto di questo file deve essere hello esatto nome di dominio verifica Token hello. (È possibile copiare il token hello da hello dominio verifica stato pannello)

1. Caricare questo file nella directory principale di hello del server web hello che ospita il dominio`/.well-known/pki-validation/starfield.html`

1. Fare clic su **aggiornamento** stato del certificato hello tooupdate dopo il completamento della verifica. Potrebbe richiedere alcuni minuti per toocomplete di verifica.

> [!TIP]
> Verificare in un terminal utilizzando `curl -G http://<domain>/.well-known/pki-validation/starfield.html` risposta hello deve contenere hello `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Verifica del record TXT DNS

1. Utilizzando il gestore DNS, creare un record TXT in hello `@` sottodominio con valore uguale toohello Token di verifica del dominio.
1. Fare clic su **"Aggiorna"** tooupdate hello stato del certificato dopo aver completata la verifica.

> [!TIP]
> È necessario un record TXT toocreate su `@.<domain>` con valore `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Assegnare tooApp certificato del servizio App

Se si seleziona **SSL basato su IP** e il dominio personalizzato viene configurato usando un record A, è necessario eseguire passaggi aggiuntivi hello:

Dopo aver configurato l'associazione SSL basata su un indirizzo IP, un indirizzo IP dedicato assegnato tooyour app. È possibile trovare questo indirizzo IP su hello **dominio personalizzato** pagina nelle impostazioni dell'app, proprio sopra hello **i nomi host** sezione. È elencato come **Indirizzo IP esterno**

![inserimento immagine di IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Si noti che questo indirizzo IP diverso indirizzo IP virtuale hello utilizzato in precedenza tooconfigure hello un record a per il dominio. Se la configurazione di toouse SSL basato su SNI o non sono configurati toouse SSL, questa voce è elencato alcun indirizzo.

Utilizzando gli strumenti di hello forniti dal registrar di nomi di dominio, modificare un record per l'indirizzo IP di toohello toopoint di nome dominio personalizzato dal passaggio precedente hello hello.

## <a name="rekey-and-sync-hello-certificate"></a>Reimpostazione delle chiavi e sincronizzazione hello certificato

Se avrai bisogno di tooRekey il certificato, selezionare **reimpostazione delle chiavi e sincronizzazione** opzione **proprietà certificato** Blade.

Fare clic su **reimpostazione** pulsante processo hello tooinitiate. Questo processo può richiedere toocomplete 1-10 minuti.

![inserimento immagine della reimpostazione SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Rigenerazione delle chiavi del certificato esegue il rollup certificato hello con un nuovo certificato rilasciato dall'autorità di certificazione hello.

## <a name="next-steps"></a>Passaggi successivi

* [Aggiungere una Rete per la distribuzione di contenuti (CDN)](app-service-web-tutorial-content-delivery-network.md)