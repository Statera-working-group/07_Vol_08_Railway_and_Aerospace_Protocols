**Volume 08. Railway and Aerospace Protocols**

# Chapter 07. ARINC 429

## 07.01. ARINC 429 Physical Layer

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

ARINC 429는 상용 항공기(Commercial Aircraft)와 수송 항공기(Transport Aircraft)의 항공전자 시스템(Avionics System)에서 널리 사용되는 단순하면서도 결정론적인 물리 통신 계층(Physical Communication Layer)을 정의한다. 물리 계층(Physical Layer)은 하나의 송신기(Transmitter)가 하나 이상의 수신기(Receiver)로 정보를 전달하는 단방향 점대점 전송(Unidirectional Point-to-Point Transmission)을 기반으로 한다. 이러한 구조는 통신 경합(Contention)을 최소화하고 중재(Arbitration)를 제거하여 안전 필수 항공전자 시스템(Safety-Critical Avionics System)에 적합한 예측 가능한 통신 동작을 제공한다.

전기적 인터페이스(Electrical Interface)는 연선(Twisted Pair)을 통해 전달되는 평형 차동 신호(Balanced Differential Signal)를 사용한다. 수신기는 각 도체(Conductor)의 전압을 독립적으로 해석하는 대신 두 도체 사이의 전압 차이를 측정한다. 차동 신호 방식(Differential Signaling)은 두 전선에 유사하게 결합되는 잡음(Noise)이 공통 모드 교란(Common-Mode Disturbance)으로 나타나도록 하므로 전자기 간섭(Electromagnetic Interference)에 대한 내성을 향상시킨다.

ARINC 429 신호 방식(Signaling)은 일반적으로 HIGH, NULL, LOW로 표현되는 세 가지 전기적 상태(Electrical State)를 사용한다. HIGH 상태는 차동 전압(Differential Voltage)의 한쪽 극성을 나타내고 LOW 상태는 반대쪽 극성을 나타낸다. NULL 상태에서는 차동 전압이 거의 0 V에 위치하며 전송되는 펄스(Pulse)를 서로 분리한다. 이러한 3레벨 영복귀 방식(Three-Level Return-to-Zero)은 별도의 클록 선(Clock Line) 없이도 수신기가 개별 비트(Bit)를 명확하게 구분할 수 있도록 한다.

HIGH 및 LOW 상태에서 공칭 차동 출력 크기(Nominal Differential Output Magnitude)는 약 10 V이며, 서로 반대되는 극성에 의해 논리 상태(Logical State)가 결정된다. NULL 상태는 약 0 V의 차동 전압을 중심으로 형성된다. 실제 송신기와 수신기는 이상적인 전압값이 아니라 규정된 전압 허용 범위(Voltage Tolerance)에서 동작하므로 케이블 손실(Cable Loss), 부품 편차(Component Variation), 온도 변화(Temperature Change), 항공기 내부의 전기적 교란(Electrical Disturbance)이 존재해도 안정적인 통신이 가능하다.

ARINC 429는 일반적으로 BPRZ로 약칭되는 바이폴라 영복귀 변조(Bipolar Return-to-Zero Modulation)를 사용한다. 각 비트 구간(Bit Interval)에서 송신기는 먼저 차동 선로를 양 또는 음의 신호 레벨로 구동한 다음, 다음 비트가 시작되기 전에 NULL 영역으로 복귀시킨다. 이러한 의도적인 영복귀(Return-to-Zero)는 규칙적인 전기적 전이(Electrical Transition)를 생성하여 수신기의 타이밍 복구(Timing Recovery)를 지원하면서 비교적 단순한 송수신 회로 구현을 가능하게 한다.

ARINC 429에는 일반적으로 두 가지 표준 전송 속도(Transmission Rate)가 사용된다. 저속 동작(Low-Speed Operation)은 약 12.0\~14.5 kbit/s 범위이며, 고속 동작(High-Speed Operation)은 100 kbit/s이다. 특정 버스(Bus)에 연결되는 장비는 서로 호환되는 데이터 속도(Data Rate)를 사용해야 한다. 이러한 비교적 낮은 대역폭(Bandwidth)은 높은 데이터 처리량보다 결정론적 전달(Deterministic Delivery), 전기적 강건성(Electrical Robustness), 인증 단순성(Certification Simplicity)이 중요했던 항공전자 환경을 반영한다.

물리적 토폴로지(Physical Topology)는 기본적으로 단방향(Simplex) 구조이다. 송신기는 전용 연선(Dedicated Pair)을 따라 외부로 데이터를 전달하지만 수신기는 동일한 배선을 통해 응답하지 않는다. 두 항공전자 장치(Avionics Unit)가 양방향으로 정보를 교환해야 하는 경우 일반적으로 별도의 ARINC 429 채널(Channel)이 필요하며, 각 장치는 한 채널에서는 송신기로, 다른 채널에서는 수신기로 동작한다. 이러한 분리는 충돌(Collision)을 방지하고 통신 방향을 물리적으로 명확하게 만든다.

하나의 송신기(Transmitter)는 일반적으로 자신의 출력에 연결된 여러 수신 장치(Receiving Device)에 동일한 정보를 전달할 수 있다. 이를 통해 다중점 중재 메커니즘(Multidrop Arbitration Mechanism)을 도입하지 않고도 센서 또는 항공전자 데이터를 여러 장치가 공유할 수 있다. 송신기는 해당 연선에서 유일한 능동 신호원(Active Source)으로 유지되며 연결된 수신기는 청취자(Listener) 역할을 한다. 따라서 수신기 추가는 전기적 부하(Electrical Loading)를 변화시키지만 메시지 충돌(Message Collision)이나 송신기 간 경쟁을 발생시키지는 않는다.

연선 케이블링(Twisted-Pair Cabling)은 전기적으로 잡음이 많은 항공기 환경에서 전자기 적합성(Electromagnetic Compatibility)을 유지하는 데 중요한 요소이다. 외부 전자기장(Electromagnetic Field)이 두 전선에 유사한 교란을 유도하도록 도체를 배치하고 이를 차동 수신(Differential Reception)과 결합함으로써 모터(Motor), 전력 변환기(Power Converter), 무선 장치(Radio), 스위칭 회로(Switching Circuit) 등에서 발생하는 공통 모드 간섭(Common-Mode Interference)에 대한 민감도를 크게 낮출 수 있다.

ARINC 429 채널과 인접한 항공기 배선 사이의 전자기 결합(Electromagnetic Coupling)을 줄이기 위해 케이블 차폐(Cable Shielding)를 추가로 적용할 수 있다. 따라서 차폐 종단(Shield Termination), 접지 방식(Grounding Practice), 커넥터 설계(Connector Design), 하네스 라우팅(Harness Routing), 고에너지 도체와의 이격(Separation)이 중요한 구현 요소가 된다. 프로토콜 자체가 전기적으로 강건하더라도 실제 항공전자 배선 시스템 전체에서 이러한 강건성을 유지하려면 적절한 설치 공학(Installation Engineering)이 필요하다.

특성 임피던스(Characteristic Impedance) 역시 중요한 물리 계층 설계 요소이다. ARINC 429 설치에서는 일반적으로 인터페이스 규격에 적합한 임피던스를 가진 연선 케이블을 사용하며, 통상 약 78 Ω의 공칭 케이블 특성(Nominal Cable Characteristic)과 연관된다. 적절한 임피던스를 유지하고 커넥터(Connector), 스플라이스(Splice), 분기(Branch)에서 발생하는 불연속성(Discontinuity)을 제어하면 특히 고속 채널에서 신호 반사(Reflection)를 제한하고 파형 품질(Waveform Quality)을 유지하는 데 도움이 된다.

송신기 출력 특성(Transmitter Output Characteristic)은 전압 진폭(Voltage Amplitude)과 전이 특성(Transition Behavior)이 수신기 요구사항과 호환되도록 제어된다. 지나치게 빠른 에지(Edge)는 전자기 방출(Electromagnetic Emission)과 링잉(Ringing)을 증가시킬 수 있으며, 지나치게 느린 전이는 타이밍 여유(Timing Margin)를 감소시킬 수 있다. 따라서 ARINC 429에서는 단순히 올바른 전압 수준에 도달하는 것뿐 아니라 상승 및 하강 특성(Rise and Fall Behavior)도 전기적 인터페이스의 일부로 취급한다.

수신기 회로(Receiver Circuitry)는 감쇠(Attenuation)와 전기적 잡음(Electrical Noise)을 허용하면서 HIGH, LOW, NULL 영역을 안정적으로 구분해야 한다. 차동 임계값 검출(Differential Threshold Detection)을 이용하면 수신기가 신호의 극성을 판단하면서 0 V 주변의 작은 교란에는 과도하게 반응하지 않을 수 있다. 수신기는 버스 접근에서 수동 참여자(Passive Participant)이므로 주요 물리 계층 역할은 신호 검출(Signal Detection), 전기적 부하 제어, 잡음 제거(Noise Rejection), 입력 파형을 디지털 비트 정보로 정확하게 변환하는 것이다.

