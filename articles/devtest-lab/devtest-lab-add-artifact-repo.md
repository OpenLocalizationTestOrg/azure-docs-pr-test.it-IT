---
title: un laboratorio di tooa repository Git in Azure DevTest Labs aaaAdd | Documenti Microsoft
description: Aggiungere un repository GitHub o Git di Visual Studio Team Services per gli elementi personalizzati in Azure DevTest Labs
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Aggiungere un artefatti della toostore repository Git personalizzati e modelli di gestione risorse di Azure

Se si desidera troppo[creare gli elementi personalizzati](devtest-lab-artifact-author.md) per hello macchine virtuali nell'ambiente lab, o [utilizzare modelli di Azure Resource Manager toocreate un ambiente di test personalizzata](devtest-lab-create-environment-from-arm.md), è necessario aggiungere anche un tooinclude di repository Git privato gli elementi di Hello o modelli di gestione risorse di Azure che crea il team. repository Hello può essere ospitato in [GitHub](https://github.com) oppure [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Microsoft ha offerto un [repository Github degli elementi](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) che può essere distribuito così com'è o personalizzato per i lab dell'utente. Quando si personalizzare o crea un elemento, non è possibile archiviarli nel repository pubblico hello: è necessario creare la propria repository privati. 

Quando si crea una macchina virtuale, è possibile salvare il modello di gestione risorse di Azure hello, personalizzarlo se si desidera e quindi utilizzarlo tooeasily successive creare più macchine virtuali. È necessario creare la propria toostore repository privati dei modelli personalizzati di gestione risorse di Azure.  

* toolearn toocreate un repository di GitHub, vedere [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toolearn toocreate un progetto Team Services con un Git Repository, vedere [connettersi tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Hello schermata riportata di seguito viene illustrato un esempio di come un repository che contiene gli elementi potrebbe apparire in GitHub:  
![Esempio di archivio elementi GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Ottenere le credenziali e le informazioni di repository hello
tooadd un ambiente lab tooyour repository, è prima necessario ottenere determinate informazioni dal repository. Nelle sezioni che seguono Hello istruzioni per ottenere queste informazioni per i repository in GitHub e Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Ottenere un token di accesso personale e URL del clone del repository GitHub hello
URL del clone del repository GitHub tooget hello e token di accesso personali, seguire questi passaggi:

1. Sfoglia toohello home page del repository GitHub hello che contiene l'elemento hello o definizioni di modello di gestione risorse di Azure.
2. Selezionare **Clona o scarica**.
3. Hello di hello selezionare pulsante toocopy **url del clone HTTPS** toohello Appunti e salvare hello URL per un uso successivo.
4. Selezionare l'immagine del profilo hello nell'angolo superiore destro di hello di GitHub e selezionare **impostazioni**.
5. In hello **impostazioni personali** menu hello a sinistra, seleziona **token di accesso personali**.
6. Selezionare **Genera nuovo token**.
7. In hello **nuovo token di accesso personali** pagina, immettere un **Token descrizione**, accettare elementi predefiniti hello in hello **selezionare gli ambiti**, quindi scegliere **genera Token**.
8. Salvare il token di hello generato in base alle esigenze in un secondo momento.
9. A questo punto, è possibile chiudere GitHub.   
10. Continuare toohello [collegare il repository toohello lab](#connect-your-lab-to-the-repository) sezione.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Ottenere un token di accesso personale e URL del clone del repository hello Visual Studio Team Services
URL del clone del repository tooget hello Visual Studio Team Services e il token di accesso personali, seguire questi passaggi:

1. Pagina iniziale aprire hello della raccolta di team (ad esempio, `https://contoso-web-team.visualstudio.com`), quindi selezionare il progetto.
2. Nella home page del progetto hello, selezionare **codice**.
3. URL del clone hello tooview, nel progetto hello **codice** selezionare **Clone**.
4. Salvare hello URL in base alle esigenze più avanti in questa esercitazione.
5. Selezionare un Token di accesso personale, toocreate **profilo personale** dal menu a discesa account utente hello.
6. Nella pagina informazioni profilo hello selezionare **sicurezza**.
7. In hello **sicurezza** , selezionare **Aggiungi**.
8. In hello **creare un token di accesso personale** pagina:

   * Immettere un **descrizione** per token hello.
   * Selezionare **180 giorni** da hello **scade In** elenco.
   * Scegliere **tutti gli account accessibili** da hello **account** elenco.
   * Scegliere hello **tutti gli ambiti** opzione.
   * Scegliere **Crea token**.
9. Al termine, il nuovo token di hello viene visualizzato in hello **i token di accesso personali** elenco. Selezionare **copia Token**e quindi salvare hello valore token per un uso successivo.
10. Continuare toohello [collegare il repository toohello lab](#connect-your-lab-to-the-repository) sezione.

## <a name="connect-your-lab-toohello-repository"></a>Collegare il repository toohello lab
1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
3. Elenco dei laboratori hello selezionare lab desiderato hello.   
4. Nel riquadro di sinistra hello, selezionare **criteri di configurazione e**.
5. Nel lab di hello **criteri di configurazione e** area selezionare **repository**.
6. In hello **repository** area selezionare **+ Aggiungi**.

    ![Pulsante di aggiunta repository](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. In hello secondo **repository** specificare hello le seguenti informazioni:

   * **Nome** -immettere un nome per il repository hello.
   * **Url Clone GIT** -immettere hello Git clone URL HTTPS copiato in precedenza da GitHub o Visual Studio Team Services.
   * **Ramo** -immettere hello ramo tooget le definizioni.
   * **Token di accesso personale** -immettere il token di accesso personale hello ottenuti in precedenza da GitHub o Visual Studio Team Services.
   * **I percorsi delle cartelle** -immettere almeno un percorso relativo toohello clone URL della cartella che contiene l'elemento o definizioni di modello di gestione risorse di Azure. Quando si specifica una sottodirectory, assicurarsi che tooinclude hello barra nel percorso di cartella hello.

     ![Area del repository](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il repository Git privato, è possibile eseguire uno o entrambi i seguenti hello, a seconda delle esigenze:
* Archivio del [elementi personalizzati](devtest-lab-artifact-author.md), che è possibile utilizzare toocreate successive nuove macchine virtuali.
* [Creare ambienti multi-VM e PaaS risorse con i modelli di Azure Resource Manager](devtest-lab-create-environment-from-arm.md) e quindi archiviare i modelli di hello nel repository di privato.

Quando si crea una macchina virtuale, è possibile verificare che gli artefatti di hello o i modelli vengono aggiunti repository Git tooyour. Sono disponibili immediatamente nell'elenco di hello di elementi o i modelli, con il nome di hello del repository di privato illustrato nella colonna hello che specifica l'origine hello. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Post di blog correlati
* [Come tootroubleshoot in mancanza di elementi in Azure DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Aggiungere un dominio di Active Directory utilizzando un modello di gestione delle risorse in Azure DevTest Labs di tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
