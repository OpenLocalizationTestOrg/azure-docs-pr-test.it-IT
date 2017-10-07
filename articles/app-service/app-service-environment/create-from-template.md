---
title: aaaCreate un ambiente del servizio App di Azure tramite un modello di gestione risorse
description: Viene illustrato come toocreate un ambiente esterno o servizio di bilanciamento del carico interno Azure App usando un modello di gestione risorse
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Creare un ambiente del servizio app usando un modello di Azure Resource Manager

## <a name="overview"></a>Panoramica
È possibile creare gli ambienti del servizio app di Azure con un endpoint accessibile da Internet o un endpoint di un indirizzo interno di una rete virtuale di Azure. Quando viene creato con un endpoint interno, tale endpoint dispone di un componente Azure denominato servizio di bilanciamento del carico interno (ILB). Hello ASE su un indirizzo IP interno viene chiamato un ASE di bilanciamento del carico interno. Hello ASE con un endpoint pubblico viene chiamato un ASE esterno. 

È possibile creare un ASE utilizzando hello portale di Azure o un modello di gestione risorse di Azure. In questo articolo vengono illustrati i passaggi di hello e la sintassi è necessario toocreate un ASE esterno o bilanciamento del carico interno ASE con modelli di gestione risorse. toolearn toocreate un ASE in hello portale di Azure, vedere [rendere un ASE esterno] [ MakeExternalASE] o [rendere ASE un bilanciamento del carico interno][MakeILBASE].

Quando si crea un ASE in hello portale di Azure, è possibile creare la rete virtuale in hello stesso ora oppure scegliere un toodeploy preesistenti di rete virtuale in. Quando si crea un modello, è necessario iniziare con: 

* Una rete virtuale di Resource Manager.
* una subnet in tale rete virtuale. Si consiglia una dimensione subnet ASE `/25` con conto della crescita futura tooaccomodate gli indirizzi a 128. Dopo la creazione di ASE hello, è possibile modificare le dimensioni di hello.
* ID di risorsa Hello da una rete virtuale. È possibile ottenere queste informazioni dal portale di Azure hello in proprietà di rete virtuale.
* sottoscrizione di Hello da toodeploy in.
* Hello posizione toodeploy in.

tooautomate la creazione di base:

1. Creare hello ASE da un modello. Se si crea un ambiente del servizio app esterno, questo è l'ultimo passaggio. Se si crea un ASE ILB, esistono alcune altre toodo di operazioni.

2. Dopo avere creato l'ambiente del servizio app con bilanciamento del carico interno, viene caricato un certificato SSL corrispondente al dominio dell'ambiente del servizio app con bilanciamento del carico interno.

