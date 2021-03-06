<div id="sect_title_img_3_6"></div>

<div id="sect_title_text"></div>

# オーディオファイルを再生する

<div id="preface"></div>

###### 本節ではBlenderが提供するオーディオファイルの再生支援モジュールであるaudモジュールを使って、オーディオファイルを再生する方法を説明します。3DCGを作成するBlenderのアドオンではオーディオファイルを扱うことはほとんどないと思いますが、このようなAPIも用意されているのだという気持ちで読んでもらえればと思います。


## 作成するアドオンの仕様

* *3Dビュー* エリアのツール・シェルフに *オーディオ再生* パネルを追加し、選択したオーディオファイルを再生する
* 再生中の音量を変更可能なUIを提供する

## アドオンを作成する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考にして以下のソースコードをテキスト・エディタに入力し、ファイル名 ```sample_3-6.py``` として保存してください。

[import](../../sample/src/chapter_03/sample_3-6.py)

## アドオンを使用する

### アドオンを有効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考に作成したアドオンを有効化すると、コンソールウィンドウに以下の文字列が出力されます。

```sh
サンプル3-6: アドオン「サンプル3-6」が有効化されました。
```


<div id="sidebyside"></div>

|また、*3Dビュー* エリアのツール・シェルフに *オーディオ再生* パネルが追加されます。|![3-6節 アドオン有効化](https://dl.dropboxusercontent.com/s/kb2nl3uogcae6ze/enable_add-on.png "3-6節 アドオン有効化")|
|---|---|


### アドオンの機能を使用する

以下の手順に従って、作成したアドオンの機能を使ってみます。

<div id="process_title"></div>

##### Work

<div id="process"></div>

|<div id="box">1</div>|*3Dビュー* エリアのツール・シェルフから *オーディオ再生* パネルを選択します。|![3-6節 アドオンの使用 手順1](https://dl.dropboxusercontent.com/s/oaqc04tyq34aad1/use_add-on_1.png "3-6節 アドオンの使用 手順1")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="process"></div>

|<div id="box">2</div>|*オーディオファイルを選択* ボタンをクリックします。|![3-6節 アドオンの使用 手順2](https://dl.dropboxusercontent.com/s/3vtpo2ozecl5zox/use_add-on_2.png "3-6節 アドオンの使用 手順2")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="process"></div>

|<div id="box">3</div>|ファイルブラウザが開くため、再生するオーディオファイルを選択して *オーディオファイルの選択* ボタンをクリックします。本節のサンプルでは、デフォルトで *.wav* 形式と *.mp3* 形式の2つの拡張子に絞って表示していますが、*ファイルのフィルタリングを有効化ボタン* をクリックすることで、他のファイルも選択できるようになります。<br>※左図では空のディレクトリを表示しています|![3-6節 アドオンの使用 手順3](https://dl.dropboxusercontent.com/s/k4724owvnjqo5pk/use_add-on_3.png "3-6節 アドオンの使用 手順3")|
|---|---|---|

<div id="process_sep"></div>

---


<div id="process"></div>

|<div id="box">4</div>|*音量* の値を変更することで、再生中の音量を変更することができます。|![3-6節 アドオンの使用 手順4](https://dl.dropboxusercontent.com/s/g6s72lth07fj96s/use_add-on_4.png "3-6節 アドオンの使用 手順4")|
|---|---|---|

<div id="process_sep"></div>

---

<div id="process"></div>

|<div id="box">5</div>|*停止* ボタンをクリックすることで、再生を停止することができます。|![3-6節 アドオンの使用 手順5](https://dl.dropboxusercontent.com/s/j0r4c5k2p75hkb2/use_add-on_5.png "3-6節 アドオンの使用 手順5")|
|---|---|---|


<div id="process_start_end"></div>

---


### アドオンを無効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考に有効化したアドオンを無効化すると、コンソールウィンドウに以下の文字列が出力されます。

```sh
サンプル3-6: アドオン「サンプル3-6」が無効化されました。
```

## ソースコードの解説


### audモジュールのインポート

BlenderのAPIを使ってオーディオファイルを再生するためには、audモジュールをインポートする必要があります。

[import:"import_aud", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)


### オーディオファイルの選択

再生するオーディオファイルを選ぶ処理は、```SelectAudioFile``` で行います。```SelectAudioFile``` は、[2-10節](../chapter_02/10_Control_Blender_UI_3.md) で説明したファイルブラウザを表示するための処理です。

ファイルブラウザの表示に関しては、[2-10節](../chapter_02/10_Control_Blender_UI_3.md) と1点だけ異なるところがあり、本節のサンプルではwavファイルとmp3のファイルしか表示しません。このように、特定のファイルのみを表示したい場合は ```filter_glob``` クラス変数を宣言します。```filter_glob``` は ```StringProperty``` クラスで定義し、```default``` に表示するファイルのリストを ```;``` （セミコロン）区切りで指定します。また、正規表現を使うこともできます。本節のサンプルでは全てのwavファイルとmp3ファイルを表示するため、```*.wav; *.mp3``` を指定しています。

[import:"filter_glob", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)


### オーディオファイルの再生

再生するオーディオファイルが決まった後は、オーディオファイルの再生の処理を実装します。オーディオファイルの再生処理は以下の処理に従って実装します。

1. サウンドデバイスを作成
2. サウンドファクトリを作成
3. サウンドハンドラを作成（オーディオファイルを再生）

ここでサウンドデバイスとサウンドファクトリ、サウンドハンドラという3つの用語が出てきましたので簡単に説明します。サウンドデバイスはOpenALやSDLなどのサウンドライブラリで扱うデバイスのことを指し、オーディオを出力するために必要なものです。サウンドファクトリは複数の音源をミックスしたり、ハイパスフィルター（HPF）やローパスフィルター（LPF）などのエフェクトをかけたりするためのオブジェクトです。サウンドを編集する時に使うことがあるかもしれませんが、Blenderはあくまで3DCGソフトなので本節のサンプルではこれらの機能を使っていません。サウンドハンドラは再生/停止/一時停止/再生再開といった再生制御や、ピッチやボリュームなどの再生時の振る舞いを変更するためのオブジェクトです。

ファイルブラウザでファイルを選択すると、```SelectAudioFile``` の ```execute()``` メソッドが実行され、オーディオファイルが再生されます。オーディオファイル再生の具体的なコードを見てみましょう。

[import:"select_audio_file_execute", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

サウンドデバイスとサウンドファクトリは、```aud.device()``` 関数および ```aud.Factory()``` 関数を実行することで作成することができます。```aud.device()``` 関数は引数が不要ですが、```aud.Factory()``` 関数は再生するオーディオファイルのパスを引数に指定する必要があります。サウンドデバイスは一度作成した後に再度作り直す必要はありませんが、サウンドファクトリは再生するオーディオファイルを変更する度に作成し直す必要があります。

その後、```aud.Factory()``` の戻り値である ```AudioDevice.factory``` を ```aud.device()``` の戻り値である ```AudioDevice.device``` の ```play()``` メソッドの引数に指定することで、サウンドハンドラが作成されてオーディオファイルが再生されます。作成されたサウンドハンドラは ```AudioDevice.handle``` に保存しました。

最後に、再生時の音量を設定するために ```AudioDevice.handle``` のメンバ変数である ```volume``` に *音量* プロパティで指定された値を代入しています。本節のサンプルでは、```AudioDevice.handle``` のメンバ変数として ```volume``` しか利用していませんが、他にも例えば次のようなメンバ変数が存在します。

|メンバ変数|意味|
|---|---|
|```volume```|音量（最大1、最小0）|
|```pitch```|ピッチ（最小0）|
|```loop_count```|ループ回数（ループ回数を指定、ループ回数が0なら1回限りの再生、負の値なら無限ループ再生）|
|```position```|再生位置（単位は秒）|
|```status```|再生状態|


### オーディオファイルの再生停止

*停止* ボタンが押された時は ```StopAudioFile``` クラスの ```execute()``` メソッドが呼び出され、オーディオファイルの再生を停止する処理が実行されます。

[import:"stop_audio_file", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

サウンドハンドラである ```AudioDevice.handle``` には再生状態を制御するために、次に示す関数が用意されています。

|関数|意味|
|---|---|
|```stop()```|オーディオファイルの再生停止|
|```pause()```|オーディオファイルの再生一時停止|
|```resume()```|オーディオファイルの再生再開|

本節のサンプルでは、オーディオファイルの再生を停止するために ```AudioDevice.handle.stop()``` 関数を利用しています。


### オーディオファイルの再生状態

本節のサンプルでは、オーディオファイルの再生状態に応じてUIを変更する処理がパネルクラス ```VIEW3D_PT_PlayAudioFileMenu``` の ```draw()``` メソッドに存在します。

[import:"check_play_status", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

オーディオファイルの再生状態は、```AudioDevice.handle.status``` の値を参照することによって判断することができます。```AudioDevice.handle.status``` に設定される値を以下に示します。

|値|意味|
|---|---|
|```True```|オーディオファイルを再生中、または再生一時停止中（```AudioDevice.handle.pause()``` が呼ばれた）|
|```False```|オーディオファイルを再生停止（```AudioDevice.handle.stop()``` が呼ばれた）、または最後まで再生完了|


### プロパティ変更の検知

本節のサンプルでは、*3Dビュー* エリアのツール・シェルフにある *オーディオ再生* パネルからユーザが音量を変更したこと検知し、即座にオーディオファイル再生へ反映しています。ここまで順を追って読み進めてきた方は、ふと疑問に思うかもしれません。[2-3節](../chapter_02/03_Use_Property_on_Tool_Shelf_1.md) で示したプロパティ値の設定直後に同じ処理を再実行するか、[3-4節](04_Use_API_for_OpenGL.md) で示したプロパティの値をユーザが設定した後に処理を行うかの2通りのパターンであったため、問題になることはありませんでした。しかし本節のサンプルでは、一度オーディオファイルを再生してしまうと再生処理がアドオンの処理とは非同期に行われてしまいます。つまり、プロパティの値を参照した後に処理を行うこれまでの方法ではうまくいかないのです。

本節のサンプルのようにプロパティの値が変わったことを検知して処理を行いたい場合は、プロパティクラスを作成する時に引数 ```set``` と ```get``` に、プロパティが変わった時に実行する関数を登録する必要があります。音量を変更するプロパティの定義の処理を見てみましょう。

[import:"prop_volume", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

引数 ```get``` に ```get_volume()``` 関数、引数 ```set``` に ```set_volume()``` 関数を指定しています。引数 ```set``` には、プロパティの値が変更された時に呼び出す関数を指定し、引数 ```get``` にはプロパティの値を参照する時に呼び出す関数を指定します。

最初に、```get_volume()``` 関数について説明します。

[import:"get_volume", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

```get_volume()``` 関数は第1引数に ```bpy.context.scene``` が代入された状態で呼び出されます。```init_props()``` 関数で ```bpy.context.scene``` にプロパティクラスを登録したことから、プロパティクラスを登録した変数へは ```bpy.context.scene['paf_volume']``` つまり ```self['paf_volume']``` としてアクセスすることができます。

```get_volume()``` 関数はプロパティを参照する時に呼び出されるため、予期しない時に呼び出される可能性があります。このため、呼び出されるタイミングによっては参照したい変数が存在しないかもしれません。そこで ```self.get()``` メソッドの第2引数にデフォルト値を指定することで、第1引数に指定したインスタンス変数が存在しない場合はデフォルト値を返すようにします。

一方で ```set_volume()``` 関数は、第1引数に ```bpy.context.scene```、第2引数にプロパティに設定された値が渡されて呼び出されます。

[import:"set_volume", unindent:"true"](../../sample_raw/src/chapter_03/sample_3-6.py)

```set_volume()``` 関数は、```self['paf_volume'] = value``` によりプロパティの値を更新した後、```AudioDevice.handle.volume``` に値を設定することで音量を変更しています。このような一連の処理を行うことで、ユーザからのプロパティ変更を検知し、オーディオファイルの再生音量を変更することができます。


## まとめ

Blenderのaudモジュールを使ってオーディオファイルを再生する方法を説明しました。筆者がaudモジュールの存在を初めて知った時、3DCGソフトであるBlenderにオーディオファイルを扱うAPIが存在しているのが疑問で、本書の話題として取り上げるかどうかを迷っていました。しかし、[4-1節](../chapter_04/01_Research_official_Blender_API_for_Add-on.md) で紹介する公式のAPIリファレンスのStandaloneモジュールに含まれることから、場違いであることを承知の上で話題として取り上げました。音を扱うという意味ではGame Engine Modulesに記載されるべきであるのに、あえてStandaloneモジュールに含めた理由はわかりませんが、動画作成時にオーディオファイルを再生することを考えてゲームエンジンだけに限定しなかったのかもしれません。

本節のサンプルではオーディオファイルの再生/停止の処理に加え、ユーザが変更した音量を検知する方法やファイルブラウザで表示するファイルをフィルタリングする方法を紹介しました。audモジュールはマイナーなモジュールのように見えて、ローパスフィルターやハイパスフィルター、ミックスなどサウンドプログラミングをする上で基本的な機能がAPIとして提供されています。扱いも非常に簡単なため、ぜひこの機会にBlenderでサウンドプログラミングに挑戦してみてはいかがでしょうか？


<div id="point"></div>

### ポイント

<div id="point_item"></div>

* オーディオファイルをアドオンで扱うためには、audモジュールをインポートする必要がある
* サウンドデバイスはサウンドを出力するために必要な、低レベルのサウンド再生デバイスである
* サウンドファクトリはオーディオファイルのデータにエフェクトをかけたりミックスしたりするために使うオブジェクトである
* サウンドハンドラはオーディオの再生制御を行うだけでなく、オーディオ再生の設定(音量やピッチなど)を参照/変更することができる
* プロパティクラスの値が参照された時に処理を実行したい場合は引数 ```get``` 、更新されたときに処理を実行したい場合は引数 ```set``` に処理を定義した関数を指定する
