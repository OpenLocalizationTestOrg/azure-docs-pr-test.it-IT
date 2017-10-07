---
title: aaaSetting di un cluster di Service Fabric con Visual Studio | Documenti Microsoft
description: Viene descritto come tooset di un'infrastruttura del servizio cluster utilizzando il modello di gestione risorse di Azure creato da un progetto di gruppo di risorse di Azure in Visual Studio
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Configurare un cluster di Service Fabric tramite Visual Studio
In questo articolo viene descritto come tooset di un'infrastruttura di Azure del servizio cluster tramite Visual Studio e un modello di gestione risorse di Azure. Verrà utilizzato un modello hello toocreate progetto di Visual Studio Azure risorse gruppo. Dopo aver creato il modello di hello, possono essere distribuito direttamente tooAzure da Visual Studio. Può anche essere usato da uno script o come parte della funzionalità di integrazione continuata (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Creare un modello di cluster di Service Fabric con un progetto Gruppo di risorse di Azure
avvio tooget, aprire Visual Studio e creare un progetto di gruppo di risorse di Azure (è disponibile in hello **Cloud** cartella):

![Finestra di dialogo Nuovo progetto con il progetto Gruppo di risorse di Azure selezionato][1]

È possibile creare una nuova soluzione di Visual Studio per questo progetto oppure aggiungerlo tooan di soluzione esistente.

