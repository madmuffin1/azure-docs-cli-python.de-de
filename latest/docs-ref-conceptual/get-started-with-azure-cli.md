---
title: Erste Schritte mit Azure CLI 2.0
description: "Enthält eine Beschreibung der ersten Schritte mit Azure CLI 2.0 unter Linux, MacOS und Windows."
keywords: Azure CLI 2.0, Linux, MacOS, Windows, OS X, Ubuntu, Debian, CentOS, RHEL, SUSE, CoreOS, Docker, Windows, Python, PIP
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 02/27/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.assetid: 85c418a8-6177-4833-bb8d-ff4ce2233c1a
ms.openlocfilehash: 11153c13fb9868897b0bb21dac9d64072c3af16e
ms.sourcegitcommit: 70c4d7a14591e5b761e261105cd2d376753f2a54
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2017
---
# <a name="get-started-with-azure-cli-20"></a><span data-ttu-id="8a2ae-104">Erste Schritte mit Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8a2ae-104">Get started with Azure CLI 2.0</span></span>

<span data-ttu-id="8a2ae-105">Azure CLI 2.0 ist die neue Befehlszeilenumgebung von Azure und dient zum Verwalten von Azure-Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-105">The Azure CLI 2.0 is Azure's new command line experience for managing Azure resources.</span></span>
<span data-ttu-id="8a2ae-106">Sie können sie in Ihrem Browser mit [Azure Cloud Shell](/azure/cloud-shell/overview) verwenden oder unter macOS, Linux und Windows [installieren](install-azure-cli.md) und über die Befehlszeile ausführen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-106">You can use it in your browser with [Azure Cloud Shell](/azure/cloud-shell/overview), or you can [install](install-azure-cli.md) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="8a2ae-107">Azure CLI 2.0 ist für die Verwaltung von Azure-Ressourcen über die Befehlszeile sowie die Erstellung von Automatisierungsskripts für Azure Resource Manager optimiert.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-107">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line, and for building automation scripts that work against the Azure Resource Manager.</span></span>
<span data-ttu-id="8a2ae-108">Dieser Artikel hilft Ihnen beim Einstieg und enthält Informationen zu den wichtigsten Konzepten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-108">This article helps get you started using it, and teaches you the core concepts behind it.</span></span>

