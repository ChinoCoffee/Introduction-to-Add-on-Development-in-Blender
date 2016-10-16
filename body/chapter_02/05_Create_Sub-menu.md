<div id="sect_title_img_2_5"></div>

<div id="sect_title_text"></div>

# サブメニューを作成する

<div id="preface"></div>

###### これまで紹介したアドオンでは1階層分のメニューを追加するだけでしたが、サブメニュー（マウスオーバーすると展開されるメニュー）を作成して2階層以上のメニューを作ることもできます。例えば、 3Dビューエリアの追加 > メッシュは、追加の親メニューの下にメッシュという子メニューがある2階層のメニューとなっています。本節では [2-4節](04_Use_Property_on_Tool_Shelf_2.md) のサンプルを改良し、複製するオブジェクトをメニューから選択できるようなメニューを構築することで、多階層のメニューを作成する方法を紹介します。

## 作成するアドオンの仕様

* [2-4節](04_Use_Property_on_Tool_Shelf_2.md) で作成したサンプルを改良し、複製するオブジェクトをメニューから選択できるようにする

## アドオンを作成する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考にして以下のソースコードをテキスト・エディタに入力し、ファイル名を ```sample_2-5.py``` として保存してください。

[import](../../sample/src/chapter_02/sample_2-5.py)

## アドオンを使用する

### アドオンを有効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md) を参考に、作成したアドオンを有効化するとコンソールに以下の文字列が出力されます。

```sh
サンプル2-5: アドオン「サンプル2-5」が有効化されました。
```

<div id="sidebyside"></div>

