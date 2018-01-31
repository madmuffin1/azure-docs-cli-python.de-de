---
title: Verwalten mehrerer Clouds mit der Azure CLI 2.0
description: "Die Azure CLI 2.0 ermöglicht die Erstellung, Anmeldung und Verwaltung von bzw. bei verschiedenen Clouds."
keywords: Azure CLI 2.0, Azure, Clouds, Datencenter, Regierung, Region, China, Deutschland
author: sptramer
manager: routlaw
ms.author: sttramer
ms.date: 10/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.openlocfilehash: 6f4cfec45becc0c4940e9066af53396b41db779d
ms.sourcegitcommit: 16426a08c0f2f62d0b9dca3df8132cece659acff
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="managing-multiple-clouds-with-azure-cli-20"></a>Verwalten mehrerer Clouds mit der Azure CLI 2.0

Wenn Sie regionsübergreifend arbeiten oder [Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/) verwenden, müssen Sie möglicherweise mehrere Clouds verwenden. Hierzu stellt Ihnen Microsoft Clouds zur Verfügung, die mit regionalen Gesetzen in Einklang stehen. In diesem Artikel erfahren Sie, wie Sie Informationen zu Clouds abrufen, die für Ihr Konto verfügbar sind, wie Sie die aktuelle Cloud ändern und wie Sie neue Clouds für die Verwendung mit Azure Stack registrieren bzw. die Registrierung aufheben.

## <a name="listing-clouds"></a>Auflisten von Clouds

Die verfügbaren Clouds können mit dem Befehl [cloud list](/cli/azure/cloud#list) aufgelistet werden. So erfahren Sie, welche Cloud derzeit aktiv ist, und erhalten Informationen zum aktuellen Profil, zu regionalen Suffixen und zu Hostnamen.

Gehen Sie wie folgt vor, um die aktive Cloud und eine Liste mit allen verfügbaren Clouds abzurufen:

```azurecli
az cloud list --output table
```

```output
IsActive    Name               Profile
----------  -----------------  ---------
True        AzureCloud         latest
            AzureChinaCloud    latest
            AzureUSGovernment  latest
            AzureGermanCloud   latest
```

Für die derzeit aktive Cloud ist in der Spalte `IsActive` der Wert `True` angegeben. Es kann immer nur eine Cloud aktiv sein. Ausführlichere Informationen zu einer Cloud (einschließlich der Endpunkte, die sie für Azure-Dienste verwendet) erhalten Sie mit dem Befehl `cloud show`:

```azurecli
az cloud show --name AzureChinaCloud --output json
```

```output
{
  "endpoints": {
    "activeDirectory": "https://login.chinacloudapi.cn",
    "activeDirectoryDataLakeResourceId": null,
    "activeDirectoryGraphResourceId": "https://graph.chinacloudapi.cn/",
    "activeDirectoryResourceId": "https://management.core.chinacloudapi.cn/",
    "batchResourceId": "https://batch.chinacloudapi.cn/",
    "gallery": "https://gallery.chinacloudapi.cn/",
    "management": "https://management.core.chinacloudapi.cn/",
    "resourceManager": "https://management.chinacloudapi.cn",
    "sqlManagement": "https://management.core.chinacloudapi.cn:8443/",
    "vmImageAliasDoc": "https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json"
  },
  "isActive": false,
  "name": "AzureChinaCloud",
  "profile": "latest",
  "suffixes": {
    "azureDatalakeAnalyticsCatalogAndJobEndpoint": null,
    "azureDatalakeStoreFileSystemEndpoint": null,
    "keyvaultDns": ".vault.azure.cn",
    "sqlServerHostname": ".database.chinacloudapi.cn",
    "storageEndpoint": "core.chinacloudapi.cn"
  }
}
```

## <a name="switching-the-active-cloud"></a>Wechseln der aktiven Cloud

Führen Sie zum Wechseln der aktiven Cloud den Befehl [cloud set](/cli/azure/cloud#set) aus. Dieser Befehl erfordert ein Argument: den Namen der Cloud.

```azurecli
az cloud set --name AzureChinaCloud
```

> [!IMPORTANT]
> Sollte die Authentifizierung für die aktivierte Cloud abgelaufen sein, müssen Sie sich erneut authentifizieren, bevor Sie weitere CLI-Aufgaben ausführen. Beim erstmaligen Wechsel zu der neuen Cloud muss auch das aktive Abonnement festgelegt werden.
> Anleitungen zur Authentifizierung finden Sie unter [Log in with Azure CLI 2.0](authenticate-azure-cli.md) (Anmelden bei der Azure CLI 2.0). Weitere Informationen zur Abonnementverwaltung finden Sie unter [Verwalten mehrerer Azure-Abonnements](manage-azure-subscriptions-azure-cli.md).

## <a name="register-a-cloud"></a>Registrieren einer Cloud

Registrieren Sie eine neue Cloud, wenn Sie über eigene Endpunkte für Azure Stack verfügen. Eine Cloud wird mit dem Befehl [cloud register](/cli/azure/cloud#register) erstellt. Dieser Befehl erfordert einen Namen und einen Satz von Funktionen mit den dazugehörigen Endpunkten. Informationen zum Registrieren einer Cloud für die Verwendung mit Azure Stack finden Sie unter [Installieren und Konfigurieren der CLI für die Verwendung mit Azure Stack](/azure/azure-stack/user/azure-stack-connect-cli#connect-to-azure-stack).

Für China, US Government oder deutsche Regionen müssen Sie Ihre eigene Cloud nicht registrieren. Diese werden von Microsoft verwaltet und sind standardmäßig verfügbar.  Weitere Informationen zu allen verfügbaren Endpunkteinstellungen finden Sie in der [Dokumentation für `az cloud register`](/cli/azure/cloud?view=azure-cli-latest#az_cloud_register).

Durch Registrieren einer Cloud wird nicht automatisch zu dieser Cloud gewechselt. Wählen Sie die neu erstellte Cloud wie weiter oben beschrieben mithilfe des Befehls `az cloud set` aus.

## <a name="update-an-existing-cloud"></a>Aktualisieren einer vorhandenen Cloud

Sie können auch eine vorhandene Cloud aktualisieren, sofern Sie über die erforderlichen Berechtigungen verfügen. Führen Sie diesen Schritt aus, wenn Sie zu einem anderen Azure-Profil wechseln oder einen Endpunkt hinzufügen oder ändern müssen.
Verwenden Sie dazu den Befehl `az cloud update`. Dieser akzeptiert die gleichen Argumente wie `az cloud register`. Weitere Informationen finden Sie in der [Dokumentation für `az cloud update`](/cli/azure/cloud?view=azure-cli-latest#az_cloud_update).

## <a name="unregister-a-cloud"></a>Aufheben der Registrierung einer Cloud

Wenn Sie eine registrierte Cloud nicht mehr benötigen, können Sie die Registrierung mit dem Befehl [cloud unregister](/cli/azure/cloud#unregister) aufheben:

```azurecli
az cloud unregister --name MyCloud
```