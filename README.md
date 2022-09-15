## 初期設定

1. headタグ内でheader-lib.cssを読み込む
2. </body>タグの直前でheader-lib.jsを読み込む
3. header-lib.jsより前でheaderOptionsを定義

```
//サンプル
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
                // {
                //     name: 'Google',
                //     link: 'https://google.com',
                //     isAnother: true,
                // },
            ],
            active: {
                // humberger: true, // ハンバーガーメニュー 表示設定
                // menuStyle: 'vertical', /// メニューのスタイル
                logo: 'https://jp.vuejs.org/images/logo.svg', // ロゴのURL 無ければエレメント自体非表示
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
4. マウントする要素を指定
```html
<div id="header-lib"></div>
```

## オプション

- menu(Object): 個別のメニュー設定
    - name(String): メニューの表示名
    - class(String): メニューのclass属性
    - link(String): メニューのhref属性
    - isAnother(Boolean): 別タブ表示
- active(Object):
    - humberger(Boolean): ハンバーガーメニュー
    - menuStyle(String): メニューの並び（デフォルトで横、現在verticalのみ指定可）
    - logo(string): ロゴのリンク
    - verticalLine(Boolean): メニュー間の区切り線
    - menuHover(Boolean): ホバーエフェクト
- mq(Array): メディアクエリ
    - max(Number): 画面幅が指定値以下の時
    - min(Number): 画面幅が指定値以上の時
    - (Object): 設定値の時、activeと入れ替わる
        - activeと同様

## その他
- グローバルナビのカレント表示は、bodyタグのclass属性と個別メニュー設定のclassが同じ場合時、表示される
- オプション外のスタイル変更は、header-lib.cssの読み込み箇所より下の位置で独自にスタイルを指定する