<span data-ttu-id="8a2ae-109">Informationen zur neuesten Version finden Sie in den [Versionshinweisen](release-notes-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-109">For information about the latest release, see the [release notes](release-notes-azure-cli.md).</span></span>

## <a name="connect"></a><span data-ttu-id="8a2ae-110">Verbinden</span><span class="sxs-lookup"><span data-stu-id="8a2ae-110">Connect</span></span>

<span data-ttu-id="8a2ae-111">Die einfachste Möglichkeit, erste Schritte auszuführen, besteht im [Starten von Cloud Shell](/azure/cloud-shell/quickstart).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-111">The simplest way to get started is to [launch Cloud Shell](/azure/cloud-shell/quickstart).</span></span>

1. <span data-ttu-id="8a2ae-112">Starten Sie Cloud Shell über den oberen Navigationsbereich im Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-112">Launch Cloud Shell from the top navigation of the Azure portal.</span></span>

   ![Shell-Symbol](media/get-started-with-azure-cli/shell-icon.png)

2. <span data-ttu-id="8a2ae-114">Wählen Sie das zu verwendende Abonnement aus, und erstellen Sie ein Speicherkonto.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-114">Choose the subscription you want to use and create a storage account.</span></span>

   ![Erstellen Sie ein Speicherkonto.](media/get-started-with-azure-cli/storage-prompt.png)

<span data-ttu-id="8a2ae-116">Sie können die CLI auch [installieren](install-azure-cli.md) und lokal über die Befehlszeile ausführen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-116">You can also [install](install-azure-cli.md) the CLI and run it locally from the command line.</span></span> <span data-ttu-id="8a2ae-117">Führen Sie nach der Installation der CLI `az login` aus, um sich mit Ihrem Standardabonnement anzumelden.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-117">Once you have installed the CLI, run `az login` to log in with your default subscription.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="8a2ae-118">Erstellen einer Ressourcengruppe</span><span class="sxs-lookup"><span data-stu-id="8a2ae-118">Create a Resource Group</span></span>

<span data-ttu-id="8a2ae-119">Nachdem nun alles eingerichtet ist, können wir mit der Azure-CLI Ressourcen in Azure erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-119">Now that we've got everything set up, let's use the Azure CLI to create resources within Azure.</span></span>

<span data-ttu-id="8a2ae-120">Erstellen Sie zunächst eine Ressourcengruppe.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-120">First, create a Resource Group.</span></span>  <span data-ttu-id="8a2ae-121">Ressourcengruppen ermöglichen in Azure die Verwaltung mehrerer Ressourcen, die Sie zu einer logischen Gruppe zusammenfassen möchten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-121">Resource Groups in Azure provide a way to manage multiple resources that you want to logically group.</span></span>  <span data-ttu-id="8a2ae-122">So können Sie etwa eine Ressourcengruppe für eine Anwendung oder für ein Projekt erstellen und darin einen virtuellen Computer, eine Datenbank und einen CDN-Dienst hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-122">For example, you might create a Resource Group for an application or project and add a virtual machine, a database and a CDN service within it.</span></span>

<span data-ttu-id="8a2ae-123">Hier erstellen wir eine Ressourcengruppe namens „MyResourceGroup“ in der Azure-Region *westus2*.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-123">Let's create a resource group named "MyResourceGroup" in the *westus2* region of Azure.</span></span>  <span data-ttu-id="8a2ae-124">Geben Sie hierzu folgenden Befehl ein:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-124">To do so type the following command:</span></span>

```azurecli-interactive
az group create -n MyResourceGroup -l westus2 
```

<span data-ttu-id="8a2ae-125">Nachdem die Ressourcengruppe erstellt wurde, werden mit dem Befehl `az group create` mehrere Eigenschaften der neu erstellten Ressource ausgegeben:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-125">Once the resource group has been created, the `az group create` command outputs several properties of the newly created resource:</span></span>

```Output
{
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup",
  "location": "westus2",
  "managedBy": null,
  "name": "MyResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="8a2ae-126">Erstellen eines virtuellen Linux-Computers</span><span class="sxs-lookup"><span data-stu-id="8a2ae-126">Create a Linux Virtual Machine</span></span>

<span data-ttu-id="8a2ae-127">Nachdem wir nun über eine Ressourcengruppe verfügen, erstellen wir darin einen virtuellen Linux-Computer.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-127">Now that we have our resource group, let's create a Linux VM within it.</span></span>

<span data-ttu-id="8a2ae-128">Sie können einen virtuellen Linux-Computer mithilfe des beliebten UbuntuLTS-Images mit zwei angefügten Speicherdatenträgern der Größe 10 GB und 20 GB erstellen, indem Sie den folgenden Befehl verwenden:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-128">You can create a Linux VM using the popular UbuntuLTS image, with two attached storage disks of 10 GB and 20 GB, with the following command:</span></span>

```azurecli-interactive
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS --data-disk-sizes-gb 10 20
```

<span data-ttu-id="8a2ae-129">Wenn Sie den obigen Befehl ausführen, sucht Azure CLI 2.0 im Verzeichnis „~/.ssh“ nach einem gespeicherten SSH-Schlüsselpaar.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-129">When you run the preceding command, the Azure CLI 2.0 looks for an SSH key pair stored under your ~/.ssh directory.</span></span>  <span data-ttu-id="8a2ae-130">Falls Sie an diesem Speicherort nicht bereits ein SSH-Schlüsselpaar gespeichert haben, können Sie es von der Azure-CLI automatisch erstellen lassen. Übergeben Sie hierzu den Parameter „--generate-ssh-keys“:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-130">If you don't already have an SSH key pair stored there, you can ask the Azure CLI to automatically create one for you by passing the --generate-ssh-keys parameter:</span></span>

```azurecli-interactive
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS --data-disk-sizes-gb 10 20 --generate-ssh-keys
```

<span data-ttu-id="8a2ae-131">Mit dem Befehl `az vm create` wird die Ausgabe durchgeführt, nachdem die VM vollständig erstellt wurde und bereit für den Zugriff und die Nutzung ist.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-131">The `az vm create` command returns output once the VM has been fully created and is ready to be accessed and used.</span></span> <span data-ttu-id="8a2ae-132">Die Ausgabe umfasst mehrere Eigenschaften der neu erstellten VM, z.B. deren öffentliche IP-Adresse:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-132">The output includes several properties of the newly created VM including its public IP address:</span></span>

```Output
{
  "fqdns": "",
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyLinuxVM",
  "location": "westus2",
  "macAddress": "xx-xx-xx-xx-xx-xx",
  "powerState": "VM running",
  "privateIpAddress": "xx.x.x.x",
  "publicIpAddress": "xx.xxx.xxx.xx",
  "resourceGroup": "MyResourceGroup"
}
```

<span data-ttu-id="8a2ae-133">Nach Erstellung des virtuellen Computers können Sie sich bei Ihrem neuen virtuellen Linux-Computer anmelden. Verwenden Sie hierzu **SSH** und die öffentliche IP-Adresse des virtuellen Computers, den Sie erstellt haben:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-133">Now that the VM has been created, you can log on to your new Linux VM using **SSH** with the public IP address of the VM you created:</span></span>

```azurecli-interactive
ssh xx.xxx.xxx.xxx
```

```Output
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sun Feb 19 00:32:28 UTC 2017

  System load: 0.31              Memory usage: 3%   Processes:       89
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

my-login@MyLinuxVM:~$
```

## <a name="create-a-windows-server-virtual-machine"></a><span data-ttu-id="8a2ae-134">Erstellen eines virtuellen Windows Server-Computers</span><span class="sxs-lookup"><span data-stu-id="8a2ae-134">Create a Windows Server Virtual Machine</span></span>

<span data-ttu-id="8a2ae-135">Als Nächstes erstellen wir eine VM basierend auf Windows Server 2016 Datacenter, indem wir den Befehl `az vm create` verwenden und die VM derselben Ressourcengruppe namens „MyResourceGroup“ hinzufügen, die wir für die Linux-VM genutzt haben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-135">Let's now create a Windows Server 2016 Datacenter-based VM using the `az vm create` command and add it to the same "MyResourceGroup" resource group that we used for our Linux VM.</span></span>  <span data-ttu-id="8a2ae-136">Wie im Beispiel für die Linux-VM auch, fügen wir mit dem Parameter `--data-disk-sizes-gb` zwei Speicherdatenträger hinzu.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-136">Like the Linux VM example, we'll also attach two storage disks using the `--data-disk-sizes-gb` parameter.</span></span>

<span data-ttu-id="8a2ae-137">Für Azure ist es erforderlich, dass Sie die Verwendung von Benutzernamen und Kennwörtern vermeiden, die leicht erraten werden können.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-137">Azure requires that you avoid using easily guessed usernames/passwords.</span></span> <span data-ttu-id="8a2ae-138">Es gelten bestimmte Regeln, welche Zeichen zulässig sind, und auch die Mindestlänge von Benutzername und Kennwort ist vorgegeben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-138">There are specific rules for what characters can be used as well as the minimum length of both username and password.</span></span>  

> [!NOTE]
> <span data-ttu-id="8a2ae-139">Beim Ausführen dieses Befehls werden Sie aufgefordert, Ihren Benutzernamen und Ihr Kennwort einzugeben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-139">You will be prompted to enter your username and password when running this command.</span></span>

```azurecli-interactive
az vm create -n MyWinVM -g MyResourceGroup --image Win2016Datacenter
```

<span data-ttu-id="8a2ae-140">Der Befehl `az vm create` gibt Ergebnisse aus, wenn der virtuelle Computer vollständig erstellt wurde und einsatzbereit ist.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-140">The `az vm create` command output results once the VM has been fully created and is ready to be accessed and used.</span></span>

```Output
{
  "fqdns": "",
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWinVM",
  "location": "westus2",
  "macAddress": "xx-xx-xx-xx-xx-xx",
  "powerState": "VM running",
  "privateIpAddress": "xx.x.x.x",
  "publicIpAddress": "xx.xxx.xx.xxx",
  "resourceGroup": "MyResourceGroup"
}
```

<span data-ttu-id="8a2ae-141">Melden Sie sich nun unter Verwendung von Remotedesktop und der öffentlichen IP-Adresse des virtuellen Computers (wird in der Ausgabe von `az vm create` zurückgegeben) bei Ihrem neu erstellten virtuellen Windows Server-Computer an.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-141">Now log on to your newly created Windows Server VM using Remote Desktop and the public IP address of the VM (which is returned in the output from `az vm create`).</span></span>  
<span data-ttu-id="8a2ae-142">Bei einem Windows-basierten System können Sie hierzu über die Befehlszeile den Befehl `mstsc` ausführen:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-142">If you are on a Windows-based system, you can do this from the command line using the `mstsc` command:</span></span>

```azurecli-interactive
mstsc /v:xx.xxx.xx.xxx
```

<span data-ttu-id="8a2ae-143">Geben Sie bei der Anmeldung die gleiche Kombination aus Benutzername und Kennwort an, die Sie auch beim Erstellen des virtuellen Computers verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-143">Supply the same username/password combination you used when creating the VM to log in.</span></span>

## <a name="creating-other-resources-in-azure"></a><span data-ttu-id="8a2ae-144">Erstellen anderer Ressourcen in Azure</span><span class="sxs-lookup"><span data-stu-id="8a2ae-144">Creating other resources in Azure</span></span>

<span data-ttu-id="8a2ae-145">Sie wissen nun, wie Sie eine Ressourcengruppe, einen virtuellen Linux-Computer und einen virtuellen Windows Server-Computer erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-145">We've now walked through how to create a Resource Group, a Linux VM, and a Windows Server VM.</span></span> <span data-ttu-id="8a2ae-146">Sie können aber auch noch viele andere Arten von Azure-Ressourcen erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-146">You can create many other types of Azure resources as well.</span></span>  

<span data-ttu-id="8a2ae-147">Alle neuen Ressourcen werden mit dem einheitlichen Benennungsmuster `az <resource type name> create` erstellt.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-147">All new resources are created using a consistent `az <resource type name> create` naming pattern.</span></span>  <span data-ttu-id="8a2ae-148">Mithilfe des folgenden create-Befehls können Sie beispielsweise einen Azure-Netzwerklastenausgleich erstellen, den wir dann unseren neu erstellten virtuellen Computern zuordnen können:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-148">For example, to create an Azure Network Load Balancer that we could then associate with our newly created VMs, we can use the following create command:</span></span>

```azurecli-interactive
az network lb create -n MyLoadBalancer -g MyResourceGroup
```

<span data-ttu-id="8a2ae-149">Wir könnten für unsere Infrastruktur auch ein neues privates virtuelles Netzwerk (in Azure für gewöhnlich als VNET bezeichnet) erstellen. Hierfür wird der folgende create-Befehl verwendet:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-149">We could also create a new private Virtual Network (commonly referred to as a "VNet" within Azure) for our infrastructure using the following create command:</span></span>

```azurecli-interactive
az network vnet create -n MyVirtualNetwork -g MyResourceGroup --address-prefix 10.0.0.0/16
```

<span data-ttu-id="8a2ae-150">Das Praktische an Azure und der Azure-CLI ist, dass wir damit nicht nur eine cloudbasierte Infrastruktur erhalten, sondern auch verwaltete Plattformdienste erstellen können.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-150">What makes Azure and the Azure CLI powerful is that we can use it not just to get cloud-based infrastructure but also to create managed platform services.</span></span>  <span data-ttu-id="8a2ae-151">Die verwalteten Plattformdienste lassen sich zudem mit Infrastrukturelementen zu noch leistungsfähigeren Lösungen kombinieren.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-151">The managed platform services can also be combined with infrastructure to build even more powerful solutions.</span></span>

<span data-ttu-id="8a2ae-152">So können Sie beispielsweise mithilfe der Azure-CLI eine Azure App Service-Instanz erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-152">For example, you can use the Azure CLI to create an Azure AppService.</span></span>  <span data-ttu-id="8a2ae-153">Azure App Service ist ein verwalteter Plattformdienst, der sich bestens zum Hosten von Web-Apps eignet, ohne dass Sie sich dabei Gedanken um die Infrastruktur machen müssen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-153">Azure AppService is a managed platform service that provides a great way to host web apps without having to worry about infrastructure.</span></span>  <span data-ttu-id="8a2ae-154">Nach der Erstellung der Azure App Service-Instanz können Sie darin mithilfe der folgenden create-Befehle zwei neue Azure-Web-Apps erstellen:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-154">After creating the Azure AppService, you can create two new Azure Web Apps within the AppService using the following create commands:</span></span>

```azurecli-interactive
# Create an Azure AppService that we can host any number of web apps within
az appservice plan create -n MyAppServicePlan -g MyResourceGroup

# Create Two Web Apps within the AppService (note: name param must be a unique DNS entry)
az webapp create -n MyWebApp43432 -g MyResourceGroup --plan MyAppServicePlan 
az webapp create -n MyWebApp43433 -g MyResourceGroup --plan MyAppServicePlan 
```

<span data-ttu-id="8a2ae-155">Wenn Sie die Funktionsweise des Musters `az <resource type name> create` verstanden haben, ist die Erstellung von Elementen sehr einfach.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-155">Once you understand the basics of the `az <resource type name> create` pattern, it becomes easy to create anything.</span></span> <span data-ttu-id="8a2ae-156">Hier sind einige gängige Azure-Ressourcentypen und die entsprechenden Erstellungsbefehle der Azure-CLI angegeben:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-156">Following are some popular Azure resource types and the corresponding Azure CLI create commands to create them:</span></span>

```
Resource Type               Azure CLI create command
-------------               ------------------------
Resource Group              az group create
Virtual Machine             az vm create
Virtual Network             az network vnet create
Load Balancer               az network lb create
Managed Disk                az disk create
Storage account             az storage account create
Virtual Machine Scale Set   az vmss create
Azure Container Service     az acs create
Web App                     az webapp create
SQL Database Server         az sql server create
Document DB                 az documentdb create
```

<span data-ttu-id="8a2ae-157">Die [Referenzdokumentation](/cli/azure) enthält weitere Informationen zu ressourcenspezifischen Parametern, die Sie an die obigen Befehle übergeben können, und zu den verfügbaren Ressourcentypen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-157">Visit the [Reference documentation](/cli/azure) to learn more about the additional resource-specific parameters that you can pass to each of the preceding commands and the resource types you can create.</span></span> 

## <a name="useful-tip-optimizing-create-operations-using---no-wait"></a><span data-ttu-id="8a2ae-158">Nützlicher Tipp: Optimieren von Erstellungsvorgängen mit „--no-wait“</span><span class="sxs-lookup"><span data-stu-id="8a2ae-158">Useful tip: Optimizing create operations using --no-wait</span></span>

<span data-ttu-id="8a2ae-159">Beim Erstellen von Ressourcen per Azure CLI 2.0 wird beim Befehl `az <resource type name> create` standardmäßig gewartet, bis die Ressource erstellt wurde und bereit für die Nutzung ist.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-159">By default when you create resources using the Azure CLI 2.0, the `az <resource type name> create` command waits until the resource has been created and is ready for you to use.</span></span>  <span data-ttu-id="8a2ae-160">Wenn Sie beispielsweise eine VM erstellen, wird die Rückgabe für den Befehl `az vm create` standardmäßig erst durchgeführt, nachdem die VM erstellt wurde und bereit für die SSH- bzw. RDP-Verbindung ist.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-160">For example, if you create a VM, the `az vm create` command will, by default, not return until the VM is created and is ready for you to SSH or RDP into it.</span></span>

<span data-ttu-id="8a2ae-161">Der Grund für diesen Ansatz ist, dass so das Schreiben von Automatisierungsskripts vereinfacht wird, die mehrere Schritte mit Abhängigkeiten enthalten (und die erfolgreiche Durchführung einer vorgeschalteten Aufgabe erfordern, bevor fortgefahren werden kann).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-161">We use this approach because it makes it easier to write automation scripts that contain multiple steps with dependencies (and need a prior task to have completed successfully before continuing).</span></span>

<span data-ttu-id="8a2ae-162">Falls Sie vor dem Fortfahren nicht auf die Erstellung einer Ressource warten müssen, können Sie die Option `no-wait` verwenden, um im Hintergrund eine Erstellungsaktion zu starten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-162">If you do not need to wait on creation of a resource before continuing, you can use the `no-wait` option to start a create action in the background.</span></span> <span data-ttu-id="8a2ae-163">Sie können die CLI für andere Befehle weiterverwenden.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-163">You can continue using the CLI for other commands.</span></span>

<span data-ttu-id="8a2ae-164">Bei der folgenden Nutzung von `az vm create` wird eine VM-Bereitstellung gestartet und die Rückgabe dann deutlich schneller durchgeführt (vor dem vollständigen Starten der VM):</span><span class="sxs-lookup"><span data-stu-id="8a2ae-164">For example, the following usage of the `az vm create` starts a VM deployment and then return much more quickly (and before the VM has fully booted):</span></span>

```azurecli-interactive
az vm create -n MyLinuxVM2 -g MyResourceGroup --image UbuntuLTS --no-wait
```

<span data-ttu-id="8a2ae-165">Der Einsatz von `--no-wait` kann bei der erheblichen Optimierung der Leistung Ihrer Automatisierungsskripts hilfreich sein.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-165">Using the `--no-wait` approach can help you optimize the performance of your automation scripts considerably.</span></span>

## <a name="listing-resources-and-formatting-output"></a><span data-ttu-id="8a2ae-166">Auflisten von Ressourcen und Formatieren der Ausgabe</span><span class="sxs-lookup"><span data-stu-id="8a2ae-166">Listing resources and formatting output</span></span>

<span data-ttu-id="8a2ae-167">Sie können den Befehl `list` in der Azure-CLI verwenden, um die in Azure ausgeführten Ressourcen zu ermitteln und aufzulisten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-167">You can use the `list` command within the Azure CLI to find and list the resources running in Azure.</span></span> 

<span data-ttu-id="8a2ae-168">Wie mit dem create-Befehl auch, können Sie Ressourcen per Azure CLI 2.0 auflisten, indem Sie das gängige Benennungsmuster `az <resource type name> list` verwenden, das für alle Ressourcentypen einheitlich ist.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-168">Like with the create command, you can list resources using the Azure CLI 2.0 using a common `az <resource type name> list` naming pattern that is consistent across all resource types.</span></span>  <span data-ttu-id="8a2ae-169">Es sind verschiedene Ausgabeformate und Abfrageoptionen verfügbar, um die Liste mit den Ressourcen auf die gewünschte Weise zu filtern und zu sortieren.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-169">There are various output formats and query options available to filter and sort the list of resources in the way you prefer to see them.</span></span>

<span data-ttu-id="8a2ae-170">Mit `az vm list` wird beispielsweise die Liste mit allen vorhandenen VMs angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-170">For example, `az vm list` shows the list of all VMs you have.</span></span>   

```azurecli-interactive
az vm list 
```
<span data-ttu-id="8a2ae-171">Die zurückgegebenen Werte liegen standardmäßig im JSON-Format vor (aus Platzgründen nur eine Teilausgabe).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-171">The values returned are by default in JSON (only showing partial output for sake of brevity).</span></span>

```json
[
  {
    "availabilitySet": null,
    "diagnosticsProfile": null,
    "hardwareProfile": {
      "vmSize": "Standard_DS1_v2"
    },
    "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/DemoVM010",
    "instanceView": null,
    "licenseType": null,
    "location": "westus2",
    "name": "MyLinuxVM",
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/demorg1/providers/Microsoft.Network/networkInterfaces/DemoVM010VMNic",
          "primary": null,
          "resourceGroup": "MyResourceGroup"
        }
      ]
    },
          ...
          ...
          ...   
]
```

<span data-ttu-id="8a2ae-172">Sie können das Ausgabeformat mit der Option `--output` optional ändern.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-172">You can optionally modify the output format using the `--output` option.</span></span>  <span data-ttu-id="8a2ae-173">Führen Sie den Befehl `az vm list` aus, um die zuvor erstellten Linux- und Windows Server-VMs sowie die am häufigsten verwendeten Eigenschaften einer VM anzuzeigen, indem Sie die leicht lesbare Formatoption *table* nutzen:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-173">Run the `az vm list` command to see both the Linux and Windows Server VMs created earlier, along with the most common properties of a VM, using the easy to read *table* format option:</span></span>

```azurecli-interactive
az vm list --output table
```

```Output
Name       ResourceGroup    Location
---------  ---------------  ----------
MyLinuxVM  MyResourceGroup  westus2
MyWinVM    MyResourceGroup  westus2
```

<span data-ttu-id="8a2ae-174">Sie können die Ausgabeoption *tsv* verwenden, um ein textbasiertes Format mit Tabulatortrennung und ohne Überschriften zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-174">The *tsv* output option can be used to get a text-based, tab-separated format without any headers.</span></span>  <span data-ttu-id="8a2ae-175">Dieses Format ist nützlich, wenn Sie die Ausgabe an ein anderes textbasiertes Tool wie beispielsweise grep senden möchten.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-175">This format is useful when you want to pipe the output into another text-based tool like grep.</span></span> 

```azurecli-interactive
az vm list --output tsv
```

```
None    None            /subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyLinuxVM        None    None    westus2 MyLinuxVM                   None        Succeeded       MyResourceGroup None                    Microsoft.Compute/virtualMachines       XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
None    None            /subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWinVM  None    None    westus2 MyWinVM                 None    Succeeded       MyResourceGroup None                    Microsoft.Compute/virtualMachines       XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```
<span data-ttu-id="8a2ae-176">Der Artikel zu den [Ausgabeformaten](format-output-azure-cli.md) enthält Informationen zu weiteren Möglichkeiten zum Auflisten von Ressourcen und Formatieren der Ausgabe.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-176">Visit the [output formats](format-output-azure-cli.md) article to learn more about the additional ways to list resources and format the output.</span></span>

## <a name="querying-resources-and-shaping-outputs"></a><span data-ttu-id="8a2ae-177">Abfragen von Ressourcen und Formen von Ausgaben</span><span class="sxs-lookup"><span data-stu-id="8a2ae-177">Querying resources and shaping outputs</span></span>

<span data-ttu-id="8a2ae-178">Es kann häufiger vorkommen, dass Sie nur nach den Ressourcen suchen möchten, die einen bestimmte Bedingung erfüllen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-178">Often you want to be able to query for only those resources that meet a specific condition.</span></span>  

<span data-ttu-id="8a2ae-179">Der Befehl `list` verfügt über eine integrierte Unterstützung von Funktionen, die das Filtern von Ressourcen nach dem Namen der Ressourcengruppe einfach machen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-179">The `list` command has built-in support that makes it easy to filter resources by Resource Group name.</span></span>  <span data-ttu-id="8a2ae-180">Beispielsweise können Sie den Parameter `--ResourceGroup` oder `-g` an den Befehl `list` übergeben, um nur die Ressourcen einer bestimmten Ressourcengruppe abzurufen:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-180">For example, you can pass either a `--ResourceGroup` or `-g` parameter to a `list` command to only retrieve those resources within a specific resource group:</span></span>


```azurecli-interactive
az vm list -g MyResourceGroup --output table
```

```Output
Name       ResourceGroup    Location
---------  ---------------  ----------
MyLinuxVM  MyResourceGroup  westus2
MyWinVM    MyResourceGroup  westus2
```

<span data-ttu-id="8a2ae-181">Zur noch besseren Unterstützung von Abfragen können Sie den Parameter `--query` verwenden, um für die Ergebnisse *jedes* `az`-Befehls eine JMESPath-Abfrage durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-181">For even more powerful querying support, you can use the `--query` parameter to execute a JMESPath query on the results of *any* `az` command.</span></span>  <span data-ttu-id="8a2ae-182">Mit JMESPath-Abfragen kann die Ausgabe aller zurückgegebenen Ergebnisse sowohl gefiltert als auch geformt werden.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-182">JMESPath queries can be used both to filter as well as shape the output of any returned result.</span></span>

<span data-ttu-id="8a2ae-183">Führen Sie beispielsweise den folgenden Befehl aus, um eine Abfrage für alle VM-Ressourcen in Ressourcengruppen durchzuführen, die „My“ enthalten:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-183">For example, execute the following command to query for any VM resource within any resource group that contains the letters "My":</span></span>

```azurecli-interactive
az vm list --output table --query "[?contains(resourceGroup,'MY')]" 
```

```Output
ResourceGroup    ProvisioningState    Name       Location    VmId
---------------  -------------------  ---------  ----------  ------------------------------------
MYRESOURCEGROUP  Succeeded            MyLinuxVM  westus2     XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
MYRESOURCEGROUP  Succeeded            MyWinVM    westus2     XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

