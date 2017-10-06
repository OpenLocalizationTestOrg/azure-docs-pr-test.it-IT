---
title: aaaConfigure SSL per un servizio cloud | Documenti Microsoft
description: Informazioni su come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione. Questi esempi utilizzano hello portale di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configurazione di SSL per un'applicazione in Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [portale di Azure classico](cloud-services-configure-ssl-certificate.md)
>

La crittografia Secure Socket Layer (SSL) è il metodo di hello più comunemente usato per proteggere i dati inviati attraverso hello internet. Questa attività viene illustrato come toospecify un endpoint HTTPS per un ruolo web e come tooupload SSL certificato toosecure l'applicazione.

> [!NOTE]
> procedure di Hello in questa attività si applicano i servizi di Cloud tooAzure; per i servizi di App, vedere [questo](../app-service-web/web-sites-configure-ssl-certificate.md).
>

In questa attività viene usata una distribuzione di produzione. Alla fine di hello di questo argomento vengono fornite informazioni sull'utilizzo di una distribuzione di gestione temporanea.

Leggere [questo articolo](cloud-services-how-to-create-deploy-portal.md) se non è stato ancora creato un servizio cloud.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Passaggio 1: Ottenere un certificato SSL
tooconfigure SSL per un'applicazione, è innanzitutto necessario tooget un certificato SSL firmato da un'autorità di certificazione, una terza parte attendibile che rilascia certificati a questo scopo. Se non hai già uno, è necessario tooobtain da una società che vende i certificati SSL.

certificato Hello deve soddisfare i seguenti requisiti per i certificati SSL in Azure hello:

* certificato di Hello deve contenere una chiave privata.
* Hello certificato deve essere creato per lo scambio di chiave, esportabile tooa file di scambio di informazioni personali (PFX).
* Hello nome soggetto del certificato deve corrispondere il servizio cloud hello di hello dominio utilizzato tooaccess. È possibile ottenere un certificato SSL da un'autorità di certificazione (CA) per il dominio cloudapp.net hello. È necessario acquisire un toouse nome di dominio personalizzato durante l'accesso al servizio. Quando si richiede un certificato da un'autorità di certificazione, nome del soggetto del certificato hello deve corrispondere tooaccess nome di dominio personalizzato hello l'applicazione. Se ad esempio il nome di dominio personalizzato è **contoso.com**, il certificato da richiedere alla CA è ***.contoso.com** o **www.contoso.com**.
* certificato di Hello deve utilizzare almeno la crittografia a 2048 bit.

Per eseguire delle prove, è possibile [creare](cloud-services-certs-create.md) e usare un certificato auto firmato. Un certificato autofirmato non viene autenticato tramite un'autorità di certificazione e utilizza dominio cloudapp.net hello come URL del sito Web di hello. Ad esempio, hello attività seguente utilizza un certificato autofirmato in cui hello è il nome comune (CN) utilizzato nel certificato hello **sslexample.cloudapp.net**.

Successivamente, è necessario includere informazioni sul certificato hello nella definizione del servizio e i file di configurazione del servizio.

<a name="modify"></a>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Passaggio 2: Modificare il file di definizione e configurazione del servizio hello
L'applicazione deve essere certificato hello toouse configurata e deve essere aggiunto un endpoint HTTPS. Di conseguenza, hello definizione del servizio e i file di configurazione del servizio necessario toobe aggiornato.

1. Nell'ambiente di sviluppo, aprire il file di definizione del servizio (CSDEF) hello, aggiungere un **certificati** sezione all'interno di hello **WebRole** sezione e includono le seguenti informazioni hello il certificato (e i certificati intermedi):

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   Hello **certificati** sezione definisce il nome di hello di questo certificato, il percorso e nome hello dell'archivio di hello in cui si trova.

   Autorizzazioni (`permisionLevel` attributi) possa essere tooone set di hello seguenti valori:

   | Valore di autorizzazione | Descrizione |
   | --- | --- |
   | limitedOrElevated |**(Impostazione predefinita)**  Tutti i processi del ruolo possono accedere la chiave privata di hello. |
   | elevated |Solo i processi con privilegi elevati possono accedere la chiave privata di hello. |

