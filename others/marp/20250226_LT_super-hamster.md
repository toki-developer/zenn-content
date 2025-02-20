---
marp: true
# theme: gaia
theme: default
style: |
  @import url('styles/theme.css')
# header: "**React Native**"
footer: "by **＠toki_dev**"
paginate: true
---

# React Native がアツいと聞いて

## React Native に興味持ち始めた自分の学習ログ

氏名: 小池 瞬生 (ときお)
日付: 2025 年 2 月 26 日

---

# 自己紹介

- LINE ヤフー株式会社所属 (新卒 2 年目)
- ヤフーショッピングで web FE 開発
- 普段使ってる技術: React、Next.js
- 最近興味ある技術: React Native、Expo
- 好きなこと: キャンプ、ハンドボール、スノボ、サウナ、旅行...
- お金使わないこと: 服(GU)、髪(1000 円カット)

これからスーハムに関わっていきます m よろしくお願いします m

---

# 目次

- React Native の特徴
- 採用事例
- パフォーマンス
- Expo
- 将来性
- まとめ

---

<!--
header: "**React Native の特徴**"
-->

# React Native の特徴

- React のスキルを転用してアプリの開発ができる
- 「Learn once, write anywhere.」IOS, Android, Desktop, VR, web まで
- ネイティブコードになる
- React のバージョンアップに追従する形で進化

<!--

 -->

---

# React と React Native のコード

<div class="split-flex gap-20">
<div class="left-50per">

```typescript
const Componet = () => {
  const [state, setState] = useState();
  const handleHoge = () => {
    //...
  };

  return (
    <div>
      <p>テキスト</p>
      <button onClick={handleHoge}>ボタン</button>
    </div>
  );
};
```

</div>
<div class="right-50per">

```typescript
const Component = () => {
  const [state, setState] = useState();
  const handleHoge = () => {
    //...
  };

  return (
    <View>
      <Text>テキスト</Text>
      <TouchableOpacity onPress={handleHoge}>
        <Text>ボタン</Text>
      </TouchableOpacity>
    </View>
  );
};
```

</div>
</div>

---

```typescript
export const Component = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Hello React Native</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  title: {
    fontSize: 20,
  },
});
```

---

# コンポーネント対応表

| React Native   | iOS              | Android        | Web                   |
| -------------- | ---------------- | -------------- | --------------------- |
| `<View>`       | `<UIView>`       | `<ViewGroup>`  | `<div>`               |
| `<Text>`       | `<UITextView>`   | `<TextView>`   | `<p>`                 |
| `<Image>`      | `<UIImageView>`  | `<ImageView>`  | `<img>`               |
| `<ScrollView>` | `<UIScrollView>` | `<ScrollView>` | `<div>`               |
| `<TextInput>`  | `<UITextField>`  | `<EditText>`   | `<input type="text">` |

<!-- ネイティブコンポーネントに変換 -->

---

<!--
header: "**採用事例**"
-->

# 採用事例

<div class="split-flex">
<div class="left-40per">

Amazon, Microsoft, Discord など

海外では、
有名企業でも使われてる

<div class="mt-50"></div>

IOS, Android だけでなく
Desktop, Meta Quest(VR)でも

<div class="mt-50"></div>