3. Hello caricato certificato SSL sia assegnato toohello ASE di bilanciamento del carico interno come il proprio certificato SSL "default".  Questo certificato viene usato per tooapps traffico SSL su hello ASE ILB quando usano hello comuni dominio radice ASE toohello assegnato (ad esempio, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Creare hello ASE
Un modello di Resource Manager che crea un ambiente del servizio app e il file dei parametri associati sono disponibili [in un esempio][quickstartasev2create] in GitHub.

Se si desidera toomake ASE un bilanciamento del carico interno, usare questi modelli di gestione risorse [esempi][quickstartilbasecreate]. Questi servizi di ristorazione toothat caso di utilizzo. La maggior parte dei parametri di hello in hello *azuredeploy.parameters.json* file sono comuni toohello la creazione di bilanciamento del carico interno ASEs e ASEs esterno. Hello elenco riportato di seguito chiama un'attenzione particolare i parametri out o che sono univoci, quando si crea un ASE di bilanciamento del carico interno:

* *interalLoadBalancingMode*: nella maggior parte dei casi, impostare questo too3, ovvero sia il traffico sulle porte 80/443 HTTP/HTTPS, e le porte canale dati di controllo/hello resta in attesa del servizio FTP hello tooby su hello ASE, sarà associato tooan allocato al bilanciamento del carico interno rete virtuale indirizzo interno. Se questa proprietà è impostata too2, solo hello FTP relativi al servizio porte (canali di controllo e i dati) sono indirizzi di bilanciamento del carico interno tooan associato. il traffico HTTP/HTTPS Hello rimanga nel VIP pubblico hello.
* *suffisso DNS*: questo parametro definisce hello predefinito dominio radice ASE toohello assegnato. Nella variante pubblica di hello del servizio App di Azure, dominio radice di hello predefinito per tutte le app web è *azurewebsites.net*. Poiché un ASE di bilanciamento del carico interno è la rete virtuale del cliente tooa interno, può non essere dominio di radice del servizio di rilevamento toouse hello pubblico predefinito. Un ambiente del servizio app con servizio di bilanciamento del carico interno deve invece avere un dominio radice predefinito appropriato per la rete virtuale interna dell'azienda. Ad esempio, Contoso Corporation potrebbe utilizzare un dominio radice predefinito di *contoso.com interna* per le app che sono previsti toobe risolvibile e accessibile solo all'interno di rete virtuale di Contoso. 
* *ipSslAddressCount*: questo parametro viene impostato automaticamente tooa valore pari a 0 in hello *azuredeploy.json* file perché il bilanciamento del carico interno ASEs avere solo un singolo indirizzo di bilanciamento del carico interno. Non esistono indirizzi IP SSL per un ambiente del servizio app con bilanciamento del carico interno. Di conseguenza, è necessario impostare hello pool di indirizzi IP SSL per un bilanciamento del carico interno di ASE toozero. In caso contrario, si verifica un errore di provisioning. 

Dopo aver hello *azuredeploy.parameters.json* file viene compilato, creare hello ASE utilizzando frammento di codice hello PowerShell. Modificare hello percorsi toomatch hello Gestione risorse file modello percorsi dei file nel computer. Ricorda toosupply i propri valori per nome della distribuzione di gestione delle risorse hello e nome del gruppo di risorse hello:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Richiede circa un'ora per hello ASE toobe creato. Quindi ASE hello viene visualizzato nel portale di hello in elenco hello ASEs per sottoscrizione hello che ha attivato la distribuzione di hello.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Caricare e configurare il certificato SSL di "predefinita" hello
Un certificato SSL deve essere associato a ASE hello come hello "default" certificato SSL usato tooestablish SSL connessioni tooapps. Se è il suffisso DNS predefinito hello del ASE *contoso.com interna*, toohttps://some-random-app.internal-contoso.com una connessione richiede un certificato SSL valido per **.internal contoso.com* . 

Ottenere un certificato SSL valido usando le autorità di certificazione interne, acquistando un certificato da un'autorità di certificazione esterna o usando un certificato autofirmato. Indipendentemente dall'origine hello del certificato SSL di hello, hello gli attributi di certificato seguenti deve essere configurato correttamente:

* **Oggetto**: questo attributo deve essere impostato troppo **.your-radice-dominio-here.com*.
* **Nome alternativo soggetto**: questo attributo deve includere sia **.your-root-domain-here.com* che **.scm.your-root-domain-here.com*. Toohello connessioni SSL sito SCM/Kudu associata a ciascuna applicazione usa un indirizzo del modulo hello *your-app-name.scm.your-root-domain-here.com*.

Dopo aver ottenuto un certificato SSL valido sono necessari altri due passaggi preliminari. Converti/Salva certificato SSL hello come file con estensione pfx. Tenere presente tale file con estensione pfx hello deve includere tutti intermedi e i certificati radice. Proteggerlo con una password.

file con estensione pfx Hello deve toobe convertito in una stringa base64 perché il caricamento del certificato SSL hello utilizzando un modello di gestione risorse. Poiché i modelli di gestione risorse sono file di testo, file con estensione pfx hello deve essere convertite in una stringa base 64. In questo modo può essere incluso come un parametro di modello hello.

Utilizzare hello seguente frammento di codice PowerShell:

* Generare un certificato autofirmato.
* Esportare il certificato di hello come file con estensione pfx.
* Convertire i file con estensione pfx hello in una stringa con codifica base64.
* Salvare file separato tooa stringa con codifica base64 di hello. 

Questo codice di PowerShell per la codifica base64 è stato adattato dall'hello [script di PowerShell blog][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Dopo certificato SSL hello è stato generato e convertita una stringa con codifica base64 tooa, usare modello di gestione risorse di esempio hello [certificato SSL predefinito di hello configura] [ quickstartconfiguressl] su GitHub. 

i parametri in hello Hello *azuredeploy.parameters.json* file sono elencati di seguito:

* *appServiceEnvironmentName*: nome hello di hello ASE ILB da configurare.
* *existingAseLocation*: stringa di testo contenente hello regione di Azure in cui hello ASE di bilanciamento del carico interno è stato distribuito.  Ad esempio "Stati Uniti centro-meridionali".
* *pfxBlobString*: hello rappresentazione di stringa codificata in formato based64 di file con estensione pfx hello. Usare il frammento di codice hello illustrato in precedenza e copiare stringa hello contenuto in "exportedcert.pfx.b64". Incollarlo come valore di hello di hello *pfxBlobString* attributo.
* *password*: file con estensione pfx hello toosecure hello password utilizzata.
* *certificateThumbprint*: hello identificazione personale del certificato. Se si recupera il valore da PowerShell (ad esempio, *$certificate. Identificazione personale* da hello frammento di codice precedente), è possibile utilizzare hello valore. Se si copia il valore di hello dalla finestra di dialogo certificato Windows hello, tenere presente toostrip out spazi hello. Hello *certificateThumbprint* dovrebbe essere simile a AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *Nomecertificato*: un identificatore di stringa di propria scelta utilizzato certificato hello tooidentity. nome di Hello viene utilizzato come parte di gestione risorse identificatore hello per hello *Microsoft.Web/certificates* entità che rappresenta i certificati SSL hello. nome Hello *deve* terminare con hello successivo suffisso: \_yourASENameHere_InternalLoadBalancingASE. Hello portale di Azure Usa questo suffisso, come un indicatore che hello certificato è usato toosecure un ASE abilitata al bilanciamento del carico interno.

Un esempio abbreviato di *azuredeploy.parameters.json* è illustrato qui:

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

Dopo aver hello *azuredeploy.parameters.json* file viene compilato, configurare il certificato SSL predefinito di hello utilizzando frammento di codice hello PowerShell. Modificare hello toomatch di percorsi di file in cui si trovano i file modello di gestione risorse di hello nel computer. Ricorda toosupply i propri valori per nome della distribuzione di gestione delle risorse hello e nome del gruppo di risorse hello:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Sono necessari circa 40 minuti per modifica hello tooapply front-end di base. Ad esempio, per ASE con dimensioni predefinite che utilizza due front-end, hello modello ha attorno un'ora e toocomplete di 20 minuti. Durante l'esecuzione di modello hello hello ASE non può essere scalato.  

Al termine del modello di hello, App in hello ASE di bilanciamento del carico interno sono accessibili tramite HTTPS. connessioni Hello sono protette mediante il certificato SSL predefinito di hello. certificato SSL di Hello predefinito viene utilizzato quando l'App in hello ASE di bilanciamento del carico interno vengono indirizzate mediante una combinazione del nome dell'applicazione hello e nome host predefinito di hello. Ad esempio, https://mycustomapp.internal-contoso.com utilizza certificato per SSL predefinito di hello **.internal contoso.com*.

Tuttavia, come App eseguibili su servizio multi-tenant pubblico di hello, gli sviluppatori possono configurare i nomi host personalizzati per le singole applicazioni. Possono anche configurare associazioni di certificati SSL basati su SNI univoche per le singole app.

## <a name="app-service-environment-v1"></a>Ambiente del servizio app 1 ##
Esistono due versioni dell'ambiente del servizio app: ASEv1 e ASEv2. Hello precedenti informazioni è basato su ASEv2. Questa sezione viene illustrata hello ASEv1 e ASEv2 differenze.

In ASEv1, gestire tutte le risorse di hello manualmente. Che include gli indirizzi IP usati per SSL basato su IP front-end hello e processi di lavoro. Prima di è possibile scalare orizzontalmente il piano di servizio App, è necessario proporzioni timeout pool di lavoro hello che si desidera toohost.

ASEv1 usa un modello tariffario diverso rispetto a ASEv2. Nella versione ASEv1, in particolare, si paga per tutti i core allocati, inclusi i core usati per i front-end o i ruoli di lavoro in cui non sono ospitati carichi di lavoro. In ASEv1, hello predefinito della scala massima pari a un ASE sono 55 host totale. inclusi ruoli di lavoro e front-end. Un vantaggio tooASEv1 è che possono essere distribuito in una rete virtuale classica e una rete virtuale di gestione risorse. vedere toolearn ulteriori informazioni su ASEv1, [introduzione v1 ambiente del servizio App][ASEv1Intro].

toocreate un ASEv1 utilizzando un modello di gestione delle risorse, vedere [crea un v1 ASE di bilanciamento del carico interno con un modello di gestione risorse][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
