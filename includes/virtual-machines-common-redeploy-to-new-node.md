## <a name="use-hello-azure-portal"></a><span data-ttu-id="1dd19-101">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1dd19-101">Use hello Azure portal</span></span>
1. <span data-ttu-id="1dd19-102">Selezionare hello macchina virtuale si desidera tooredeploy, quindi seleziona hello *ridistribuire* pulsante hello *impostazioni* blade.</span><span class="sxs-lookup"><span data-stu-id="1dd19-102">Select hello VM you wish tooredeploy, then select hello *Redeploy* button in hello *Settings* blade.</span></span> <span data-ttu-id="1dd19-103">Potrebbe essere necessario tooscroll verso il basso hello toosee **supporto e risoluzione dei problemi** sezione contenente pulsante 'Ridistribuire' hello come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1dd19-103">You may need tooscroll down toosee hello **Support and Troubleshooting** section that contains hello 'Redeploy' button as in hello following example:</span></span>
   
    ![Pannello VM di Azure](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="1dd19-105">operazione select hello hello tooconfirm *ridistribuire* pulsante:</span><span class="sxs-lookup"><span data-stu-id="1dd19-105">tooconfirm hello operation, select hello *Redeploy* button:</span></span>
   
    ![Pannello Ridistribuire una VM](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="1dd19-107">Hello **stato** di hello VM cambia troppo*aggiornamento* come hello VM Prepara tooredeploy, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="1dd19-107">hello **Status** of hello VM changes too*Updating* as hello VM prepares tooredeploy, as shown in hello following example:</span></span>
   
    ![Aggiornamento di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="1dd19-109">Hello **stato** viene quindi modificato troppo*iniziale* come hello macchina virtuale viene avviato un nuovo host di Azure, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="1dd19-109">hello **Status** then changes too*Starting* as hello VM boots up on a new Azure host, as shown in hello following example:</span></span>
   
    ![Avvio di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="1dd19-111">Al termine di processo di avvio hello, hello VM hello **stato** restituisce quindi troppo*esecuzione*, che indica di hello macchina virtuale è stata ridistribuita correttamente:</span><span class="sxs-lookup"><span data-stu-id="1dd19-111">After hello VM finishes hello boot process, hello **Status** then returns too*Running*, indicating hello VM has been successfully redeployed:</span></span>
   
    ![Esecuzione di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