<span data-ttu-id="8a2ae-184">Anschließend können wir die Ausgabe weiter verfeinern, indem wir die Formungsfunktion von JMESPath-Abfragen zum zusätzlichen Ausgeben von unterschiedlichen Werten verwenden.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-184">We could then choose to further refine the output by using the shaping capability of JMESPath queries to output different values as well.</span></span>  <span data-ttu-id="8a2ae-185">Mit dem folgenden Befehl wird beispielsweise der Typ des Betriebssystemdatenträgers abgerufen, über den die VM ermitteln kann, ob ein Linux- oder Windows-basiertes Betriebssystem verwendet wird:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-185">For example, the following command retrieves the type of OS disk the VM is using to determine whether the OS is Linux or Windows based:</span></span>

```azurecli-interactive
az vm list --output table --query "[?contains(resourceGroup,'MY')].{ VMName:name,OSType:storageProfile.osDisk.osType }" 
```

```Output
VMName     OSType
---------  --------
MyLinuxVM  Linux
MyWinVM    Windows
```

<span data-ttu-id="8a2ae-186">Die JMESPath-Unterstützung in der Azure-CLI ist sehr leistungsstark.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-186">The JMESPath support in Azure CLI is powerful.</span></span>  <span data-ttu-id="8a2ae-187">Weitere Informationen zur Verwendung finden Sie im Artikel zu [Abfragen](query-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-187">Learn more about how to use it in our [query](query-azure-cli.md) article.</span></span>

