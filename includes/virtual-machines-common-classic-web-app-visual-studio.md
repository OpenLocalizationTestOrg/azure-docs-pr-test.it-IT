

Quando si crea un progetto di applicazione web per Azure, è possibile eseguire il provisioning di una macchina virtuale in Azure. È quindi possibile configurare la macchina virtuale hello con altri prodotti software o utilizzare macchina virtuale hello per scopi di debug e diagnostica.

toocreate una macchina virtuale quando si crea un'applicazione web, seguire questi passaggi:

1. In Visual Studio, fare clic su **File** > **New** > **progetto** > **Web**, quindi scegliere **Applicazione Web ASP.NET** (in hello **Visual c#** o **Visual Basic** nodi).
2. In hello **nuovo progetto ASP.NET** della finestra di dialogo Tipo selezionare hello dell'applicazione web che si desidera e in hello Azure sezione della finestra di dialogo hello (nell'angolo inferiore destro hello), assicurarsi che tale hello **Host nel cloud hello**casella di controllo è selezionata (questa casella di controllo **crea risorse remote** in alcune installazioni).
   
    ![][0]
3. In questo esempio, nell'elenco a discesa hello in Microsoft Azure, scegliere **macchina virtuale (v1)**, quindi fare clic su hello **OK** pulsante.
4. Accedi tooAzure se viene richiesto. Hello **crea macchina virtuale** viene visualizzata la finestra di dialogo.
   
    ![][2]
5. In hello **nome DNS** , immettere un nome per la macchina virtuale hello. nome DNS Hello deve essere univoco in Azure. Se il nome di hello immesso non è disponibile, viene visualizzato un punto esclamativo rosso.
6. In hello **immagine** scegliere hello l'immagine macchina virtuale di toobase hello in. È possibile scegliere una delle immagini di macchina virtuale di Azure standard hello o l'immagine che hai caricato tooAzure.
7. Lasciare hello **abilitare IIS e distribuzione Web** selezionata a meno che non si prevede un server web diverso tooinstall casella di controllo. Se si disabilita distribuzione Web, sarà in grado di toopublish da Visual Studio. È possibile aggiungere IIS e distribuzione Web tooany di immagini di Windows Server hello incluso nel pacchetto, incluse le immagini personalizzate.
8. In hello **dimensioni** scegliere dimensioni hello della macchina virtuale hello.
9. Specificare hello credenziali di accesso per questa macchina virtuale. Prendere nota di essi, poiché sarà necessario tooaccess hello computer tramite Desktop remoto.
10. In hello **percorso** scegliere la macchina virtuale hello area toohost hello.
11. Fare clic su hello **OK** toostart pulsante Creazione macchina virtuale hello. È possibile seguire lo stato di avanzamento hello dell'operazione di hello in hello **Output** finestra.
    
    ![][3]
12. Provisioning della macchina virtuale hello, vengono creati gli script pubblicati in un **PublishScripts** nodo della soluzione. Hello pubblicati viene eseguito lo script ed esegue il provisioning una macchina virtuale in Azure. Hello **Output** finestra viene visualizzato lo stato di hello. lo script di Hello esegue hello seguente tooset azioni hello della macchina virtuale:
    
    * Crea macchina virtuale hello se non esiste già.
    * Crea un account di archiviazione con un nome che inizia con `devtest`, ma solo se esiste già un account di archiviazione nell'area specificata hello.
    * Crea un servizio cloud come contenitore per la macchina virtuale hello e crea un ruolo web per un'applicazione web hello.
    * Configura distribuzione Web nella macchina virtuale hello.
    * Configura IIS e ASP.NET nella macchina virtuale hello.
    
    ![][4]
13. (Facoltativo) È possibile connettersi toohello nuova macchina virtuale. In **Esplora Server**, espandere hello **macchine virtuali** nodo, scegliere il nodo di hello per la macchina virtuale hello è stato creato e il relativo menu di scelta rapida, scegliere **connessione tramite Desktop remoto**. In alternativa, in **Cloud Explorer** è possibile scegliere **Apri nel portale** hello menu di scelta rapida e connettere toohello della macchina virtuale non esiste.
    
    ![][5]

## <a name="next-steps"></a>Passaggi successivi
Se si desidera toocustomize hello script pubblicato è stato creato, leggere informazioni più dettagliate in [tooDev tooPublish tramite script di Windows PowerShell e gli ambienti di Test](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