2. Nel file di definizione del servizio, aggiungere un **InputEndpoint** elemento all'interno di hello **endpoint** sezione tooenable HTTPS:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. Nel file di definizione del servizio, aggiungere un **associazione** elemento all'interno di hello **siti** sezione. Questo elemento viene aggiunto un toomap associazione HTTPS del sito tooyour endpoint:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   Una volta completati tutti i file di definizione del servizio hello le modifiche necessarie toohello; Tuttavia, è necessario le informazioni sul certificato per il file di configurazione servizio hello tooadd hello.
4. Nel file di configurazione del servizio (CSCFG), ServiceConfiguration.Cloud.cscfg, aggiungere in **Certificates** un valore corrispondente al proprio certificato. Hello nell'esempio di codice seguente vengono fornite informazioni dettagliate di hello **certificati** sezione, tranne il valore di identificazione personale hello.

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(In questo esempio Usa **sha1** per l'algoritmo di identificazione digitale hello. Specifica valore appropriato di hello per l'algoritmo di identificazione personale del certificato).

Ora che sono stati aggiornati hello servizio definizione e il servizio file di configurazione, la distribuzione per il caricamento tooAzure del pacchetto. Se si usa **cspack**, non usare il flag **/generateConfigurationFile**, poiché questo sovrascriverebbe le informazioni del certificato appena inserite.

## <a name="step-3-upload-a-certificate"></a>Passaggio 3: Caricare un certificato
Connettersi toohello portale di Azure e...

1. In hello **tutte le risorse** sezione di hello portale, selezionare il servizio cloud.

    ![Pubblicare il servizio cloud](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Fare clic su **Certificati**.

    ![Fare clic sull'icona di certificati hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Fare clic su **caricare** nella parte superiore di hello dell'area di certificati hello.

    ![Fare clic sulla voce di menu caricamento hello](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Fornire hello **File**, **Password**, quindi fare clic su **caricare** nella parte inferiore di hello dell'area di immissione dati hello.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Passaggio 4: Connettere l'istanza del ruolo toohello tramite HTTPS
Ora che la distribuzione sia in esecuzione in Azure, è possibile connettersi tooit tramite HTTPS.

1. Fare clic su hello **URL del sito** tooopen browser web hello.

   ![Fare clic su hello URL del sito](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. Nel web browser, modificare hello collegamento toouse **https** anziché **http**e quindi visitare la pagina hello.

   > [!NOTE]
   > Se si utilizza un certificato autofirmato, quando si passa l'endpoint HTTPS tooan associato hello autofirmato che venga visualizzato un errore di certificato nel browser hello. L'utilizzo di un certificato firmato da un'autorità di certificazione attendibile Elimina questo problema. in hello frattempo, è possibile ignorare errore hello. (Un'altra opzione è l'archivio certificati Autorità di certificati attendibili dell'utente di tooadd hello certificato autofirmato toohello).
   >
   >

   ![Anteprima del sito](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Se si desidera toouse SSL per una distribuzione di gestione temporanea invece di una distribuzione di produzione, è prima necessario toodetermine hello URL utilizzato per la distribuzione di gestione temporanea hello. Una volta distribuito il servizio cloud, hello URL toohello ambiente di gestione temporanea è determinato dal hello **ID distribuzione** GUID nel formato seguente:`https://deployment-id.cloudapp.net/`  
   >
   > Creare un certificato con hello comune (CN) uguale toohello basato su GUID URL nome (ad esempio, **328187776e774ceda8fc57609d404462.cloudapp.net**). Utilizzare hello tooadd portale hello certificato tooyour di gestione temporanea del servizio cloud. Aggiungere quindi hello informazioni tooyour estensione CSCFG e CSDEF file di certificato, ricreare il pacchetto dell'applicazione e aggiornare il pacchetto di distribuzione di gestione temporanea toouse hello nuovo.
   >

## <a name="next-steps"></a>Passaggi successivi
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurare un [nome di dominio personalizzato](cloud-services-custom-domain-name-portal.md).
* [Gestire il servizio cloud](cloud-services-how-to-manage-portal.md).
