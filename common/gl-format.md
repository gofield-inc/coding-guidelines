# フォーマット
- 文字コードはUTF-8（BOM無し）。
- 改行コードはLF（本番環境でシェアの高い Linux の改行コードに合わせる）。
- インデントは半角スペース2つ。
- 案件ガイドラインや使用フレームワークによりタブを使用する場合、タブによるインデントとスペースによるインデントが混在しないないようにする。

上記のフォーマット設定をVScodeに反映する場合、`setting.json`に以下を貼り付けます。

command + shift + p  
「Preferences: Open Settings(JSON)」

```
{
  "files.encoding": "utf8",
  "files.eol": "\n",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
}
```
※`{}`は初期値で入力されていると思われるので、中身を貼付