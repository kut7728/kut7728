> [!important] ios 기기에서는 애플에서 자체 생산한 ARM아키텍처 프로세서인 A시리즈 칩을 사용하고 있습니다. A시리즈 칩셋들은 SoC로 제작되어 CPU, GPU, NPU, 메모리가 하나의 다이에 붙어 있습니다. 이런식의 SoC 설계는 발열관리에 효과적이고 데이터의 이동이 빨라 병목이 줄어드는 장점이 있습니다.

  

## AP

- AP는 **Application Processor**, 스마트폰, 태블릿 등의 모바일 기기에서 **운영체제와 앱을 실행하는 중심적인 역할**을 수행하는 칩입니다.
- AP는 단순히 연산만 수행하는 게 아니라, **전체 앱 실행, 사용자 인터페이스 처리, 센서 제어 등** 모든 **시스템 동작의 중심** 역할을 합니다

## iOS의 AP 특징

### 1. Apple Silicon (A 시리즈)

- Apple은 A4부터 시작해 현재는 A17 Pro 등 최신 칩셋까지 자체 설계하고 있음
- ARM 아키텍처 기반의 SoC(System on a Chip)

### 2. SoC 구조

- AP는 단일 칩 안에 CPU, GPU, Neural Engine(NPU), ISP, 메모리 컨트롤러, 보안 모듈 등이 통합되어 있음
- 이는 공간 절약, 발열 감소, 전력 효율 개선, 데이터 전송 속도 향상에 기여

### 3. CPU (Central Processing Unit)

- 명령어 처리와 앱 실행을 담당
- A 시리즈 칩에서는 고성능 코어와 고효율 코어로 구성된 big.LITTLE 아키텍처 채택

### 4. GPU (Graphics Processing Unit)

- UI 렌더링, 3D 그래픽, Metal 기반 연산 등 시각적 처리 담당

### 5. Neural Engine

- Face ID, 사진 보정, Siri 등에서 활용되는 머신 러닝 연산 전용 유닛
- ML모델의 실시간 추론을 담당

> [!important]
> 
> > 뉴럴 엔진 VS GPU
> 
> **왜 GPU가 아닌 Neural Engine인가?**
> 
> 1. **전용 설계**
>     
>     → 딥러닝에 자주 쓰이는 연산(MAC, Matrix Multiply)만 수행하도록 설계
>     
>     → 덕분에 속도도 빠르고 전력 효율도 GPU 대비 매우 높음
>     
> 2. **iOS 생태계에 특화**
>     
>     → Apple은 Neural Engine을 iOS SDK(Core ML 등)와 tightly coupled 시킴
>     
>     → 개발자가 딥러닝 연산을 할 때 특별한 설정 없이도 활용 가능
>     
> 3. **Always-on ML 기능 지원**
>     
>     → 예: 잠금 해제 전 Face ID 스캔, Siri의 연속 음성 인식
>     
>     → **저전력 상태에서도 동작 가능**하도록 설계
>     
> 
> ---
> 
> **🧠 면접에서 강조하면 좋은 포인트**
> 
> - "GPU도 병렬 연산을 잘하지만, **Neural Engine은 딥러닝 연산에 특화된 전용 하드웨어**라서, 더 적은 전력으로 더 빠른 결과를 얻을 수 있다."
> - "iOS에서는 Core ML이 자동으로 연산을 최적 경로(GPU, CPU, Neural Engine 중 선택)로 보내기 때문에, 개발자는 편하게 고성능 ML 기능을 쓸 수 있다."
> - "Neural Engine 덕분에 iOS 기기는 ML 기능을 **온디바이스로 빠르게 처리**할 수 있어서 **프라이버시와 반응 속도**가 크게 향상된다."

### 6. 보안 설계

- Secure Enclave를 포함하여 Face ID, Touch ID 등의 생체인식 정보를 안전하게 보호