공유 클록(Shared Clock)이 존재하지 않는다는 점도 중요하다. 타이밍 정보(Timing Information)는 알려진 비트 전송률(Bit Rate)과 영복귀 파형(Return-to-Zero Waveform)에서 발생하는 전이로부터 얻어진다. 각 수신기는 자체 타이밍 회로(Local Timing Circuitry)를 사용하여 예상되는 비트 구간에서 입력 신호를 샘플링한다. 따라서 신뢰성 있는 통신은 별도의 클록 신호 배포가 아니라 송신기 타이밍, 수신기 허용 오차, 파형 형상(Waveform Shape), 발진기 정확도(Oscillator Accuracy)의 적절한 제어에 의존한다.

항공전자 아키텍처(Avionics Architecture)의 관점에서 물리 계층은 네트워크 효율성(Network Efficiency)보다 격리(Isolation)를 우선한다. 전용 송신 채널은 현대적인 스위치드 네트워크(Switched Network)보다 많은 배선을 요구하지만 통신 경계를 명확하게 만든다. 하나의 ARINC 429 연선에서 발생한 고장이나 비정상 전송은 본질적으로 다른 독립 채널에서 경합을 발생시키지 않는다. 이러한 특성은 고장 격리(Fault Containment)에 기여하고 항공전자 장비 사이의 통신 의존성 분석을 단순화한다.

따라서 물리 계층 문제 해결(Physical-Layer Troubleshooting)은 상위 수준 정보의 해석보다 전기적 측정에서 시작된다. 엔지니어는 차동 진폭(Differential Amplitude), 극성(Polarity), 비트 타이밍(Bit Timing), 상승 및 하강 특성, NULL 구간, 잡음, 반사, 연선의 연속성(Continuity)을 검사할 수 있다. 오실로스코프(Oscilloscope) 또는 전용 ARINC 인터페이스 분석기(ARINC Interface Analyzer)를 사용하면 송신기, 하네스, 커넥터, 수신기 부하, 접지, 신호 무결성(Signal Integrity) 중 어디에서 통신 문제가 발생하는지 분석할 수 있다.

하네스 설계(Harness Design)는 항공기의 전체 운용 수명(Service Life)에 걸친 항공우주 환경(Aerospace Environment)도 고려해야 한다. 진동(Vibration), 온도 사이클링(Temperature Cycling), 습기(Moisture), 커넥터 열화(Connector Degradation), 기계적 응력(Mechanical Stress), 정비 작업(Maintenance Activity), 전자기 노출(Electromagnetic Exposure)은 시간이 지나면서 전기적 성능을 변화시킬 수 있다. 따라서 항공우주 등급 배선과 커넥터, 차폐, 스트레인 릴리프(Strain Relief), 적절한 라우팅 및 검사 절차가 통신 무결성(Communication Integrity)을 유지하는 데 필요하다.

ARINC 429는 복잡한 네트워크 스케줄링(Network Scheduling)이 아니라 물리적 아키텍처 자체를 통해 결정론적 동작(Deterministic Behavior)을 구현할 수 있음을 보여준다. 하나의 채널에는 하나의 송신기만 허용되므로 물리 인터페이스에 충돌 검출(Collision Detection), 토큰 패싱(Token Passing), 동적 중재(Dynamic Arbitration)가 필요하지 않다. 연결성과 통신 방향을 제한함으로써 예측 가능성을 확보하며, 배선 효율과 대역폭을 희생하는 대신 단순성, 격리성, 높은 분석 가능성(Analyzability)을 얻는다.

이러한 설계 철학(Design Philosophy)은 이후 다루어지는 ARINC 429 워드 구조(Word Structure), 레이블 할당(Label Allocation), 버스 아키텍처(Bus Architecture), UAV 항공전자 통합(UAV Avionics Integration)을 이해하기 위한 기반을 제공한다. 물리 계층은 이러한 기능이 동작하는 전기적 채널을 형성하며, 전용 차동 연선(Differential Twisted Pair), 제어된 바이폴라 신호(Controlled Bipolar Signaling), 정의된 전송 속도, 단방향 통신, 예측 가능한 송신기-수신기 연결성이 그 핵심을 구성한다.

## 07.02. ARINC 429 Word Structure

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

ARINC 429는 전송 정보를 고정 길이 32비트 워드(Fixed-Length 32-Bit Word)로 구성하여 항공전자 통신(Avionics Communication)을 위한 간결하고 매우 예측 가능한 데이터 형식(Data Format)을 제공한다. 전송되는 매개변수(Parameter)의 종류와 관계없이 모든 워드(Word)는 동일한 수의 비트 위치를 사용한다. 이러한 고정 구조는 송신기(Transmitter)와 수신기(Receiver)의 구현을 단순화하고 비행 제어(Flight Control), 항법(Navigation), 센서(Sensor), 디스플레이(Display), 항공기 관리 장비(Aircraft Management Equipment)에서 결정론적 처리(Deterministic Processing)를 지원한다.

32비트 워드(32-Bit Word)는 전송 정보의 식별, 출처 또는 목적지 해석, 데이터 내용, 상태 및 무결성(Integrity)을 나타내는 기능 필드(Functional Field)로 구분된다. 일반적인 표기에서 비트 1\~8은 레이블(Label), 비트 9\~10은 출처/목적지 식별자(Source/Destination Identifier), 비트 11\~29는 일반적으로 데이터(Data), 비트 30\~31은 부호/상태 매트릭스(Sign/Status Matrix), 비트 32는 패리티(Parity)를 구성한다.

레이블(Label)은 워드에 포함된 정보의 의미를 식별하는 데 사용되는 8비트 필드(8-Bit Field)이다. ARINC 429는 긴 텍스트 형태의 매개변수 이름을 전송하는 대신 특정 항공전자 데이터(Avionics Data) 범주에 레이블을 할당한다. 수신기는 레이블을 검사하여 해당 워드가 자신에게 필요한 정보를 포함하고 있는지 판단하고, 나머지 데이터 필드(Data Field)를 어떠한 방식으로 해석해야 하는지 결정한다.

ARINC 429 레이블(Label)은 전통적으로 8개의 레이블 비트를 세 자리 값으로 간결하게 표현할 수 있는 8진수 표기법(Octal Notation)을 사용한다. 구현 과정에서 자주 혼동되는 사항 중 하나는 레이블 비트(Label Bit)의 전송 순서와 표시 순서이다. 엔지니어는 캡처된 버스 트래픽(Bus Traffic)을 분석할 때 레이블의 논리적 표현(Logical Representation)과 통신 채널에서 실제 관찰되는 직렬 비트 시퀀스(Serial Bit Sequence)를 구분해야 한다.

비트 9와 10에는 일반적으로 SDI로 약칭되는 출처/목적지 식별자(Source/Destination Identifier)가 위치한다. 특정 레이블의 정의에 따라 이 비트들은 유사한 정보를 생성하는 여러 출처(Source)를 구분하거나 서로 다른 목적지(Destination)에 필요한 해석을 식별할 수 있다. 별도의 출처 또는 목적지 식별이 필요하지 않은 응용에서는 SDI 위치를 데이터 표현(Data Representation)의 일부로 사용할 수도 있다.

주요 정보 필드(Information Field)는 일반적으로 비트 11\~29를 차지하며 인코딩된 매개변수(Encoded Parameter)를 위한 19개의 비트 위치를 제공한다. 정확한 해석 방법은 레이블(Label)과 관련 데이터 형식(Data Format)에 따라 달라진다. 따라서 ARINC 429는 전송 구조(Transport Structure)와 매개변수 의미(Parameter Meaning)를 분리하며, 물리적인 워드는 항상 32비트이지만 데이터 필드의 의미는 송신 장비와 수신 장비가 공유하는 사전 정의된 규칙에 의해 결정된다.

일반적으로 BNR이라고 하는 이진수 표현(Binary Number Representation)은 연속적으로 변화하는 수치량(Numerical Quantity)에 자주 사용된다. BNR 인코딩(BNR Encoding)에서는 선택된 데이터 비트가 고도(Altitude), 위치(Position), 속도(Velocity), 각도(Angle) 또는 기타 측정량과 같은 공학적 매개변수(Engineering Parameter)의 이진 스케일 값(Binary-Scaled Value)을 표현한다. 분해능(Resolution)과 범위(Range)는 모든 BNR 워드에 동일한 수치 스케일을 적용하는 것이 아니라 각 매개변수의 정의에 따라 결정된다.

이진화 십진수(Binary Coded Decimal), 즉 BCD는 ARINC 429에서 사용되는 또 다른 중요한 표현 방식이다. BCD는 이진 비트 그룹(Binary Bit Group)을 이용해 십진 숫자(Decimal Digit)를 인코딩하여 수치 정보를 구성한다. 순수 이진 인코딩(Pure Binary Encoding)보다 비트 효율(Bit Efficiency)은 낮지만, 본래 십진수로 표현되는 매개변수나 전송 값과 표시되는 십진 정보 사이의 직접적인 관계를 유지해야 하는 항공전자 장비에서 편리하게 사용할 수 있다.

