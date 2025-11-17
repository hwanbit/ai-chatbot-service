## 🤖 Ollama 웹 챗 서비스 (AI Chat Service)

이 프로젝트는 **Flask**와 **Ollama**를 활용하여 웹에서 대규모 언어 모델(LLM)과 대화할 수 있는 스트리밍 챗봇 서비스를 구축한 것입니다. 사용자는 웹 인터페이스를 통해 Ollama에 호스팅된 3개 모델과 실시간으로 대화할 수 있습니다.

-----

### ✨ 주요 기능

  * **실시간 스트리밍 응답:** Ollama API와 Flask의 `stream_with_context` 기능을 사용하여 모델의 응답을 실시간(NDJSON 형식)으로 브라우저에 표시합니다.
  * **대화 기록(History) 유지:** 사용자와 모델 간의 대화 기록을 `messages` 리스트에 저장하여, 새로운 요청 시 이전 문맥을 유지합니다.
  * **모델 선택 기능:** 웹 인터페이스에서 모델명(예: `gemma3:4b`)을 입력하여 실시간으로 사용할 모델을 변경할 수 있습니다.
      * **기본 모델:** `gemma3:4b`
      * **사용 가능 모델:** `gemma3:4b`, `llama2`, `exaone3.5`
  * **친절한 시스템 메시지:** 기본 시스템 역할(`role: "system"`)이 **"너는 사용자의 친절한 친구야."** 로 설정되어 있습니다.
  * **간결한 웹 UI:** HTML, CSS, JavaScript만으로 구현되어 있으며, 다크 모드를 지원합니다.

-----

### 🛠️ 개발 환경 및 준비 사항

1.  **Python 3.8 이상**
2.  **Ollama 설치 및 실행:** Ollama 서버가 실행 중이어야 합니다.
3.  **Python 의존성:** `Flask`와 `requests` 라이브러리가 필요합니다.
    ```bash
    pip install Flask requests
    ```
4.  **Ollama 모델 다운로드:** 사용할 모델(예: `gemma3:4b`)이 Ollama에 pull 되어 있어야 합니다.

-----

### ⚙️ 설정 및 실행 방법

#### 1\. 저장소 클론 (Clone Repository)

먼저 Git을 사용하여 이 프로젝트 저장소를 로컬 환경에 복제합니다.

```bash
git clone https://github.com/hwanbit/ai-chatbot-service.git
cd ai-chatbot-service # 프로젝트 디렉토리로 이동
```

#### 2\. Ollama 연결 설정

`app.py` 파일에서 Ollama API의 주소를 설정합니다. 기본값은 Docker 환경을 가정하고 있습니다.

```python
# app.py

# Ollama 서버의 API 주소이며, 환경에 맞게 수정해야 합니다.
OLLAMA_CHAT_URL = "http://host.docker.internal:11434/api/chat"
```

> **참고:** Ollama를 로컬에서 직접 실행하는 경우, `http://host.docker.internal:11434` 대신 `http://localhost:11434` 또는 실제 Ollama 서버 주소를 사용해야 할 수 있습니다.

#### 3\. 프로젝트 구조

Flask 애플리케이션이 `templates` 폴더의 `index.html`을 찾고, `static` 폴더에서 폰트를 제공할 수 있도록 다음과 같은 구조를 유지해야 합니다.

```
.
├── app.py
├── templates/
│   └── index.html
└── static/
    └── fonts/
        └── NanumSquareB.otf # 폰트 파일
```

#### 4\. 애플리케이션 실행

`app.py` 파일을 실행합니다.

```bash
python app.py
```

  * Flask 서버는 기본적으로 `http://0.0.0.0:5000`에서 실행됩니다.

-----

### 💻 사용 방법

1.  **웹 접속:** 웹 브라우저를 열고 `http://localhost:5000`으로 접속합니다.
2.  **모델 설정:** 상단 **Model** 입력창에 사용할 Ollama 모델명(예: `llama2`)을 입력할 수 있습니다. (입력하지 않으면 기본값 `gemma3:4b` 사용)
3.  **메시지 전송:** **Message** 입력창에 질문을 입력합니다.
      * **Enter** 키를 누르면 메시지가 전송됩니다.
      * **Shift+Enter** 키를 누르면 줄바꿈이 됩니다.
4.  **대화 초기화:** **Clear** 버튼을 클릭하여 현재 화면에 보이는 대화 내용과 내부의 대화 기록(`history`)을 초기화할 수 있습니다.
