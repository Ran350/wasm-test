# Web Assembly 備忘録

## これはなに
Rust プログラムを Web Assembly 化して JavaScript から利用する備忘録．
- Rust プログラムは 
  - JS の alert() を呼び出して 
  - alert("Hello") を wasm 化する，だけ
- JS プログラムは
  -  Web ページで wasm を読み込み実行する

## 準備

- [Rust のインストール](https://www.rust-lang.org/ja/tools/install#:~:text=curl%20--proto%20%27%3Dhttps%27%20--tlsv1.2%20-sSf%20https%3A//sh.rustup.rs%20%7C%20sh)

- [wasm-pack のインストール](https://rustwasm.github.io/wasm-pack/installer/)
   - Rust プロジェクトを wasm に変換してくれるやつ

- [Node.js のインストール](https://nodejs.org/ja/) 

## clone して試してみる場合
```sh
git clone <this repo>
cd <this repo>

cd wasm
wasm-pack build

cd ../www
npm install
npm run start
```


## 一からプロジェクトを作成する手順
- フォルダを作成
   ```sh
   mkdir wasm-test
   cd $_
   ```

### Rust プロジェクトをつくる
- [cargo-generate](https://github.com/cargo-generate/cargo-generate) で Rust テンプレートプロジェクト作成
   ```sh
   cargo install cargo-generate
   cargo generate --git https://github.com/rustwasm/wasm-pack-template --name wasm
   cd wasm
   ```

- wasm ファイルを生成
   ```sh
   wasm-pack build
   ```
   pkg ディレクトリに wasm バイナリとそれを利用するためのjs, tsファイルが生成される

### Webページ用プロジェクトをつくる
- wasmを実行できるプロジェクトを生成する
   ```sh
   cd ../
   npm init wasm-app www
   npm install
   ```

- [`index.js`](./www/index.js)で，作成した wasm プロジェクトを読み込ませるよう書き換える
    ```js
    import * as wasm from "../wasm/pkg/wasm";
    ```

- 実行
    ```sh
    npm run start
    ```
    [localhost:8080](http://localhost:8080/) にアクセスしてアラートが表示されたら成功




## 参考
[RustでWebAssembly入門のためのまとめ │ Web備忘録](https://webbibouroku.com/Blog/Article/rust-wasm)