일부 ARINC 429 워드는 BNR이나 BCD 수치 데이터 대신 이산 데이터(Discrete Data)를 사용한다. 개별 비트 또는 비트 그룹은 활성/비활성(Enabled/Disabled), 유효/무효(Valid/Invalid), 선택된 모드(Selected Mode), 장비 상태(Equipment Condition), 경고(Warning), 제어 상태(Control State) 등을 나타낼 수 있다. 따라서 32비트 배치만 이해하는 것으로는 충분하지 않으며 수신기는 특정 레이블 정의와 데이터 비트에 할당된 인코딩 방식을 알고 있어야 한다.

비트 30과 31은 일반적으로 SSM으로 약칭되는 부호/상태 매트릭스(Sign/Status Matrix)를 구성한다. 이 비트들의 해석은 워드에 포함된 정보의 종류에 따라 달라진다. 수치 데이터(Numerical Data)의 경우 이 비트들은 부호 정보(Sign Information)와 상태 의미(Status Semantics)를 함께 전달할 수 있으며, 다른 형식에서는 주로 동작 상태나 유효성 조건(Validity Condition)을 표시하는 데 사용할 수 있다. 따라서 SSM은 수신기가 전송 데이터의 상태를 판단할 수 있도록 추가적인 문맥 정보(Contextual Information)를 제공한다.

항공전자 시스템에서는 올바른 형식의 전기적 워드(Electrical Word)를 수신했다는 사실만으로 해당 매개변수를 신뢰할 수 있는 것은 아니기 때문에 상태 정보(Status Information)가 특히 중요하다. 장비는 초기화(Initialization), 감지된 고장(Detected Fault), 사용할 수 없는 센서 입력(Unavailable Sensor Input), 비정상 운용 조건(Abnormal Operating Condition)으로 인해 유효한 정보를 생성하지 못할 수 있다. 적절한 SSM 해석을 통해 수신 시스템은 사용 가능한 정보와 무효 또는 성능 저하 상태의 출처에서 생성된 데이터를 구분할 수 있다.

비트 32는 패리티 비트(Parity Bit)이며 전송 오류(Transmission Error)를 검출하기 위한 기본적인 메커니즘을 제공한다. ARINC 429는 일반적으로 전체 32비트 워드에 홀수 패리티(Odd Parity)를 사용한다. 송신기는 워드 전체에 포함된 논리 1(Logical One)의 총개수가 홀수가 되도록 비트 32를 설정한다. 수신기는 패리티를 독립적으로 검사하며 수신된 비트 패턴이 예상되는 패리티 조건을 만족하지 않을 경우 해당 워드를 거부하거나 오류로 표시할 수 있다.

패리티(Parity)는 간단한 오류 검출(Error Detection)을 제공하지만 포괄적인 오류 정정(Error Correction) 메커니즘은 아니다. 많은 단일 비트 오류(Single-Bit Error)를 검출할 수 있지만 어느 비트가 잘못되었는지 판단하거나 손상된 워드를 복구할 수는 없다. 또한 모든 다중 비트 오류(Multi-Bit Error)를 검출할 수도 없다. 패리티의 가치는 ARINC 429의 단순하고 결정론적인 항공전자 통신 철학에 적합한 낮은 복잡도의 무결성 검사(Integrity Check)를 제공한다는 데 있다.

직렬 전송 순서(Serial Transmission Order)는 중요한 구현 고려사항이다. ARINC 429 필드는 엔지니어가 종이에 32비트 워드를 표현하는 시각적 순서와 실제 통신 채널에서 인식되는 순서가 항상 동일하게 보이는 것은 아니다. 레이블(Label)이 먼저 전송되고 이후 워드의 나머지 부분이 정의된 비트 순서(Bit Ordering)에 따라 전송된다. 따라서 버스 분석기(Bus Analyzer)와 소프트웨어 드라이버(Software Driver)는 캡처된 데이터가 원시 직렬 시퀀스(Raw Serial Sequence)와 다르게 보이게 하는 변환을 수행하기도 한다.

고정된 워드 길이(Fixed Word Length)는 예측 가능한 타이밍(Predictable Timing)에도 기여한다. ARINC 429의 전송 속도가 알려져 있으면 32비트를 채널에 전송하는 데 필요한 시간을 직접 계산할 수 있으며 연속되는 워드 사이에는 워드 간 간격(Interword Gap)이 존재한다. 이를 통해 항공전자 설계자는 가변 길이 패킷 분석이나 복잡한 프레임 협상 없이 업데이트 주기(Update Period), 버스 사용률(Bus Utilization), 송신기 스케줄링(Transmitter Scheduling), 수신기 처리 시간을 분석할 수 있다.

현대적인 패킷 네트워크(Packet Network)와 달리 ARINC 429 워드는 일반적인 출발지 및 목적지 주소(Source and Destination Address), 패킷 길이 필드(Packet-Length Field), 프로토콜 식별자(Protocol Identifier), 대규모 오류 검사 시퀀스(Error-Checking Sequence)를 포함하지 않는다. 통신 의미의 상당 부분은 물리 채널(Physical Channel), 송신기 식별(Transmitter Identity), 레이블(Label), SDI, 사전 정의된 데이터 인코딩(Data Encoding), SSM의 조합을 통해 결정된다. 따라서 워드 구조는 간결하지만 통제된 시스템 통합(System Integration)에 크게 의존한다.

수신기 소프트웨어(Receiver Software)는 일반적으로 먼저 레이블(Label)을 식별하고 해당 매개변수가 필요한 정보인지 판단하는 것으로 처리를 시작한다. 이후 SDI를 적절하게 해석하고 예상되는 BNR, BCD 또는 이산 표현(Discrete Representation)을 사용하여 데이터 필드를 추출한 뒤 SSM과 패리티를 검사한다. 이렇게 변환된 공학적 값(Engineering Value)은 항법, 비행 제어, 디스플레이, 모니터링 또는 기타 항공전자 기능으로 전달될 수 있다.

따라서 올바른 디코딩(Decoding)을 위해서는 인터페이스 사양(Interface Specification)과 실제 구현 사이의 일치가 필요하다. 두 장치가 모두 전기적으로 ARINC 429를 지원하더라도 레이블, 스케일링(Scaling), SDI 사용 방법, 비트 할당(Bit Assignment), 업데이트 속도(Update Rate), 상태 해석(Status Interpretation)이 서로 다르면 의미 있는 정보를 교환하지 못할 수 있다. 따라서 통합 시험(Integration Testing)은 유효한 32비트 전기적 워드가 버스에 존재하는지만 확인하는 것이 아니라 의미적 호환성(Semantic Compatibility)도 검증해야 한다.

시스템 설계(System Design)의 관점에서 ARINC 429 워드 구조는 전통적인 항공전자 네트워킹(Avionics Networking)의 핵심 원칙을 보여준다. 전송 단위(Transmitted Unit)를 작고 고정적이며 결정론적으로 유지하면서 제어된 인터페이스 사양을 통해 매개변수 의미를 정의하는 방식이다. 레이블(Label), SDI, 데이터(Data), SSM, 패리티(Parity)는 단순한 직렬 비트 스트림(Serial Bit Stream)을 수신 항공전자 장비가 식별하고 해석하며 상태를 판단하고 오류를 검사할 수 있는 정보로 변환한다.

이러한 워드 구성(Word Organization)은 이후 다루어지는 ARINC 429 레이블 할당(Label Allocation), 버스 아키텍처(Bus Architecture), UAV 항공전자 통합(UAV Avionics Integration)을 이해하기 위한 논리적 기반을 형성한다. 물리 계층(Physical Layer)이 전용 차동 채널(Dedicated Differential Channel)을 통해 전기적 비트가 이동하는 방식을 결정한다면, 32비트 워드 구조(32-Bit Word Structure)는 상위 수준의 시스템 통합이 이루어지기 전에 이러한 비트들이 어떻게 의미 있는 항공전자 정보로 변환되는지를 결정한다.

## 07.03. ARINC 429 Label Allocation

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

ARINC 429 레이블 할당(Label Allocation)은 수신 항공전자 장비(Receiving Avionics Equipment)가 전송된 각각의 32비트 워드(32-Bit Word)의 의미를 판단할 수 있도록 하는 식별 메커니즘(Identification Mechanism)을 제공한다. 레이블(Label)은 비트 1\~8을 차지하며 기본적인 매개변수 식별자(Parameter Identifier) 역할을 한다. 매번 설명적인 이름을 전송하는 대신 항공전자 시스템은 사전에 정의된 숫자 레이블을 사용하여 간결한 이진 패턴(Binary Pattern)을 특정 항공기 정보 범주와 연결한다.

레이블(Label)은 8비트 필드(8-Bit Field)를 편리하게 표현할 수 있기 때문에 일반적으로 세 자리 8진수(Three-Digit Octal Number)로 나타낸다. 사용 가능한 레이블 공간(Label Space)은 8진수 000에서 377까지이며, 이는 256개의 가능한 8비트 조합에 해당한다. 따라서 엔지니어는 송신기와 수신기 내부에서 사용되는 전체 이진 표현(Binary Representation)을 기록하는 대신 일반적으로 ARINC 429 매개변수를 8진수 레이블(Octal Label)로 지칭한다.

레이블(Label)은 단순히 일반적인 데이터 형식만을 식별하는 것이 아니다. 레이블의 해석은 항공전자 장비(Avionics Equipment)와 관련 인터페이스 사양(Interface Specification)의 문맥에서 결정된다. 수신 장치는 레이블을 사용하여 해당 워드가 필요한 정보인지 판단한 다음 적절한 디코딩 규칙(Decoding Rule)을 적용한다. 이 규칙은 데이터 필드(Data Field), SDI 비트, SSM 비트, 스케일링(Scaling), 분해능(Resolution), 유효성 정보(Validity Information)를 해석하는 방법을 결정한다.

따라서 레이블 할당(Label Allocation)은 독립적으로 개발된 항공전자 장치 사이에 논리적 인터페이스(Logical Interface)를 형성한다. 항법 컴퓨터(Navigation Computer), 대기자료 시스템(Air-Data System), 비행 제어 컴퓨터(Flight-Control Computer), 디스플레이 장치(Display Unit) 등의 하위 시스템은 양쪽 장치가 각 레이블에 연결된 의미 정의(Semantic Definition)에 동의할 때만 정보를 안정적으로 교환할 수 있다. 전기적으로 유효한 ARINC 429 워드라도 레이블 정의가 다르면 잘못 해석될 수 있으므로 전기적 호환성만으로 상호운용성(Interoperability)을 보장할 수 없다.

비트 9와 10에 위치하는 출처/목적지 식별자(Source/Destination Identifier), 즉 SDI는 레이블(Label)이 제공하는 식별 기능을 확장할 수 있다. 여러 출처가 동일한 종류의 정보를 생성하는 경우 SDI를 이용해 출처를 구분할 수 있다. 다른 응용에서는 목적지(Destination) 또는 설치별 해석(Installation-Specific Interpretation)을 나타낼 수 있다. 따라서 전송 정보의 실질적인 식별은 레이블, SDI, 물리 채널(Physical Channel), 송신 장비(Transmitting Equipment)의 조합에 의해 결정될 수 있다.

이러한 관계는 동일한 항공기 내부에 유사한 센서나 이중화 항공전자 채널(Redundant Avionics Channel)이 존재할 때 특히 유용하다. 여러 항법 정보원(Navigation Source), 대기자료 정보원(Air-Data Source), 관성 시스템(Inertial System) 또는 기타 이중화 장치는 서로 관련된 매개변수를 제공할 수 있다. 수신 시스템은 매개변수가 무엇을 의미하는지뿐 아니라 어느 출처에서 생성되었는지도 알아야 하며, 레이블과 SDI 해석을 통해 간결한 32비트 워드 구조를 유지하면서 이러한 구분을 지원할 수 있다.

레이블 할당(Label Allocation)은 데이터 인코딩(Data Encoding)과도 밀접하게 연결된다. 수신기는 레이블을 인식한 후 관련 정보가 이진수 표현(Binary Number Representation), 이진화 십진수(Binary Coded Decimal), 이산 상태(Discrete State) 또는 다른 정의된 표현을 사용하는지 결정한다. 따라서 레이블은 단순히 워드에 붙어 있는 숫자 이름이 아니라 해당 데이터의 디코딩 정의(Decoding Definition)로 진입하는 기준 역할을 한다.

BNR 매개변수(BNR Parameter)의 경우 레이블 정의에는 수치 범위(Numerical Range), 스케일링(Scaling), 분해능(Resolution), 공학 단위(Engineering Unit) 등의 정보가 연결되어야 한다. 데이터 필드의 동일한 이진 패턴도 서로 다른 정의에 따라 해석하면 완전히 다른 물리량을 나타낼 수 있다. 올바른 레이블 할당은 수신기가 전송된 이진 값을 의도된 고도(Altitude), 속도(Velocity), 각도(Angle), 위치(Position) 또는 기타 공학적 매개변수로 변환하도록 한다.

BCD 기반 레이블(BCD-Oriented Label) 역시 십진 숫자(Decimal Digit)와 각 자릿수 위치에 대한 합의된 해석이 필요하다. 이산 레이블(Discrete Label)은 개별 상태 또는 제어 비트(Control Bit)에 대한 정의를 필요로 한다. 특정 비트는 사용 가능 여부(Availability), 선택 상태(Selection), 작동 상태(Engagement), 경고(Warning) 또는 다른 장비 상태를 나타낼 수 있다. 따라서 인터페이스 문서(Interface Documentation)는 어떤 레이블을 전송하는지만이 아니라 해당 레이블과 연결된 비트들의 상세한 의미도 정의해야 한다.

부호/상태 매트릭스(Sign/Status Matrix), 즉 SSM 역시 레이블과 연결된 데이터 유형(Data Type)에 따라 해석해야 한다. 비트 30과 31은 부호(Sign) 또는 운용 상태(Operating Status) 정보를 전달할 수 있지만 정확한 의미는 해당 워드 정의에 따라 결정된다. 따라서 레이블 할당은 수신기가 SSM을 어떻게 해석하고 수신된 매개변수를 정상(Normal), 무효(Invalid), 성능 저하(Degraded) 또는 기타 상태로 판단하는지에도 간접적으로 영향을 준다.

구현 과정에서 특히 주의해야 하는 사항은 ARINC 429 레이블 비트 순서(Label Bit Ordering)이다. 레이블은 엔지니어링 편의를 위해 일반적으로 8진수로 작성하지만, 레이블 비트에는 일반적인 이진 표기법(Binary Notation)과 비교할 때 반대로 보일 수 있는 정의된 직렬 전송 동작(Serial Transmission Behavior)이 존재한다. 버스 분석기(Bus Analyzer)와 인터페이스 장치는 레이블을 디코딩된 8진수 형태로 표시할 수 있지만 저수준 캡처(Low-Level Capture)에서는 실제 전송된 비트 시퀀스가 나타날 수 있다.

이러한 차이는 소프트웨어 개발자가 ARINC 429 워드를 직접 구성하거나 디코딩할 때 통합 오류(Integration Error)를 발생시킬 수 있다. 인터페이스 제어 문서(Interface Control Document)에 올바르게 표시된 레이블도 잘못된 비트 순서 규칙을 사용하여 송신 레지스터(Transmit Register)에 입력하면 예상하지 못한 값으로 전송될 수 있다. 따라서 소프트웨어가 원시 ARINC 429 워드(Raw ARINC 429 Word)를 직접 처리하는 경우 드라이버 문서(Driver Documentation)와 하드웨어 동작을 주의 깊게 확인해야 한다.

레이블 할당(Label Allocation)은 수신기 필터링(Receiver Filtering)에도 영향을 준다. 항공전자 장치는 일반적으로 입력 채널에 나타나는 모든 워드가 아니라 필요한 일부 워드만 사용한다. 하드웨어 또는 소프트웨어는 입력되는 레이블을 검사하고 수신 기능에 필요한 매개변수만 유지할 수 있다. 이러한 필터링은 불필요한 처리를 줄이고 입력 통신과 항법, 제어, 모니터링 또는 디스플레이 기능에서 사용하는 내부 애플리케이션 변수(Application Variable) 사이의 직접적인 매핑을 제공한다.

송신기(Transmitter)는 관련 정보가 얼마나 빠르게 변화하고 수신기가 얼마나 자주 갱신을 요구하는지에 따라 서로 다른 레이블을 서로 다른 반복률(Repetition Rate)로 전송하는 경우가 많다. 레이블 자체에는 업데이트 주기(Update Period)가 인코딩되지 않지만 인터페이스 정의는 각 매개변수에 예상되는 전송 동작을 연결한다. 따라서 레이블 관리는 버스 스케줄링(Bus Scheduling), 대역폭 사용률(Bandwidth Utilization), 지연시간 요구사항(Latency Requirement), 수신 장비의 데이터 최신성 감시(Freshness Monitoring)와 연결된다.

수신기는 예상되는 레이블 반복(Label Repetition)을 이용하여 통신 이상(Communication Abnormality)을 검출할 수 있다. 필요한 레이블이 규정된 업데이트 간격(Update Interval) 안에 도착하지 않으면 마지막으로 수신한 워드가 유효한 데이터를 포함하고 있더라도 관련 매개변수를 오래된 데이터(Stale Data) 또는 사용 불가능한 정보로 판단할 수 있다. 따라서 신뢰성 있는 항공전자 통합은 레이블의 의미뿐 아니라 해당 레이블 정보에 할당된 시간적 동작(Temporal Behavior)에도 의존한다.

