**Volume 08. Railway and Aerospace Protocols**

# Chapter 08. ARINC 664 (AFDX)

## 08.01. AFDX Virtual Link Design

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

AFDX는 스위치드 이더넷 네트워크(switched Ethernet network)에서 결정론적 통신(deterministic communication)을 구성하기 위한 기본 메커니즘으로 가상 링크(Virtual Link)를 사용합니다. 가상 링크(Virtual Link)는 하나의 송신 종단 시스템(transmitting end system)에서 시작하여 하나 이상의 수신 종단 시스템(receiving end system)으로 프레임(frame)을 전달하는 논리적 단방향 통신 경로입니다. 이러한 추상화를 통해 애플리케이션 통신 요구사항(application communication requirements)을 물리적 이더넷 토폴로지(physical Ethernet topology)와 분리할 수 있습니다.

일반적인 이더넷 통신(Ethernet communication)에서는 애플리케이션이 비교적 제한 없이 트래픽(traffic)을 생성할 수 있지만, AFDX 가상 링크(Virtual Link)는 사전에 정의된 통신 매개변수(communication parameters)를 기반으로 구성됩니다. 각 송신 애플리케이션(transmitting application)은 운용 전에 최대 전송 동작이 결정된 제어된 트래픽 흐름(controlled traffic flows)과 연결됩니다. 이를 통해 네트워크 설계자는 대역폭 요구량(bandwidth demand), 스위치 부하(switch loading), 지연시간(latency), 그리고 서로 경쟁하는 데이터 흐름(data flows) 사이의 간섭을 계산할 수 있습니다.

가상 링크(Virtual Link)는 AFDX 네트워크 내부에서 식별되므로 스위치(switch)는 수신된 프레임을 인식하고 사전에 결정된 출력 포트(output ports)를 통해서만 전달할 수 있습니다. 이러한 전달 경로(forwarding path)는 항공기 운용 중 동적으로 학습되는 것이 아니라 정적 네트워크 구성(static network configuration)을 통해 설정됩니다. 이 방식은 범용 이더넷(general-purpose Ethernet)에서 발생할 수 있는 여러 예측 불가능성을 제거하고 반복 가능한 통신 타이밍(repeatable communication timing)을 지원합니다.

AFDX 가상 링크(Virtual Link)는 본질적으로 단방향(unidirectional)입니다. 두 항공전자 컴퓨터(avionics computers)가 양방향으로 정보를 교환해야 한다면 일반적으로 각 방향에 대해 별도의 가상 링크가 구성됩니다. 이러한 설계는 모든 가상 링크가 명확하게 정의된 하나의 송신원(source)을 가지므로 트래픽 분석(traffic analysis)을 단순화합니다. 그러나 하나의 송신 흐름에 여러 수신 목적지(receiving destinations)를 연결할 수 있으므로 동일한 정보를 여러 수신 시스템에 효율적으로 배포할 수 있습니다.

가상 링크(Virtual Link)의 통신 계약(communication contract)은 대역폭 할당 간격(Bandwidth Allocation Gap, BAG) 및 해당 링크에서 허용되는 최대 프레임 크기(maximum frame size)와 밀접하게 관련됩니다. 대역폭 할당 간격(BAG)은 연속적인 프레임 전송 사이의 최소 간격을 정의하며, 최대 프레임 크기는 각 전송 기회에 네트워크로 주입될 수 있는 데이터의 양을 제한합니다. 이 두 매개변수는 함께 네트워크 대역폭 소비량(network bandwidth consumption)의 상한을 설정합니다.

예를 들어 비행 제어 컴퓨터(flight-control computer)는 하나의 가상 링크를 통해 항공기 상태 정보(aircraft state information)를 전송하고, 항법 컴퓨터(navigation computer)는 다른 가상 링크를 통해 위치 정보(position information)를 전송할 수 있습니다. 두 데이터 흐름이 동일한 물리적 이더넷 스위치와 케이블을 공유하더라도 논리적 통신 특성(logical communication properties)은 서로 독립적으로 유지됩니다. 따라서 각각의 데이터 흐름에는 항공전자 기능(avionics function)에 따라 별도로 설계된 대역폭과 전달 특성이 적용됩니다.

가상 링크 설계(Virtual Link design)는 이더넷 배선(Ethernet wiring)이 아니라 통신 요구사항(communication requirements)에서 시작됩니다. 엔지니어는 데이터 생성자(data producers), 필요한 수신자(consumers), 메시지 크기(message sizes), 갱신 주기(update rates), 지연시간 제약(latency constraints), 중요도 특성(criticality characteristics)을 식별합니다. 이후 이러한 요구사항을 논리적 흐름(logical flows)으로 변환합니다. 타이밍과 목적지 요구사항이 호환되는 관련 애플리케이션 메시지는 하나의 가상 링크를 공유할 수 있으며, 호환되지 않는 트래픽은 서로 다른 링크로 분리됩니다.

신중한 그룹화(grouping)가 중요한 이유는 지나친 통합이 가상 링크의 효율성을 낮추거나 검증을 어렵게 만들 수 있는 반면, 지나친 세분화는 구성 복잡성(configuration complexity)과 네트워크 관리 오버헤드(network-management overhead)를 증가시키기 때문입니다. 따라서 설계자는 기능적 분리(functional separation)와 효율적인 대역폭 활용(bandwidth utilization) 사이에서 균형을 유지해야 합니다. 최종 가상 링크 아키텍처(Virtual Link architecture)는 항공전자 요구사항에서 구성된 네트워크 통신 자원까지 명확한 추적성(traceability)을 유지해야 합니다.

