FROM python:3.12-slim

WORKDIR /app

# 가상 환경 설정
RUN python3 -m venv /app/venv
ENV PATH="/app/venv/bin:$PATH"

# 의존성 설치
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 소스 코드 복사
COPY . .

# 클라이언트 실행
CMD ["python", "run_client.py"]