항공기 통합(Aircraft Integration)에서는 서로 다른 항공전자 공급업체가 장비를 독립적으로 개발할 수 있기 때문에 레이블 정의에 대한 엄격한 관리가 필요하다. 따라서 일반적으로 ICD라고 하는 인터페이스 제어 문서(Interface Control Document)는 어떤 레이블을 송수신하는지, SDI를 어떻게 사용하는지, 데이터 비트를 어떻게 인코딩하는지, 어떤 공학 단위와 스케일링을 적용하는지, SSM을 어떻게 해석하는지, 어떤 업데이트 속도(Update Rate)를 사용하는지를 정의하는 핵심 문서가 된다.

통합 시험(Integration Testing) 과정에서 엔지니어는 실제 전송되는 레이블이 이러한 인터페이스 정의와 일치하는지 검증한다. 버스 모니터링 장비(Bus Monitoring Equipment)는 ARINC 429 트래픽을 캡처하고 레이블과 함께 데이터, SDI, SSM, 패리티(Parity), 타이밍 정보를 표시할 수 있다. 관찰된 트래픽을 의도된 인터페이스 사양과 비교하면 잘못된 레이블 할당, 비트 순서 문제, 스케일링 불일치, 누락된 매개변수, 비정상 반복률, 잘못된 상태 조건을 식별하는 데 도움이 된다.

레이블 할당(Label Allocation)은 복잡한 항공전자 시스템에서 아키텍처 분리(Architectural Separation)도 지원한다. 각각의 전용 ARINC 429 채널에는 알려진 송신기가 존재하고 해당 채널의 워드에는 관리되는 레이블이 할당되므로 물리적 연결성(Physical Connectivity)과 논리적 식별(Logical Identification)의 조합을 통해 매우 명확한 정보 흐름(Information Flow)을 구성할 수 있다. 엔지니어는 매개변수가 생성되는 항공전자 장치에서 정의된 채널과 레이블을 거쳐 해당 정보를 사용하는 각각의 수신 기능까지 추적할 수 있다.

이러한 방식은 현대적인 자기 기술형 네트워크 프로토콜(Self-Describing Network Protocol)과 상당히 다르다. ARINC 429 워드는 텍스트 형태의 매개변수 설명이나 수신기가 의미를 동적으로 발견할 수 있도록 하는 풍부한 스키마(Rich Schema)를 포함하지 않는다. 의미는 운용 전에 통제된 공학적 정의(Engineering Definition)를 통해 설정된다. 결과적으로 통신 형식은 작고 결정론적으로 유지되지만 구성 관리(Configuration Management)와 인터페이스 문서가 시스템 정확성(System Correctness)의 중요한 요소가 된다.

UAV 및 기타 현대적인 항공전자 아키텍처(Modern Avionics Architecture)에서도 ARINC 429를 기존 또는 인증된 하위 시스템(Legacy or Certified Subsystem)과 최신 컴퓨팅 플랫폼 사이의 통합에 사용할 경우 동일한 원칙이 중요하다. 게이트웨이(Gateway) 또는 비행 컴퓨터(Flight Computer)는 ARINC 429와 내부 소프트웨어 인터페이스 또는 최신 네트워크 사이에서 정보를 변환하면서 레이블의 의미를 보존해야 한다. 잘못된 매핑(Mapping)은 전기적 데이터를 그대로 유지하면서도 시스템 수준의 의미를 손상시킬 수 있다.

따라서 ARINC 429 레이블 할당(Label Allocation)은 고정된 32비트 워드 구조와 더 큰 항공전자 아키텍처 사이의 의미적 연결고리(Semantic Bridge)를 제공한다. 레이블은 매개변수 계열(Parameter Family)을 식별하고, SDI, 데이터(Data), SSM, 물리 채널 식별(Physical Channel Identity), 인코딩 규칙(Encoding Rule), 타이밍이 그 해석을 완성한다. 이러한 통제된 정의를 결합함으로써 단순한 직렬 워드가 독립적으로 구현된 항공전자 장비 사이에서 신뢰할 수 있는 항공기 정보를 표현할 수 있다.

첨부된 볼륨 구조(Volume Structure)에서 이 주제는 ARINC 429 물리 계층(Physical Layer)과 워드 구조(Word Structure) 다음에 위치하며 버스 아키텍처(Bus Architecture)와 UAV 항공전자 통합(UAV Avionics Integration)에 앞선다. 이러한 순서는 전기 신호의 전송에서 시작하여 이를 32비트 워드로 구성하고, 레이블을 통해 의미를 부여한 다음, 최종적으로 여러 항공전자 기능을 하나의 완전한 통신 아키텍처로 연결하는 자연스러운 발전 과정을 반영한다.

## 07.04. ARINC 429 Bus Architecture

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

ARINC 429 버스 아키텍처(Bus Architecture)는 하나의 항공전자 송신기(Avionics Transmitter)가 전용 채널(Dedicated Channel)을 통해 하나 이상의 수신기(Receiver)로 데이터를 전송하는 단순한 단방향 통신 모델(Unidirectional Communication Model)을 기반으로 한다. 여러 송신기가 경쟁하는 공유형 다중점 버스(Shared Multidrop Bus)와 달리 하나의 ARINC 429 채널에는 하나의 능동 송신기(Active Transmitter)만 허용된다. 이러한 기본적인 제약은 버스 중재(Bus Arbitration)를 제거하고 항공전자 응용에서 매우 예측 가능한 통신 동작을 제공한다.

각 ARINC 429 통신 채널(Communication Channel)은 물리 계층(Physical Layer)에서 정의된 차동 전기 신호(Differential Electrical Signaling)를 전달하는 전용 연선(Dedicated Twisted Pair)을 사용한다. 송신기(Transmitter)는 요구되는 업데이트 속도(Update Rate)에 따라 32비트 ARINC 워드(32-Bit ARINC Word)를 이 연선에 연속적 또는 주기적으로 전송한다. 연결된 수신기는 동일한 전송 정보를 감시하지만 해당 채널에서 응답을 전송하지 않으므로 아키텍처의 단방향 특성(Simplex Nature)이 유지된다.

하나의 송신기(Transmitter)는 일반적으로 여러 수신기(Receiver)에 정보를 배포하여 일대다 통신 관계(One-to-Many Communication Relationship)를 형성할 수 있다. 이러한 기능은 여러 항공전자 기능이 동일한 센서 또는 하위 시스템 데이터를 필요로 할 때 유용하다. 예를 들어 항법 시스템(Navigation System)이나 대기자료 시스템(Air-Data System)이 생성한 정보는 각각의 수신기가 독립적인 통신 세션을 구성하지 않아도 비행 제어, 디스플레이, 모니터링 및 기록 장비에서 동시에 사용할 수 있다.

여러 수신기가 하나의 송신기를 청취할 수 있지만 여러 송신기가 동일한 ARINC 429 연선(Pair)을 능동적인 신호원으로 공유할 수는 없다. 여러 항공전자 장치가 정보를 송신해야 하는 경우 각각의 송신원(Transmitting Source)은 일반적으로 자체 출력 채널(Output Channel)을 필요로 한다. 따라서 복잡한 항공기에는 많은 수의 독립적인 ARINC 429 링크(Link)가 존재할 수 있다. 배선은 증가하지만 통신 채널의 소유권과 정보의 출처는 물리적으로 명확하게 유지된다.

두 항공전자 장치 사이에서 양방향 통신(Bidirectional Communication)을 수행하려면 두 개의 독립적인 단방향 채널(Simplex Channel)이 필요하다. 하나의 연선은 장치 A에서 장치 B로 데이터를 전달하고 다른 연선은 장치 B에서 장치 A로 정보를 전달한다. 각각의 ARINC 429 통신 방향은 자체적인 전기적 연결, 워드 스케줄링(Word Scheduling), 레이블(Label), 수신기 동작을 가진 독립적인 송신 채널로 정의된다는 점에서 일반적인 전이중 네트워크 인터페이스(Full-Duplex Network Interface)와 차이가 있다.

중재(Arbitration)가 존재하지 않는 것은 ARINC 429의 가장 중요한 아키텍처 특성 중 하나이다. 각 채널은 하나의 송신기만 제어하기 때문에 장치들이 통신 매체(Communication Medium)에 접근하기 위해 경쟁하지 않는다. 충돌(Collision), 경합 윈도(Contention Window), 토큰 메커니즘(Token Mechanism), 동적 우선순위(Dynamic Priority)가 필요하지 않다. 따라서 채널의 타이밍 동작은 주로 송신기에 설정된 워드 시퀀스(Word Sequence), 반복률(Repetition Rate), 데이터 속도(Data Rate), 워드 간 간격(Interword Spacing)에 의해 결정된다.

