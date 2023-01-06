# next-app-practice

[参考サイト](https://nextjs.org/learn/basics/create-nextjs-app/setup "")

Node.js バージョン 10.13以降がインストールされている必要がある。
Windows の場合、Git Bash を使うことが推奨される。WSLも使うことができる。

Next.jsアプリをインストールする。

`
mkdir workspace
cd workspace
npx create-next-app@latest nextjs-blog --use-npm --example "https://github.com/vercel/next-learn/tree/master/basics/learn-starter"
`

Next.jsアプリの開発サーバを起動する。
`
cd next-js-blog
npm run dev
`

---

[参考サイト](https://nextjs.org/learn/basics/create-nextjs-app/welcome-to-nextjs "")

上記作業を中断した際、作業を再開するときのコマンドは以下の通り。

`
cd workspace/nex-js-blog
npm run dev
`

上記コマンドを実行の上、ブラウザから [開発環境](http://localhost:3000 "") へアクセスすると、「Welcome to Next.js」のページが表示される。

上記ページは、Next.js のスターターテンプレートのページになっている。

[参考サイト](https://nextjs.org/learn/basics/create-nextjs-app/editing-the-page "")

テキストエディタで、 pages/index.js ファイルを開き、編集する。

`
<h1 className={styles.title}>
  Welcome to <a href="https://nextjs.org">Next.js!</a>
</h1>
`

上記の記述を下記の記述に変更してファイルを保存すると、ブラウザが自動的に更新されて変更をすぐさま確認することができる。

Next.jsの開発環境では、Fast Refreshの機能が有効になっているので、ファイルを変更するとNext.jsは自動的にほぼ瞬時にその変更をブラウザに反映することができ、すばやく開発サイクルを回すことができる。

`
<h1 className={styles.title}>
  Learn <a href="https://nextjs.org">Next.js!</a>
</h1>
`

Next.jsの開発環境を停めたい場合は、Ctrl + c で開発サーバを停めることができる。

[参考サイト](https://nextjs.org/learn/basics/navigate-between-pages "")
[参考サイト](https://nextjs.org/learn/basics/navigate-between-pages/setup "")
[参考サイト](https://nextjs.org/learn/basics/navigate-between-pages/pages-in-nextjs "")

Next.js におけるページとは、pages/ディレクトリにあるファイルからエクスポートされた React Component になっている。

pages/index.js ファイルは、`/` に関連付けられている。
pages/posts/first-post.js ファイルは、 `/posts/first-post` に関連付けられている。

試しに、pages/posts/first-post.js ファイルを用意して、ルーティングの挙動を確認する。

`
cd workspace/nex-js-blog/pages
mkdir posts
cd posts
touch first-post.js
`

first-post.js ファイルに以下を記述する。

`
export default function FirstPost() {
  return <h1>First Post</h1>;
}
`

Componentには任意の名前をつけることができるが、export default としてエクスポートする必要がある。

ブラウザから http://localhost:3000/posts/first-post へアクセスすると、「First Post」と書かれたh1要素が表示される。

上記のような手順で、Next.jsは様々なページを生成することができる。

1. pages/ディレクトリに任意のディレクトリやJavascriptファイルを生成する。
2. 生成したディレクトリとJavascriptファイル名がURLのパスになる。

HTMLを書く替わりにJSXにReact Component を書くようなイメージ。

[参考サイト](https://nextjs.org/learn/basics/navigate-between-pages/link-component "")

HTMLでは、aタグでページ間のリンクを行うが、Next.js では、next/link をインポートし、Link Component を使ってアプリケーション内のページ間のリンクを行う。

Link Component は、クライアント側のナビゲーションを実現し、ナビゲーション動作をより適切に制御できるPropsを受け入れる。

pages/index.js ファイルを開き、next/link をインポートする。

`
import Link from 'next/link';
`

aタグの記述をLink Component の記述に書き換える。

`
Learn <a href="https://nextjs.org">Next.js!</a>
`

上記の記述を、下記の記述に書き換える。

`
Learn <Link href="/posts/first-post">This page!</Link>
`

index.js ファイルと相互リンクできるように、/pages/posts/first-post.js ファイルの記述も置き換える。

`
return <h1>First Post</h1>;
`

`
import Link from 'next/link';

export default function FirstPost() {
  return (
  <>
    <h1>First Post</h1>
    <h2>
      <Link href="/">Back to home</Link>
    </h2>
  </>
  );
}
`

[参考サイト](https://nextjs.org/learn/basics/navigate-between-pages/client-side "")

Link Component は、アプリ内のページ遷移をクライアントサイドナビゲーションによって実現する。

クライアントサイドナビゲーションとは、Javascriptによるページ遷移。
クライアントサイドナビゲーションは、ブラウザが提供しているページ遷移よりも高速に行われる。
クライアントサイドナビゲーションでは、

クライアントサイドナビゲーションを確認する方法。
Next.jsアプリを起動し、ブラウザのDevツールで背景色を変更する。
背景色が変更された状態でページ遷移を行っても、ページ遷移によって背景色が切り替わることはない。

ページ遷移を <Link href=""> ではなく、<a href=""> で実装した場合、クライアントサイドナビゲーションは機能しない。

Next.js は自動的にページを分割し、各ページはそのページに必要なものだけを読み込む。これにより、トップページの読み込みが速くなる。
Next.js は自動的に該当ページに必要なものだけを読み込むため、あるページでエラーが発生しても他のページは稼働する。

Next.js の本番ビルドでは、ブラウザにLink Componentが表示されると、バックグラウンドで自動的にリンク先ページのコードをプリフェッチする。
Link Componentによってバックグラウンドでリンク先ページのコードがプリフェッチされることで、ページ遷移がほぼ瞬時に行われる。

Next.js は、（1）コード分割、（2）クライアントサイドナビゲーション、（3）プリフェッチ によって、アプリケーションを自動的に最適化し、最高のパフォーマンスを実現する。

[参考サイト](https://nextjs.org/learn/basics/assets-metadata-css "")

Next.js では、 CSSとSassがサポートされている。
Next.js では、画像や<head>内に記述されるページのメタデータも処理することができる。
