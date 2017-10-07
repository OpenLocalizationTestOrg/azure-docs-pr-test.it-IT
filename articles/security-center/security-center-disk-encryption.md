---
title: aaaEncrypt una macchina virtuale di Azure | Documenti Microsoft
description: Questo documento consente di tooencrypt una macchina virtuale di Azure dopo la ricezione di un avviso da Centro sicurezza di Azure.
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Crittografare una macchina virtuale di Azure
Centro sicurezza di Azure invia avvisi in caso di macchine virtuali non crittografate. Questi avvisi verranno visualizzato come livello di gravità elevato e hello raccomandazione è tooencrypt queste macchine virtuali.

![Raccomandazione di crittografare il disco](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> informazioni di Hello in questo documento si applicano tooencrypting le macchine virtuali senza utilizzare una chiave di crittografia (che è obbligatorio per il backup di macchine virtuali tramite Backup di Azure). Vedere l'articolo hello [Azure crittografia disco per Windows e le macchine virtuali Linux Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) per informazioni su come toouse toosupport una chiave di crittografia crittografata macchine virtuali di Azure Backup di Azure.
>
>

tooencrypt macchine virtuali di Azure che sono stati identificati dal Centro sicurezza di Azure come crittografia, è consigliabile hello alla procedura seguente:

* Installare e configurare Azure PowerShell. Ciò consentirà toorun hello PowerShell i comandi necessari tooset backup hello prerequisiti necessari tooencrypt macchine virtuali di Azure.
* Ottenere ed eseguire script di PowerShell Azure prerequisiti di Azure disco crittografia hello
* Crittografare le macchine virtuali.

obiettivo di Hello di questo documento è tooenable si tooencrypt le macchine virtuali, anche se si dispone di background senza alcuna in Azure PowerShell.
Questo documento si presuppone che si usa Windows 10 come computer client hello da cui si configurerà la crittografia del disco di Azure.

Esistono molti approcci che possono essere utilizzati toosetup hello prerequisiti e la crittografia tooconfigure macchine virtuali di Azure. Se si è già esperti in materia di Azure PowerShell o l'interfaccia CLI di Azure, è preferibile approcci alternativi toouse.

> [!NOTE]
> toolearn ulteriori informazioni su crittografia tooconfiguring approcci alternativi per macchine virtuali di Azure, vedere [Azure crittografia disco per Windows e le macchine virtuali Linux Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Installare e configurare Azure PowerShell
È necessario che Azure PowerShell 1.2.1 o versione successiva sia installato nel computer. articolo Hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) contiene tutti i passaggi di hello è necessario tooprovision toowork il computer con Azure PowerShell. approccio più semplice Hello è toouse approccio di installazione guidata piattaforma Web hello indicata in tale articolo. Anche se si dispone già di Azure PowerShell è installato, installare nuovamente approccio hello installazione guidata piattaforma Web in modo da avere più recente di Azure PowerShell hello.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Ottenere ed eseguire script di configurazione di prerequisiti per la crittografia su disco di Azure hello
Script di configurazione di Azure disco crittografia prerequisiti Hello imposterà tutti i prerequisiti di hello richiesti per la crittografia delle macchine virtuali di Azure.

1. Pagina di GitHub passare toohello con hello [Script il programma di installazione dei prerequisiti di Azure disco crittografia](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Nella pagina GibHub hello, fare clic su hello **Raw** pulsante.
3. Utilizzare **CTRL + A** tooselect tutti hello testo hello pagina e quindi usare **CTRL-C** toocopy tutti hello testo negli Appunti di toohello pagina hello.
4. Aprire **Notepad** e incollare testo hello copiato nel blocco note.
5. Creare una nuova cartella nell'unità C: denominata **AzureADEScript**.
6. Salvare il file di blocco note hello: fare clic su **File**, quindi fare clic su **Salva con nome**. Nella casella Nome File hello immettere **"ADEPrereqScript.ps1"** e fare clic su **salvare**. (assicurarsi di inserire hello nome tra virgolette hello, in caso contrario verrà salvato il file hello con un'estensione di file con estensione txt).

Ora che viene salvato il contenuto dello script hello, aprire script hello in PowerShell ISE hello:

1. Nel Menu Start hello, fare clic su **Cortana**. Chiedere **Cortana** "PowerShell" digitando **PowerShell** nella casella di testo hello Cortana Cerca.
2. Fare clic con il pulsante destro del mouse su **Windows PowerShell ISE** e scegliere **Esegui come amministratore**.
3. In hello **amministratore: Windows PowerShell ISE** finestra, fare clic su **vista** e quindi fare clic su **Mostra riquadro di Script**.
4. Se viene visualizzato hello **comandi** riquadro sul lato destro hello della finestra hello, fare clic su hello **"x"** in hello angolo superiore destro di hello riquadro tooclose è. Se il testo hello è troppo piccolo per si toosee, utilizzare **CTRL + Aggiungi** ("Aggiungi" hello è "+" firma). Se il testo hello è troppo grande, utilizzare **CTRL + Subtract** (Subtract è hello "-" sign).
5. Fare clic su **File** e quindi su **Apri**. Passare toohello **C:\AzureADEScript** cartella e hello fare doppio clic su hello **ADEPrereqScript**.
6. Hello **ADEPrereqScript** contenuto dovrebbe ora apparire in PowerShell ISE hello ed è contraddistinto dal colore toohelp viene visualizzato più facilmente diversi componenti, ad esempio i comandi, parametri e variabili.

Dovrebbe essere simile al seguente hello nella figura seguente.

![Finestra di PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

riquadro superiore Hello è tooas cui hello "riquadro di script" e riquadro inferiore hello è tooas cui hello "console". Questi termini verranno usati più avanti nell'articolo.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Eseguire il comando PowerShell prerequisiti di hello Azure disco crittografia
Hello script Azure prerequisiti per la crittografia su disco richiesto per hello dopo l'avvio dello script hello le seguenti informazioni:

* **Nome gruppo di risorse** : nome del gruppo di risorse che si desidera tooput hello hello in insieme di credenziali chiave.  Se esiste già uno con lo stesso nome creato, verrà creato un nuovo gruppo di risorse con nome hello che immesso. Se si dispone già di un gruppo di risorse che si desidera toouse in questa sottoscrizione, quindi immettere il nome di hello del gruppo di risorse.
* **Nome dell'insieme di credenziali chiave** -nome dell'insieme di credenziali chiave hello in crittografia chiavi sono toobe inserito. Viene creato un nuovo insieme di credenziali delle chiavi con il nome immesso, se non esiste già. Se si dispone già di un insieme di credenziali chiave che si desidera toouse, immettere il nome di hello di hello esistente dell'insieme di credenziali chiave.
* **Percorso** -percorso di hello insieme di credenziali chiave. Verificare che siano hello insieme di credenziali chiave e le macchine virtuali toobe crittografato hello nello stesso percorso. Se non si conosce il percorso di hello, vi sono passaggi più avanti in questo articolo viene illustrato come toofind out.
* **Nome di Active Directory dell'applicazione Azure** -nome dell'applicazione di Azure Active Directory che sarà utilizzato toowrite segreti toohello insieme di credenziali chiave hello. Viene creata una nuova applicazione con questo nome, se non esiste già. Se si dispone già di un'applicazione Azure Active Directory che si desidera toouse, immettere il nome di hello dell'applicazione Azure Active Directory.

> [!NOTE]
> Se si desidera come toowhy occorre toocreate un'applicazione Azure Active Directory, vedere *registrare un'applicazione con Azure Active Directory* sezione articolo hello [Introduzionedell'insiemedicredenzialichiavediAzure](../key-vault/key-vault-get-started.md).
>
>

Eseguire hello seguendo i passaggi tooencrypt una macchina virtuale di Azure:

1. Se è stata chiusa hello PowerShell ISE, aprire un'istanza con privilegi elevata di hello PowerShell ISE. Istruzioni hello in precedenza in questo articolo se hello che PowerShell ISE non è già aperto. Se si chiude script hello, quindi aprire hello **ADEPrereqScript.ps1** facendo clic su **File**, quindi **aprire** e selezionando script hello hello **c:\. AzureADEScript** cartella. Se in questo articolo è stata seguita dall'inizio di hello, quindi spostare nel passaggio successivo toohello.
2. Nella console di hello di hello PowerShell ISE (riquadro hello inferiore di hello PowerShell ISE), modificare hello messa a fuoco toohello locale dello script hello digitando **cd c:\AzureADEScript** e premere **invio**.
3. Impostare i criteri di esecuzione hello nel computer in modo che è possibile eseguire script hello. Tipo **Set-ExecutionPolicy Unrestricted** in hello console e quindi premere INVIO. Se viene visualizzato una finestra di dialogo indicante gli effetti di hello dei criteri di tooexecution hello modifica, fare clic su **Sì tooall** o **Sì** (se viene visualizzato **Sì tooall**, selezionare tale opzione: non è visualizzato **Sì tooall**, quindi fare clic su **Sì**).
4. Accedere all'account Azure. Nella console di hello, digitare **accesso AzureRmAccount** e premere **invio**. Verrà visualizzata una finestra di dialogo in cui inserire le credenziali (assicurarsi di disporre di diritti toochange le macchine virtuali hello: se non si dispone di diritti, non sarà in grado di tooencrypt li. In caso di dubbi, contattare l'amministratore o il proprietario della sottoscrizione). Verranno visualizzate le informazioni su **ambiente**, **account**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**. Hello copia **SubscriptionId** tooNotepad. Sarà necessaria toouse nel passaggio &#6;.
5. Trovare quale sottoscrizione macchina virtuale appartiene tooand posizione. Andare troppo[https://portal.azure.com](ttps://portal.azure.com) ed effettuare l'accesso.  Scegliere hello il lato sinistro di pagina hello, **macchine virtuali**. Verrà visualizzato un elenco delle macchine virtuali e le sottoscrizioni di hello a che appartengono.

   ![Macchine virtuali](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Restituire toohello PowerShell ISE. Impostare il contesto di sottoscrizione hello in cui verrà eseguito uno script hello. Nella console di hello, digitare **selezionare AzureRmSubscription – SubscriptionId < your_subscription_Id >** (sostituire **< your_subscription_Id >** con l'ID sottoscrizione effettivo) e premere  **Immettere**. Verranno visualizzate informazioni sull'ambiente, hello **Account**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**.
7. Si è ora script hello toorun pronto. Fare clic su hello **Esegui Script** o preme **F5** tastiera hello.

   ![Esecuzione dello script di PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. script Hello chiede **resourceGroupName:** -immettere il nome di hello del *gruppo di risorse* desiderato toouse, quindi premere **invio**. Se non si dispone di uno, immettere un nome che si desidera toouse uno nuovo. Se si dispone già di un *gruppo di risorse* che si desidera toouse (ad esempio hello uno presente nella macchina virtuale), immettere il nome di hello del gruppo di risorse esistente hello.
9. script Hello chiede **Microsoft:** -immettere il nome di hello di hello *insieme di credenziali chiave* toouse desiderato, quindi premere INVIO. Se non si dispone di uno, immettere un nome che si desidera toouse uno nuovo. Se si dispone già di un insieme di credenziali chiave che si desidera toouse, immettere il nome di hello hello esistenti *insieme di credenziali chiave*.
10. script Hello chiede **percorso:** : immettere il nome di hello del percorso di hello in cui hello macchina virtuale che si desidera tooencrypt trova, quindi premere **invio**. Se non si ricorda il percorso di hello, tornare toostep #5.
11. script Hello chiede **aadAppName:** -immettere il nome di hello di hello *Azure Active Directory* applicazione cui si desidera toouse, quindi premere **invio**. Se non si dispone di uno, immettere un nome che si desidera toouse uno nuovo. Se si dispone già di un *applicazione Azure Active Directory* che si desidera toouse, immettere il nome di hello hello esistenti *applicazione Azure Active Directory*.
12. Viene visualizzata una finestra di dialogo di accesso. Fornire le credenziali (Sì, aver effettuato l'accesso una sola volta, ma è ora necessario toodo nuovamente).
13. esecuzione dello script Hello e al termine, verrà chiesto valori hello toocopy di hello **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**e **keyVaultResourceId**. Copia negli Appunti toohello valori e incollarli nel blocco note.
14. Restituire toohello PowerShell ISE e posizionare il cursore di hello alla fine di hello dell'ultima riga hello e premere **invio**.

output di Hello dello script hello dovrebbe essere simile al seguente hello schermata riportata di seguito:

![Output di PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Crittografare hello macchina virtuale di Azure
Si sono ora pronti tooencrypt la macchina virtuale. Se la macchina virtuale si trova hello stesso gruppo di risorse come insieme di credenziali chiave, è possibile spostare nella sezione passaggi di crittografia toohello. Tuttavia, se la macchina virtuale non è presente hello stesso gruppo di risorse come l'insieme di credenziali chiave, sarà necessario seguente hello tooenter nella console di hello in PowerShell ISE hello:

**$resourceGroupName = &lt;'Virtual_Machine_RG'&gt;**

Sostituire **< Virtual_Machine_RG >** con nome hello hello del gruppo di risorse in cui sono contenute le macchine virtuali, racchiuso tra virgolette. e quindi premere **INVIO**.
tooconfirm hello corretto è stato immesso il nome di gruppo di risorse, digitare hello segue nella console di PowerShell ISE hello:

**$resourceGroupName**

Premere **INVIO**. Verrà visualizzato il nome di hello del gruppo di risorse che si trovano le macchine virtuali in. ad esempio:

![Output di PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Passaggi di crittografia
È innanzitutto necessario nome hello di PowerShell tootell della macchina virtuale hello desiderato tooencrypt. Nella console di hello, digitare:

**$vmName = &lt;'your_vm_name'&gt;**

Sostituire **<'your_vm_name ' >** con nome hello della macchina virtuale (assicurarsi che il nome di hello è racchiuso tra virgolette) e quindi premere **invio**.

tooconfirm hello corretto è stato immesso il nome di macchina virtuale, digitare:

**$vmName**

Premere **INVIO**. Verrà visualizzato il nome di hello della macchina virtuale hello desiderato tooencrypt. ad esempio:

![Output di PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Esistono due metodi toorun hello crittografia comando tooencrypt tutte le unità sulla macchina virtuale hello. il primo metodo di Hello è hello tootype comando nella console di PowerShell ISE hello seguente:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Dopo aver digitato il comando, premere **INVIO**.

Hello secondo metodo è tooclick nel riquadro di script hello (hello riquadro superiore di hello PowerShell ISE) e scorrere verso il basso nella parte inferiore toohello dello script hello. Evidenziare il comando hello elencato in precedenza e quindi pulsante destro del mouse e quindi fare clic su **Esegui selezione** o premere **F8** tastiera hello.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Indipendentemente dal metodo hello usata, verrà visualizzata una finestra di dialogo che informa che richiederà 10-15 minuti per hello operazione toocomplete. Fare clic su **Sì**.

Durante il processo di crittografia di hello, è possibile restituire toohello portale di Azure e visualizzare lo stato di hello della macchina virtuale hello. Scegliere hello il lato sinistro di pagina hello, **macchine virtuali**, quindi nella hello **macchine virtuali** pannello, fare clic sul nome della macchina virtuale hello si esegue la crittografia hello. Nel pannello hello che viene visualizzato, si noterà che hello **stato** costituisce **aggiornamento**. Ciò dimostra che la crittografia è in corso.

![Ulteriori dettagli su hello VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Restituire toohello PowerShell ISE. Al termine dell'esecuzione dello script hello, si noterà quanto visualizzato nella figura hello seguente.

![Output di PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate che hello macchina virtuale ora viene crittografato, restituire toohello portale di Azure e fare clic su **macchine virtuali** sul lato sinistro di pagina hello hello. Fare clic su nome hello della macchina virtuale hello che è crittografato. In hello **impostazioni** pannello, fare clic su **dischi**.

![Opzioni delle impostazioni](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

In hello **dischi** pannello, si noterà che **crittografia** è **abilitato**.

![Proprietà dei dischi](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Passaggi successivi
In questo documento, si è appreso come tooencrypt una macchina virtuale di Azure. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure
