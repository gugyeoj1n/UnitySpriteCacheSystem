### 🎨 유니티 스프라이트 캐시 시스템

    Addressables 또는 Resources 기반의 스프라이트 전용 캐시 시스템입니다.
    중복 로드를 방지하고, 메모리 예산을 지키며, 저메모리 상황에서는 안전하게 정리합니다.

### 🖥️ 개발 환경

    Unity 6000.1.4f1

### ✨ 주요 기능

    Addressables / Resources 모두 지원
    LRU(Least Recently Used) 방식 캐시 (참조 카운트 0인 항목만 제거)
    중복 로딩 방지 (동일 키 요청 시 하나의 Task 공유)
    텍스처 단위 메모리 관리 (Atlas로 묶인 여러 Sprite도 1회만 용량 계산)
    저메모리 신호 대응 (Application.lowMemory 발생 시 즉시 정리)
    UI용 컴포넌트 제공 (Image에 붙이면 자동 로드/해제)

### 📦 설치 방법

아래 스크립트를 프로젝트의 Scripts/ 폴더 등에 내장

    SpriteCache.cs
    SpriteCacheHandle.cs
    ISpriteProvider.cs
    AddressablesSpriteProvider.cs   // Addressables 사용 시
    ResourcesSpriteProvider.cs      // Resources 전용/백업용

### 🧩 사용법

    1) 초기 설정
    빈 GameObject 생성 → SpriteCache 컴포넌트 추가

    옵션 설정
    Use Addressables: Addressables 사용 시 체크
    Memory Budget (MB): 기기 사양에 맞게 지정 (예: 64~128MB)
 
    2) 자동 사용 (UI Image)
    Image가 붙은 오브젝트에 SpriteCacheHandle 추가
    key 입력 → OnEnable 시 자동 로드, OnDisable 시 자동 해제

    3) 코드에서 직접 사용
    // 로드
    var sprite = await SpriteCache.Instance.LoadAsync("ui/icons/sword");
    myImage.sprite = sprite;

    // 다 쓰면 해제 (Load와 짝 맞추기)
    SpriteCache.Instance.Release("ui/icons/sword");
