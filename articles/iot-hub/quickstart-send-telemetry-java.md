---
title: Azure IoT Hub への利用統計情報の送信に関するクイック スタート (Java) | Microsoft Docs
description: このクイック スタートでは、2 つのサンプル Java アプリケーションを実行して、IoT ハブにシミュレートされた利用統計情報を送信し、クラウドで処理するために IoT ハブから利用統計情報を読み取ります。
services: iot-hub
author: dominicbetts
manager: timlt
editor: ''
ms.service: iot-hub
ms.devlang: java
ms.topic: quickstart
ms.custom: mvc
ms.tgt_pltfrm: na
ms.workload: ns
ms.date: 04/30/2018
ms.author: dobett
ms.openlocfilehash: d887c690a5f0bc8120daa74d6076083634da08f6
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-the-telemetry-from-the-hub-with-a-back-end-application-java"></a>クイック スタート: デバイスから IoT ハブに利用統計情報を送信し、バックエンド アプリケーション (Java) でハブから利用統計情報を読み取る

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

IoT Hub は、保管や処理のために IoT デバイスから大量の利用統計情報をクラウドに取り込むことを可能にする Azure サービスです。 このクイック スタートでは、シミュレートされたデバイス アプリケーションから、IoT ハブを経由して、処理のためのバックエンド アプリケーションに、利用統計情報を送信します。

このクイック スタートでは、あらかじめ作成されている 2 つの Java アプリケーションを使います。1 つは利用統計情報を送信し、もう 1 つはハブから利用統計情報を読み取ります。 これら 2 つのアプリケーションを実行する前に、IoT ハブを作成し、デバイスをハブに登録します。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Azure サブスクリプションがない場合は、開始する前に[無料アカウント](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)を作成してください。

## <a name="prerequisites"></a>前提条件

このクイック スタートで実行する 2 つのサンプル アプリケーションは、Java を使って書かれています。 開発用コンピューター上に Java SE 8 以降が必要です。

複数のプラットフォームに対応する Java を [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html) からダウンロードできます。

開発コンピューターに現在インストールされている Java のバージョンは、次のコマンドを使って確認できます。

```cmd/sh
java --version
```