정보 다중화(Information Multiplexing)는 여러 송신기가 물리적 매체를 공유하는 방식이 아니라 ARINC 429 레이블(Label)을 통해 이루어진다. 하나의 송신기는 서로 다른 레이블을 가진 워드를 전송하여 하나의 출력 연선에서 여러 매개변수를 반복적으로 전달할 수 있다. 수신기는 입력되는 각각의 32비트 워드에서 레이블을 검사하고 자신의 기능과 관련된 매개변수만 처리한다. 따라서 하나의 물리 채널(Physical Channel)을 통해 여러 논리적 정보 흐름(Logical Information Flow)을 전달할 수 있다.

전송 스케줄(Transmission Schedule)은 서로 다른 레이블의 업데이트 요구사항(Update Requirement)을 고려해야 한다. 빠르게 변화하거나 제어에 중요한 매개변수는 빈번한 전송이 필요할 수 있으며 천천히 변화하는 정보는 상대적으로 낮은 빈도로 전송할 수 있다. 사용 가능한 채널 대역폭(Channel Bandwidth)은 제한되어 있으므로 항공전자 설계자는 필요한 매개변수가 충분히 최신 상태를 유지하면서 송신기의 통신 용량을 초과하지 않도록 워드 반복률을 조정해야 한다.

따라서 수신기 필터링(Receiver Filtering)은 버스 통합(Bus Integration)의 중요한 요소이다. 수신 항공전자 장치는 연결된 채널에서 전송되는 모든 워드를 물리적으로 관찰할 수 있지만 정의된 일부 레이블만 받아들일 수 있다. 하드웨어 인터페이스(Hardware Interface), 장치 드라이버(Device Driver), 애플리케이션 소프트웨어(Application Software)가 이러한 필터링을 수행할 수 있다. 선택된 워드는 레이블(Label), SDI, 데이터(Data), SSM, 패리티(Parity) 정의에 따라 디코딩된 후 해당 정보를 사용하는 기능으로 전달된다.

물리 채널(Physical Channel) 자체도 출처 식별(Source Identification)에 기여한다. 특정 ARINC 429 입력은 알려진 송신기의 출력에 배선되어 있기 때문에 수신 시스템은 도착한 정보의 출처에 대한 아키텍처 수준의 정보를 이미 가지고 있다. 레이블(Label)과 SDI는 추가적인 논리적 식별(Logical Identification)을 제공한다. 이러한 고정 배선과 통제된 워드 정의의 조합은 설계, 검증 및 고장 분석 과정에서 데이터 출처(Data Provenance)를 비교적 명확하게 추적할 수 있게 한다.

이중화(Redundancy)는 이중화된 항공전자 정보원(Redundant Avionics Source)으로부터 독립적인 채널을 제공하는 방식으로 구현할 수 있다. 예를 들어 기능적으로 유사한 두 개의 센서 또는 컴퓨터가 각각 별도의 ARINC 429 출력을 수신 시스템에 연결할 수 있다. 수신기는 시스템 요구사항에 따라 이러한 정보원을 선택, 비교 또는 감시할 수 있다. 물리적 채널 분리(Physical Channel Separation)는 하나의 정보원 경로에서 발생한 통신 고장이 다른 독립 경로를 직접 손상시키는 것을 방지하는 데 도움이 된다.

그러나 이러한 이중화가 정보원 선택(Source Selection) 방법을 자동으로 결정하는 것은 아니다. 수신 애플리케이션은 채널 식별(Channel Identity), SDI, SSM, 데이터 유효성(Data Validity), 최신성(Freshness), 장비 상태(Equipment Health)와 함께 시스템 수준 로직(System-Level Logic)을 사용해야 한다. ARINC 429는 통신 경로와 상태 메커니즘을 제공하고 항공전자 아키텍처는 이중화 정보를 비교하고 정상 또는 성능 저하 운용 조건에서 어떤 정보원을 사용할 것인지 결정한다.

ARINC 429 장비가 다른 통신 기술을 사용하는 시스템과 정보를 교환해야 할 경우 게이트웨이(Gateway)가 중요해진다. 게이트웨이는 ARINC 429 워드를 수신하고 레이블과 데이터 정의를 해석하여 다른 네트워크 또는 소프트웨어 표현(Software Representation)으로 매핑한다. 반대 방향에서는 다른 시스템으로부터 정보를 받아 올바른 형식의 ARINC 429 워드를 구성하고 전용 출력 채널을 통해 전송할 수 있다.

게이트웨이 설계(Gateway Design)는 원시 비트(Raw Bit)를 단순히 복사하는 것이 아니라 의미(Semantics)를 보존해야 한다. 레이블 정의, SDI 사용 방법, 수치 스케일링(Numerical Scaling), 공학 단위(Engineering Unit), SSM 해석, 업데이트 속도, 패리티, 정보원 식별(Source Identity)을 적절하게 매핑해야 한다. ARINC 429와 다른 항공전자 통신 아키텍처 사이에서 변환할 때 매개변수의 의미나 타이밍이 변경되면 전기적으로 올바른 변환이라도 기능적으로 잘못될 수 있다.

고장 격리(Fault Containment)는 전용 채널 아키텍처(Dedicated-Channel Architecture)의 주요 장점이다. 고장 난 수신기는 일반적으로 해당 연선에서 허가된 송신기가 아니므로 채널을 장악할 수 없다. 마찬가지로 송신기 고장은 공유형 다중 마스터 통신 매체(Shared Multi-Master Communication Medium) 전체가 아니라 주로 해당 송신기가 구동하는 채널과 관련된다. 이러한 물리적 분리는 통신 고장의 전파(Failure Propagation)를 비교적 쉽게 분석할 수 있도록 한다.

그러나 전용 배선(Dedicated Wiring)은 아키텍처 비용도 증가시킨다. 항공전자 장치와 교환되는 신호가 증가하면 송신기 출력, 수신기 입력, 연선, 커넥터 접점(Connector Contact), 하네스 경로(Harness Route)의 수가 상당히 증가할 수 있다. 이에 따라 항공기 중량(Aircraft Weight), 설치 복잡도(Installation Complexity), 유지보수 작업(Maintenance Effort), 인터페이스 하드웨어 요구사항이 증가하며, 이것이 최신 항공기 아키텍처에서 대규모 데이터 교환에 고대역폭 스위치드 네트워크(High-Bandwidth Switched Network)를 사용하는 이유 중 하나이다.

그럼에도 ARINC 429는 네트워크 효율성(Network Efficiency)보다 적당한 대역폭(Moderate Bandwidth), 예측 가능한 통신, 명확한 인증 근거(Certification Evidence), 기존 항공전자 장비와의 호환성이 중요한 환경에서 여전히 유용하다. 특히 알려진 종단점(Known Endpoint) 사이에서 비교적 작은 규모의 매개변수를 교환하는 데 적합하다. 물리적 토폴로지 자체가 통신 관계의 상당 부분을 나타내므로 동적 네트워크 검색(Dynamic Network Discovery)이나 복잡한 실행시간 구성(Runtime Configuration)에 대한 의존성을 줄일 수 있다.

통합 엔지니어링(Integration Engineering)은 일반적으로 채널 수준 인터페이스 정의(Channel-Level Interface Definition)를 작성하는 것에서 시작한다. 엔지니어는 각각의 송신기, 물리적 ARINC 429 출력, 연결된 수신기, 전송 레이블, 예상 반복률, 데이터 인코딩(Data Encoding), SDI 사용 방법, SSM 동작, 전기적 속도(Electrical Speed)를 정의한다. 이러한 정보는 일반적으로 인터페이스 문서를 통해 관리되어 배선 설계, 소프트웨어 구성, 검증 및 장비 통합이 동일한 통신 정의를 공유하도록 한다.

버스 시험(Bus Testing)에서는 물리적 연결성과 논리적 동작을 모두 검증한다. 엔지니어는 ARINC 429 분석기(ARINC 429 Analyzer)를 이용하여 개별 채널을 감시하고 예상되는 레이블, 워드 값, 패리티, 상태, 반복 간격(Repetition Interval), 신호 품질(Signal Quality)을 확인할 수 있다. 누락된 레이블은 송신기 설정 또는 배선 문제를 의미할 수 있으며 예상하지 못한 값은 전기적 고장보다 잘못된 스케일링, 정보원 선택, SDI 해석 또는 인터페이스 매핑에서 발생할 수 있다.

시스템 관점(System Perspective)에서 ARINC 429는 하나의 공유형 항공기 전체 버스(Aircraft-Wide Bus)가 아니라 통제된 단방향 정보 채널(Simplex Information Channel)의 집합으로 이해할 수 있다. 각각의 송신기는 하나 이상의 전용 데이터 경로(Dedicated Data Path)를 구성하고 각 경로는 사전에 정의된 레이블 정보를 선택된 수신기에 배포한다. 더 큰 항공전자 아키텍처는 장비와 게이트웨이를 통해 이러한 개별적이고 단순한 통신 관계를 다수 연결함으로써 구성된다.

