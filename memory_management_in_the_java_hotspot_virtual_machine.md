## Memory Management in the Java HotSpot™ Virtual Machine

Java™ 2 플랫폼인 Standard Edition(J2SE™)의 한 가지 장점은 자동 메모리 관리를 수행하여 개발자를 명시적 메모리 관리의 복잡함으로부터 보호한다는 것입니다.

이 백서에서는 Sun의 J2SE 5.0 릴리스에서 Java HotSpot Virtual Machine (JVM)의 메모리 관리에 대해 광범위하게 설명합니다. 메모리 관리를 수행하는 데 사용할 수 있는 가비지 수집기(Garbage Collector)에 대해 설명하고, 수집기 선택, 설정과 메모리 크기 구성에 대한 몇 가지 조언을 제공합니다. 또한 가비지 수집기 동작에 영향을 미치는 가장 일반적으로 사용되는 몇 가지 옵션을 나열하고 보다 자세한 설명서에 대한 수많은 링크를 제공하는 리소스 역할도 합니다.

섹션 2는 자동 메모리 관리 개념을 처음 접하는 독자들을 위한 것입니다. 이 자료에는 이러한 관리의 이점과 프로그래머가 데이터를 위한 공간을 명시적으로 할당 해제해야 하는 이점에 대한 간략한 설명이 포함되어 있습니다. 그런 다음 섹션 3은 일반적인 가비지 수집 개념, 설계 선택 및 성능 측정 기준에 대한 개요를 제시합니다. 또한 일반적으로 사용되는 메모리를 개체의 예상 수명을 기반으로 세대(Generations) 라고 하는 다른 영역으로 구성되는 것에 대해 소개합니다. 이러한 세대별 분리는 광범위한 애플리케이션에서 가비지 수집 중지 시간과 전체 비용을 줄이는 데 효과적이라는 것이 입증되었습니다.

본 문서의 나머지 부분에서는 HotSpot JVM 관련 정보를 제공한다. 섹션 4에서는 J2SE 5.0 업데이트 6에 새로 추가된 것을 포함하여 사용 가능한 4개의 가비지 수집기를 설명하고 있으며, 이들 수집기가 모두 사용하는 세대 메모리 조직을 문서화합니다. 각 수집기에 대해 섹션 4는 사용되는 수집 알고리즘의 유형을 요약하고 해당 수집기를 선택하는 것이 적절한 시기를 지정합니다.

섹션 5에서는 애플리케이션이 실행 중인 플랫폼 및 운영 체제를 기반으로 (1) 가비지 수집기, 힙 크기 및 HotSpot JVM(클라이언트 또는 서버)의 자동 선택과 (2) 사용자가 지정한 원하는 동작을 기반으로 한 동적 가비지 수집 튜닝을 결합한 새로운 기술을 설명합니다. 이 기술을 ergonomics 이라고 합니다.

섹션 6에서는 가비지 수집기를 선택하고 구성하기 위한 권장 사항을 제공합니다. 또한 `OutOfMemoryError`에 대해 수행할 작업에 대한 조언을 제공합니다. 섹션 7은 가비지 수집 성능을 평가하는 데 사용할 수 있는 몇 가지 도구를 간략하게 설명하고 섹션 8은 가비지 수집기 선택 및 동작과 관련하여 가장 일반적으로 사용되는 명령줄 옵션을 나열합니다. 마지막으로, 섹션 9는 본 논문에서 다루는 다양한 주제에 대한 자세한 설명서에 대한 링크를 제공합니다.

**추가 예정**

## 참고

- [공식 문서](https://www.oracle.com/technetwork/java/javase/memorymanagement-whitepaper-150215.pdf)