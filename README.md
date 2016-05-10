# tamant-hp
多摩ニュータウン学会HP関連

# サムネイルが崩れる
- http://clubringo.com/wp%E7%94%BB%E5%83%8F%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3-nextgen-gallery-%E3%82%B5%E3%83%A0%E3%83%8D%E3%82%A4%E3%83%AB%E3%81%8Cie%E3%81%A0%E3%81%A8%E3%80%81%E3%81%A1%E3%82%83%E3%82%93/

# 記事内のドメインの変更
以下を参考に、www3の切り替えを試して手順化し、最終的にwwwに書き換える
- http://fm575.net/?p=1480

## 手順メモ
- https://interconnectit.com/products/search-and-replace-for-wordpress-databases/ を開く
- 参考サイトでは、3.0.0beta だと文字化けするということで古いバージョンをダウンロードしていたが、3.1.0が出ていたのでそちらを試す
- サイト上部のDOWNLOADで Search-Replace-DB-master.zip をダウンロードして解凍
- フォルダ名を任意の予測が難しいものに変更する
- WordPressのインストールフォルダーにフォルダーをアップロードする。以下のような配置になる。間違えないこと！
  - /your-secret-search-replace-folder
  - /wp-admin
  - /wp-content
  - /wp-includes
 

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


