# 🧠 Ollama + Open WebUI 통합 실행 환경

이 저장소는 [Ollama](https://ollama.com/)와 [Open WebUI](https://github.com/open-webui/open-webui)를 Docker Compose를 사용하여 쉽게 연동할 수 있도록 구성된 통합 실행 환경입니다.  
로컬에서 LLM을 편리하게 테스트하고 WebUI를 통해 인터랙티브하게 사용할 수 있습니다.

---

## 📁 프로젝트 구조

```bash
.
├── docker-compose.yml         # Ollama + Open WebUI 실행 환경 구성
├── ollama/                    # Ollama 백엔드 코드
├── llama.cpp/                 # GGUF 변환 및 로컬 모델 관리 도구
└── open-webui/                # 오픈소스 Web UI for Ollama
```

---

## 🚀 실행 방법

### 1. 모델 준비 (예: phi4, gemma3 등)
Ollama에서 사용할 모델을 먼저 다운로드합니다. 예:

```bash
ollama pull gemma3:12b
```

또는 커스텀 모델을 직접 변환해 사용할 경우 `llama.cpp` 내 `convert_*.py` 스크립트를 사용할 수 있습니다.

---

### 2. Docker 실행

```bash
docker compose up -d
```

- Ollama: `localhost:11434`
- Open WebUI: [http://localhost:8080](http://localhost:8080)

---

## ⚙️ 환경설정

- `OLLAMA_BASE_URLS`: WebUI가 참조할 Ollama 서버 주소
- `WEBUI_AUTH=False`: 로그인 없이 사용 가능
- `USE_CUDA_DOCKER=true`: GPU 가속 설정
- `WEBUI_NAME`: 웹 인터페이스에 표시될 이름

---

## 🖥️ 접속

- 웹 브라우저에서 [http://localhost:8080](http://localhost:8080) 접속
- `ollama run mistral` 등을 통해 CLI에서도 테스트 가능

---

## 🧩 모델 포맷 변환 (선택)

`llama.cpp`에 포함된 스크립트를 사용해 huggingface 모델을 GGUF 포맷으로 변환할 수 있습니다.

예:
```bash
python convert_hf_to_gguf.py ./google \
--outfile gemma-3-12b-it.gguf
```

---

## 🛠️ 커스텀 설정/디버깅

- 환경 설정은 각 컨테이너의 `environment` 블록에서 수정 가능
- `volumes`를 통해 로컬 코드 수정 가능
- WebUI 설정 파일은 `open-webui/` 내에 위치

---

## 📦 요구 사항

- Docker 및 Docker Compose 설치
- NVIDIA GPU 사용 시: [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) 설치 필요

---

## 📜 라이선스

- Ollama: [MIT License](https://github.com/jmorganca/ollama/blob/main/LICENSE)
- Open WebUI: [Apache 2.0 License](https://github.com/open-webui/open-webui/blob/main/LICENSE)
- llama.cpp: [MIT License](https://github.com/ggerganov/llama.cpp/blob/master/LICENSE)
