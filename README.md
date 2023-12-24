# MyElectronBoilerplate
2023.12.24
Qiitaの記事を参考に一から環境構築(Qiitaの記事に掲載されているコードは一部明らかな誤りがあるので、適宜修正)。レポジトリのソースは「環境構築手順」で作成したもの

# リンク
* [Electron + TypeScript + React + Webpackのプロジェクト作成から基本操作まで](https://qiita.com/uta-member/items/0590bb3832cac9fd41ec)


# 環境構築手順
node v20.2.0
npm 10.2.3
yarn 1.22.21

## setup
## react以外をインストール。
```
yarn create electron-app my-electron-boilerplate --template=webpack-typescript
```

## reactをインストール
```
yarn add react react-dom
yarn add --dev @types/react @types/react-dom
```


## templateソースを作成
### フォルダ作成
```
cd src
make renderer main
```
### ファイル移動
```
mv index.css renderer
mv index.html renderer
mv renderer.ts render
mv index.ts main
mv preload.ts main
```
### ファイル名変更
```
mv main/index.ts main/main.ts
mv renderer/renderer.ts renderer/index.tsx
```
### 設定ファイルの変更
forge.config.ts
* html → ./src/renderer/index.html
* js → ./src/renderer/index.tsx
* preload → ./src/main/preload.ts

webpack.mainconfig.ts
* entry → ./src/main/main.ts
* modules: ["./src", "./node_modules"],

webpack.renderer.config.ts
* modules: ["./src", "./node_modules"],

tsconfig.json
* baseUrl → ./src
* "strict": true, → 追加
* "jsx": "react-jsx" → 追加
* "types": ["node"] → 追加

### サンプルソースの作成
src/renderer/App.tsx
```
const App = () => {
  return <div>App</div>;
};

export default App;
```

src/renderer/index.tsx
```
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(
  document.getElementById("root") as HTMLElement
);

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

index.html
```
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Electron My App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```