AFDX 스위치(AFDX switch)는 구성된 가상 링크 정보를 이용하여 결정론적 전달(deterministic forwarding)을 수행합니다. 연결된 장치 사이에서 임의의 통신을 허용하는 대신 네트워크는 각 송신원에서 허가된 목적지(authorized destinations)까지 사전에 정의된 경로를 따릅니다. 따라서 스위치 구성(switch configuration)은 항공전자 네트워크 정의(avionics network definition)의 일부가 되며, 종단 시스템 구성(end-system configuration), 물리적 토폴로지(physical topology), 이중화 전략(redundancy strategy), 시스템 통합 요구사항(system integration requirements)과 일관성을 유지해야 합니다.

이중화(redundancy)는 가상 링크 설계에서 또 하나의 핵심 고려사항입니다. AFDX는 일반적으로 네트워크 A(Network A)와 네트워크 B(Network B)라고 하는 두 개의 물리적으로 독립된 네트워크를 사용합니다. 종단 시스템(end system)은 두 네트워크를 통해 동일한 프레임의 이중화 복사본(redundant copies)을 전송할 수 있으며, 이를 통해 하나의 통신 경로에 장애가 발생하더라도 수신 측에서 유효한 정보를 받아들일 수 있습니다. 순서 정보(sequence information)는 수신 측에서 중복 프레임 처리(duplicate handling)를 지원합니다.

네트워크의 결정론적 동작(deterministic behavior)은 가상 링크 트래픽 셰이핑(Virtual Link traffic shaping), 제한된 프레임 크기(bounded frame sizes), 제어된 전달 경로(controlled forwarding paths), 그리고 설계된 스위치 자원(engineered switch resources)의 결합을 통해 구현됩니다. 네트워크 분석(network analysis)을 통해 동일한 스위치 출력 포트를 공유하는 다른 링크로부터 특정 가상 링크가 받을 수 있는 간섭을 평가할 수 있습니다. 따라서 설계자는 평균적인 이더넷 성능에만 의존하지 않고 최악 조건 전송 지연시간(worst-case transmission delay)을 추정할 수 있습니다.

가상 링크 구성(Virtual Link configuration)은 하나의 데이터 흐름에 대한 변경이 공유 네트워크 자원(shared network resources)에 영향을 줄 수 있기 때문에 시스템 수준 엔지니어링(system-level engineering) 활동으로 고려되어야 합니다. 메시지 전송률(message rate)을 증가시키거나 허용 프레임 크기를 확대하고, 목적지를 변경하거나 새로운 가상 링크를 추가하면 대역폭 활용률과 최악 조건 지연시간(worst-case latency)이 달라질 수 있습니다. 따라서 항공전자 시스템 개발 전 과정에서 구성 관리(configuration control)와 반복 가능한 네트워크 분석(repeatable network analysis)이 필수적입니다.

잘 설계된 AFDX 아키텍처(AFDX architecture)는 애플리케이션이 공통의 스위치드 이더넷 인프라(shared switched Ethernet infrastructure)를 사용하면서도 명시적으로 설계된 통신 채널(engineered communication channels)을 통해 정보를 교환할 수 있는 논리적 통신 계층(logical communication layer)을 제공합니다. 가상 링크(Virtual Link)는 기능적 항공전자 데이터 흐름(functional avionics data flows)과 결정론적 네트워크 동작(deterministic network behavior)을 연결하는 역할을 하며, 핵심 항공우주 시스템(critical aerospace systems)에 요구되는 제한된 통신 특성(bounded communication properties)을 유지하면서 확장 가능한 시스템 통합(scalable integration)을 가능하게 합니다.

## 08.02. Bandwidth Allocation Gap (BAG)

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

AFDX는 대역폭 할당 간격(Bandwidth Allocation Gap, BAG)이라고 하는 매개변수를 통해 각 가상 링크(Virtual Link)의 전송 동작을 제어합니다. BAG는 동일한 가상 링크에서 연속적으로 전송되는 프레임(frame) 사이에 허용되는 최소 시간 간격을 정의합니다. AFDX는 프레임이 네트워크에 유입될 수 있는 빈도를 제한함으로써 본래 가변적일 수 있는 이더넷 트래픽(Ethernet traffic)을 경계가 명확하고 분석 가능한 통신 흐름으로 변환합니다.

BAG는 관련 항공전자 기능(avionics functions)의 통신 요구사항에 따라 각각의 가상 링크에 독립적으로 설정됩니다. 빈번한 갱신이 필요한 데이터에는 짧은 BAG를 할당할 수 있으며, 천천히 변화하는 상태 정보 또는 정비 정보(maintenance information)에는 더 긴 BAG를 사용할 수 있습니다. 이를 통해 모든 애플리케이션에 무제한적인 이더넷 대역폭(Ethernet bandwidth)을 제공하는 대신 기능별 타이밍 요구사항에 따라 네트워크 자원을 분배할 수 있습니다.

표준화된 AFDX 운용에서 BAG 값은 일반적으로 1, 2, 4, 8, 16, 32, 64 또는 128밀리초(ms)의 2의 거듭제곱 형태로 구성된 이산적인 시간 간격(discrete intervals) 중에서 선택됩니다. 이렇게 제한된 값의 집합은 트래픽 엔지니어링(traffic engineering)과 결정론적 분석(deterministic analysis)을 단순화합니다. BAG가 4ms인 가상 링크는 BAG가 32ms인 링크보다 더 빈번하게 프레임을 전송할 수 있으므로 잠재적으로 더 많은 네트워크 용량을 소비합니다.

BAG를 단순히 애플리케이션 메시지 주기(application message period)와 동일한 개념으로 해석해서는 안 됩니다. 애플리케이션은 자체 실행 주기(execution cycle)에 따라 데이터를 생성할 수 있지만, AFDX 종단 시스템(end system)은 실제로 프레임이 네트워크에 주입되는 동작을 조절합니다. 트래픽 셰이핑(traffic shaping)은 애플리케이션이 일시적으로 예상보다 빠르게 데이터를 생성하더라도 가상 링크가 설정된 통신 계약보다 공격적으로 프레임을 전송하지 못하도록 합니다.

가상 링크의 대역폭 요구량(bandwidth demand)은 BAG뿐만 아니라 해당 링크에서 전송하도록 허용된 최대 프레임 크기(maximum frame size)에 의해 결정됩니다. 짧은 BAG와 큰 최대 프레임이 결합되면 상대적으로 높은 잠재적 대역폭 요구량이 발생합니다. 반대로 긴 BAG와 작은 프레임 크기는 네트워크 부하를 감소시킵니다. 따라서 이 두 매개변수는 AFDX 통신 용량을 설계할 때 사용되는 기본적인 트래픽 범위(traffic envelope)를 형성합니다.

개념적 분석에서 최대 예약 트래픽 전송률(maximum reserved traffic rate)은 각각의 BAG 간격 동안 전송될 수 있는 최대 데이터량으로부터 근사적으로 계산할 수 있습니다. 실제 엔지니어링 계산에서는 설정된 프레임 특성과 함께 이더넷 및 AFDX 프레이밍 오버헤드(framing overhead)를 고려해야 합니다. 중요한 설계 원칙은 BAG가 감소할수록 가능한 전송 빈도가 증가하며, 이에 따라 네트워크 분석에서 고려해야 하는 대역폭도 증가한다는 것입니다.

따라서 BAG 선택은 항공전자 데이터(avionics data)에 요구되는 갱신 동작(update behavior)에서 시작됩니다. 비행 제어(flight control), 항법(navigation), 센서(sensor), 디스플레이(display), 모니터링(monitoring), 정비(maintenance) 정보는 서로 매우 다른 타이밍 요구사항을 가질 수 있습니다. 엔지니어는 정보가 수신 시스템에 얼마나 자주 도달해야 하는지를 결정한 후, 불필요하게 많은 네트워크 용량을 예약하지 않으면서 통신 요구사항을 만족하는 적절한 BAG를 선택합니다.

BAG를 지나치게 길게 설정하면 통신 지연시간(communication latency)이 증가하거나 요구되는 갱신 주기로 정보를 전달하지 못할 수 있습니다. 반대로 불필요하게 짧은 BAG를 선택하면 해당 기능이 실제로 요구하는 것보다 많은 전송 기회를 할당하게 되어 공유 스위치 자원(shared switch resources)에 대한 경쟁이 증가합니다. 따라서 효율적인 AFDX 설계에서는 관련 데이터 흐름의 타이밍 및 성능 요구사항을 만족하면서 가능한 한 긴 BAG를 선택하는 것이 중요합니다.

여러 가상 링크가 동일한 물리적 이더넷 경로(physical Ethernet path)를 공유할 때 BAG의 중요성은 더욱 명확해집니다. 각각의 링크가 생성하는 트래픽 양에는 상한이 존재하지만, 여러 링크의 프레임이 공통 스위치 출력 포트(switch output port)에 집중될 수 있습니다. 네트워크 분석(network analysis)은 이러한 상호작용을 평가하여 최악 조건(worst-case conditions)에서도 큐(queue), 스위칭 지연(switching delay), 경쟁 데이터 흐름이 요구되는 지연시간 제한을 만족할 수 있는지를 판단합니다.

각 가상 링크에는 알려진 BAG와 제한된 프레임 크기(bounded frame size)가 존재하기 때문에 엔지니어는 스위치에 도착할 수 있는 트래픽의 상한을 계산할 수 있습니다. 이는 예측할 수 없는 버스트(burst)로 인해 엄격한 타이밍 보장이 어려운 일반적인 최선형 이더넷(best-effort Ethernet)과 근본적으로 다릅니다. AFDX는 종단 시스템에서 트래픽 생성을 의도적으로 제한하여 이후의 스위치드 네트워크(switched network)를 제어되고 반복 가능한 조건을 바탕으로 분석할 수 있도록 합니다.

BAG는 항공전자 기능 사이의 트래픽 격리(traffic isolation)에도 기여합니다. 특정 애플리케이션은 처리 자원이나 이더넷 용량에 여유가 있다는 이유만으로 자신의 가상 링크를 통해 프레임을 지속적으로 주입할 수 없습니다. 설정된 전송 계약(transmission contract)이 네트워크 동작을 제한하기 때문입니다. 이를 통해 높은 전송률을 가진 송신원이 대역폭을 무제한으로 소비하는 것을 방지하고 동일한 스위칭 인프라를 공유하는 다른 가상 링크를 보호할 수 있습니다.

이중화된 AFDX 네트워크 A(Network A)와 네트워크 B(Network B)를 사용하는 경우 설정된 트래픽 특성은 이중화 아키텍처(redundancy architecture)와 일관성을 유지해야 합니다. 동일한 통신 흐름에 속하는 프레임은 두 개의 독립된 네트워크를 통해 전송될 수 있으며, 수신 종단 시스템은 이중화된 정보를 적절하게 처리합니다. 따라서 BAG 기반 트래픽 조절은 이중화 메커니즘을 대체하는 것이 아니라 이중 네트워크(dual-network)의 신뢰성 메커니즘과 함께 동작합니다.

BAG의 변경은 하나 이상의 애플리케이션에 영향을 미칠 수 있기 때문에 BAG 구성(configuration)은 엄격한 구성 관리(configuration management) 아래 유지되어야 합니다. 특정 가상 링크의 BAG를 감소시키면 해당 링크의 갱신 기회는 증가할 수 있지만, 동시에 스위치 부하(switch loading)와 다른 데이터 흐름이 경험하는 간섭도 증가할 수 있습니다. 따라서 BAG를 변경한 경우 수정된 구성을 승인하기 전에 적절한 대역폭, 지연시간, 큐잉(queueing), 최악 조건 네트워크 분석을 수행해야 합니다.

적절하게 설계된 AFDX 네트워크에서 BAG는 이더넷 대역폭을 단순히 공유되고 기회적으로 사용되는 자원에서 항공전자 요구사항에 따라 할당되는 제어된 통신 자원(controlled communication resource)으로 변환합니다. 가상 링크 정의(Virtual Link definitions), 최대 프레임 크기, 정적 전달(static forwarding), 종단 시스템 트래픽 셰이핑(end-system traffic shaping), 이중화 네트워크와 함께 BAG는 예측 가능한 대역폭 활용(predictable bandwidth utilization)을 가능하게 하며, 핵심 항공우주 네트워크(critical aerospace networking)에 요구되는 결정론적 통신 동작을 지원합니다.

## 08.03. Deterministic Ethernet (AFDX)

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

AFDX는 종단 시스템(end system)이 트래픽을 생성하는 방식, 스위치(switch)가 프레임을 전달하는 방식, 그리고 네트워크 자원이 할당되는 방식을 제한함으로써 결정론적 이더넷 통신(deterministic Ethernet communication)을 구현합니다. 일반적인 이더넷(Ethernet)이 유연한 연결성과 통계적 성능을 중시하는 반면, AFDX는 사전에 정의된 통신 동작을 적용하여 항공전자 엔지니어가 지정된 운용 조건에서 제한된 지연시간(bounded latency), 제어된 대역폭 사용(controlled bandwidth usage), 예측 가능한 전달(predictable delivery)을 확보할 수 있도록 합니다.

결정론(determinism)은 모든 AFDX 프레임이 정확히 동일한 시점에 도착한다는 의미가 아닙니다. 대신 중요한 타이밍 특성(timing characteristics)의 상한을 설정하고 분석할 수 있도록 네트워크를 설계한다는 의미입니다. 전송률, 최대 프레임 크기, 전달 경로, 스위치 동작, 경쟁 트래픽이 구성을 통해 알려져 있으므로 엔지니어는 통신이 항공전자 기능에 요구되는 지연시간 및 대역폭 한계 내에서 유지되는지를 판단할 수 있습니다.

가상 링크(Virtual Link)는 이러한 결정론적 아키텍처(deterministic architecture)의 중심 요소입니다. 각 가상 링크는 하나의 송신 종단 시스템에서 하나 이상의 수신 종단 시스템으로 연결되는 단방향 논리적 통신 경로(unidirectional logical communication path)를 정의합니다. 송신원, 목적지, 통신 매개변수가 사전에 정의되기 때문에 트래픽을 동적으로 통신하는 장치 사이의 임의적인 이더넷 교환이 아니라 제어된 데이터 흐름(controlled flows)의 집합으로 분석할 수 있습니다.

네트워크에 유입되는 트래픽은 송신 종단 시스템(transmitting end system)에서 조절됩니다. 대역폭 할당 간격(Bandwidth Allocation Gap, BAG)은 하나의 가상 링크에서 연속적인 프레임 전송을 제어하는 최소 간격을 정의하며, 설정된 최대 프레임 크기(maximum frame size)는 각 전송 기회에 전달할 수 있는 데이터의 양을 제한합니다. 이 두 매개변수는 애플리케이션이 공유 네트워크 인프라에 제어되지 않은 버스트(uncontrolled burst)를 주입하지 못하도록 제한된 트래픽 범위(bounded traffic envelope)를 형성합니다.

이러한 트래픽 셰이핑(traffic shaping) 메커니즘이 중요한 이유는 결정론적 스위칭(deterministic switching)에 예측 가능한 입력 동작이 필요하기 때문입니다. 애플리케이션이 예상보다 빠르게 데이터를 생성하더라도 종단 시스템은 설정된 가상 링크 매개변수에 따라 전송을 제한합니다. 따라서 하나의 애플리케이션이 사용 가능한 이더넷 용량 전체를 임의로 소비할 수 없으며, 다른 통신 흐름이 받을 수 있는 최대 간섭(maximum interference)을 정의된 조건에 따라 분석할 수 있습니다.

AFDX 스위치는 중요한 아키텍처적 측면에서 일반적인 학습형 이더넷 스위치(learning Ethernet switch)와도 차이가 있습니다. 프레임 전달(frame forwarding)은 항공기 운용 중 동적으로 학습되는 연결 정보에 의존하지 않고 정적으로 구성된 가상 링크 경로(statically configured Virtual Link paths)를 따릅니다. 스위치는 관련 통신 흐름을 식별하고 사전에 결정된 출력 포트를 통해 프레임을 전달하므로 실제 운용에 앞서 전달 동작이 확립된 네트워크 토폴로지(network topology)를 구성할 수 있습니다.

여러 가상 링크는 동일한 물리적 링크와 스위치 출력 포트(switch output port)를 공유할 수 있으므로 결정론적 운용이 경합(contention) 자체를 제거하는 것은 아닙니다. 대신 AFDX는 이러한 경합을 분석 가능하게 만듭니다. 엔지니어는 각 네트워크 자원에서 어떤 데이터 흐름이 집중될 수 있는지를 파악하고 BAG 값, 프레임 크기, 경로 및 스위칭 상호작용을 평가합니다. 이러한 정보는 최악 조건 지연시간(worst-case delay)을 계산하고 종단 간 통신 요구사항(end-to-end communication requirements)을 검증하는 데 사용됩니다.

특히 여러 프레임이 짧은 시간 간격으로 공통 스위치 출력에 도착하면 큐잉 지연(queueing delay)이 중요해집니다. 두 데이터 흐름이 모두 설정된 트래픽 제한을 준수하더라도 하나의 프레임이 전송되는 동안 다른 프레임은 대기해야 할 수 있습니다. 따라서 결정론적 네트워크 엔지니어링(deterministic network engineering)은 이더넷 스위칭 자체가 일정한 지연시간을 제공한다고 가정하지 않고 직렬화(serialization), 스위칭(switching), 큐잉(queueing), 전파(propagation), 간섭(interference)의 영향을 함께 고려합니다.

