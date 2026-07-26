# 1단계: MkDocs 정적 파일 빌드
FROM python:3.11-slim AS builder

WORKDIR /app

# 필요 라이브러리 설치 (Material 테마 사용 시)
RUN pip install --no-cache-dir mkdocs mkdocs-material

COPY . .

# docs를 HTML 정적 파일로 빌드 (out/site 폴더에 생성됨)
RUN mkdocs build --site-dir site

# 2단계: Nginx를 통한 경량 배포 환경 구성
FROM nginx:alpine

# 빌드된 정적 웹 파일을 Nginx 기본 HTML 경로로 복사
COPY --from=builder /app/site /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]