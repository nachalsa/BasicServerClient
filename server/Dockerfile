# 1. 베이스 이미지 선택
FROM python:3.12-slim

# 2. 'git' 설치 및 캐시 정리
RUN apt-get update && \
    apt-get install -y git --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 3. GitHub에서 소스 코드를 /code 디렉토리에 클론
# WORKDIR을 먼저 설정하지 않고 특정 디렉토리에 클론합니다.
RUN git clone https://github.com/nachalsa/BasicServerClient.git /code

# 4. 작업 디렉토리를 클론된 프로젝트의 'server' 폴더로 변경
# 이제부터 모든 명령어는 /code/server 디렉토리 안에서 실행됩니다.
WORKDIR /code/server

# 5. 가상 환경 생성 및 PATH 설정 (권장)
# 가상 환경은 현재 작업 디렉토리(/code/server) 내에 'venv'라는 이름으로 생성됩니다.
RUN python3 -m venv venv
ENV PATH="/code/server/venv/bin:$PATH"

# 6. 'server' 폴더 안에 있는 requirements.txt로 의존성 설치
RUN pip install --no-cache-dir -r requirements.txt

# 7. FastAPI 애플리케이션을 위한 포트 노출
EXPOSE 8000

# 8. 컨테이너 시작 시 'server' 폴더 안에 있는 main.py를 실행
# WORKDIR이 /code/server로 설정되어 있으므로, 경로는 자동으로 인식됩니다.
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
