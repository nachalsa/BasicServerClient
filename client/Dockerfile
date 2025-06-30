# 1. 베이스 이미지 선택 (동일)
FROM python:3.12-slim

# 2. 'git' 설치 및 캐시 정리 (동일)
RUN apt-get update && \
    apt-get install -y git --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 3. GitHub에서 소스 코드를 /code 디렉토리에 클론 (동일)
RUN git clone https://github.com/nachalsa/BasicServerClient.git /code

# 4. 작업 디렉토리를 클론된 프로젝트의 'client' 폴더로 변경
# (가장 중요한 변경점)
WORKDIR /code/client

# 5. 가상 환경 생성 및 PATH 설정 (경로만 변경)
RUN python3 -m venv venv
ENV PATH="/code/client/venv/bin:$PATH"

# 6. 'client' 폴더 안에 있는 requirements.txt로 의존성 설치
RUN pip install --no-cache-dir -r requirements.txt

# 7. 컨테이너 시작 시 'client' 폴더 안에 있는 run_client.py를 실행
# (두 번째 중요한 변경점)
CMD ["python", "run_client.py"]