|アドオンを有効化後、3Dビューエリアのメニューであるオブジェクト > オブジェクトの複製にサブメニューが追加されていることを確認します。<br>サブメニューには、3Dビューエリアに存在するオブジェクト名が追加されています。|![オブジェクトの複複1](https://dl.dropboxusercontent.com/s/suhwkprgpkrrwqh/use_add-on_1.png "オブジェクトの複製1")|
|---|---|


### アドオンの機能を使用する

<div id="process_title"></div>

##### Work

<div id="process_noimg"></div>

|<div id="box">1</div>|3Dビューエリアのメニューであるオブジェクト > オブジェクトの複製から複製するオブジェクト名を選んで実行すると、選択したオブジェクトが複製されます。|
|---|---|

<div id="process_sep"></div>

---

<div id="process"></div>

|<div id="box">2</div>|[2-4節](04_Use_Property_on_Tool_Shelf_2.md) と同様、複製されたオブジェクトの拡大率・回転角度・配置先を *ツール・シェルフ* の *オプション* から変更することができます。|![オブジェクトの複複2](https://dl.dropboxusercontent.com/s/o0ten4sgfm8jter/use_add-on_2.png "オブジェクトの複製2")|
|---|---|---|

<div id="process_start_end"></div>

---


### アドオンを無効化する

[1-5節](../chapter_01/05_Install_own_Add-on.md)を参考に、有効化したアドオンを無効化するとコンソールに以下の文字列が出力されます。

```sh
サンプル2-5: アドオン「サンプル2-5」が無効化されました。
```


## ソースコードの解説

サブメニューを作成するコードを除き、ソースコードの大部分は [2-4節](04_Use_Property_on_Tool_Shelf_2.md) からの流用です。
ここでは、新規で追加した部分についてのみ解説します。

### サブメニューの追加

サブメニューを追加するためには、 ```bpy.types.Menu``` クラスを継承したメニュークラスを作成する必要があります。

```python
# メインメニュー
class ReplicateObjectMenu(bpy.types.Menu):
    bl_idname = "uv.replicate_object_menu"
    bl_label = "オブジェクトの複製"
    bl_description = "オブジェクトを複製します"

    def draw(self, context):
        layout = self.layout
        # サブメニューの登録＋出力文字列の登録
        # bpy.data.objects：オブジェクト一覧
        for o in bpy.data.objects:
            layout.operator(ReplicateObject.bl_idname, text=o.name).src_obj_name = o.name
```

オペレータクラスと同様、メニュークラスにはメンバ変数 ```bl_idname``` 、 ```bl_label``` 、 ```bl_description``` を指定する必要がありますが、 ```bl_options``` を指定する必要はありません。

メニュークラスでは、メニューの描画に必要な ```draw()``` メソッドを実装する必要があります。メニューが表示される度に ```draw()``` メソッドが呼ばれ、以下の引数が渡されてきます。

|引数|型|値の説明|
|---|---|---|
|```self```|呼ばれた ```draw()``` メソッドが定義されているメニュークラス|メニュークラスのインスタンス|
|```context```|```bpy.types.Context```|```draw()``` メソッドが呼ばれた時のコンテキスト|

オペレータクラスをメニューに登録した時と同様、サブメニューへの項目追加は ```self.layout.operator()``` 関数で行うことができます。本節のサンプルでは3Dビューエリア上の全てのオブジェクト名をメニュー項目に追加するため、 ```layout.operator()``` 関数の第1引数にオペレータクラスの ```bl_idname``` を指定し、 引数 ```text``` にオブジェクト名を指定しています。

オペレータクラスは、複製するオブジェクトをオブジェクト名で判定するため、オペレータクラスのメンバ変数 ```src_obj_name``` にオブジェクト名を代入します。```src_obj_name``` は ```StringProperty``` クラスとして用意します。

```python
src_obj_name = bpy.props.StringProperty()
```

オペレータクラスの ```execute()``` メソッドでは、メンバ変数 ```src_obj_name``` に代入されたオブジェクト名を用いてオブジェクトを複製するように処理を変更しています。ソースコードのコメントを参考に確認してください。

最後に、 3Dビューエリアのメニューであるオブジェクトへ項目を追加します。

```python
def menu_fn(self, context):
    self.layout.separator()
    self.layout.menu(ReplicateObjectMenu.bl_idname)
```

これまでオペレータクラスをメニューに追加する時は ```self.layout.operator()``` 関数を利用していましたが、メニュークラスをメニューに追加する場合は ```self.layout.menu()``` 関数を利用します。```self.layout.menu()``` 関数にメニュークラスのメンバ変数 ```bl_idname``` を引数として渡すことで、メニューをメニュー項目に追加することができます。

### 3階層以上のメニュー

サブメニューにさらにサブメニュー（サブサブメニュー）を追加するなど、3階層以上のメニューを作成することもできます。

以下のサンプルでは、先ほど作成したサンプルのメニューとサブメニューの間にオブジェクトの複製（サブメニュー）を追加しています。

[import](../../sample/src/chapter_02/sample_2-5_alt.py)

<div id="sidebyside"></div>

| アドオンを作成し有効化すると、右図のように以下のように3階層のメニューが作成されていることが確認できます。|![多階層メニュー](https://dl.dropboxusercontent.com/s/rrpepaa9eygx9qt/multilevel_menu.png "多階層メニュー")|
|---|---|


サンプルを見てもらえばわかると思いますが、3階層のメニューは2階層のメニューを作成した時の応用であることがわかります。

```python
# サブメニュー
class ReplicateObjectSubMenu(bpy.types.Menu):
    bl_idname = "uv.replicate_object_sub_menu"
    bl_label = "オブジェクトの複製（サブメニュー）"
    bl_description = "オブジェクトを複製します（サブメニュー）"

    def draw(self, context):
        layout = self.layout
        # サブサブメニューの登録
        for o in bpy.data.objects:
            layout.operator(ReplicateObject.bl_idname, text=o.name).src_obj_name = o.name


# メインメニュー
class ReplicateObjectMenu(bpy.types.Menu):
    bl_idname = "uv.replicate_object_menu"
    bl_label = "オブジェクトの複製"
    bl_description = "オブジェクトを複製します"

    def draw(self, context):
        layout = self.layout
        # サブメニューの登録
        layout.menu(ReplicateObjectSubMenu.bl_idname)
```

サブメニュー登録時に ```self.layout.operator()``` 関数の代わりに ```self.layout.menu()``` 関数を用い、サブメニュー用に作成したメニュークラスのメンバ変数 ```bl_idname``` を指定します。そしてサブメニュー用に作成したクラスの中で、オペレータクラスを登録することで、3階層のメニューを作成することができます。

このような手順を踏むことで、4階層、5階層、・・・とメニューの階層を増やすことができます。

## まとめ

[2-4節](04_Use_Property_on_Tool_Shelf_2.md) を改造し、複製するオブジェクトをメニューから選択できるようにしました。また、サブメニューから複製するオブジェクトを選べるようにしました。

サブメニューを用いることで、本節のサンプルのように処理対象を選択できるようにしたり、メニュー項目を機能ごとに整理することができるようになります。ぜひここでサブメニューの作り方を習得し、わかりやすいUI作りに活かしましょう。

<div id="space_xxs"></div>


<div id="point"></div>

### ポイント

<div id="point_item"></div>

* メニュークラスは、 ```bpy.types.Menu``` クラスを継承して作成する
* メニュークラスの ```draw()``` メソッド内で、 オペレータクラスのメンバ変数 ```bl_idname ``` を ```self.layout.operation()``` 関数の引数に指定し、メニュークラスのメンバ変数 ```bl_idname``` を引数にして ```self.layout.menu()``` 関数 を呼び出すことで、サブメニューを作成できる
* メニュークラスの ```draw()``` メソッド内でサブメニュー用に作成したクラスのメンバ変数 ```bl_idname``` を ```self.layout.menu()``` 関数の引数に指定することで、3階層以上のメニューを作成することができる
