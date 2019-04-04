# 4d-utility-restore-object-with-font-number

v17コンポーネントです。

オブジェクト記法を使用しています。

ホストのオブジェクト記法は無効でも構いません。

実行すると，ホスト側の``Logs``フォルダーにログファイルが作成されます。

## 概要

フォームエディターのプロパティリストでオブジェクトのフォント名を設定した場合，保存されるのはフォント名ではなく，フォント番号です。たとえば，``ＭＳ　Ｐゴシック``に設定した場合，フォント番号``16384``が保存されます。

フォントを番号で管理する仕組みは，Mac OS/QuickDrawから引き継がれた古い仕様ですが，64ビット版の4DはMac/Windowsともにフォント番号を扱うことができないので，そのようなフォームを64ビット版の4Dで開くと，プロパティリストにフォント名が表示されません。32ビット版であれば，フォント名が表示され，フォント番号も参照することができます。

番号ではなく，名前でフォントを管理するためには，ツールボックスで作成したスタイルシートをオブジェクトに設定する必要があります。