## <a name="deleting-resources"></a><span data-ttu-id="8a2ae-188">Löschen von Ressourcen</span><span class="sxs-lookup"><span data-stu-id="8a2ae-188">Deleting resources</span></span>

<span data-ttu-id="8a2ae-189">Sie können den Befehl `delete` in der Azure-CLI nutzen, um nicht mehr benötigte Ressourcen zu löschen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-189">You can use the `delete` command within Azure CLI to delete the resources you no longer need.</span></span> <span data-ttu-id="8a2ae-190">Sie können den Befehl `delete` – wie auch beim Befehl `create` – mit einer beliebigen Ressource verwenden.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-190">You can use the `delete` command with any resource just like you can with the `create` command.</span></span>

```azurecli-interactive
az vm delete -n MyLinuxVM -g MyResourceGroup
```

<span data-ttu-id="8a2ae-191">Standardmäßig zeigt die CLI eine Aufforderung zum Bestätigen des Löschvorgangs an.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-191">By default the CLI prompts to confirm deletion.</span></span>  <span data-ttu-id="8a2ae-192">Sie können diese Aufforderung für automatisierte Skripts unterdrücken.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-192">You can suppress this prompt for automated scripts.</span></span>

```Output
Are you sure you want to perform this operation? (y/n): y
EndTime                           Name                                  StartTime                         Status
--------------------------------  ------------------------------------  --------------------------------  ---------
2017-02-19T02:35:56.678905+00:00  5b74ab80-9b29-4329-b483-52b406583e2f  2017-02-19T02:33:35.372769+00:00  Succeeded
```

