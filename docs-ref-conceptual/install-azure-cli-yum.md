---
title: Installieren der Azure CLI 2.0 unter Linux mit yum
description: Installieren der Azure CLI 2.0 mit yum
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 01/29/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-cli
ms.devlang: azure-cli
ms.openlocfilehash: b3c82825af3d1d2420b0111d1a370a17f37d9426
ms.sourcegitcommit: ae72b6c8916aeb372a92188090529037e63930ba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="install-azure-cli-20-with-yum"></a>Installieren der Azure CLI 2.0 mit yum

Wenn Sie eine Distribution mit `yum` verwenden (etwa RHEL, Fedora oder CentOS), steht ein Paket für die Azure CLI zur Verfügung. Dieses Paket wurde mit RHEL 7, Fedora 19 (und höher) und CentOS 7 getestet.

[!INCLUDE [linux-install-requirements.md](includes/linux-install-requirements.md)]

## <a name="install"></a>Installieren

1. Importieren Sie den Microsoft-Repositoryschlüssel.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

2. Erstellen Sie lokale `azure-cli`-Repositoryinformationen.

   ```bash
   sudo sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
   ```

3. Installieren Sie mit dem Befehl `yum install`. 

   ```bash
   sudo yum install azure-cli
   ```

Sie können dann die Azure CLI mit dem Befehl `az` ausführen. Führen Sie den Befehl `az login` aus, um sich anzumelden.

```azurecli
az login
```

Weitere Informationen zu verschiedenen Anmeldemethoden finden Sie unter [Anmelden mit Azure CLI 2.0](authenticate-azure-cli.md).

## <a name="update"></a>Aktualisieren

Aktualisieren Sie die Azure CLI mit dem Befehl `yum update`.

```bash
sudo yum update azure-cli
```

## <a name="uninstall"></a>Deinstallieren

[!INCLUDE [uninstall-boilerplate.md](includes/uninstall-boilerplate.md)]

1. Entfernen Sie das Paket aus Ihrem System.

   ```bash
   sudo yum remove azure-cli
   ```

2. Entfernen Sie die Repositoryinformationen, wenn Sie nicht planen, die CLI neu zu installieren.

   ```bash
   sudo rm /etc/yum.repos.d/azure-cli.repo
   ```

3. Entfernen Sie auch den Microsoft GPG-Signaturschlüssel, falls Sie die Repositoryinformationen entfernt haben.

  ```bash
  MSFT_KEY=`rpm -qa gpg-pubkey /* --qf "%{version}-%{release} %{summary}\n" | grep Microsoft | awk '{print $1}'`
  sudo rpm -e --allmatches gpg-pubkey-$MSFT_KEY
  ```
