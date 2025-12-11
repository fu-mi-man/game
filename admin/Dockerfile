# admin/Dockerfile
# マルチステージビルド（開発環境と本番環境を分離）

# ========================================
# Stage 1: 開発環境
# ========================================
FROM node:20-bookworm-slim AS development

# pnpm をグローバルインストール
RUN npm install -g pnpm

# 作業ディレクトリ
WORKDIR /app

# package.json と pnpm-lock.yaml だけ先にコピー（キャッシュ効率化）
# COPY package.json pnpm-lock.yaml ./

# 依存関係インストール（初回はスキップ、後でマウント先で実行）
# RUN pnpm install

# 開発サーバーのポート（Viteのデフォルト）
EXPOSE 5173

# 開発サーバー起動コマンド
CMD ["pnpm", "dev", "--host", "0.0.0.0"]

# ========================================
# Stage 2: ビルド環境
# ========================================
# FROM node:20-bookworm-slim AS builder
#
# RUN npm install -g pnpm
#
# WORKDIR /app
#
# # package.json をコピー
# COPY package.json pnpm-lock.yaml ./
#
# # 依存関係インストール
# RUN pnpm install --frozen-lockfile
#
# # ソースコードをコピー
# COPY . .
#
# # 本番用ビルド
# RUN pnpm build
#
# # ========================================
# # Stage 3: 本番環境（nginx で静的ファイル配信）
# # ========================================
# FROM nginx:1.25-alpine AS production
#
# # ビルド成果物をコピー
# COPY --from=builder /app/dist /usr/share/nginx/html
#
# # nginx 設定（必要なら追加）
# # COPY nginx.conf /etc/nginx/conf.d/default.conf
#
# EXPOSE 80
#
# CMD ["nginx", "-g", "daemon off;"]