<span data-ttu-id="8a2ae-193">Außerdem können Sie den Befehl `delete` nutzen, um mehrere Ressourcen gleichzeitig zu löschen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-193">You can also use the `delete` command to delete many resources at a time.</span></span> <span data-ttu-id="8a2ae-194">Der folgende Befehl löscht beispielsweise alle Ressourcen der Ressourcengruppe „MyResourceGroup“, die wir in den Beispielen dieses Tutorials verwendet haben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-194">For example, the following command deletes all the resources in the "MyResourceGroup" resource group that we've used for all the samples in this Get Started tutorial.</span></span>

```azurecli-interactive
az group delete -n MyResourceGroup
```

```Output
Are you sure you want to perform this operation? (y/n): y
```

## <a name="get-samples"></a><span data-ttu-id="8a2ae-195">Herunterladen von Beispielen</span><span class="sxs-lookup"><span data-stu-id="8a2ae-195">Get samples</span></span>

<span data-ttu-id="8a2ae-196">Weitere Informationen zu den Verwendungsmöglichkeiten der Azure-CLI finden Sie in unseren allgemeinen Skripts für [virtuelle Linux-Computer](/azure/virtual-machines/virtual-machines-linux-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), [virtuelle Windows-Computer](/azure/virtual-machines/virtual-machines-windows-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), [Web-Apps](/azure/app-service-web/app-service-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json) und [SQL-Datenbank](/azure/sql-database/sql-database-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a2ae-196">To learn more about ways to use the Azure CLI, check out our most common scripts for [Linux VMs](/azure/virtual-machines/virtual-machines-linux-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), [Windows VMs](/azure/virtual-machines/virtual-machines-windows-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), [Web apps](/azure/app-service-web/app-service-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), and [SQL Database](/azure/sql-database/sql-database-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json).</span></span>

## <a name="read-the-api-reference-docs"></a><span data-ttu-id="8a2ae-197">Lesen Sie die API-Referenzdokumente</span><span class="sxs-lookup"><span data-stu-id="8a2ae-197">Read the API reference docs</span></span>

[<span data-ttu-id="8a2ae-198">API-Referenz</span><span class="sxs-lookup"><span data-stu-id="8a2ae-198">API reference</span></span>](/cli/azure)

## <a name="get-help"></a><span data-ttu-id="8a2ae-199">Hier erhalten Sie Hilfe</span><span class="sxs-lookup"><span data-stu-id="8a2ae-199">Get help</span></span>

<span data-ttu-id="8a2ae-200">Die Azure-CLI verfügt über eine integrierte Hilfedokumentation, die unserer Webdokumentation entspricht. Sie können sie über die Befehlszeile ausführen:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-200">The Azure CLI has built-in help documentation, which matches our web documentation that you can run from the command line:</span></span>

```azurecli-interactive
az [command-group [command]] -h
```

<span data-ttu-id="8a2ae-201">Verwenden Sie beispielsweise Folgendes, um anzuzeigen, welche Befehle und Untergruppen für VMs verfügbar sind:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-201">For example, to see what commands and subgroups are available for VMs, use:</span></span>

```azurecli-interactive
az vm -h
```

<span data-ttu-id="8a2ae-202">Verwenden Sie Folgendes, um Hilfe zum Befehl für die Erstellung einer VM zu erhalten:</span><span class="sxs-lookup"><span data-stu-id="8a2ae-202">To get help with the command to create a VM, use:</span></span>

```azurecli-interactive
az vm create -h
```

## <a name="switch-from-azure-cli-10"></a><span data-ttu-id="8a2ae-203">Durchführen der Umstellung von Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8a2ae-203">Switch from Azure CLI 1.0</span></span>

<span data-ttu-id="8a2ae-204">Wenn Sie mit der Nutzung von Azure CLI 1.0 (azure.js) bereits vertraut sind, wird Ihnen auffallen, dass sich einige Befehle geändert haben.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-204">If you already know how to use Azure CLI 1.0 (azure.js), you'll notice places where the commands aren't quite the same.</span></span>
<span data-ttu-id="8a2ae-205">In einigen Fällen unterscheiden sich die Befehle zum Durchführen einer Aufgabe relativ stark.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-205">Sometimes the commands to perform a task are significantly different.</span></span>
<span data-ttu-id="8a2ae-206">Als Hilfe für die Umstellung von Azure CLI 1.0 auf Azure CLI 2.0 haben wir damit begonnen, [diese Befehlszuordnung](https://github.com/Azure/azure-cli/blob/master/doc/azure2az_commands.rst) zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a2ae-206">To help you make the switch from Azure CLI 1.0 to Azure CLI 2.0, we've started this [command mapping](https://github.com/Azure/azure-cli/blob/master/doc/azure2az_commands.rst).</span></span>

## <a name="send-us-your-feedback"></a><span data-ttu-id="8a2ae-207">Senden Sie uns Feedback</span><span class="sxs-lookup"><span data-stu-id="8a2ae-207">Send us your feedback</span></span>

```azurecli-interactive
az feedback
```