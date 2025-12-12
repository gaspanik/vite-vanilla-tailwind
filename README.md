# Vite + Vanilla + Tailwind CSS v4

ViteとTailwind CSS v4を使用したシンプルなVanilla JavaScriptプロジェクトのテンプレートです。

## 🚀 特徴

- ⚡️ [Vite](https://vitejs.dev/) - 高速な開発サーバーとビルドツール
- 🎨 [Tailwind CSS v4](https://tailwindcss.com/) - ユーティリティファーストのCSSフレームワーク
- 📦 [Lucide Icons](https://lucide.dev/) - 美しいオープンソースアイコンライブラリ
- 🔧 Vanilla JavaScript - フレームワークなしのシンプルなセットアップ
- 📄 複数HTMLページ対応 - プロジェクトルートの全HTMLファイルを自動ビルド

## 📋 必要要件

- Node.js 18.x 以上
- pnpm (推奨)

## 🛠️ セットアップ

### 依存関係のインストール

```bash
pnpm install
```

## 🏃 実行方法

### 開発サーバーの起動

```bash
pnpm dev
```

ブラウザで [http://localhost:5173](http://localhost:5173) を開きます。

### 本番用ビルド

```bash
pnpm build
```

ビルド結果は `dist` ディレクトリに出力されます。

### ビルドのプレビュー

```bash
pnpm preview
```

## 📁 プロジェクト構成

```
vite-vanilla-tailwind/
├── index.html         # トップページ
├── about.html         # Aboutページ
├── public/            # 静的ファイル
├── src/
│   ├── main.js        # エントリーポイント
│   └── style.css      # Tailwind CSSのインポート
├── vite.config.js     # Vite設定（マルチページビルド対応）
├── package.json       # 依存関係とスクリプト
└── README.md          # このファイル
```

## 📄 マルチページビルド

このプロジェクトは複数のHTMLページを自動的にビルドするよう設定されています。

### HTMLページの追加方法

プロジェクトのルートディレクトリに新しいHTMLファイルを追加するだけで、自動的にビルド対象に含まれます：

```
vite-vanilla-tailwind/
├── index.html
├── about.html
├── contact.html
└── ...
```

ビルド結果:
```
dist/
├── index.html
├── about.html
└── contact.html
```

### 仕組み

`vite.config.js`で[glob](https://www.npmjs.com/package/glob)を使用して、プロジェクトルート直下の全ての`*.html`ファイルを検出し、Viteのマルチページビルドに登録しています。

```javascript
const files = glob.sync('*.html')
const input = Object.fromEntries(
  files.map((file) => [
    path.basename(file, '.html'),
    path.resolve(__dirname, file),
  ]),
)
```

開発時は通常通り各HTMLファイルに直接アクセスできます：
- `http://localhost:5173/` - index.html
- `http://localhost:5173/about.html` - about.html

## 🎨 Tailwind CSS v4 の使い方

このプロジェクトではTailwind CSS v4を使用しています。v4では`@tailwindcss/vite`プラグインを使用するため、従来の`postcss.config.js`や`tailwind.config.js`は不要です。

### 設定ファイル

- **vite.config.js** - Tailwind Viteプラグインを設定
- **src/style.css** - `@import "tailwindcss";`でTailwindをインポート

### HTMLでの使用例

```html
<div class="flex items-center gap-2">
  <h1 class="font-medium text-gray-900 text-2xl">Hello Tailwind!</h1>
  <p class="text-gray-600">ユーティリティクラスを使って簡単にスタイリング</p>
</div>
```

## 🎭 Lucide Icons の使い方

[Lucide](https://lucide.dev/)は、美しくカスタマイズ可能なオープンソースのアイコンライブラリです。このプロジェクトでは軽量な実装が可能です。

### 基本的な使い方

#### 1. JavaScriptでアイコンをインポート

使用したいアイコンを`src/main.js`でインポートして初期化します：

```javascript
import { createIcons, IceCreamCone, Heart, Star } from 'lucide'

// 使用するアイコンだけをインポート（バンドルサイズを最小化）
createIcons({ 
  icons: { 
    IceCreamCone,
    Heart,
    Star
  } 
})
```

#### 2. HTMLで`data-lucide`属性を使用

HTMLで`data-lucide`属性を持つ要素を配置します：

```html
<i data-lucide="ice-cream-cone"></i>
<i data-lucide="heart"></i>
<i data-lucide="star"></i>
```

アイコン名はキャメルケースをケバブケースに変換します：
- `IceCreamCone` → `ice-cream-cone`
- `Heart` → `heart`
- `ArrowRight` → `arrow-right`

### アイコンのカスタマイズ

Tailwindのクラスでサイズや色を調整できます：

```html
<div class="flex items-center gap-2">
  <i data-lucide="heart" class="text-red-500 w-6 h-6"></i>
  <i data-lucide="star" class="text-yellow-400 w-8 h-8"></i>
</div>
```

### 利用可能なアイコン

[Lucide公式サイト](https://lucide.dev/icons/)で1,500以上のアイコンを検索できます。使用したいアイコンを見つけたら：

1. アイコン名をパスカルケースで`main.js`にインポート
2. HTMLでケバブケースの名前を`data-lucide`属性に指定

## 📦 使用技術

- [Vite 7.x](https://vitejs.dev/)
- [Tailwind CSS 4.x](https://tailwindcss.com/)
- [Lucide Icons](https://lucide.dev/)

## 📝 ライセンス

MIT