UAV 항공전자 시스템(UAV Avionics)에서 이러한 아키텍처는 ARINC 429 인터페이스를 제공하는 인증된 센서(Certified Sensor), 항법 장비(Navigation Equipment), 대기자료 시스템, 임무 장비(Mission Equipment) 또는 기타 항공우주 하위 시스템과 연결하기 위한 실용적인 인터페이스가 될 수 있다. 최신 비행 컴퓨터(Flight Computer)는 내부적으로 더 빠른 컴퓨팅 및 네트워크 기술을 사용하면서 여러 ARINC 429 송수신 채널을 제공하여 기존 항공우주 인터페이스와 최신 항공전자 처리 아키텍처가 공존하도록 할 수 있다.

따라서 주요 설계 절충(Design Trade-Off)은 명확하다. ARINC 429는 배선 및 대역폭 효율성을 희생하는 대신 단순성(Simplicity), 결정론(Determinism), 정보원 격리(Source Isolation), 분석 가능한 정보 흐름(Analyzable Information Flow)을 얻는다. 전용 송신기, 단방향 채널, 수신기 팬아웃(Receiver Fan-Out), 레이블 기반 다중화(Label-Based Multiplexing), 통제된 업데이트 속도, 독립적인 이중화 경로가 결합되어 물리적 배선과 사전 정의된 인터페이스를 통해 동작을 명확하게 이해할 수 있는 아키텍처를 형성한다.

첨부된 장 구조(Chapter Structure)에서 ARINC 429 버스 아키텍처(Bus Architecture)는 물리 계층(Physical Layer), 32비트 워드 구조(32-Bit Word Structure), 레이블 할당(Label Allocation) 다음에 위치하며 ARINC 429의 UAV 항공전자 통합(UAV Avionics Integration)에 앞선다. 이러한 진행 과정은 전기적 신호 전달, 데이터 구성, 의미적 식별(Semantic Identification), 시스템 토폴로지(System Topology)를 연결한 후 이러한 요소들이 완전한 UAV 항공전자 시스템에 어떻게 통합되는지를 살펴보는 구조를 형성한다.

## 07.05. ARINC 429 in UAV Avionics

ARINC 429는 비교적 낮은 대역폭의 결정론적 매개변수 데이터(Deterministic Parameter Data)를 교환해야 하는 비행 핵심 장비(Flight-Critical Equipment) 또는 항공우주 인증 장비(Aerospace-Qualified Equipment)를 연결해야 할 때 무인항공기(UAV)의 항공전자 인터페이스(Avionics Interface)로 실용적으로 사용할 수 있다. UAV에서는 비행 컴퓨터(Flight Computer), 항법 장비(Navigation Equipment), 대기자료 시스템(Air-Data System), 센서(Sensor), 임무 컴퓨터(Mission Computer), 특수 탑재 장비(Specialized Payload Equipment) 등을 연결하면서 기존 항공기의 단순하고 결정론적인 통신 원칙을 유지할 수 있다.

기본적인 UAV 구현에서도 ARINC 429의 단방향 통신 구조(Simplex Architecture)는 그대로 유지된다. 하나의 송신기(Transmitter)가 전용 차동 연선(Dedicated Differential Twisted Pair)을 통해 하나 이상의 수신기로 32비트 워드를 전송한다. 따라서 UAV의 비행 컴퓨터(Flight Computer)는 여러 개의 독립적인 송수신 채널(Transmit and Receive Channel)을 가질 수 있으며, 각각의 물리 채널(Physical Channel)은 특정 장비 간 통신 관계에 할당된다. 양방향 정보 교환에는 양쪽 통신 방향을 위한 별도의 채널이 필요하다.

항법(Navigation)은 UAV에서 ARINC 429를 적용하기에 자연스러운 영역이다. UAV의 유도(Guidance)는 지속적으로 갱신되는 위치(Position), 속도(Velocity), 고도(Altitude), 방위(Heading) 및 관련 상태 정보를 필요로 한다. ARINC 429 출력을 제공하는 항공우주 항법 장비(Aerospace Navigation Equipment)는 사전에 정의된 레이블(Label)을 통해 이러한 매개변수를 비행 제어 컴퓨터(Flight-Control Computer)에 제공할 수 있다. 수신 컴퓨터는 해당 정보를 항법 기능에 사용하기 전에 각 워드를 Label, SDI, Data, SSM, Parity 정의에 따라 디코딩한다.

대기자료(Air-Data) 정보도 유사한 방식으로 통합할 수 있다. 고도(Altitude), 대기속도(Airspeed), 압력(Pressure), 온도(Temperature) 및 기타 비행 조건과 관련된 측정값이나 계산된 매개변수는 적절한 항공전자 장비에서 비행 제어 시스템으로 전송될 수 있다. 결정론적인 레이블 기반 인터페이스(Label-Based Interface)를 사용하면 수신 소프트웨어가 각각의 입력 매개변수를 정의된 공학적 값(Engineering Quantity), 스케일링 규칙(Scaling Convention), 유효성 상태(Validity State), 예상 업데이트 동작(Update Behavior)과 연결할 수 있다.

ARINC 429는 이러한 장치가 호환 가능한 항공우주 인터페이스를 제공하는 경우 임무 및 탑재체 하위 시스템(Mission and Payload Subsystem)도 연결할 수 있다. 예를 들어 화물 UAV(Cargo UAV)는 중앙 항공전자 컴퓨터(Central Avionics Computer)와 상태 정보 또는 명령을 교환해야 하는 임무 장비를 포함할 수 있다. 비교적 단순한 워드 구조(Simple Word Structure)는 이산 상태(Discrete State), 수치 측정값(Numerical Measurement), 장비 상태(Equipment Condition), 운용 모드(Operating Mode) 및 높은 대역폭을 필요로 하지 않는 기타 간결한 정보를 전달하는 데 적합하다.

반면 ARINC 429는 고해상도 카메라(High-Resolution Camera), 영상 레이더(Imaging Radar), 대규모 3차원 센싱 스트림(Three-Dimensional Sensing Stream)과 같은 높은 대역폭의 UAV 센서에는 적합하지 않다. 이러한 정보는 일반적으로 더 빠른 네트워크 기술을 필요로 한다. 따라서 ARINC 429는 특히 최신 인지(Perception), 자율성(Autonomy), 임무 컴퓨팅(Mission Computing) 시스템이 포함되는 경우 UAV의 유일한 온보드 네트워크(Onboard Network)가 아니라 이기종 통신 아키텍처(Heterogeneous Communication Architecture)의 한 구성요소로 이해하는 것이 적절하다.

실제 UAV는 ARINC 429와 함께 이더넷 기반 네트워크(Ethernet-Based Network) 및 기타 임베디드 통신 인터페이스(Embedded Communication Interface)를 결합할 수 있다. ARINC 429는 기존 항공전자 매개변수 교환(Avionics Parameter Exchange)을 담당하고, 고대역폭 네트워크는 영상, 지도, 인지 결과, 임무 데이터베이스, 진단 정보(Diagnostic Data), 자율 시스템 관련 데이터를 전달할 수 있다. 이러한 역할 분담은 각 통신 기술이 전기적 특성, 타이밍, 대역폭 및 통합 요구사항에 따라 적절하게 사용되도록 한다.

게이트웨이(Gateway)는 이러한 서로 다른 통신 영역 사이의 연결을 제공한다. ARINC 429 인터페이스를 갖춘 게이트웨이 또는 비행 컴퓨터는 레이블이 부여된 워드를 수신하고 그 내용을 내부 소프트웨어 메시지(Software Message) 또는 다른 네트워크 표현(Network Representation)으로 변환한다. 반대 방향에서는 UAV 내부 정보를 올바르게 구성된 ARINC 429 워드로 변환하여 기존 항공우주 인터페이스를 요구하는 장비에 전송할 수 있다.

게이트웨이가 올바르게 동작하려면 단순한 비트 전달(Bit Forwarding)이 아니라 의미적 매핑(Semantic Mapping)이 필요하다. 게이트웨이는 레이블의 의미, SDI 해석, BNR 또는 BCD 스케일링, 이산 비트 정의(Discrete Bit Definition), SSM 상태, 패리티 동작, 정보원 식별(Source Identity), 업데이트 타이밍(Update Timing)을 보존해야 한다. 매개변수를 다른 통신 시스템으로 변환할 때 공학적 의미와 유효성 조건이 양쪽 인터페이스에서 일관되게 유지되어야 한다.

이중화 UAV 항공전자 시스템(Redundant UAV Avionics)은 ARINC 429의 물리적으로 분리된 채널(Physically Separated Channel)을 활용할 수 있다. 두 개의 항법 장치(Navigation Unit), 센서 또는 컴퓨터가 비행 제어 시스템에 독립적인 출력을 제공할 수 있다. 수신기는 시스템 수준의 이중화 로직(Redundancy Logic)에 따라 이러한 정보원을 비교하거나 선택할 수 있다. 하나의 송신기 채널에 고장이 발생하더라도 각 ARINC 429 링크에는 전용 송신원이 존재하기 때문에 다른 채널에서 통신 경합이 발생하지 않는다.