[Showcase | React Native](https://reactnative.dev/showcase) 参考

</div>
<div class="right-60per">
  <img src="./20250226_LT_super-hamster/react-native-use-app.png">
</div>
</div>

---

<!--
header: "**パフォーマンス**"
-->

# パフォーマンス

React Native はパフォーマンスが悪いというイメージ

→ New Architecture や JavaScript エンジンの進化で大幅改善

---

# New Architecture

- React Native 0.76、Expo SDK52 からデフォルト
- 2018 年から開発に取り組まれていた
- React Native の基盤となる主要なシステムを完全に書き直し
- C++で書き直された

<!--
11月位 (10月後半と11月前半)
React Nativeの最新: 0.77
Expoの最新: 52.0.23

app.json "newArchEnabled": true,

基盤となる主要なシステム
→ コンポーネントのレンダリング方法、JavaScript 抽象化とネイティブ抽象化の通信方法、異なるスレッド間での作業のスケジュール方法

C++で書き直された

(Facebookとかでも既に動いている)
-->

---

<div class="split-flex">
<div class="left-50per">

# <u>Old Architecture</u>

<div>

- 非同期ブリッジで Native と通信
  → JSON データのシリアル化必要
- JavaScript エンジン
  → 主に JSC

</div>
</div>
<div class="split-50per">
<div>

# <u>New Architecture</u>

</div>
<div>

- JSI で同期的に Native と通信
  → JSON データを使わず直接通信
- ネイティブモジュール
  → TurboModules (改善版, JSI 利用)
- レンダリングシステム
  → Fabric Renderer (書き直し, JSI 利用)
- JavaScript エンジン
  → Hermes

</div>
</div>
</div>

<!--
old
ブリッジ時のシリアライズがボトルネック (頻繁な更新とか大きいオブジェクトの時に)
新しいReactの機能（Suspense や Concurrent Modeなどは対応できない

new
SuspenseやuseTransitionなども使える

JavaScriptInterface (JSI)

-->

---

### Bridge の除去

<div class="box-center">
<img width="800" src="./20250226_LT_super-hamster/0.76-bridge-diagram-a653d794d04871e5b7a026e35d8edf03.png">

[参考](https://reactnative.dev/blog/2024/10/23/the-new-architecture-is-here#removing-the-bridge)

</div>

---

### Old Architecture

<div class="box-center">
<img width="900" src="./20250226_LT_super-hamster/116824533-a8249500-ab82-11eb-9b9e-640047262351.png">

[参考](https://github.com/facebook/react-native/issues/31469)

</div>

---

### New Architecture

<div class="box-center">
<img width="900" src="./20250226_LT_super-hamster/0_ZyFDEuUAt2ZeeLlJ.webp">

[参考](https://medium.com/@anisurrahmanbup/react-native-new-architecture-in-depth-hermes-jsi-fabric-fabric-renderer-yoga-turbo-module-1284a192a82b#:~:text=%F0%9F%9A%A9%20Flow%20of%20New%20Architecture)

</div>

---

# JavaScript エンジン

<div><div class="mt-50">

| 時期   | エンジン       | 説明                             |
| ------ | -------------- | -------------------------------- |
| 昔     | JavaScriptCore | 実行時にバイトコードを生成・実行 |
| 今     | Hermes         | 事前にバイトコードを生成         |
| 開発中 | Static Hermes  | 事前にネイティブコードを生成     |

<!--

React Native v0.7からHermesがデフォルト (2022年の後半)
HermesはReactNative 用に最適化された JavaScript エンジン
事前にバイトコードにコンパイルすると
・アプリの起動時間が短縮される。
・実行時のリソース使用量が抑えられる。
・バイトコードのみを保持するため、メモリ効率が向上。

Static Hermesは、(実行時にHermesやその他の)JavaScriptエンジンが不要
TypeScriptみたいな型チェックのあるツールを使う時にのみ使える

実装も進み、Static Hermes 採用提案のための Issueとかも上がってる
 -->

---

### おまけ ( Static Hermes 採用提案のための Issue )

<div class="box-center mt-50">
<img width="800" src="./20250226_LT_super-hamster/static-hermes-benchmarks.png">

<div class="mt-50"></div>

参考: GitHub Issue: [Static Hermes for React Native #48531](https://github.com/facebook/react-native/pull/48531)

</div>

---

<!--
header: "**Expo**"
-->

# Expo とは

- Expo SDK は React Native フレームワーク
- コアに含まれないネイティブ API（カメラ, ビデオ, 通知など）を提供
- ファイルベースのルーティングを提供 (Expo Router)
- アプリ用の設定やネイティブコードなどを楽に管理 (Expo CNG)
- Expo Modules API を利用してネイティブコードも書ける (Swift や Kotlin)
- API Routes でエンドポイントも作れる
- Expo Application Services という有料サービスがある
  (EAS Build, EAS Update, EAS Hosting...)

<!--

React Nativeが結構ミニマムになっていて、足りない機能を補完したり、簡単に扱えるようにしている感

CNGはios や android といったディレクトリを作成せずにモバイルアプリの開発を進めるワークフロー
これなしで素のReactNativeだと、iosディレクトリやandroidディレクトリを作って、設定とかが必要になるみたいです。expoならapp.jsonやpackage.jsonの設定からそれらを自動生成

React NativeでもNative Moduleという仕組みでネイティブのコードを書けるようなのですが一部でObjective-Cが必要だったりするようで、Expo Modules APIだとそういうのも不要になる

昔はExpoを使ったら、ネイティブコードを含むライブラリとかは使えなくて、通常のReact Nativeプロジェクトにする必要があった。(expo ejectは今は非推奨)

expoが提供するExpo Application Service(EAS)という有料サービスもある。EASにデプロイとかもできるし、別のホスティングサービスとか使うこともできるみたい。

他には
開発環境のセットアップが楽にできたりもします。expo goというアプリをiPhoneにダウンロードして、expo startを実行すれば実機で動作確認ができる。

 -->

---

# 公式でもフレームワークの利用が推奨

> 新しいアプリを作成する場合、Expo などの React Native フレームワークを使用することが推奨されるようになりました。
> ...
> 現時点では、React Native に推奨される唯一のコミュニティ フレームワークは Expo です。Expo のスタッフは、React Native の初期の頃から React Native エコシステムに投資しており、現時点では、Expo が提供する開発者エクスペリエンスは最高クラスであると考えています。 (google 翻訳) [参考](https://reactnative.dev/blog/2024/06/25/use-a-framework-to-build-react-native-apps#:~:text=%E6%96%B0%E3%81%97%E3%81%84%E3%82%A2%E3%83%97%E3%83%AA%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B%E5%A0%B4%E5%90%88%E3%80%81Expo%20%E3%81%AA%E3%81%A9%E3%81%AE%20React%20Native%20%E3%83%95%E3%83%AC%E3%83%BC%E3%83%A0%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E6%8E%A8%E5%A5%A8%E3%81%95%E3%82%8C%E3%82%8B%E3%82%88%E3%81%86%E3%81%AB%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%97%E3%81%9F%E3%80%82)

---

# おまけ: Web まで Expo で作ってしまうパターンも

<div class="split-flex gap-20">
<div class="left-40per">
<img src="./20250226_LT_super-hamster/tweet-evan-bacon-expo-router.png">
</div>
<div class="right-40per">
<img src="./20250226_LT_super-hamster/tweet-meltohamy-to-expo-fromnext.js.png">
</div>
</div>

<div class="center">

[Tweet](https://x.com/m090009/status/1873731110892458129)

</div>

---

# Expo Router で画面遷移

テスト

---

<!--
header: "**その他、機能紹介とか**"
-->

# その他、機能紹介とか

---

# React Sercer Components

- Expo で開発者プレビューがリリースされた[参考](https://expo.dev/blog/universal-react-server-components-developer-preview)
- アプリサイズの削減
- 審査なしで更新できる
  - 今後、規制される可能性もある

<!--
将来的にはExpoでもReact Server Componentsが使えるようになりそう

サーバーから「`<Text>`を使います」みたいなデータが送信される

Next.jsとかはサーバーがデフォルト、Expoではクライアントがデフォルト
 -->

---

# DOM Components

- Web 用のコンポーネントを React Native で表示できる (内部的には WebView)
- 爆速でアプリ移行して、徐々に React Native に置き換えていけるのが推しポイント
- `use dom` ディレクティブで使える
- Web 用のコンポーネントに Native の関数を渡せる

<div class="split-flex gap-20">
<div class="left-50per">

```typescript
"use dom";

export default function MyComponent({
  hello,
}: {
  hello: (data: string) => Promise<void>;
}) {
  return <p onClick={() => hello("world")}>Click me</p>;
}
```

</div>
<div class="right-50per">

```typescript
import DomComponent from "./my-component";

export default function App() {
  return (
    <DomComponent
      hello={(data: string) => {
        console.log("Hello", data);
      }}
    />
  );
}
```

</div>
</div>

---

<!--
header: ""
-->

# まとめ

- 進化してる React Native がアツい！
- いろんな理由で将来性がある！
  (パフォーマンス,React ユーザー増加,RSC などの React 最新機能,VR など)
- 今年は React Native をがっつり学びます！ (一緒に学びましょ)
- いつかの Next.js の競合は Expo かも?

---

# おまけ:

- 最初に読むのに良さそうな記事 ( React から React Native に入門する記事 )
  - [From Web to Native with React | Expo Blog](https://expo.dev/blog/from-web-to-native-with-react)
- 深いところまで理解するのに良さそうな記事
  - [React-Native-Advanced-Guide](https://github.com/anisurrahman072/React-Native-Advanced-Guide)
- React Native のライブラリを探すツール
  - [React Native Directory](https://reactnative.directory/)
  - [Raycast の拡張もある](https://www.raycast.com/shubh_porwal/react-native-directory)