종단 간 지연시간 분석(end-to-end latency analysis)은 송신 종단 시스템에서 중간 네트워크 자원을 거쳐 수신 종단 시스템까지 이어지는 전체 경로를 대상으로 수행됩니다. 각 구성요소는 전체 지연시간 예산(delay budget)의 일부를 차지합니다. 분석의 목적은 여러 정상적인 가상 링크가 불리한 트래픽 조합을 생성하는 조건까지 포함하여 발생 가능한 최대 통신 지연시간이 항공전자 기능에 할당된 제한보다 낮다는 것을 입증하는 것입니다.

AFDX는 통신 가용성(communication availability)을 향상하기 위해 네트워크 이중화(network redundancy)도 사용합니다. 일반적으로 네트워크 A(Network A)와 네트워크 B(Network B)로 구분되는 두 개의 물리적으로 독립된 네트워크가 동일한 정보의 이중화 복사본(redundant copies)을 전달할 수 있습니다. 따라서 한쪽의 스위치, 케이블, 커넥터 또는 네트워크 경로에 장애가 발생하더라도 독립된 이중화 경로가 정상이고 수신 종단 시스템이 유효한 복사본을 처리할 수 있다면 통신이 반드시 중단되는 것은 아닙니다.

이중화(redundancy)와 결정론(determinism)은 서로 다르지만 상호 보완적인 요구사항을 해결합니다. 결정론은 언제 얼마나 많은 트래픽이 네트워크를 통과할 수 있는지를 제어하고 제한된 타이밍 동작(bounded timing behavior)을 제공하는 반면, 이중화는 지정된 장애로부터 통신을 보호합니다. 견고한 항공전자 아키텍처(avionics architecture)는 이러한 특성을 결합하여 하나의 통신 네트워크에 장애가 발생하더라도 핵심 정보가 시간적으로 예측 가능하면서 동시에 가용성을 유지하도록 합니다.

따라서 정적 구성(static configuration)은 AFDX에서 핵심적인 엔지니어링 산출물(engineering artifact)입니다. 가상 링크 정의, BAG 값, 최대 프레임 크기, 송신원과 목적지 관계, 스위치 전달 정보, 이중화 경로는 서로 일관성을 유지해야 합니다. 모든 물리적 이더넷 구성요소가 정상적으로 동작하더라도 구성 오류(configuration error)는 대역폭 활용, 도달 가능성(reachability), 지연시간 또는 격리(isolation)에 영향을 줄 수 있으므로 구성 검증(configuration verification)이 필수적입니다.

항공전자 시스템이 변경될 때에도 결정론적 동작을 유지해야 합니다. 새로운 애플리케이션 추가, 목적지 변경, 프레임 크기 증가, BAG 단축 또는 스위치 경로 변경은 공유 자원에서 발생하는 경합을 변화시킬 수 있습니다. 따라서 외관상 국부적인 변경이라도 네트워크의 다른 위치에 존재하는 기존 가상 링크의 최악 조건 통신 성능(worst-case communication performance)에 영향을 줄 수 있으므로 영향 분석(impact analysis)이 필요합니다.

따라서 검증(verification)은 기능적 통신 시험(functional communication testing)과 타이밍 및 자원 분석(timing and resource analysis)을 결합하여 수행됩니다. 엔지니어는 프레임이 의도된 목적지에 도달하는지를 확인하는 동시에 네트워크 부하와 최악 조건 지연시간이 할당된 제한 범위 안에 유지되는지를 입증해야 합니다. 시험은 구현상의 문제를 발견할 수 있으며, 분석적 방법(analytical methods)은 실험실 또는 항공기 수준 시험에서 모든 경우를 재현하기 어려운 정상 트래픽 조합까지 평가할 수 있습니다.

결과적으로 AFDX는 아키텍처적 제약(architectural constraints)을 적용하여 이더넷을 핵심 항공전자 시스템 통합(critical avionics integration)에 적합한 통신 인프라로 변환한 기술로 이해할 수 있습니다. 가상 링크는 제어된 논리적 데이터 흐름을 정의하고, BAG와 프레임 크기 제한은 트래픽을 조절하며, 정적 스위칭(static switching)은 전달 경로를 제한합니다. 여기에 이중화가 가용성을 향상하고 최악 조건 분석(worst-case analysis)이 타이밍 상한을 확립함으로써 확장 가능한 항공우주 통신 시스템에 필요한 결정론적 동작을 제공합니다.

## 08.04. AFDX End System Design

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

AFDX 종단 시스템(AFDX End System)은 항공전자 애플리케이션(avionics application)과 결정론적 이더넷 네트워크(deterministic Ethernet network) 사이의 인터페이스입니다. 애플리케이션 데이터를 사전에 정의된 가상 링크(Virtual Link) 특성을 준수하는 네트워크 트래픽으로 변환하고, 수신되는 트래픽에 대해서는 이에 대응하는 수신 기능을 수행합니다. 따라서 종단 시스템은 단순한 이더넷 인터페이스 이상의 역할을 수행하며, AFDX 아키텍처에서 요구하는 통신 동작을 강제합니다.

송신 측에서 애플리케이션 데이터는 하나 이상의 설정된 가상 링크(Virtual Link)와 연결됩니다. 각 가상 링크에는 송신원(source), 목적지(destination), 대역폭 할당 간격(Bandwidth Allocation Gap, BAG), 허용되는 프레임 특성(frame characteristics)을 포함하는 사전 정의된 통신 속성이 존재합니다. 종단 시스템은 이러한 구성을 이용하여 애플리케이션 정보가 네트워크에 진입하는 방식을 결정하며, 소프트웨어가 할당된 통신 자원을 벗어나 임의의 이더넷 트래픽을 전송하지 못하도록 합니다.

