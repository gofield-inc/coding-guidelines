# Gitのコミットメッセージのガイドライン

- [Gitのコミットメッセージのガイドライン](#gitのコミットメッセージのガイドライン)
  - [前提](#前提)
  - [コミットメッセージに書くこと・書かないこと](#コミットメッセージに書くこと書かないこと)
  - [コミットメッセージのフォーマット](#コミットメッセージのフォーマット)
    - [`<Prefix>` 何をしたのかを動詞で伝える](#prefix-何をしたのかを動詞で伝える)
    - [`<Subject>` 何をしたのかを文章で伝える](#subject-何をしたのかを文章で伝える)
    - [`<Description>` なぜそれをしたのかを文章で伝える](#description-なぜそれをしたのかを文章で伝える)
    - [補足情報を伝える（Github・Backlog）](#補足情報を伝えるgithubbacklog)
  - [参考記事](#参考記事)

## 前提
このガイドラインでは、いくつかの状況を前提としています。

- 1コミットに1つの対応とする
- クライアントは「[Fork](https://git-fork.com/)」（別のものでも問題ありませんが、UIの名称などForkに準じて記述しています）
- ベストよりもベター（誰でも簡単に導入できる）


## コミットメッセージに書くこと・書かないこと
コミットメッセージには「何を」「なぜ（※任意）」したのかを書きます。  
下記のように5W1Hに当てはめたときに、「いつ」「どこで」「誰が」「どうやって」はコミットメッセージ以外で分かるからです。

- いつ（When）：タイムスタンプ
- どこで（Where）：ファイル名・ディレクトリ名
- 誰が（Who）：author（作者）
- 何を（What）：コミットのタイトル（Subject）
- なぜ（Why）：コミットメッセージ（Body）
- どうやって（How）：コード・diff

コミットメッセージでは、「何をしたのか？」「なぜそれをしたのか？」を伝えることを主題とします。


## コミットメッセージのフォーマット
コミットメッセージは以下のフォーマットを使用します。

```
<Prefix>: <Subject>

<Description>
```

`<Subject>`はコミットのタイトル、`<Description>`はコミットの本文です。


### `<Prefix>` 何をしたのかを動詞で伝える
`<Prefix>`には、そのコミットで何をしたのかを英語の動詞で伝えます。  
なんらかの問題が起きたとき、ツリー上で過去のコミットを絞り込みやすくなります。

以下の動詞をベースにします。

| 動詞        | 説明                               |
|----------- |---------------------------------- |
| Add:       | （機能・ファイルなどを）追加             |
| Fix:       | （コードなどを）修正・改善する            |
| Update:    | （パッケージやドキュメントなどを）更新する   |
| Remove:    | （ファイル名やコードを）除去・削除する      |
| Rename:    | （ファイル名を）変更する                |
| Move:      | （AをBに）移動する                    |
| Change:    | （AをBに）変更する                    |

- `Fix`はバグの修正専用に使うこともありますが、ここではコードなどの修正をまとめて`Fix`としています。
- `Update`はコード自体の更新には使いません。パッケージ（ライブラリ）やドキュメントをアップデートしたときに使います。
- `Remove`（除去、一部を取り除く）と`Delete`（削除、完全に消す）は使い分けるほうが正確に伝えられますが、ここでは除去・削除含めて`Remove`としています。


### `<Subject>` 何をしたのかを文章で伝える
`<Subject>`には、そのコミットで何をしたのかを文章で伝えます。
以下の点に注意してください。

- 50文字未満（もしくは72文字未満）に収める
  - 長すぎると内容が把握しにくい
  - GitHubでは50文字を越えると警告、72を越えると省略されてしまう

```html
<!-- Good -->
Add: 画像追加
```


### `<Description>` なぜそれをしたのかを文章で伝える
`<Description>`は任意ですが、何らかのバグ修正の際は必ず記述するようにします。

`<Description>`には、なぜ追加や修正、削除が必要だったのかを文章で伝えます。
リスト表示（`-`か`*`で始める）や改行・空行を入れて読みやすくしてください。


### 補足情報を伝える（Github・Backlog）
GitHubにもBacklogにもイシュー番号（課題キー）をコミットメッセージに載せると、イシュー（課題）ページにコミット情報を登録することができます。
また、キーワードを含めると、状態も変更することができます。

- GitHub： `Closes #123`や`Closes: #123`のようにコミットに含めると、コミット後にイシューもクローズする（[Closing issues using keywords - User Documentation](https://help.github.com/articles/closing-issues-using-keywords/)）
- Backlog： `#fix`を含めると「処理済み」になり、`#close`を含めると「完了」に状態を更新する（[コミットログでの課題の操作 - Backlog（バックログ）](https://backlog.com/ja/help/usersguide/git/userguide1400/)）


## 参考記事
- [コミットメッセージの書き方 – risacan – Medium](https://medium.com/@risacan/%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88%E3%83%A1%E3%83%83%E3%82%BB%E3%83%BC%E3%82%B8%E3%81%AE%E6%9B%B8%E3%81%8D%E6%96%B9-64aeadd92057)
- [[転載] gitにおけるコミットログ/メッセージ例文集100](https://gist.github.com/mono0926/e6ffd032c384ee4c1cef5a2aa4f778d7)
- [Gitのコミットメッセージの書き方 | POSTD](https://postd.cc/how-to-write-a-git-commit-message/)
- [GitHubで使われている実用英語コメント集 - Qiita](https://qiita.com/shikichee/items/a5f922a3ef3aa58a1839)
- [ネイティブと働いて分かった英語コミットメッセージの頻出動詞10つ - Qiita](https://qiita.com/gogotanaka/items/b65e1b081fa976e5d754)
