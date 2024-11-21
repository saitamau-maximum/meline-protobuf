# Meline Protobuf

このリポジトリは Meline の API スキーマを管理するための protobuf ファイルを格納したリポジトリです。

このリポジトリの main ブランチに変更があると、自動的に GitHub Actions によって web / server にビルド要求が dispatch され、型更新PRが作成されることで、API スキーマの変更を自動的に反映し型安全な開発を実現します。

## 開発について

Node.js 環境が必要です。
また、protobuf-gen ライブラリとして [protoc-gen-openapiv2](https://github.com/googleapis/googleapis) を利用しているため、そのインストールが必要です。

Go環境がある場合はとても簡単です。

```bash
go install github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2@latest
```

### Pnpm のインストール

```bash
npm install -g pnpm
```

### 依存関係の更新

`google/api/annotations.proto`等を利用できるようにするためbuild前に依存関係の更新をしてください。

```bash
pnpm update:proto
```

### ビルド

```bash
pnpm build
```

これで proto フォルダに定義された protocol buffer の定義から、[protoc-gen-openapiv2](https://github.com/googleapis/googleapis) によってOpenAPI v2 の定義が生成ます。
さらにそれを[swagger-cli](https://github.com/APIDevTools/swagger-cli)によってバンドルし、`docs`フォルダに静的HTMLアセットとして出力します。

```bash
pnpm serve
```

することで、`http://localhost:3000`にビルドしたAPIスキーマのドキュメントが表示されます。

### Buf依存関係の更新

```bash
pnpm update:proto
```