サンプルをビルドするには、Maven 3 をインストールする必要があります。 複数のプラットフォームに対応する Maven を [Apache Maven](https://maven.apache.org/download.cgi) からダウンロードできます。

開発コンピューターに現在インストールされている Maven のバージョンは、次のコマンドを使って確認できます。

```cmd/sh
mvn --version
```

https://github.com/Azure-Samples/azure-iot-samples-java/archive/master.zip からサンプル Java プロジェクトをダウンロードし、ZIP アーカイブを抽出します。

## <a name="create-an-iot-hub"></a>IoT Hub の作成

[!INCLUDE [iot-hub-quickstarts-create-hub](../../includes/iot-hub-quickstarts-create-hub.md)]

## <a name="register-a-device"></a>デバイスの登録

デバイスを IoT ハブに接続するには、あらかじめ IoT ハブに登録しておく必要があります。 このクイック スタートでは、Azure CLI を使用して、シミュレートされたデバイスを登録します。

1. IoT Hub CLI 拡張機能を追加し、デバイス ID を作成します。 `{YourIoTHubName}` は、IoT ハブ用に選んだ名前に置き換えます。

    ```azurecli-interactive
    az extension add --name azure-cli-iot-ext
    az iot hub device-identity create --hub-name {YourIoTHubName}--device-id MyJavaDevice
    ```

1. 次のコマンドを実行して、登録したデバイスの "_デバイス接続文字列_" を取得します。

    ```azurecli-interactive
    az iot hub device-identity show-connection-string --hub-name {YourIoTHubName} --device-id MyJavaDevice --output table
    ```

    `Hostname=...=` のようなデバイス接続文字列をメモしておきます。 この値は、このクイック スタートの後の方で使います。

1. また、バックエンド アプリケーションが IoT ハブに接続してメッセージを取得できるようにするには、IoT ハブからの "_Event Hubs 互換エンドポイント_"、"_Event Hubs 互換パス_"、および "_iothubowner 主キー_" も必要です。 次のコマンドは、お使いの IoT ハブに対するこれらの値を取得します。

    ```azurecli-interactive
    az iot hub show --query properties.eventHubEndpoints.events.endpoint --name {YourIoTHubName}

    az iot hub show --query properties.eventHubEndpoints.events.path --name {YourIoTHubName}

    az iot hub policy show --name iothubowner --query primaryKey --hub-name {your IoT Hub name}
    ```

    クイック スタートの後の方で使うので、これら 3 つの値をメモしておきます。

## <a name="send-simulated-telemetry"></a>シミュレートされた利用統計情報の送信

シミュレートされたデバイス アプリケーションは、IoT ハブ上のデバイスに固有のエンドポイントに接続し、シミュレートされた温度と湿度の利用統計情報を送信します。

1. ターミナル ウィンドウで、サンプルの Java プロジェクトのルート フォルダーに移動します。 **Quickstarts\simulated-device** フォルダーに移動します。

1. 適当なテキスト エディターで **src/main/java/com/microsoft/docs/iothub/samples/SimulatedDevice.java** ファイルを開きます。

    `connString` 変数の値を、前にメモしたデバイス接続文字列に置き換えます。 その後、変更を **SimulatedDevice.java** ファイルに保存します。

1. ターミナル ウィンドウで次のコマンドを実行して、必要なライブラリをインストールし、シミュレートされたデバイス アプリケーションをビルドします。

    ```cmd/sh
    mvn clean package
    ```

1. ターミナル ウィンドウで次のコマンドを実行して、シミュレートされたデバイス アプリケーションを実行します。

    ```cmd/sh
    java -jar target/simulated-device-1.0.0-with-deps.jar
    ```

    次のスクリーンショットは、シミュレートされたデバイス アプリケーションが IoT ハブに利用統計情報を送信したときの出力を示しています。

    ![シミュレートされたデバイスを実行する](media/quickstart-send-telemetry-java/SimulatedDevice.png)

## <a name="read-the-telemetry-from-your-hub"></a>ハブから利用統計情報を読み取る

バックエンド アプリケーションは、IoT ハブ上のサービス側 **Events** エンドポイントに接続します。 このアプリケーションは、シミュレートされたデバイスから送信されたデバイスとクラウドの間のメッセージを受信します。 通常、IoT Hub のバックエンド アプリケーションはクラウド内で実行され、デバイスとクラウドの間のメッセージ受信して処理します。

1. 別のターミナル ウィンドウで、サンプルの Java プロジェクトのルート フォルダーに移動します。 **Quickstarts\read-d2c-messages** フォルダーに移動します。

1. 適当なテキスト エディターで **src/main/java/com/microsoft/docs/iothub/samples/ReadDeviceToCloudMessages.java** ファイルを開きます。

    `eventHubsCompatibleEndpoint` 変数の値を、前にメモした Event Hubs 互換エンドポイントに置き換えます。

    `eventHubsCompatiblePath` 変数の値を、前にメモした Event Hubs 互換パスに置き換えます。

    `iotHubSasKey` 変数の値を、前にメモした iothubowner 主キーに置き換えます。 **ReadDeviceToCloudMessages.java** ファイルに変更を保存します。

1. ターミナル ウィンドウで次のコマンドを実行して、必要なライブラリをインストールし、バックエンド アプリケーションをビルドします。

    ```cmd/sh
    mvn clean package
    ```

1. ターミナル ウィンドウで次のコマンドを実行して、バックエンド アプリケーションを実行します。

    ```cmd/sh
    java -jar target/read-d2c-messages-1.0.0-with-deps.jar
    ```

    次のスクリーンショットは、シミュレートされたデバイスがハブに送信した利用統計情報をバックエンド アプリケーションが受信したときの出力を示しています。

    ![バックエンド アプリケーションを実行する](media/quickstart-send-telemetry-java/ReadDeviceToCloud.png)

## <a name="clean-up-resources"></a>リソースのクリーンアップ

次のクイック スタートを行う場合は、リソース グループと IoT ハブをそのままにしておき、後で再利用します。

IoT ハブが必要でなくなった場合は、ポータルを使用して IoT ハブとリソース グループを削除します。 これを行うには、IoT ハブを含む **qs-iot-hub-rg** リソース グループを選び、**[削除]** をクリックします。

## <a name="next-steps"></a>次の手順

このクイック スタートでは、IoT ハブをセットアップし、デバイスを登録し、Java アプリケーションを使ってハブにシミュレートされた利用統計情報を送信し、簡単なバックエンド アプリケーションを使ってハブから利用統計情報を読み取りました。

バックエンド アプリケーションからシミュレートされたデバイスを制御する方法を学習するには、次のクイック スタートに進んでください。

> [!div class="nextstepaction"]
> [クイック スタート: IoT ハブに接続されたデバイスを制御する](quickstart-control-device-java.md)