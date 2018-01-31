---
title: "Azure CLI 2.0 – Interaktiver Modus"
description: Verwenden Sie die Azure CLI 2.0 im interaktiven Modus.
keywords: Azure CLI 2.0, interaktiver Modus
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/06/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: fb260d7385728acd0c699488ecb5b108afefd08c
ms.sourcegitcommit: 2e4d0bdd94c626e061434883032367b5619de4fe
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/09/2017
---
# <a name="interactive-azure-cli-20"></a>Interaktive Azure CLI 2.0

Sie können die Azure CLI 2.0 im interaktiven Modus verwenden, indem Sie den Befehl `az interactive` ausführen.
So gelangen Sie zu einer interaktiven Shell, in der Ihre Befehle automatisch vervollständigt werden und in der Sie auf Beschreibungen von Befehlen und ihren Parametern sowie auf Befehlsbeispiele zugreifen können.

![Interaktiver Modus](./media/interactive-azure-cli/webapp-create.png)

> [!NOTE]
> Wir verwenden hier nicht das Standarddesign, da es auf einem schwarzen Hintergrund nicht so gut lesbar ist.

Wenn Sie noch nicht bei Ihrem Konto angemeldet sind, verwenden Sie dazu den `login`-Befehl.

## <a name="configure"></a>Konfigurieren

Im interaktiven Modus werden optional Beschreibungen zu Befehlen und Parametern sowie Befehlsbeispiele angezeigt.
Über `F1` können Sie Beschreibungen und Beispiele aktivieren oder deaktivieren.

![Beschreibungen und Beispiele](./media/interactive-azure-cli/descriptions-and-examples.png)

Sie können die Anzeige von Standardwerten für Parameter über `F2` aktivieren oder deaktivieren.

![Standardwerte](./media/interactive-azure-cli/defaults.png)

`F3` schaltet die Anzeige einiger Tastenkombinationen ein oder aus.

![Tastenkombinationen](./media/interactive-azure-cli/gestures.png)

## <a name="scope"></a>Umfang

Sie können den Bereich Ihres interaktiven Modus auf eine bestimmte Befehlsgruppe wie `vm` oder `vm image` festlegen.
In diesem Fall werden alle Befehle für diesen Bereich interpretiert.
Dies ist eine hervorragende Kompakteigenschaft, wenn Sie Ihre gesamte Arbeit in dieser Befehlsgruppe ausführen.

Statt diese Befehle einzugeben:

```azurecli
az>> vm create -n myVM -g myRG --image UbuntuLTS
az>> vm list -o table
```

können Sie den Bereich auf die Befehlsgruppe „vm“ festlegen und folgende Befehle eingeben:

```azurecli
az>> %%vm
az vm>> create -n myVM -g myRG --image UbuntuLTS
az vm>>list -o table
```

Sie können den Bereich auch auf Befehlsgruppen einer niedrigeren Ebene beschränken.
Mit `%%vm image` können Sie den Bereich auf `vm image` festlegen.
Da der Bereich bereits auf `vm` festgelegt ist, verwenden wir in diesem Fall `%%image`.

```azurecli
az vm>> %%image
az vm image>>
```

An diesem Punkt können wir den Bereich mit `%%..` wieder auf `vm` erweitern oder einfach mit `%%` auf das Stammverzeichnis festlegen.

```azurecli
az vm image>> %%
az>>
```

## <a name="query"></a>Abfrage

Sie können eine JMESPath-Abfrage für die Ergebnisse des zuletzt ausgeführten Befehls ausführen.
Beispielsweise können Sie nach der Erstellung eines virtuellen Computers sicherstellen, dass er vollständig bereitgestellt wurde.

```azurecli
az>> vm create --name myVM --resource-group myRG --image UbuntuLTS --no-wait
az>> ? [*].provisioningState
```

```
[
  "Creating"
]
```

Weitere Informationen zum Abfragen der Ergebnisse Ihrer Befehle finden Sie unter [Verwenden von JMESPath-Abfragen mit Azure CLI 2.0](query-azure-cli.md).

## <a name="bash-commands"></a>Bash-Befehle

Mit `#[cmd]` können Sie Shellbefehle ausführen, ohne den interaktiven Modus zu verlassen.

```azurecli
az>> #dir
```

## <a name="examples"></a>Beispiele

Für einige Befehle gibt es zahlreiche Beispiele.
Mit `CTRL-N` können Sie zur nächsten und mit `CTRL-Y` zur vorherigen Seite mit Beispielen scrollen.

![Beispiele](./media/interactive-azure-cli/examples.png)

Über `::#` können Sie sich auch ein bestimmtes Beispiel ansehen.

```azurecli
az>> vm create ::8
```