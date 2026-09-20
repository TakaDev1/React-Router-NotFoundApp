# React-Router-NotFoundApp

React Router の `*`（キャッチオールルート）を使用して、存在しない URL にアクセスしたときに 404 ページを表示する練習アプリ。

## 1. 学習内容

* `BrowserRouter`
* `Routes`
* `Route`
* `Link`
* `*` によるキャッチオールルート
* 404 Not Found ページ
* コンポーネントとページの分離

## 2. 使用技術

* React
* TypeScript
* React Router
* Tailwind CSS
* Vite

## 3. ディレクトリ構成

```text
React-Router-NotFoundApp/
├── src/
│   ├── components/
│   │   └── Navigation.tsx
│   ├── pages/
│   │   ├── Home.tsx
│   │   ├── About.tsx
│   │   └── NotFound.tsx
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css
├── public/
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

## 4. ルーティング

| URL      | 表示ページ    |
| -------- | -------- |
| `/`      | Home     |
| `/about` | About    |
| その他      | NotFound |

## 5. キャッチオールルート

存在しない URL を `*` で受け取る。

```tsx
<Route path="*" element={<NotFound />} />
```

例えば、

```text
/users
/test
/abc
/hello
```

など、定義されていない URL にアクセスすると `NotFound` が表示される。

## 6. Navigation

`Navigation.tsx` では `Link` を使用してページを移動する。

```tsx
import { Link } from "react-router";

const Navigation = () => {
  return (
    <nav className="flex gap-4 bg-gray-200 p-2">
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </nav>
  );
};

export default Navigation;
```

`Link` を使用することで、ブラウザを完全にリロードせずに React Router のルートを切り替えられる。

## 7. NotFound

```tsx
const NotFound = () => {
  return (
    <h1 className="mt-10 text-center text-3xl font-bold text-red-600">
      404 Not Found
    </h1>
  );
};

export default NotFound;
```

## 8. App.tsx

```tsx
import { BrowserRouter, Route, Routes } from "react-router";
import "./App.css";
import Navigation from "./components/Navigation";
import Home from "./pages/Home";
import About from "./pages/About";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <BrowserRouter>
      <Navigation />

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

## 9. 確認方法

開発サーバーを起動する。

```bash
npm run dev
```

以下をブラウザで確認する。

### Home

```text
/
```

→ `Home` が表示される。

### About

```text
/about
```

→ `About` が表示される。

### 存在しない URL

```text
/test
```

→ `404 Not Found` が表示される。

## 10. ポイント

### `*` はキャッチオール

```tsx
<Route path="*" element={<NotFound />} />
```

`*` は、他の定義されたルートにマッチしなかった URL を受け取る。

### Navigation は components

```text
components/
└── Navigation.tsx
```

`Navigation` は複数のページで共通して使用する UI コンポーネントなので、`components` に配置する。

### NotFound は pages

```text
pages/
└── NotFound.tsx
```

404 ページとして URL に応じて表示されるため、`pages` に配置する。

## 11. まとめ

このアプリでは、React Router の `*` を利用して存在しない URL を 404 ページにルーティングする方法を学習した。

```text
URL
 ↓
Routes
 ↓
┌─────────────────┐
│ /               │ → Home
│ /about          │ → About
│ その他          │ → NotFound
└─────────────────┘
```
