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

[参考サイト](https://nextjs.org/learn/basics/assets-metadata-css/setup "")
[参考サイト](https://nextjs.org/learn/basics/assets-metadata-css/assets "")

Next.js では、publicディレクトリ内に画像などの静的アセットを入れることができる。

静的アセットは、アプリケーションのルートから指定する。

publicディレクトリには、画像ファイルのほか、robots.txt や Google のサイト所有権の為のファイルを入れます。

1. プロフィール用のjpg画像（400x400）をprofile.jpgという名前で用意する。
2. publicディレクトリ以下に、imagesディレクトリをつくる。
3. imagesディレクトリ内に、profile.jpgを入れる。
4. ページ生成用のJavascriptファイル内で、以下のように画像を呼び出す。

`
<img src="/images/profile.jpg" alt="Your Name" />
`

画像の表示に伴う以下のような処理は手動で行う必要がある。
（1）レスポンシブ用画像の生成
（2）サードパーティ製ツールやライブラリを使った画像の最適化
（3）ビューポートに入った時だけ画像を読み込む処理

next/image は、HTMLのimg要素の拡張機能です。

Next.js は、デフォルトで画像最適化機能をサポートしているので、WebPフォーマットでの画像リサイズ、最適化、配信を行うことができ、小さなデバイスに大きな画像を配信することを避けることができる。

Next.js は、将来的な画像フォーマットを自動で採用し、サポートしているブラウザに提供することもできる。

外部データソースによってホストされている画像に対しても、画像の最適化をかけることができる。

Next.js は、ビルド時に画像を最適化するのではなく、ユーザーからのリクエスト時にオンデマンドで画像を最適化するので、保持している画像量によってビルド時間が増えることはない。

画像は、ビューポートに入った時に読み込まれる（遅延ロード）ので、ビューポート外にある画像によって、ページ速度が遅くなることはない。

画像は、Core Web Vital の Cumulative Layout Shift を回避するようにレンダリングされる。

Component として画像を呼び出す時は、以下のように記述する。

`
import Image from 'next/image';

const YourComponent = () => (
  <Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
  />
);
`

width と height の Props は、ソース画像と同じアスペクト比のレンダリングサイズを指定する。

[参考サイト](https://nextjs.org/learn/basics/assets-metadata-css/metadata "")

pages/index.jsファイルを例にとると、 <Head>という React Component を使うと、<head>要素を変更することができる。

<Head> Component は、 next/head モジュールからインポートして使う。

`
import Head from 'next/head'
`

`
<Head>
  <title>First Post</title>
</Head>
`

[参考サイト](https://nextjs.org/learn/basics/assets-metadata-css/third-party-javascript "")

サードパーティ製スクリプトは、分析、広告などゼロから記述する必要のない新しい機能をサイトに導入するために使う。

できるだけ早くロードして実行する必要があるスクリプトは、<Head> Component 内に追加する。

<Head> Component 内にそのままスクリプトの読み込みを記述すると、他のJavascriptコードに対していつ読み込まれるか分からない上、スクリプトの読み込みに問題があった場合にページの読み込みに影響を与える恐れがある。

サードパーティ製スクリプトを読み込む場合、next/script モジュールをインポートしてから使う。

`
import Script from 'next/script';
`

next/script モジュールは、<script> 要素の拡張機能です。

<Script> Component は、<Head> Component の外に記述する。

`
<Script
  src="https://connect.facebook.net/en_US/sdk.js"
  strategy="lazyOnload"
  onLoad={() =>
    console.log(`script loaded correctly, window.FB has been populated`)
  }
/>
`

Strategyプロパティは、サードパーティ製スクリプトがどのタイミングでロードされるかを指定する。lazyOnload は、ブラウザのアイドル中にスクリプトを遅延ロードするように指定する。

onLoad は、サードパーティ製スクリプトが読み込まれた直後に実行するJavascriptコード。

※ sdk.js の読み込みは検証後に必ず削除する。

最初のNext.jsアプリを作成するセクション終了まで、あと30ページ程度。
検索エンジン最適化セクションは、29ページ。
TypeScriptセクションは、3ページ。


