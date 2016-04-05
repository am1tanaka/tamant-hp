# tamant-hp
多摩ニュータウン学会HP関連

# WordPress変更メモ
## 2016/4/5
### スラッグの日本語禁止設定
スラッグを未設定のまま記事を書くと、スラッグにタイトルがそのまま使われてしまい、エラーが表示される。そこで、以下のサイトを参考にして、タイトルが日本語だった場合は自動的に半角英数からなるスラッグを設定するようにした。
- 参考URL: http://www.warna.info/archives/2317/
- WordPressの管理画面にログイン
- 外観>テーマの編集を選択
- functions.phpを選択
- 最後に以下のコードを追加
```
/*-------------------------------------------*/
/*	Auto Post Slug(http://www.warna.info/archives/2317/)
/*-------------------------------------------*/
function auto_post_slug( $slug, $post_ID, $post_status, $post_type ) {
    if ( preg_match( '/(%[0-9a-f]{2})+/', $slug ) ) {
        $slug = utf8_uri_encode( $post_type ) . '-' . $post_ID;
    }
    return $slug;
}
add_filter( 'wp_unique_post_slug', 'auto_post_slug', 10, 4  );
```

### ptをページタイトルに設定
幾つかのページには、ページトップへのページ内リンクがあったので、自動的にタイトルにptのidを設定して、リンクが機能するようにした。
- WordPressの管理画面にログイン
- 外観>テーマの編集を選択
- single.phpを選択
- ページタイトルの箇所を以下のように修正
```
<h1 class="entryPostTitle entry-title" id="pt"><?php the_title(); ?><?php edit_post_link(__('Edit', 'biz-vektor'), ' <span class="edit-link edit-item">[ ', ' ]' ); ?></h1>
```


# サンプル
- [トップページ](http://am1tanaka.github.io/tamant-hp/top/index-utf8.html)
- [詳細ページ](http://am1tanaka.github.io/tamant-hp/contents/index-utf8.html)
- [活動報告ページ](http://am1tanaka.github.io/tamant-hp/activities/index-utf8.html)