트래픽 셰이핑(traffic shaping)은 가장 중요한 송신 기능 중 하나입니다. 종단 시스템은 대역폭 할당 간격(BAG)에 따라 연속적인 전송을 조절하여 특정 가상 링크에 속하는 프레임이 허용된 빈도보다 더 자주 네트워크에 주입되지 않도록 합니다. 최대 프레임 크기(maximum frame size) 제한은 각 전송 기회에 생성되는 트래픽 양을 추가로 제한하여 이후의 네트워크 분석을 위한 예측 가능한 트래픽 범위(traffic envelope)를 형성합니다.

따라서 애플리케이션 실행 타이밍(application execution timing)과 네트워크 전송 타이밍(network transmission timing)은 서로 분리하여 다루어야 합니다. 애플리케이션은 자체 계산 주기(computational cycle)에 따라 정보를 생성할 수 있지만, 해당 네트워크 프레임이 실제로 언제 전송되는지는 종단 시스템이 제어합니다. 버퍼링(buffering)과 스케줄링(scheduling) 메커니즘은 이러한 경계를 처리하면서 생성되는 이더넷 트래픽이 설정된 가상 링크 통신 계약을 준수하도록 합니다.

송신 종단 시스템은 AFDX 네트워크를 통한 통신에 필요한 이더넷 프레임(Ethernet frame)도 구성합니다. 애플리케이션 데이터는 네트워크 전송과 가상 링크 식별(Virtual Link identification)에 필요한 프로토콜 정보와 함께 캡슐화(encapsulation)됩니다. 스위치는 설정된 통신 식별자를 이용하여 사전에 정의된 경로를 따라 허가된 수신 종단 시스템으로 프레임을 전달하므로 올바른 캡슐화가 필수적입니다.

AFDX는 일반적으로 네트워크 A(Network A)와 네트워크 B(Network B)라고 하는 두 개의 물리적으로 독립된 네트워크 채널(network channel)을 사용합니다. 이중화된 종단 시스템 인터페이스(redundant End System interface)는 두 네트워크를 통해 대응하는 프레임을 전송할 수 있으므로 하나의 네트워크에 장애가 발생하더라도 반드시 통신이 중단되는 것은 아닙니다. 두 경로는 해당 가상 링크의 일관된 통신 특성을 유지하면서 충분한 독립성을 확보해야 합니다.

순서 정보(sequence information)는 이중화 전송(redundant transmission)을 관리하는 데 사용됩니다. 독립된 네트워크를 통해 대응하는 프레임이 도착하면 수신 종단 시스템은 이들 사이의 관계를 인식하고 불필요한 중복 정보가 애플리케이션으로 전달되지 않도록 해야 합니다. 따라서 이중화 관리(redundancy management)는 독립적인 물리적 통신 경로와 수신 측 처리를 결합하여 항공전자 소프트웨어에 적절한 데이터 흐름을 제공합니다.

수신 과정에서 종단 시스템은 설정된 가상 링크와 관련된 프레임을 받아들이고 확립된 통신 관계에 따라 처리합니다. 프레임은 검사되고 분류된 후 적절한 수신 애플리케이션 인터페이스(receiving application interface)로 매핑됩니다. 이러한 제어된 수신 모델(controlled reception model)은 임의의 네트워크 트래픽이 자동으로 애플리케이션 데이터가 되는 것을 방지하고 AFDX 통신 구성을 통해 설정된 논리적 분리(logical separation)를 유지합니다.

네트워크 도착 타이밍(network arrival timing)과 애플리케이션 소비 타이밍(application consumption timing)이 반드시 동일하지 않기 때문에 버퍼 설계(buffer design)가 중요합니다. 수신 프레임은 소프트웨어가 처리하기 전까지 임시 저장이 필요할 수 있으며, 송신 애플리케이션 데이터는 허용된 전송 기회까지 대기할 수 있습니다. 따라서 버퍼 용량과 관리 정책은 허용할 수 없는 데이터 손실, 과도한 지연시간 또는 예측 불가능한 자원 소비를 발생시키지 않으면서 예상 트래픽 동작을 지원해야 합니다.

종단 시스템은 통신 격리(communication isolation)를 위한 중요한 경계 역할도 수행합니다. 여러 항공전자 애플리케이션이 동일한 물리적 네트워크 인터페이스를 공유하면서 서로 다른 가상 링크와 통신 요구사항을 사용할 수 있습니다. 종단 시스템은 이러한 데이터 흐름 사이의 분리를 유지하여 하나의 애플리케이션 동작이 동일한 네트워크 연결을 공유하는 다른 애플리케이션에 할당된 대역폭이나 통신 특성을 위반하지 않도록 해야 합니다.

따라서 구성 데이터(configuration data)는 종단 시스템 운용의 핵심 요소입니다. 가상 링크 정의, BAG 값, 최대 프레임 크기, 송신원과 목적지 관계, 인터페이스 할당(interface assignment), 이중화 네트워크 정보는 AFDX 스위치 및 다른 종단 시스템에서 사용되는 구성과 일치해야 합니다. 구성이 일치하지 않으면 통신 손실, 잘못된 라우팅, 과도한 네트워크 부하 또는 타이밍 요구사항 미충족이 발생할 수 있습니다.

결정론적 성능(deterministic performance)은 네트워크 스위치뿐만 아니라 종단 시스템 내부의 예측 가능한 처리에도 의존합니다. 데이터 캡슐화, 트래픽 셰이핑, 큐 처리(queue handling), 이중화 전송, 프레임 수신, 중복 관리(duplicate management), 애플리케이션 전달은 모두 종단 간 통신 동작(end-to-end communication behavior)에 영향을 줍니다. 따라서 전체 항공전자 통신 경로를 평가할 때 이러한 처리 지연과 자원 제한도 함께 고려해야 합니다.

