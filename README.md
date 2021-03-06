# 4d-utility-restore-object-with-font-number

v17コンポーネントです。

オブジェクト記法を使用しています。

ホストのオブジェクト記法は無効でも構いません。

実行すると，ホスト側の``Logs``フォルダーにログファイルが作成されます。

## 概要

フォームエディターのプロパティリストでオブジェクトのフォント名を設定した場合，保存されるのはフォント名ではなく，フォント番号です。たとえば，``ＭＳ　Ｐゴシック``に設定した場合，フォント番号``16384``が保存されます。

フォントを番号で管理する仕組みは，Mac OS/QuickDrawから引き継がれた古い仕様ですが，64ビット版の4DはMac/Windowsともにフォント番号を扱うことができないので，そのようなフォームを64ビット版の4Dで開くと，プロパティリストにフォント名が表示されないことがあります。




番号ではなく，名前でフォントを管理するためには，ツールボックスで作成したスタイルシートをフォームエディターのプロパティリストでオブジェクトに設定するか，``OBJECT SET FONT`` ``OBJECT SET STYLESHEET``等のコマンドで明示的にフォント名を設定する必要があります。

**注記**: スタイルシートが設定されていないオブエジェクトを``FORM Convert to JSON``でエクスポートした場合，``fontFamily``プロパティは省略されます。

## 使い方

1. コンポーネントをインストールします。

2. 32ビット版でデータベースを開きます。

問題のあるオブジェクトのプロパティ（例）

<img width="290" alt="スクリーンショット 2019-04-04 15 20 00" src="https://user-images.githubusercontent.com/1725068/55533702-233dc780-56ed-11e9-8301-f7787fdb8bad.png">

3. 共有メソッドの``restore_object_with_font_number``を実行します。

<img width="646" alt="スクリーンショット 2019-04-04 15 21 24" src="https://user-images.githubusercontent.com/1725068/55533768-52eccf80-56ed-11e9-8f47-b462ac4ea3cd.png">

下記のようなコードがフォームメソッドに追加されます。

```

If (Form event=On Load) | (Form event=On Header) | (Form event=On Printing Detail) | (Form event=On Printing Break) | (Form event=On Printing Footer)
	OBJECT SET FONT(*;"Variable";"MS PGothic")
	OBJECT SET FONT(*;"Button";"MS PGothic")
	OBJECT SET FONT(*;"Radio Button";"MS PGothic")
End if 
```

または

```
If (Form event=On Load) | (Form event=On Header) | (Form event=On Printing Detail) | (Form event=On Printing Break) | (Form event=On Printing Footer)
	OBJECT SET FONT(*;"obj1";"ＭＳ Ｐゴシック")
	OBJECT SET FONT(*;"obj2";"ＭＳ Ｐゴシック")
	OBJECT SET FONT(*;"obj3";"ＭＳ Ｐゴシック")
End if 
```

できれば，データベースを作成したのと同じプラットフォームで実行してください。

