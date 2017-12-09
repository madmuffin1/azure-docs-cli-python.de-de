---
title: Installieren der Azure CLI mit Docker
description: Installieren eines Docker-Containers mit der Azure CLI 2.0
keywords: Azure CLI,Azure CLI installieren,Azure Docker,Azure Docker-Image,
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 10/30/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 76ecf2c9cd0e6e694a31ac160112d1348863f118
ms.sourcegitcommit: 905939cc44764b4d1cc79a9b36c0793f7055a686
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="install-azure-cli-20-with-docker"></a>Installieren der Azure CLI 2.0 mit Docker

Sie können Docker zum Installieren eines eigenständigen Linux-Containers mit der vorinstallierten Azure CLI 2.0 verwenden. Dies ermöglicht einen schnellen Einstieg in eine Umgebung, in der Sie die CLI ausprobieren und somit testen können, ob sie für Sie geeignet ist. Eine Verwendung als Basisimage ist ebenfalls möglich.

## <a name="install-with-docker"></a>Installieren mit Docker

Installieren Sie die CLI mit `docker run`.

   ```bash
   docker run -it azuresdk/azure-cli-python:<version>
   ```

Verfügbare Versionen finden Sie in unseren [Docker-Tags](https://hub.docker.com/r/azuresdk/azure-cli-python/tags/).

Die CLI wird in dem Image als Befehl `az` in `/usr/local/bin` installiert.

> [!NOTE]
> Wenn Sie die SSH-Schlüssel aus Ihrer Benutzerumgebung übernehmen möchten, können Sie `-v ${HOME}:/root` verwenden, um $HOME als `/root` bereitzustellen.

> ```bash
> docker run -it -v ${HOME}:/root azuresdk/azure-cli-python:<version>
> ```

### <a name="update-with-docker"></a>Aktualisieren mit Docker

Für die Aktualisierung mit Docker ist das Abrufen des neuen Images per Pull und das Neuerstellen vorhandener Container erforderlich. Aus diesem Grund sollten Sie die Verwendung eines Containers vermeiden, der die CLI als Datenspeicher hostet.

1. Aktualisieren Sie Ihr lokales Image mit `docker pull`.

   ```bash
   docker pull azuresdk/azure-cli-python
   ```

2. Rufen Sie die Container ab, die derzeit das CLI-Image verwenden.

   ```bash
   docker container ls -a --filter 'ancestor=azuresdk/azure-cli-python'
   ```

   ```output
   CONTAINER ID        IMAGE                              COMMAND             CREATED             STATUS                        PORTS               NAMES
   34a868beb2ab        azuresdk/azure-cli-python:latest      "/bin/sh -c bash"   8 minutes ago       Exited (0) 8 minutes ago                       inspiring_benz
   ```

  > [!NOTE]
  > Wenn Sie eine bestimmte Version des Images installiert haben, müssen Sie `:<version>` ans Ende des Imagenamens anfügen.

3. Halten Sie die Container an, und erstellen Sie sie neu.

   ```bash
   docker stop inspiring_benz
   docker rm inspiring_benz
   docker run azuresdk/azure-cli-python
   ```

### <a name="uninstall-with-docker"></a>Deinstallieren mit Docker

Es tut uns leid, wenn Sie die Azure CLI deinstallieren möchten. Teilen Sie uns vor der Deinstallation mithilfe des Befehls `az feedback` mit, warum Sie sich für die Deinstallation entschieden haben und wie wir die CLI verbessern können. Wir möchten sicherstellen, dass die Azure CLI möglichst fehlerfrei und benutzerfreundlich ist. Sie können auch ein [GitHub-Problem melden](https://github.com/Azure/azure-cli/issues).

Um das CLI-Docker-Image ordnungsgemäß zu deinstallieren, müssen Sie alle Container mit diesem Image entfernen und dann das lokale Image löschen.

1. Rufen Sie die Container ab, die das azure-cli-Image ausführen.

   ```bash
   docker container ls -a --filter 'ancestor=azuresdk/azure-cli-python'
   ```

   ```output
   CONTAINER ID        IMAGE                              COMMAND             CREATED             STATUS                        PORTS               NAMES
   34a868beb2ab        azuresdk/azure-cli-python:latest      "/bin/sh -c bash"   8 minutes ago       Exited (0) 8 minutes ago                       inspiring_benz
   ```
  > [!NOTE]
  > Wenn Sie eine bestimmte Version des Images installiert haben, müssen Sie `:<version>` ans Ende des Imagenamens anfügen.

2. Löschen Sie alle Container mit dem CLI-Image.

   ```bash
   docker rm 34a868beb2ab
   ```

3. Entfernen Sie das lokal installierte CLI-Image.

   ```bash
   docker rmi azuresdk/azure-cli-python
   ```