장애 처리(fault handling)와 모니터링(monitoring) 역시 중요한 종단 시스템 기능입니다. 구현 시스템은 비정상 트래픽(invalid traffic), 데이터 누락(missing data), 인터페이스 장애(interface failure), 이중화 문제 또는 구성 불일치와 같은 비정상 통신 상태를 탐지할 수 있는 메커니즘을 제공해야 합니다. 진단 정보(diagnostic information)는 정상적인 애플리케이션 데이터 경로와 통신 모니터링 사이의 분리를 유지하면서 시스템 수준 장애 관리를 지원할 수 있습니다.

AFDX 종단 시스템 검증(verification)은 기능적 정확성과 설정된 네트워크 동작에 대한 적합성을 모두 입증해야 합니다. 시험을 통해 애플리케이션 데이터가 의도된 가상 링크와 목적지에 도달하는지, 전송 제한이 준수되는지, 이중화 경로가 올바르게 동작하는지, 수신 프레임이 적절하게 처리되는지 확인해야 합니다. 또한 비정상 조건이 제어되지 않은 트래픽이나 허용할 수 없는 간섭을 발생시키지 않는지도 검증해야 합니다.

따라서 잘 설계된 AFDX 종단 시스템은 항공전자 소프트웨어와 스위치드 네트워크(switched network) 사이에서 결정론적 통신 게이트웨이(deterministic communication gateway) 역할을 수행합니다. 가상 링크 매핑, BAG 기반 트래픽 셰이핑, 제한된 프레임 생성, 버퍼링, 이중화된 네트워크 A와 네트워크 B 인터페이스, 수신 처리, 격리, 모니터링 및 제어된 구성을 결합함으로써 애플리케이션이 이더넷을 사용하면서도 핵심 항공우주 시스템에 요구되는 예측 가능한 통신 동작을 유지할 수 있도록 합니다.

## 08.05. AFDX for Cargo UAV

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

화물 무인항공기(Cargo UAV)는 비행 제어 컴퓨터(flight-control computer), 항법 장치(navigation unit), 추진 제어기(propulsion controller), 전력 관리 시스템(power-management system), 탑재 장비(payload equipment), 센서(sensor), 임무 컴퓨터(mission computer)를 연결하면서 예측 가능한 타이밍을 유지할 수 있는 내부 통신 아키텍처가 필요합니다. AFDX는 스위치드 이더넷(switched Ethernet)의 대역폭과 제어된 가상 링크(Virtual Link), 제한된 트래픽 생성(bounded traffic generation), 정적 전달(static forwarding), 이중화 네트워크 경로(redundant network path)를 결합하므로 이러한 시스템을 위한 유용한 아키텍처 모델을 제공합니다.

화물 무인항공기의 항공전자 네트워크(avionics network)는 매우 다양한 통신 특성을 가진 기능들을 지원해야 합니다. 비행 상태 및 제어 관련 정보는 빈번하면서 엄격하게 제한된 시간 내에 전달되어야 하는 반면, 상태 모니터링(health monitoring), 화물 상태(cargo status), 정비 기록(maintenance record), 진단 정보(diagnostic information)는 상대적으로 느린 갱신을 허용할 수 있습니다. AFDX는 이러한 트래픽 종류가 공통 물리적 이더넷 인프라를 공유하면서도 각각 별도로 설계된 통신 특성을 유지할 수 있도록 합니다.

가상 링크(Virtual Link)는 이러한 UAV 데이터 흐름을 분리하기 위한 논리적 기반을 제공합니다. 비행 제어 컴퓨터는 하나의 가상 링크를 통해 상태 정보를 전송하고, 항법 시스템은 다른 가상 링크를 통해 위치 및 자세 정보(position and attitude information)를 배포하며, 화물 관리 제어기(cargo-management controller)는 추가 링크를 이용하여 탑재 화물 상태를 전달할 수 있습니다. 각각의 가상 링크는 단방향(unidirectional)을 유지하며 알려진 송신원, 목적지 및 트래픽 특성에 따라 구성됩니다.

대역폭 할당 간격(Bandwidth Allocation Gap, BAG)은 각 통신 흐름의 타이밍 요구사항에 따라 선택할 수 있습니다. 비행 제어 또는 항법과 관련된 빠르게 변화하는 정보에는 짧은 BAG 값을 사용할 수 있으며, 열 모니터링(thermal monitoring), 배터리 상태, 화물 상태 또는 정비 정보에는 더 긴 간격을 사용할 수 있습니다. BAG는 최대 프레임 크기(maximum frame size) 제한과 결합되어 각 가상 링크의 대역폭 사용량에 상한을 설정하고 공유 네트워크 자원을 보호합니다.

AFDX 종단 시스템(AFDX End System)의 트래픽 셰이핑(traffic shaping)은 개별 UAV 애플리케이션이 설정된 통신 계약을 초과하여 데이터를 전송하는 것을 방지합니다. 이러한 특성은 비행 필수 애플리케이션(flight-critical application)과 비필수 애플리케이션이 동일한 네트워크 하드웨어를 공유할 때 특히 중요합니다. 탑재 데이터, 진단 정보 또는 기록된 센서 데이터의 갑작스러운 버스트(burst)가 네트워크 용량을 예측 불가능하게 소비하여 비행 관련 통신을 방해하지 않도록 해야 합니다.

정적 전달(static forwarding)은 예측 가능성을 더욱 향상합니다. 스위치가 임의의 통신 관계를 동적으로 탐색하도록 하는 대신 가상 링크의 전달 경로를 구성을 통해 사전에 설정합니다. 따라서 비행 제어 데이터는 의도된 수신 시스템으로만 전달되고, 항법, 추진, 전력, 화물 및 모니터링 정보는 각각 사전에 정의된 경로를 따를 수 있습니다. 이러한 구조는 기능 요구사항과 네트워크 구성 사이의 명확한 추적성(traceability)도 제공합니다.