그러나 정보원 선택(Source Selection)은 물리적인 통신 메커니즘만으로 결정되지 않는다. 비행 제어 시스템은 정보를 수용하기 전에 물리 채널 식별, SDI, SSM, 매개변수의 타당성(Plausibility), 업데이트 최신성(Update Freshness), 장비 상태(Equipment Health)를 고려할 수 있다. ARINC 429는 예측 가능한 통신과 상태 정보를 제공하지만, 비정상 운용 조건에서 서로 충돌하거나 성능이 저하된 이중화 정보원을 어떻게 처리할지는 UAV 아키텍처가 정의해야 한다.

부호/상태 매트릭스(Sign/Status Matrix)는 외부에서 공급되는 항공전자 데이터에 비행 제어 기능이 의존하는 경우 특히 중요하다. 올바른 형식의 워드를 수신했다고 해서 그 내부의 실제 측정값이 반드시 유효한 것은 아니다. 장비가 초기화 중이거나 사용할 수 없거나 성능이 저하되었거나 고장을 보고하고 있을 수 있다. 따라서 비행 소프트웨어는 수신된 모든 매개변수를 즉시 사용할 수 있는 것으로 간주하기보다는 실제 데이터 값과 상태 정보를 함께 해석해야 한다.

데이터 최신성(Data Freshness) 역시 중요하다. 각각의 필수 레이블은 레이블 자체에 업데이트 주기가 직접 인코딩되어 있지는 않더라도 일반적으로 예상되는 반복 동작(Repetition Behavior)을 가진다. UAV 소프트웨어는 중요한 워드의 수신 시간을 감시하고 업데이트가 중단되거나 허용된 간격을 초과하면 해당 매개변수를 오래된 데이터(Stale Data)로 판단할 수 있다. 이를 통해 마지막으로 수신된 워드가 전기적으로 유효하더라도 더 이상 최신이 아닌 값을 계속 사용하는 것을 방지할 수 있다.

고정된 32비트 워드(Fixed 32-Bit Word)와 통제된 반복 동작은 ARINC 429 통신을 비교적 쉽게 분석할 수 있도록 한다. 설계자는 선택된 전송 속도(Transmission Speed), 전송되는 레이블의 수, 반복률, 워드 간 간격(Interword Spacing)을 이용하여 채널 사용률(Channel Utilization)을 계산할 수 있다. 이러한 예측 가능성은 동적 매체 접근(Dynamic Medium Access)이나 가변 길이 네트워크 트래픽(Variable-Length Network Traffic)을 필요로 하지 않으면서 통신 타이밍 요구사항을 평가할 수 있다는 점에서 비행 관련 장비의 인터페이스 정의에 유용하다.

하네스 엔지니어링(Harness Engineering) 역시 UAV에서 중요한 고려사항이다. 각각의 ARINC 429 채널은 자체적인 차동 연선(Differential Twisted Pair)을 필요로 하므로 복잡한 양방향 또는 이중화 아키텍처에서는 배선, 커넥터 접점, 중량 및 설치 복잡도가 증가할 수 있다. 이러한 영향은 항공기 중량이 탑재량(Payload Capacity), 체공시간(Endurance), 추진 요구사항(Propulsion Requirement), 전체 임무 성능에 직접적인 영향을 미치는 UAV에서 더욱 중요하다.

전자기 적합성(Electromagnetic Compatibility)도 고려해야 한다. UAV에는 추진 모터(Propulsion Motor), 인버터(Inverter), DC/DC 컨버터, 무선 장비(Radio), 고출력 탑재체(High-Power Payload), 스위칭 전자장치(Switching Electronics)가 포함될 수 있다. 적절한 연선 라우팅, 필요한 경우의 차폐(Shielding), 접지(Grounding), 커넥터 선택, 잡음이 많은 전력 도체와의 이격(Separation), 임피던스 제어(Controlled Impedance)를 통해 ARINC 429의 신호 무결성(Signal Integrity)을 유지할 수 있다. 프로토콜 자체의 강건성은 적절한 물리적 설치에 의존한다.

화물 UAV(Cargo UAV)는 특히 다양한 항공전자 시스템이 공존하는 이기종 환경(Heterogeneous Avionics Environment)이 될 수 있다. 비행 제어 및 항법 기능은 화물 관리(Cargo Management), 상태 감시(Health Monitoring), 임무 컴퓨팅, 통신, 전력 관리(Power Management), 자율 기능(Autonomous Function)과 함께 동작할 수 있다. ARINC 429는 선택된 항공우주 하위 시스템에 결정론적인 인터페이스를 제공하고, 최신 네트워크 기술은 대용량 데이터와 광범위한 시스템 통합을 담당할 수 있다. 이를 통해 기존 항공전자 기술과 최신 기술을 점진적으로 통합할 수 있다.

인터페이스 제어 문서(Interface Control Document, ICD)는 이러한 혼합형 아키텍처(Mixed Architecture)를 구현할 때 필수적이다. 각각의 ARINC 429 채널에 대해 UAV 통합 정의(UAV Integration Definition)는 송신기, 수신기, 레이블, SDI 사용 방법, 데이터 인코딩, 공학 단위, 스케일링, SSM 해석, 전송 속도, 예상 반복 간격, 고장 동작(Failure Behavior)을 명확하게 정의해야 한다. 이러한 정의는 전기적 설계, 소프트웨어 구현, 하네스 엔지니어링, 시험, 시스템 안전 분석(System Safety Analysis)을 연결한다.

검증(Verification)은 전기적 동작과 의미적 동작을 모두 확인해야 한다. 엔지니어는 ARINC 429 분석 장비(ARINC 429 Analysis Equipment)를 사용하여 신호 품질, 레이블, 워드 내용, 패리티, 상태, 타이밍을 검사할 수 있다. 시스템 수준 시험(System-Level Test)에서는 수신된 데이터를 올바른 공학적 값으로 변환하는지, 누락되거나 유효하지 않은 정보를 검출하는지, 이중화 정보원을 올바르게 선택하는지, 통신 고장이 발생했을 때 적절한 동작을 수행하는지도 검증해야 한다.

ARINC 429는 명확한 정보 흐름 경계(Information-Flow Boundary)를 제공하므로 시스템 분석을 단순화하는 데에도 도움이 된다. 전용 송신기 채널은 알려진 출처와 정의된 레이블을 가지므로 어떤 장비가 특정 매개변수를 생성하고 어떤 기능이 그 정보를 사용하는지를 쉽게 식별할 수 있다. 이러한 명시적인 연결성(Explicit Connectivity)은 UAV 항공전자 아키텍처에서 통합, 문제 해결, 구성 관리(Configuration Management), 안전 중심 분석(Safety-Oriented Analysis)을 지원할 수 있다.

그러나 ARINC 429의 한계도 중요하다. ARINC 429는 비교적 낮은 대역폭을 제공하고 채널 수가 증가하면 추가적인 배선이 필요하며 최신 이더넷 기반 항공전자 네트워크(Ethernet-Based Avionics Network)의 유연한 스위치드 연결성(Switched Connectivity)을 제공하지 않는다. 따라서 모든 UAV 데이터 경로에 무차별적으로 적용하기보다는 결정론적인 단방향 동작, 기존 항공우주 생태계(Aerospace Ecosystem), 단순한 매개변수 교환이 의미 있는 장점을 제공하는 인터페이스에 선택적으로 적용하는 것이 적절하다.

결과적으로 이러한 UAV 아키텍처는 순수한 레거시 방식(Pure Legacy Architecture)도 아니고 순수한 네트워크 중심 방식(Pure Network-Centric Architecture)도 아닌 하이브리드 구조(Hybrid Architecture)가 된다. 기존 항공우주 장비는 전용 ARINC 429 채널을 통해 통신하고, 게이트웨이는 선택된 매개변수를 변환하며, 최신 컴퓨팅 플랫폼은 자율 기능과 고대역폭 처리를 위해 더 빠른 네트워크를 내부적으로 사용할 수 있다. 이를 통해 UAV는 기존 항공전자 인터페이스를 유지하면서도 점점 더 강력한 임무 및 자율 컴퓨팅 시스템을 통합할 수 있다.

첨부된 볼륨 구조에서 ARINC 429의 UAV 항공전자 적용(ARINC 429 in UAV Avionics)은 물리 계층, 워드 구조, 레이블 할당, 버스 아키텍처에 이어지는 ARINC 429 장의 마지막 주제를 구성한다. 이 네 가지 주제는 전기적 전송에서 데이터 형식, 의미적 식별, 네트워크 토폴로지, 최종적인 시스템 통합으로 단계적으로 확장되며, 이후에는 ARINC 664 AFDX 및 기타 더욱 발전된 핵심 통신 아키텍처로 이어진다.
