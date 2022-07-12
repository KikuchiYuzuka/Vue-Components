# Vueで作成したコンポーネントをまとめ

## 各ファイル構成
・ 検索フォーム (views/SearchForm.vue) <br>
<br>
・ テーブルのソート機能 (views/Table.vue) <br>
→ ヘッダーを1回タップで昇順、2回タップで降順に切り替わる <br>
<br>
・ ページネーション (components/TablePagination.vue) <br>
→ ページネーション時にソートをしていた場合や検索条件があった場合も値を保持したままページネーションを行う <br>
<br>
・ 画像アップロード時のプレビュー機能 (views/PreviewPicture.vue) <br>
→ アップロードした画像をその場でプレビューする <br>
 <br>
・ 画像の複数選択機能 (views/SelectImages.vue) <br>
<br>
・ Ajax通信時のプログレスバー (views/ProgressBar.vue) <br>
→ 非同期通信時に通信状況をプログレスバーで表示する <br>
<br>
・ パスワード入力時の強弱表示機能 (views/CheckPassword.vue) <br>



