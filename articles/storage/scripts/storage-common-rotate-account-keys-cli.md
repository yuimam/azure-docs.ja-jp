---
title: "Azure CLI のサンプル スクリプト - ストレージ アカウント アクセス キーのローテーション | Microsoft Docs"
description: "Azure Storage アカウントを作成し、そのアカウント アクセス キーを取得してローテーションします。"
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: sample
ms.date: 06/22/2017
ms.author: tamram
ms.openlocfilehash: 160509a5a82b71b281d57d97e103bb4190605b7c
ms.sourcegitcommit: 8c3267c34fc46c681ea476fee87f5fb0bf858f9e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2018
---
# <a name="create-a-storage-account-and-rotate-its-account-access-keys"></a>ストレージ アカウントを作成してアカウント アクセス キーのローテーションを行う

このスクリプトは、Azure Storage アカウントを作成し、新しいストレージ アカウントのアクセス キーを表示した後、キーの更新 (ローテーション) を行います。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>サンプル スクリプト

[!code-azurecli-interactive[main](../../../cli_scripts/storage/rotate-storage-account-keys/rotate-storage-account-keys.sh "Rotate storage account keys")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ 

次のコマンドを実行して、リソース グループ、ストレージ アカウント、すべての関連リソースを削除します。

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使って、ストレージ アカウントを作成し、そのアクセス キーを取得してローテーションを行います。 表内の各項目は、コマンドごとのドキュメントにリンクされています。

| コマンド | メモ |
|---|---|
| [az group create](/cli/azure/group#az_group_create) | すべてのリソースを格納するリソース グループを作成します。 |
| [az storage account create](/cli/azure/storage/account#az_storage_account_create) | 特定のリソース グループに Azure Storage アカウントを作成します。 |
| [az storage account keys list](/cli/azure/storage/account/keys#az_storage_account_keys_list) | 指定されたアカウントのストレージ アカウント アクセス キーを表示します。 |
| [az storage account keys renew](/cli/azure/storage/account/keys#az_storage_account_keys_renew) | プライマリまたはセカンダリのストレージ アカウント アクセス キーを再生成します。 |

## <a name="next-steps"></a>次の手順

Azure CLI の詳細については、[Azure CLI のドキュメント](/cli/azure)のページをご覧ください。

その他のストレージ CLI サンプル スクリプトは、[Azure Blob ストレージ用の Azure CLI サンプル](../blobs/storage-samples-blobs-cli.md)のページにあります。
