# Dockerfile
# ベースとなるイメージ（公式のnginx）
FROM nginx:1.25-alpine

# 自分の設定ファイルをコンテナ内にコピー
COPY conf.d/default.conf /etc/nginx/conf.d/default.conf

# 動作確認用のHTMLファイルを作成
RUN echo '<h1>nginx is working!</h1>' > /usr/share/nginx/html/index.html