> [!NOTE]
> Se il progetto di gruppo di risorse di Azure hello nel nodo Cloud hello non viene visualizzata, non si dispone hello Azure SDK installato. Avviare Installazione guidata piattaforma Web ([installarlo ora](http://www.microsoft.com/web/downloads/platform.aspx) se non è già disponibile), quindi cercare "Azure SDK per .NET" e installare la versione di hello compatibile con la versione di Visual Studio.
> 
> 

Dopo che si raggiunge pulsante OK hello, Visual Studio chiederà modello di gestione risorse di hello tooselect da toocreate:

![Finestra di dialogo Seleziona modello di Azure con il modello Service Fabric Cluster selezionato][2]

Selezionare il modello di Cluster di Service Fabric hello e pulsante hello hit OK. progetto Hello e del modello di gestione risorse di hello è stati creati.

## <a name="prepare-hello-template-for-deployment"></a>Preparare il modello di hello per la distribuzione
Prima che il modello di hello sia cluster hello toocreate distribuito, è necessario fornire valori per parametri modello hello necessario. Questi valori di parametro sono leggervi hello `ServiceFabricCluster.parameters.json` file hello `Templates` nella cartella del progetto di gruppo di risorse hello. Aprire il file hello e fornire hello seguenti valori:

| Nome parametro | Descrizione |
| --- | --- |
| adminUserName |nome Hello dell'account amministratore hello per le macchine di Service Fabric (nodi). |
| certificateThumbprint |Hello identificazione personale del certificato hello che protegge cluster hello. |
| sourceVaultResourceId |Hello *ID risorsa* dell'insieme di credenziali chiave di hello in cui memorizzare hello certificato che protegge cluster hello. |
| certificateUrlValue |URL di Hello hello cluster del certificato di sicurezza. |

modello di gestione di risorse dell'infrastruttura di Visual Studio servizio Hello creato un cluster protetto è protetto da un certificato. Questo certificato è identificato da hello ultimi tre parametri di modello (`certificateThumbprint`, `sourceVaultValue`, e `certificateUrlValue`), e deve esistere in un **insieme credenziali chiavi Azure**. Per ulteriori informazioni su come toocreate hello certificato di sicurezza cluster, vedere [scenari di sicurezza di Service Fabric cluster](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) articolo.

## <a name="optional-change-hello-cluster-name"></a>Facoltativo: modificare il nome del cluster hello
Ogni cluster di Service Fabric ha un nome. Quando viene creato un cluster di infrastruttura in Azure, il nome del cluster determina (insieme con Buongiorno regione di Azure) nome di sistema DNS (Domain Name) hello per cluster hello. Ad esempio, se si assegna il nome del cluster `myBigCluster`e il percorso di hello (regione di Azure) del gruppo di risorse hello che ospiterà il nuovo cluster di hello è Stati Uniti orientali, hello di nome DNS del cluster hello sarà `myBigCluster.eastus.cloudapp.azure.com`.

Per impostazione predefinita il nome del cluster hello è generato automaticamente e resi univoco collegando un prefisso di "cluster" tooa suffisso casuale. Questo rende molto semplice toouse modello di hello come parte di un **integrazione continua** sistema (CI). Se si desidera toouse un nome specifico per il cluster, ovvero tooyou significativo, imposta il valore di hello di hello `clusterName` variabile nel file di modello di gestione risorse hello (`ServiceFabricCluster.json`) nome tooyour scelto. È prima variabile hello definita in tale file.

## <a name="optional-add-public-application-ports"></a>Facoltativo: aggiungere le porte pubbliche dell'applicazione
È inoltre possibile le porte pubbliche applicazione hello toochange per cluster hello prima di distribuirlo. Per impostazione predefinita, il modello di hello apre solo due porte TCP pubbliche (80 e 8081). Se è necessario maggiore per le applicazioni, è possibile modificare una definizione bilanciamento del carico di Azure hello in modello hello. definizione di Hello viene archiviata nel file di modello principale hello (`ServiceFabricCluster.json`). Aprire il file e cercare `loadBalancedAppPort`. Ogni porta è associata a tre elementi:

1. Una variabile del modello che definisce il valore di porta TCP di hello per la porta hello:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. Oggetto *probe* che definisce la frequenza e per quanto tempo hello bilanciamento carico di Azure tenta toouse un nodo specifico di Service Fabric prima che si verifichi su tooanother uno. probe Hello fanno parte di hello risorsa di bilanciamento del carico. Qui è hello probe definizione porta applicazione predefinita prima di hello:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. Oggetto *regola di bilanciamento del carico* che collega porta hello e probe hello, che consente il bilanciamento del carico in un set di nodi del cluster di Service Fabric:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Se le applicazioni di hello che si prevede di cluster toohello toodeploy richiedono più porte, è possibile aggiungere la creazione di probe aggiuntivi e le definizioni delle regole di bilanciamento del carico. Per ulteriori informazioni su come toowork con bilanciamento del carico di Azure tramite i modelli di gestione delle risorse, vedere [iniziare a creare un servizio di bilanciamento del carico interno utilizzando un modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Distribuire il modello di hello tramite Visual Studio
Dopo aver salvato tutte hello valori dei parametri obbligatori nel`ServiceFabricCluster.param.dev.json` file, sono pronti toodeploy hello modello e creare il cluster di Service Fabric. Fare clic sul progetto in Esplora soluzioni di Visual Studio gruppo risorse hello e scegliere **Distribuisci | Nuova distribuzione...** . Se necessario, verrà visualizzato in Visual Studio hello **distribuire tooResource gruppo** della finestra di dialogo che chiede tooauthenticate tooAzure:

![Finestra di dialogo gruppo tooResource Distribuisci][3]

la finestra di dialogo Hello consente di scegliere un gruppo di risorse esistente di gestione risorse per cluster hello e permette hello opzione toocreate uno nuovo. È in genere un gruppo di risorse distinto per un cluster di Service Fabric toouse senso.

Dopo che si raggiunge pulsante Distribuisci hello, Visual Studio richiederà i valori dei parametri modello tooconfirm hello. Hello hit **salvare** pulsante. Un parametro non ha un valore persistente: password dell'account amministrativo hello per cluster hello. È necessario un valore di password tooprovide quando Visual Studio ti chiede di uno.

> [!NOTE]
> A partire da Azure SDK 2.9, Visual Studio supporta la lettura password dall'**insieme di credenziali delle chiavi di Azure** durante la distribuzione. Nella finestra di dialogo parametri modello hello si noti che hello `adminPassword` casella di testo del parametro è una piccola icona "chiave" su hello destra. Questa icona consente tooselect un segreto dell'insieme di credenziali chiave esistente come password amministrativa di hello per cluster hello. È sufficiente Assicurarsi toofirst che abilita l'accesso di gestione risorse di Azure per la distribuzione dei modelli nei criteri di accesso avanzate hello di credenziali delle chiavi. 
> 
> 

È possibile monitorare lo stato di avanzamento hello del processo di distribuzione hello nella finestra di output di hello Visual Studio. Una volta completata la distribuzione dei modelli di hello, il nuovo cluster è pronto toouse!

> [!NOTE]
> Se PowerShell è stato mai usato tooadminister Azure dal computer hello che attualmente in uso, è necessario toodo manutenzione una piccola.
> 
> 1. Attivare PowerShell scripting eseguendo hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) comando. Per i computer di sviluppo, i criteri "Unrestricted" sono in genere accettabili.
> 2. Decidere se la raccolta di dati diagnostici tooallow da comandi di PowerShell di Azure ed eseguire [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) o [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) in base alle esigenze. In questo modo, si eviteranno richieste non necessarie durante la distribuzione del modello.
> 
> 

Se sono presenti errori, passare toohello [portale di Azure](https://portal.azure.com/) e hello aprire gruppo di risorse che è stato distribuito a. Fare clic su **tutte le impostazioni**, quindi fare clic su **distribuzioni** nel pannello impostazioni hello. Nel caso in cui la distribuzione del gruppo di risorse non sia riuscita, in questa sezione saranno presenti informazioni di diagnostica dettagliate.

> [!NOTE]
> I cluster di Service Fabric richiedono un certo numero di nodi toobe la disponibilità di toomaintain e mantengono lo stato, di cui viene fatto riferimento tooas "gestione quorum". Pertanto, non è sicuro tooshut verso il basso tutti i computer hello hello cluster a meno che non è stata innanzitutto eseguita una [backup completo dello stato del](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni sulla configurazione di cluster di Service Fabric utilizzando hello portale di Azure](service-fabric-cluster-creation-via-portal.md)
* [Informazioni su come toomanage e distribuire applicazioni di Service Fabric utilizzando Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
