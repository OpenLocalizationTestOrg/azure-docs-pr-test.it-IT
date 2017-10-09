
1. <span data-ttu-id="b3604-101">In hello **connessioni ibride** pannello, fare clic su connessione ibrida hello appena creato, quindi fare clic su **Listener installazione**.</span><span class="sxs-lookup"><span data-stu-id="b3604-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="b3604-103">Hello **le proprietà di connessione ibrida** apre blade.</span><span class="sxs-lookup"><span data-stu-id="b3604-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="b3604-104">In **locale di Hybrid Connection Manager**, scegliere **scaricare e configurare manualmente**, salvare il pacchetto di HybridConnectionManager.msi hello scaricato e copiare una stringa di connessione del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="b3604-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Fare clic qui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="b3604-106">Da un prompt dei comandi di amministratore, digitare quanto segue di hello comandi installer hello toostart:</span><span class="sxs-lookup"><span data-stu-id="b3604-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="b3604-107">Dopo hello esegue l'installazione, fare clic su **non ora**, quindi cartella %ProgramFiles%\Microsoft\HybridConnectionManager toohello, eseguire HCMConfigWizard.exe e fare clic su **Sì** in hello **utente Controllo dell'account** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="b3604-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="b3604-108">Incollare una stringa di connessione ibrida hello copiato in precedenza e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3604-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installazione](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="b3604-110">Al termine dell'installazione di hello, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="b3604-110">When hello install completes, click **Close**.</span></span>
   
    ![Fare clic su Chiudi](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="b3604-112">In hello **connessioni ibride** blade, hello **stato** colonna Mostra ora **connesso**.</span><span class="sxs-lookup"><span data-stu-id="b3604-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Stato connesso](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

