# 실시간 웹캠 자세 추정 데모 (각도 조절 및 오디오 피드백)

이 프로젝트는 웹 브라우저 환경에서 실시간으로 웹캠 영상을 받아 **사람의 자세를 추정**하고, **무릎 각도를 기반**으로 '앉기(Sitting)'와 '서기(Standing)' 자세를 분류하는 간단한 데모입니다. 사용자가 직접 자세 판별 기준이 되는 **각도 임계값을 조절**할 수 있으며, 인식된 자세에 따라 **다른 톤의 소리(사인파) 피드백**을 제공합니다.

## ✨ 주요 기능

*   **실시간 자세 추정:** 웹캠 영상에서 사람의 주요 관절 위치를 실시간으로 감지합니다. (TensorFlow.js MoveNet 모델 사용)
*   **자세 분류 (앉기/서기):** 감지된 관절 정보를 바탕으로 무릎 각도를 계산하여 '앉기'와 '서기' 상태를 분류합니다.
*   **시각적 피드백:**
    *   웹캠 영상 위에 감지된 뼈대(스켈레톤)를 그립니다.
    *   판별된 자세(Sitting 🧘 / Standing🧍)를 텍스트와 이모지로 화면 좌측 상단에 표시합니다.
*   **인터랙티브 임계값 조절:**
    *   '앉기'와 '서기'를 판별하는 무릎 각도 임계값을 사용자가 슬라이더를 통해 직접 조절할 수 있습니다.
*   **오디오 피드백:**
    *   Web Audio API를 사용하여 자세에 따라 다른 주파수의 사인파 소리를 생성합니다. (앉기: 낮은 톤, 서기: 높은 톤)
    *   오디오 피드백을 켜고 끌 수 있는 버튼을 제공합니다.

## 📸 데모 (스크린샷 또는 GIF 추가 권장)

(여기에 작동 모습을 보여주는 스크린샷이나 GIF 이미지를 추가하면 좋습니다.)
![데모 이미지](path/to/your/demo_image.gif)

## 🛠️ 기술 스택

*   **HTML:** 웹 페이지 구조
*   **CSS:** 스타일링
*   **JavaScript:** 로직 구현, DOM 조작, 이벤트 처리
*   **TensorFlow.js:**
    *   `@tensorflow/tfjs-core`, `@tensorflow/tfjs-converter`, `@tensorflow/tfjs-backend-webgl`: 핵심 라이브러리 및 WebGL 백엔드
    *   `@tensorflow-models/pose-detection`: 사전 훈련된 자세 추정 모델(MoveNet) 로드 및 실행
*   **Web Audio API:** 실시간 오디오 생성 및 제어

## 🚀 실행 방법

1.  **저장소 복제 또는 다운로드:**
    ```bash
    git clone https://github.com/hwkims/body.git
    ```
    또는 ZIP 파일로 다운로드하여 압축을 해제합니다.

2.  **HTML 파일 열기:**
    *   다운로드 받은 폴더 내의 `pose_interactive_audio_demo.html` (또는 최종 파일명) 파일을 웹 브라우저(Chrome, Firefox 등 최신 버전 권장)에서 직접 엽니다.
    *   **로컬 웹 서버** (예: VS Code의 Live Server 확장 기능)를 사용하여 실행하는 것을 권장합니다. 일부 브라우저는 로컬 파일 접근 시 보안 제한이 있을 수 있습니다.

3.  **권한 허용:**
    *   브라우저가 **웹캠 접근 권한**을 요청하면 '허용'을 클릭합니다.
    *   오디오 피드백 버튼을 처음 클릭 시 **오디오 사용 권한**이 필요할 수 있습니다.

4.  **실행 확인:**
    *   웹캠 영상과 함께 뼈대가 그려지고, 자세에 따라 좌측 상단에 텍스트가 표시되는지 확인합니다.
    *   슬라이더를 조절하여 각도 임계값을 변경해 봅니다.
    *   오디오 버튼을 눌러 소리 피드백을 테스트합니다.

**참고:** TensorFlow.js 라이브러리를 CDN을 통해 로드하므로 **인터넷 연결이 필요**합니다.

## ⚙️ 설정 및 조작

*   **앉기 판별 각도:** 슬라이더를 조절하여 이 각도 *미만*일 때 '앉기'로 판별하도록 설정합니다.
*   **서기 판별 각도:** 슬라이더를 조절하여 이 각도 *초과*일 때 '서기'로 판별하도록 설정합니다. (앉기 판별 각도보다 커야 의미가 있습니다.)
*   **오디오 버튼:** 버튼을 클릭하여 자세에 따른 소리 피드백을 켜거나 끌 수 있습니다.

## ⚠️ 제한 사항

*   **사람 모델 사용:** 사용된 MoveNet 모델은 **사람 자세 추정**에 최적화되어 있어, 강아지 등 다른 동물에게는 정확도가 매우 낮거나 작동하지 않을 수 있습니다.
*   **기본적인 분류:** '앉기'/'서기' 분류는 무릎 각도만을 이용한 단순한 규칙 기반으로, 다양한 자세나 카메라 각도, 가려짐 등에 의해 부정확할 수 있습니다.
*   **성능:** 실시간 영상 처리는 사용자의 컴퓨터 성능에 따라 프레임 속도(FPS)가 달라질 수 있습니다.
*   **웹캠 및 오디오 필수:** 웹캠과 오디오 출력 장치가 필요하며, 브라우저에서 관련 권한을 허용해야 합니다.

## 🌱 향후 개선 아이디어

*   **동물 특화 모델 적용:** 강아지 또는 다른 동물을 위한 자세 추정 모델을 찾아 적용하거나 직접 훈련하여 사용.
*   **더 많은 자세 분류:** '눕기', '걷기' 등 더 다양한 자세를 인식하도록 로직 개선 또는 머신러닝 분류기 도입.
*   **UI/UX 개선:** 시각적 요소를 더 보기 좋게 다듬고 사용자 인터페이스 개선.
*   **오류 처리 강화:** 웹캠/오디오 접근 실패, 모델 로딩 실패 등에 대한 처리 보강.
*   **성능 최적화:** WebAssembly(WASM) 백엔드 사용 등 성능 개선 방안 탐색.

## 📄 라이선스

이 프로젝트는 [MIT 라이선스](LICENSE)를 따릅니다. (저장소에 LICENSE 파일을 추가하는 것을 권장합니다.)