화물 무인항공기는 독립적인 네트워크 A(Network A)와 네트워크 B(Network B) 경로를 사용하는 기존 AFDX 이중 네트워크 개념(dual-network concept)을 활용할 수 있습니다. 핵심 종단 시스템은 두 네트워크를 통해 이중화된 프레임(redundant frame)을 전송할 수 있으므로 한쪽의 스위치, 케이블, 커넥터 또는 네트워크 인터페이스에 장애가 발생하더라도 통신 기능이 자동으로 상실되지는 않습니다. 수신 종단 시스템은 이중화된 정보를 처리하여 적절한 데이터를 애플리케이션에 전달합니다.

이러한 이중화 개념을 항공기에 적용할 때는 물리적 독립성(physical independence)이 중요합니다. 두 개의 논리적 네트워크가 동일한 취약 하드웨어를 통해 연결되거나 동일한 장애 위험이 있는 설치 구역을 통과한다면 의도한 이중화 효과가 감소할 수 있습니다. 따라서 네트워크 아키텍처는 이중화가 UAV의 가용성(availability)에 어떻게 기여하는지를 판단할 때 독립된 인터페이스, 스위칭 자원, 케이블 경로, 전원 의존성(power dependency), 장애 전파(failure propagation)를 고려해야 합니다.

화물 UAV 아키텍처에는 기존 항공전자 기능 이외의 통신 인터페이스도 포함됩니다. 화물 관리 시스템(cargo-management system)은 적재 상태(load status), 잠금 장치(locking mechanism), 환경 조건(environmental condition), 도어(door), 액추에이터(actuator), 임무 전용 탑재 장비를 모니터링할 수 있습니다. 이러한 기능은 전용 가상 링크를 통해 통합할 수 있으며 트래픽 동작을 제어된 상태로 유지함으로써 화물 및 임무 기능이 고도화되어도 항공기 네트워크를 확장할 수 있습니다.

추진 및 전기 에너지 시스템(propulsion and electrical-energy system)은 또 다른 중요한 통합 영역입니다. 대형 화물 UAV에서는 추진 상태, 배터리 또는 하이브리드 전원 상태(hybrid-power condition), 전력 분배(power distribution), 열 상태(thermal state), 시스템 장애와 관련된 정보를 교환해야 할 수 있습니다. AFDX는 이러한 상위 감독 정보(supervisory information)를 위한 결정론적 이더넷 백본(deterministic Ethernet backbone)을 제공할 수 있으며, 더 엄격한 로컬 제어 요구사항이나 기존 장비 인터페이스가 필요한 경우 하위 수준 제어 인터페이스는 특수 버스를 유지할 수 있습니다.

따라서 네트워크 통신(network communication)과 실시간 액추에이터 제어(real-time actuator control)를 구분하는 것이 중요합니다. AFDX가 UAV 내부의 모든 로컬 센서, 모터 제어 또는 임베디드 제어 버스(embedded control bus)를 자동으로 대체해야 하는 것은 아닙니다. 대신 주요 컴퓨팅 및 서브시스템 영역을 연결하는 결정론적 항공전자 백본으로 사용할 수 있으며, 로컬 제어기는 적합한 하위 수준 인터페이스를 사용할 수 있습니다. 이후 게이트웨이(gateway)를 통해 필요한 서브시스템 정보를 상위 AFDX 네트워크에 제공할 수 있습니다.

비행 관련 가상 링크에는 종단 간 지연시간 분석(end-to-end latency analysis)이 필수적입니다. 엔지니어는 종단 시스템 처리, BAG에 따른 전송 동작, 프레임 직렬화(frame serialization), 스위칭(switching), 큐잉(queueing), 전파(propagation), 다른 정상 트래픽으로부터 발생하는 간섭을 고려해야 합니다. 목적은 평균적인 이더넷 성능에 의존하는 것이 아니라 발생 가능한 최악 조건의 통신 지연시간이 각 기능에 할당된 타이밍 요구사항 안에 유지된다는 것을 입증하는 것입니다.

화물 UAV가 발전함에 따라 네트워크 구성(network configuration)도 통제된 엔지니어링 프로세스를 통해 변경되어야 합니다. 센서를 추가하거나 새로운 임무 컴퓨터를 도입하고, 탑재 데이터량을 증가시키거나 BAG 값을 변경하거나 목적지를 수정하면 공유 스위치 자원과 기존 가상 링크에 영향을 줄 수 있습니다. 따라서 구성 변경은 항공기 통신 아키텍처에 적용되기 전에 영향 평가(impact assessment), 갱신된 대역폭 계산, 지연시간 분석 및 검증을 수행해야 합니다.

대형 화물 UAV 플랫폼에서는 분산 전자 시스템(distributed electronic system)의 수와 교환되는 정보량이 증가하는 경향이 있으므로 구조화된 이더넷(structured Ethernet)의 장점이 더욱 중요해집니다. 결정론적 스위치드 백본(deterministic switched backbone)은 다수의 독립적인 점대점 연결(point-to-point connection)에 대한 의존성을 줄이면서 중앙집중형 및 분산형 컴퓨팅 아키텍처를 지원할 수 있습니다. 그러나 확장성은 체계적인 가상 링크 및 대역폭 엔지니어링을 통해 제한되고 관리되어야 합니다.

따라서 AFDX는 첨단 화물 UAV 항공전자 시스템에서 핵심 통신을 통합하기 위한 참조 아키텍처(reference architecture)를 제공할 수 있습니다. 가상 링크는 기능별 데이터 흐름을 분리하고, BAG와 프레임 크기 제한은 대역폭을 제어하며, 종단 시스템은 네트워크 접근을 조절하고, 정적 스위치는 예측 가능한 전달을 제공합니다. 여기에 이중화 네트워크가 가용성을 향상함으로써 비행, 항법, 추진, 에너지, 화물, 모니터링 및 임무 시스템을 연결하면서 결정론적 동작을 유지할 수 있는 확장 가능한 통신 백본을 구성할 수 있습니다.
