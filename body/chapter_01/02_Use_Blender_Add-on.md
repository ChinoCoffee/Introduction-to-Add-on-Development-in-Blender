# 2. Blenderのアドオンを使ってみよう

Blenderのアドオンの開発に入る前に、他の人が作成したアドオンを使ってみましょう。
ここで紹介する手順は今後アドオンを開発する時に頻繁に行うため、ぜひ覚えておきましょう。

## Blenderの日本語化

Blenderは公式で日本語をサポートしています。
英語では敷居が高いと感じてしまう方もいらっしゃると思いますので、Blenderを日本語化してしまいましょう。

**Info** ウィンドウの **File** > **User Preferences...** を選択してください。

![アドオンの日本語化 手順1](https://dl.dropboxusercontent.com/s/8xx2l59wy2d7c8y/localizing_into_japanese_1.png "アドオン日本語化 手順1")

すると、 **Blender User Preferences** ウィンドウが立ち上がりますので、 **System** タブを選択してください。
**International Fonts** にチェックを入れると、Blenderの言語を変更することができます。

![アドオンの日本語化 手順2](https://dl.dropboxusercontent.com/s/6uwpij0r5riiqk3/localizing_into_japanese_2.png "アドオン日本語化 手順2")

**Language** を **Japanese（日本語）** に、 **Translate** で日本語化したいものを選択することで日本語化されます。

![アドオンの日本語化 手順3](https://dl.dropboxusercontent.com/s/s5mrd72si2xq910/localizing_into_japanese_3.png "アドオン日本語化 手順3")

以降の説明では、Blenderが日本語化されていることを前提に解説します。

## アドオンの種類

Blenderのアドオンには、**サポートレベル** により以下の3種類に分類されます。

|サポートレベル|説明|
|---|---|
|Release|Blenderが公式にサポートしているアドオンで、Blender本体と共に提供されます。アドオンは厳密にレビュー（審査）され、不具合が比較的少ない安定したアドオンです。|
|Contrib|Blender本体と共に提供されます。サポートは各個人が行うためofficialに比べて品質は落ちます。しかしContribとして登録されるためには、コミュニティのレビューにて一定の評価を得る必要があるため、一定の品質が保たれテイルと共に、新規性のある機能が集まっています。|
|External|Blender本体には含まれないアドオンで、ユーザ自らアドオンをインストールする必要があります。レビューされていないため、利用は自己責任となります。作業効率化等のBlenderの機能をサポートするものが多く含まれるようですが、中にはContrib以上の機能性を持つアドオンも存在します。|

## アドオンのインストール

**Release** と **Contrib** は、Blender本体と共に提供されるため、インストール作業は不要です。
ここでは、 **External** のアドオンのインストール方法について説明します。
筆者がアドオン開発でいつもお世話になっている **mifth** さんのアドオン **Mira Tools** をインストールしてみます。
**Mira Tools** の機能は、 https://github.com/mifth/mifthtools/wiki/Mira-Tools から確認することができます。
すべて英語であるため、やや敷居が高くなってしまっていますが、 **External** のアドオンの中でも非常に高機能なアドオンですので、ぜひ1度使ってみてください。
**Mira Tools** のインストール方法は前述のURLにも記載されていますが、改めてここでもインストール方法を紹介します。

1. アドオンのダウンロード
  * https://github.com/mifth/mifthtools/archive/master.zip からmifthさんが作成したアドオン一式をダウンロードします。
2. ダウンロードした **mifthtools-master.zip** を解凍します
3. **Mira Tools** は、解凍してできたディレクトリの中から ```mifthtools-master/blender/addons/mira_tools``` にあります。このフォルダ一式を、Blenderが用意しているフォルダ内にコピーします。コピーが完了したら、インストールが完了です。

OSごとのアドオンのインストール先を以下に示します。
インストール先のフォルダが無い場合は、新たに作成してください。

|OS|インストール先|
|---|---|
|Windows|```C:\Users\<ユーザ名>\AppData\Roaming\Blender Foundation\Blender\<Blenderのバージョン>\scripts\addons```|
|Mac|```/Users/<ユーザ名>/Library/Application Support/Blender/<Blenderのバージョン>/scripts/addons```|
|Linux|```/home/<ユーザ名>/.config/blender/<Blenderのバージョン>/scripts/addons```|

ここでコピーしたファイルの中に、拡張子が ```.py``` であるファイルがあったと思います。
このファイルはアドオンの **ソースコード** と呼ばれ、 **Python** というプログラミング言語で書かれています。

## アドオンの有効化

アドオンを有効化して、使えるようにしましょう。
紹介する手順は、 **Release**・**Contrib**・**External** いずれのアドオンについても共通の方法で有効化できます。
ここでは、先ほどダウンロードした **Mira Tools** を有効化します。

最初にBlenderを開きます。
Blenderを開いたら、**情報** ウィンドウの **ファイル** > **ユーザ設定** を選択してください。

![アドオンの有効化 手順1](https://dl.dropboxusercontent.com/s/9it3p8rth2heyqi/enable_add-on_1.png "アドオンの有効化 手順1")

**Blenderユーザ設定** が別窓で開くので、**アドオン** タブを選択しましょう。
検索窓に *mira tools* と入力しましょう。
すると右側にインストールした **Mira Tools** が表示されるので、チェックボックスにチェックを入れます。

![アドオンの有効化 手順2](https://dl.dropboxusercontent.com/s/k4xq9zyhk0hbivp/enable_add-on_2.png "アドオンの有効化 手順2")

これでアドオン **Mira Tools** が有効化されました。
実際にアドオンが有効化されているかは、 **3Dビュー** の左側の **ツールシェルフ** のタブに **Mira** が追加されていることで確認できます。

![アドオンの有効化 手順3](https://dl.dropboxusercontent.com/s/qqvxodqbs67yy45/enable_add-on_3.png "アドオンの有効化 手順3")

## アドオンの無効化

続いてアドオンを無効化する方法を示します。
紹介する手順は、 **Release**・**Contrib**・**External** いずれのアドオンについても共通の方法で無効化できます。
先ほど有効化した **Mira Tools** を無効化してみましょう。

![アドオンの無効化](https://dl.dropboxusercontent.com/s/t15vvgofl5gs50d/disable_add-on.png "アドオンの無効化")

アドオンを有効化した時と同様、 **Blenderユーザ設定** ウィンドウを開いてください。
**アドオン** タブを選択し、 **Mira Tools** のチェックボックスのチェックを外せばアドオンが無効化されます。

## アドオンのアンインストール

インストールしたアドオンのアンインストールは、アドオン本体を直接削除する方法と、 **Blenderユーザ設定**
からアンインストールする方法の2通りがあります。
インストールした **Mira Tools** をアンインストールしてみましょう。

### アドオン本体を直接削除する方法

アドオンのインストール先からアドオン本体を直接削除することで、アドオンをアンインストールすることができます。

アドオン本体のファイルが分からない場合は、 **Blenderユーザ設定** の **アドオン** タブから確認することができます。
左の矢印をクリックして **Mira Tools** の詳細情報を確認してみましょう。
詳細情報の中の **ファイル** がアドオン本体が置かれた場所です。

![アドオンの詳細情報を表示](https://dl.dropboxusercontent.com/s/7onrbdzxctp4uqw/show_add-on_detail.png "アドオンの詳細情報を表示")

この時注意する必要があるのは、アドオン本体が複数のファイルの場合とアドオン本体が単一のファイルの場合の2通りあることです。

ファイル名が ```__init__.py``` である場合は、アドオンが複数のファイルで構成されています。
複数のファイルで構成されている場合は、 ```__init__.py``` が置かれているディレクトリごと削除する必要があります。

もし ```__init__.py``` 以外であれば単一ファイルで構成されているので、詳細情報中の **ファイル** に示されたファイルを削除すれば、アンインストールが完了したことになります。

### Blederユーザ設定からアンインストールする方法

**Blenderユーザ設定** からアンインストールすることもできます。
**Blenderユーザ設定** の **アドオン** タブを選択し、**Mira Tools** の左の矢印をクリックして詳細情報を開きます。
**削除** ボタンをクリックすることで、アンインストールすることができます。

![アドオンのアンインストール](https://dl.dropboxusercontent.com/s/0hkgrg49n0kh880/uninstall_add-on.png "アドオンのアンインストール")

## まとめ

### ポイント