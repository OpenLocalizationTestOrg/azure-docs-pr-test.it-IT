---
title: aaaHow tooCreate un bilanciamento del carico interno ASE con Azure Resource Manager modelli | Documenti Microsoft
description: Informazioni su come toocreate un interno caricare ASE di bilanciamento del carico tramite modelli di gestione risorse di Azure.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Come tooCreate un bilanciamento del carico interno ASE utilizzando Azure modelli di gestione risorse

> [!NOTE] 
> Questo articolo è sull'ambiente del servizio App v1 hello. È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Panoramica
È possibile creare ambienti del servizio app con un indirizzo interno di rete virtuale anziché un indirizzo VIP pubblico.  Questo indirizzo interno è fornito da un componente Azure denominato servizio di bilanciamento del carico interno hello (ILB).  ASE un bilanciamento del carico interno può essere creata usando hello portale di Azure.  L'ambiente può anche essere creato con l'automazione, usando i modelli di Azure Resource Manager.  In questo articolo vengono illustrati i passaggi di hello e sintassi necessari toocreate ASE un bilanciamento del carico interno con modelli di gestione risorse di Azure.

L'automazione della creazione di un ambiente del servizio app con servizio di bilanciamento del carico interno prevede tre passaggi:

1. Primo ASE di base hello viene creato in una rete virtuale usando un indirizzo di bilanciamento del carico interno anziché un VIP pubblico.  Come parte di questo passaggio, un nome di dominio radice viene assegnato toohello ASE di bilanciamento del carico interno.
2. Dopo aver caricato hello che ase di bilanciamento del carico interno viene creato, un certificato SSL.  
3. Hello caricato certificato SSL viene assegnato esplicitamente toohello ASE di bilanciamento del carico interno come il proprio certificato SSL "default".  Questo certificato SSL da utilizzare per tooapps traffico SSL su hello ASE ILB quando hello App vengono risolti utilizzando hello comuni radice dominio assegnato toohello ASE (ad esempio https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Creazione di hello ASE di bilanciamento del carico interno di Base
Un modello di Azure Resource Manager di esempio e il file dei parametri associati sono disponibili in GitHub [qui][quickstartilbasecreate].

La maggior parte dei parametri di hello in hello *azuredeploy.parameters.json* file sono comuni toocreating entrambi ASEs di bilanciamento del carico interno, nonché ASEs associato VIP pubblico tooa.  Hello elenco riportato di seguito chiama un'attenzione particolare i parametri out o che sono univoci, quando si crea un ASE di bilanciamento del carico interno:

* *interalLoadBalancingMode*: nella maggior parte dei casi, impostare questo too3, ovvero sia il traffico sulle porte 80/443 HTTP/HTTPS, e le porte canale dati di controllo/hello resta in attesa del servizio FTP hello tooby su hello ASE, verranno associati tooan ILB allocate rete virtuale indirizzo interno.  Se questa proprietà è invece impostata too2, hello solo il servizio FTP relative porte (canali di controllo e i dati) verranno associate indirizzo tooan ILB, mentre il traffico HTTP/HTTPS hello rimarrà sul VIP pubblico hello.
* *suffisso DNS*: questo parametro definisce dominio di radice hello predefinito che verrà assegnato ASE toohello.  Nella variante pubblica di hello del servizio App di Azure, dominio radice di hello predefinito per tutte le app web è *azurewebsites.net*.  Tuttavia, poiché la rete virtuale del cliente interno tooa ASE un bilanciamento del carico interno, può non essere dominio di radice del servizio di rilevamento toouse hello pubblico predefinito.  Un ambiente del servizio app con servizio di bilanciamento del carico interno deve invece avere un dominio radice predefinito appropriato per la rete virtuale interna dell'azienda.  Ad esempio, un ipotetico di Contoso Corporation potrebbe utilizzare un dominio radice predefinito di *contoso.com interna* per le app che sono previsti tooonly sia risolvibile e accessibile in rete virtuale di Contoso. 
* *ipSslAddressCount*: questo parametro viene automaticamente impostato come valore predefinito tooa valore pari a 0 in hello *azuredeploy.json* file perché il bilanciamento del carico interno ASEs avere solo un singolo indirizzo di bilanciamento del carico interno.  Nessun indirizzo IP SSL esplicita per ASE un bilanciamento del carico interno e pertanto il pool di indirizzi IP SSL per un bilanciamento del carico interno di ASE hello deve essere impostato toozero, in caso contrario si verificherà un errore di provisioning. 

Una volta hello *azuredeploy.parameters.json* file è stato compilato per ASE un bilanciamento del carico interno, hello ASE ILB può quindi essere creato utilizzando hello seguente frammento di codice di Powershell.  Modificare hello toomatch di percorsi di file in cui risiedono i file di modello di hello Azure Resource Manager nel computer.  Ricordare anche toosupply i propri valori per nome della distribuzione Azure Resource Manager hello e nome del gruppo di risorse.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Dopo aver hello Azure Resource Manager modello inviato che richiederà alcune ore per hello ASE ILB toobe creato.  Una volta completata la creazione di hello, hello ASE ILB verrà visualizzati nel portale di hello UX nell'elenco di hello degli ambienti di servizio App per la sottoscrizione di hello che ha attivato la distribuzione di hello.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Caricamento e la configurazione hello "Default" certificato SSL
Una volta hello che ase di bilanciamento del carico interno viene creato, un certificato SSL deve essere associato a ASE hello come l'uso di certificati SSL predefinita"hello" per stabilire tooapps connessioni SSL.  Continuare l'esempio di Contoso Corporation ipotetico hello, hello del ASE predefinito DNS suffisso è *contoso.com interna*, quindi una connessione troppo*https://some-random-app.internal-contoso.com*richiede un certificato SSL valido per **.internal contoso.com*. 

Esistono diversi modi tooobtain un certificato SSL valido inclusi autorità di certificazione interne, acquistare un certificato da un'autorità di certificazione esterna e l'utilizzo di un certificato autofirmato.  Indipendentemente dall'origine hello del certificato SSL di hello, hello seguenti attributi di certificato necessario toobe configurato correttamente:

* *Oggetto*: questo attributo deve essere impostato troppo **.your-radice-dominio-here.com*
* *Nome alternativo del soggetto*: questo attributo deve includere entrambe **.your-radice-dominio-here.com*, e **.scm.your-radice-dominio-here.com*.  motivo per la seconda voce hello Hello è tale toohello connessioni SSL sito SCM/Kudu associato a ogni app verrà effettuata utilizzando un indirizzo del modulo hello *your-app-name.scm.your-root-domain-here.com*.

Dopo aver ottenuto un certificato SSL valido sono necessari altri due passaggi preliminari.  certificato SSL Hello deve toobe convertito/salvato come file con estensione pfx.  Tenere presente il file con estensione pfx hello deve tooinclude tutti intermedi e i certificati radice e deve inoltre toobe protetto da password.

File con estensione pfx risultante hello deve quindi toobe convertito in una stringa base64 perché verrà caricato il certificato SSL hello utilizzando un modello di gestione risorse di Azure.  Poiché i modelli di gestione risorse di Azure sono file di testo, file con estensione pfx hello deve toobe convertito in una stringa base 64 in modo che può essere incluso come un parametro di modello hello.

frammento di codice Powershell Hello seguente viene illustrato un esempio di generazione di un certificato autofirmato, esportazione hello certificato come file con estensione pfx, conversione di file con estensione pfx hello in base 64 in una stringa codificata e salvando hello base64 codifica file separato tooa di stringa.  Hello codice di Powershell per la codifica base64 è stata adattata dall'hello [Blog di script di Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Una volta certificato SSL hello è stata generata e stringa con codifica base64 tooa convertito, hello modello di esempio di gestione risorse di Azure su GitHub per [configurazione certificato SSL predefinito di hello] [ configuringDefaultSSLCertificate] può essere utilizzato.

i parametri in hello Hello *azuredeploy.parameters.json* file sono elencati di seguito:

* *appServiceEnvironmentName*: nome hello di hello ASE ILB da configurare.
* *existingAseLocation*: stringa di testo contenente hello regione di Azure in cui hello ASE di bilanciamento del carico interno è stato distribuito.  Ad esempio "Stati Uniti centro-meridionali".
* *pfxBlobString*: hello based64 codificato rappresentazione di stringa del file con estensione pfx hello.  Tramite il frammento di codice hello illustrato in precedenza, si sarebbe copiare hello stringa contenuto in "exportedcert.pfx.b64" e incollarlo come valore di hello di hello *pfxBlobString* attributo.
* *password*: file con estensione pfx hello toosecure hello password utilizzata.
* *certificateThumbprint*: hello identificazione personale del certificato.  Se si recupera il valore da Powershell (ad esempio *$certificate. Identificazione personale* da hello frammento di codice precedente), è possibile utilizzare il valore di hello come-è.  Se si copia il valore di hello dalla finestra di dialogo certificato Windows hello, tenere presente, tuttavia toostrip out spazi hello.  Hello *certificateThumbprint* dovrebbe essere simile al seguente: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *Nomecertificato*: un identificatore di stringa di propria scelta utilizzato certificato hello tooidentity.  nome di Hello viene utilizzato come parte di gestione risorse di Azure identificatore hello per hello *Microsoft.Web/certificates* entità che rappresenta il certificato SSL hello.  nome Hello **deve** terminare con hello successivo suffisso: \_yourASENameHere_InternalLoadBalancingASE.  Il suffisso viene utilizzato dal portale hello come un indicatore che hello certificato viene utilizzato per proteggere un ASE abilitata al bilanciamento del carico interno.

Un esempio abbreviato di *azuredeploy.parameters.json* è illustrato di seguito:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Una volta hello *azuredeploy.parameters.json* file è stato compilato, il certificato SSL predefinito di hello può essere configurato tramite hello seguente frammento di codice di Powershell.  Modificare hello toomatch di percorsi di file in cui risiedono i file di modello di hello Azure Resource Manager nel computer.  Ricordare anche toosupply i propri valori per nome della distribuzione Azure Resource Manager hello e nome del gruppo di risorse.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Dopo aver hello Azure Resource Manager modello inviato che richiederà circa 40 minuti minuti per modifica di hello ASE tooapply front-end.  Ad esempio, con valore predefinito è ASE dimensioni utilizzando due server front-end, modello hello richiederà intorno a un'ora e toocomplete di venti minuti.  Durante l'esecuzione di modello hello hello ASE non saranno in grado di tooscaled.  

Dopo aver completato il modello di hello, App in hello ASE di bilanciamento del carico interno è possibile accedere tramite HTTPS e le connessioni hello verranno protetti tramite certificato SSL di hello predefinito.  certificato SSL di Hello predefinito da utilizzare quando le app su hello ASE di bilanciamento del carico interno vengono risolti utilizzando una combinazione del nome dell'applicazione hello e nome host predefinito hello.  Ad esempio *https://mycustomapp.internal-contoso.com* utilizzerà il certificato SSL predefinito di hello per **.internal contoso.com*.

Tuttavia, come App in esecuzione nel servizio multi-tenant pubblico di hello, gli sviluppatori possono inoltre configurare i nomi host personalizzati per singole App e quindi configurare le associazioni certificato SNI SSL univoche per le singole applicazioni.  

## <a name="getting-started"></a>introduttiva
tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione dell'ambiente del servizio](app-service-app-service-environment-intro.md)

Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

