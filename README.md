## 初期設定

1. headタグ内でheader-lib.cssを読み込む
2. </body>タグの直前でheader-lib.jsを読み込む
3. header-lib.jsより前でheaderOptionsを定義

```
const headerOptions = {
      menus: [ // メニューの設定
                {
                    name: 'TOP',
                    class: 'index',
                    link: '#',
                },
                {
                    name: 'お知らせ',
                    class: 'news',
                    link: '#',
                },
                {
                    name: 'サービス',
                    class: 'service',
                    link: '#',
                },
                {
                    name: '会社概要',
                    class: 'company',
                    link: '#',
                },
                {
                    name: 'お問い合わせ',
                    class: 'contact',
                    link: '#',
                },
            ],
            active: {
                // humberger: true, // ハンバーガーメニュー 表示設定
                // menuStyle: 'vertical', /// メニューのスタイル
                logo: '/img/logo.82b9c7a5.png', // ロゴのURL 無ければエレメント自体非表示
                // verticalLine: true, // メニュー間の縦線 縦のときは無し
                menuHover: true, // ホバーエフェクト
            },
            mq:[
                'max', 767,
                // 'min', 767,
                {
                    humberger: true, // ハンバーガーメニュー 表示設定
                    menuStyle: 'vertical',/// メニューのスタイル
                },
            ],
    }

```

## オプション

- menu(Object): 個別のメニュー設定
    - name(String): メニューの表示名
    - class(String): メニューのclass属性
    - link(String): メニューのhref属性
    - isAnothe(Boolean): 別タブ表示（Boolean）
- active(Object):
    - humberger(Boolean): ハンバーガーメニュー
    - menuStyle(String): メニューの並び（デフォルトで横、現在verticalのみ指定可）
    - logo(string): ロゴのリンク
    - verticalline(Boolean): メニュー間の区切り線
    - menuHover(Boolean): ホバーエフェクト
- mq(Array): メディアクエリ
    - max(Number): 画面幅が指定値以下の時
    - min(Number): 画面幅が指定値以上の時
    - (Object): 設定値の時、activeと入れ替わる
        - activeと同様
