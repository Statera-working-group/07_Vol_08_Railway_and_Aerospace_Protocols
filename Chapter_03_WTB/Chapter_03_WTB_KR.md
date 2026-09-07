**Volume 08. Railway and Aerospace Protocols**

# Chapter 03. WTB

## 03.01. WTB Train Coupling

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

열차 와이어 버스(Wire Train Bus, WTB)는 IEC 61375 열차 통신 네트워크(Train Communication Network, TCN) 프레임워크에서 정의된 열차 수준 백본 통신 시스템이다. WTB의 기본 목적은 기계적으로 연결되어 하나의 완전한 열차를 구성하는 개별 차량 그룹 또는 편성(Consist) 사이에 신뢰성 높은 통신을 구축하는 것이다. 단일 차량 내부에 한정된 통신망과 달리 WTB는 차량이 연결(Coupling)되거나 분리(Uncoupling)될 때마다 물리적 구성이 변경될 수 있는 토폴로지(Topology)를 처리하도록 설계되었다.

열차 연결(Train Coupling)은 영구적으로 구성된 기계 내부의 네트워킹과 근본적으로 다른 통신 문제를 발생시킨다. 철도 차량은 운용 요구에 따라 추가되거나 제거될 수 있으며, 방향이 반전되거나 순서가 재배치될 수도 있다. 따라서 통신 백본(Communication Backbone)은 물리적 시스템이 변경되었다는 사실을 인식하고, 차량 간 통신(Inter-Vehicle Communication)에 의존하는 정상적인 분산 기능이 동작하기 전에 새로운 열차 구성에 대응하는 유효한 논리 네트워크(Logical Network)를 구축해야 한다.

WTB는 열차 전체에 걸쳐 서로 분리된 철도 차량 또는 편성의 통신 영역(Communication Domain)을 연결한다. 각각의 편성은 자체적인 내부 통신 네트워크를 가질 수 있으며, 전통적으로 다기능 차량 버스(Multifunction Vehicle Bus, MVB)와 같은 기술이 사용된다. WTB는 이러한 로컬 차량 범위(Local Vehicle Scope)의 상위에서 독립적으로 동작하는 차량 단위들을 연결하는 백본을 제공한다. 로컬 네트워크(Local Network)와 동적으로 구성되는 백본(Dynamic Backbone)의 분리는 열차 통신 네트워크(TCN)의 핵심적인 아키텍처 원칙이다.

기계적 연결(Mechanical Coupling)과 전기적 통신 연결(Electrical Communication Coupling)은 밀접하게 관련되어 있지만 동일한 작업으로 간주해서는 안 된다. 두 철도 차량을 물리적으로 연결하면 기계적인 열차가 형성되지만, 통신 인터페이스(Communication Interface)는 백본에 필요한 전기적 경로를 구축한다. 이후 네트워크는 연결된 노드(Node)들이 유효한 통신 구조를 형성하는지 판단해야 한다. 이러한 논리적 구성이 완료된 후에야 열차 전체의 정보 교환이 통제되고 예측 가능한 방식으로 진행될 수 있다.

WTB의 주요 특징 중 하나는 열차의 구성이 영구적으로 정해져 있지 않은 상황을 처리할 수 있다는 점이다. 일반적인 고정형 산업 네트워크(Fixed Industrial Network)는 사전에 정의된 노드 주소(Node Address)와 케이블 배치(Cable Layout)를 기반으로 설계할 수 있다. 그러나 열차는 서로 다른 편성을 서로 다른 시점에 조합하여 구성할 수 있다. 따라서 WTB는 네트워크가 현재 구성을 발견하고 노드 간 관계를 설정하며 새롭게 형성된 열차에 필요한 통신 구조를 생성하는 초기화 과정(Inauguration Process)을 지원한다.

이러한 초기화 과정(Inauguration Process)은 물리적 연결 상태를 실제로 사용할 수 있는 논리 토폴로지(Logical Topology)로 변환한다. 참여 노드는 자신의 상대적인 위치를 파악하고 열차를 순서화하여 표현하는 구조를 설정해야 한다. 이렇게 생성된 구성 정보를 이용하면 애플리케이션(Application)은 통신 참여자를 조립된 차량 순서에서의 위치와 연관시킬 수 있다. 따라서 열차 전체 기능은 연결 또는 분리 이전에 유효했던 과거 구성에 의존하지 않고 현재 편성 구조를 기준으로 동작할 수 있다.

방향(Direction)은 철도 차량이 서로 다른 방향으로 연결될 수 있기 때문에 특히 중요하다. 통신 시스템은 모든 차량이 항상 동일한 전방 방향으로 영구 설치되어 있다고 가정할 수 없다. 따라서 WTB 메커니즘(Mechanism)은 방향 정보를 고려하는 열차 토폴로지(Orientation-Aware Train Topology)의 구축을 지원한다. 상대적인 위치와 방향을 파악함으로써 분산 시스템(Distributed System)은 운행 중 물리적 배열이 변경될 수 있는 열차에서도 명령, 상태 정보, 차량 식별 정보를 일관되게 해석할 수 있다.

초기화가 성공적으로 완료되면 WTB는 열차 전체의 프로세스 정보(Process Information)를 교환할 수 있는 백본을 제공한다. 이러한 통신은 차량 아키텍처에 따라 협조 제어되는 견인(Coordinated Traction), 제동 관련 정보 교환(Braking-Related Information Exchange), 출입문 기능(Door Function), 승객 시스템(Passenger System), 진단(Diagnostics), 상태 감시(Status Monitoring) 및 기타 분산 철도 기능을 지원할 수 있다. 핵심 원칙은 독립적으로 구성된 차량들이 열차가 조립된 이후 하나의 공통 통신 환경(Common Communication Environment)에 참여한다는 것이다.

열차 연결은 네트워크 견고성(Network Robustness)에 대한 중요한 요구사항도 발생시킨다. 커넥터(Connector), 배선(Wiring), 종단 조건(Termination Condition), 통신 인터페이스는 반복적인 기계적 연결 과정뿐만 아니라 철도 운용 과정에서 발생하는 진동(Vibration), 전기적 교란(Electrical Disturbance), 다양한 환경 조건(Environmental Condition)을 견뎌야 한다. 열차 백본은 논리적인 프로토콜 정확성(Protocol Correctness)에만 의존할 수 없으며, 각 차량 간 연결 지점에서 물리적 통신 경로가 충분한 신뢰성을 유지해야 논리 토폴로지도 의미를 유지할 수 있다.

열차 편성이 동적으로 변경된다는 특성은 토폴로지 변화(Topology Change)를 체계적으로 관리해야 한다는 것을 의미한다. 차량이 제거되거나 새로운 편성이 연결되면 기존 네트워크 표현(Network Representation)은 더 이상 실제 열차의 물리적 구성과 일치하지 않을 수 있다. 따라서 통신 시스템은 변경된 상태를 인식하고 필요에 따라 백본을 재구성해야 한다. 이를 통해 분산 애플리케이션이 차량 식별 정보, 차량 순서, 연결 상태 또는 열차 길이에 관한 잘못된 가정을 기반으로 계속 동작하는 것을 방지할 수 있다.

WTB 열차 연결은 네트워크 발견(Network Discovery)과 애플리케이션 통신(Application Communication) 사이의 중요한 차이를 보여준다. 운용 데이터를 의미 있게 교환하기 전에 통신 인프라는 먼저 어떤 장치가 연결되어 있는지, 참여 장치들이 어떻게 배열되어 있는지, 현재 열차에서 어떻게 주소가 지정되어야 하는지를 결정해야 한다. 따라서 네트워크 관리(Network Management)는 단순한 유지보수 기능이 아니라 핵심적인 기반 기능이 되며, 특히 독립적인 서브시스템(Subsystem)을 동적으로 조립하여 구성하는 시스템에서는 더욱 중요하다.

이러한 아키텍처는 WTB와 MVB가 전체 열차 통신 네트워크(TCN) 구조에서 상호 보완적인 역할을 수행하는 이유도 보여준다. MVB는 주로 차량 또는 편성 내부 장치 간 통신을 담당하고, WTB는 전통적으로 연결된 열차 전체에 걸친 통신을 제공한다. 따라서 게이트웨이(Gateway)는 로컬 차량 정보를 열차 백본으로 연결할 수 있으며, 모든 내부 서브시스템이 직접 WTB 노드로 동작하지 않더라도 선택된 데이터를 내부 장치와 열차 수준의 통신 참여자 사이에서 전달할 수 있다.

시스템 엔지니어링(Systems Engineering) 관점에서 WTB 연결은 독립적으로 기능할 수 있는 여러 차량 단위를 하나의 협조된 분산 시스템(Coordinated Distributed System)으로 변환한다. 기계적 조립(Mechanical Assembly)은 물리적인 열차를 결정하고, 초기화(Inauguration)는 통신 토폴로지를 결정하며, 애플리케이션 프로토콜(Application Protocol)은 이 토폴로지를 활용하여 열차 수준의 동작을 조정한다. 이러한 단계는 물리적 연결, 네트워크 구성, 기능적 정보 교환을 하나의 과정으로 취급하지 않고 서로 구분한다는 점에서 유용한 개념적 계층 구조를 형성한다.

동일한 원칙은 다른 모듈형 사이버 물리 시스템(Modular Cyber-Physical System)을 분석할 때도 유용하다. 이동 로봇(Mobile Robot), 자율주행 차량(Autonomous Vehicle), 무인항공기 그룹(UAV Group), 탈착식 임무 모듈(Detachable Mission Module) 역시 운용 중 구성원이 변경되는 임시 시스템을 형성할 수 있다. 통신 기술 자체는 WTB와 크게 다를 수 있지만, 새롭게 연결된 장치를 발견하고 식별하며 체계적으로 구성한 후 공통 통신 구조에 참여시켜야 협조 동작(Coordinated Behavior)을 안전하게 수행할 수 있다는 아키텍처 문제는 유사하다.

화물 무인항공기(Cargo UAV)와 피지컬 AI(Physical AI) 아키텍처에서 가장 유용하게 적용할 수 있는 WTB 개념은 철도에 특화된 전기적 인터페이스 자체가 아니라 동적 시스템 구성(Dynamic System Formation)이다. 플릿(Fleet)에는 차량, 페이로드 모듈(Payload Module), 충전 인터페이스(Charging Interface), 임무 참여자가 추가되거나 제거될 수 있다. WTB와 유사한 아키텍처 원칙을 적용한다는 것은 새롭게 연결된 참여자가 협조 임무 동작에 영향을 미치도록 허용하기 전에 물리적 결합 또는 네트워크 접속 가능성과 논리적 구성원 자격(Logical Membership), 토폴로지 인식(Topology Recognition), 식별 관리(Identity Management), 운용 승인(Operational Authorization)을 분리하여 처리한다는 의미이다.

결국 WTB 열차 연결(WTB Train Coupling)은 변화하는 물리적 구성을 전제로 설계된 성숙한 통신 아키텍처의 대표적인 사례이다. 영구적으로 배선된 시스템을 가정하는 대신 토폴로지 구축(Topology Establishment)을 정상 운용 과정의 일부로 취급한다. 이러한 특성으로 인해 WTB는 이후 다루게 될 자동 열차 편성 인식(Automatic Train Consist Recognition), WTB 프레임 구성(WTB Frame Structure), 그리고 동적으로 구성되는 철도 네트워크와 협조형 자율 플릿(Coordinated Autonomous Fleet) 사이의 유사성을 이해하기 위한 중요한 기반이 된다.

## 03.02. Automatic Train Consist Recognition

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

자동 열차 편성 인식(Automatic Train Consist Recognition)은 IEC 61375 열차 통신 네트워크(Train Communication Network, TCN) 프레임워크에서 와이어 열차 버스(Wire Train Bus, WTB) 아키텍처의 핵심 기능이다. 이 기능을 통해 열차 통신 시스템은 현재 어떤 차량 또는 편성(Consist)이 연결되어 있는지를 판단하고, 조립된 열차의 논리적 표현(Logical Representation)을 구축할 수 있다. 철도 편성은 차량의 연결(Coupling), 분리(Uncoupling), 순서 변경 또는 방향 반전에 따라 달라질 수 있기 때문에 이러한 기능은 필수적이다.

열차 편성(Train Consist)은 일반적으로 하나의 기능적 단위로 운행되며 자체적인 내부 통신 구조를 포함하는 차량 그룹으로 이해할 수 있다. 여러 편성은 기계적·전기적으로 연결되어 하나의 완전한 열차를 구성할 수 있다. 이렇게 만들어진 열차 구성이 항상 고정되어 있는 것은 아니므로 통신 백본(Communication Backbone)은 사전에 정의된 토폴로지(Predefined Topology)에만 의존할 수 없다. 연결 이후 실제로 형성된 편성을 인식할 수 있어야 한다.

편성 인식(Consist Recognition)은 물리적 연결성(Physical Connectivity)과 논리적 네트워크 구성원 자격(Logical Network Membership)을 구분하는 것에서 시작한다. 기계식 커플러(Mechanical Coupler)는 철도 차량 사이의 물리적 관계를 형성하고, 전기 인터페이스(Electrical Interface)는 차량 간 통신 경로를 제공한다. 그러나 통신 경로가 존재한다는 사실만으로 전체 열차의 구성을 설명할 수는 없다. 네트워크는 어떤 통신 노드(Communication Node)가 존재하며 이들 노드가 실제 물리적 배열과 어떤 관계를 가지는지 판단해야 한다.

WTB 운용에서 이러한 과정은 네트워크 초기화(Network Inauguration)와 밀접하게 관련된다. 초기화(Inauguration)는 열차가 조립되거나 열차 구성이 변경된 이후 필요한 통신 구성을 설정한다. 참여 노드(Participating Node)는 서로 협력하여 현재 네트워크 구조를 식별하고, 감지된 열차 배열에 따라 스스로를 구성하며, 이후 주소 지정(Addressing)과 열차 전체 통신(Train-Wide Communication)에 사용할 수 있는 정보를 구축한다.

인식 과정에서는 단순히 연결된 통신 노드의 개수만 판단해서는 안 된다. 차량 또는 편성의 상대적인 순서(Relative Order)가 중요하다. 분산 철도 애플리케이션(Distributed Railway Application)은 열차 내부의 물리적 위치에 따라 데이터를 해석할 수 있기 때문이다. 편성의 한쪽 끝에 위치한 차량은 다른 차량과 맺는 물리적 관계가 중앙에 위치한 차량과 다르며, 두 차량이 동일하거나 유사한 통신 장비를 갖추고 있더라도 이러한 위치 관계는 구별되어야 한다.

철도 차량과 편성은 방향이 반전된 상태로 연결될 수도 있으므로 방향(Orientation) 역시 고려해야 한다. 참여 장치만 식별하고 상대적인 방향을 표현하지 않는 토폴로지 설명(Topology Description)은 완전하지 않다. 자동 인식 기능은 통신 시스템이 방향을 고려한 표현(Orientation-Aware Representation)을 구축하도록 하며, 이를 통해 서로 다른 연결 구성이 형성된 이후에도 열차 전체 애플리케이션이 차량 간 관계를 일관성 있게 해석할 수 있다.

현재의 편성 배열이 인식되면 통신 시스템은 논리적 통신 식별자(Logical Communication Identity)를 발견된 토폴로지와 연계할 수 있다. 이를 통해 네트워크 수준의 주소 지정(Network-Level Addressing)과 실제 열차 구성 사이에 사용할 수 있는 관계가 형성된다. 이후 애플리케이션은 백본을 순서가 없는 통신 장치의 집합으로 취급하는 대신, 각 참여 노드가 조립된 열차의 어느 위치에 속하는지를 이해하면서 정보를 교환할 수 있다.

자동 인식은 정상적인 철도 운용 과정에서 열차 구성이 변경될 때 특히 중요하다. 편성이 제거되거나 추가되거나 순서가 변경되면 이전 열차를 설명하던 정보가 더 이상 유효하지 않을 수 있다. 기존 논리 구성을 계속 사용하면 통신 시스템이 잘못된 위치나 참여자를 참조할 가능성이 있다. 따라서 토폴로지 관련 변경(Topology-Related Change)이 발생하면 새롭게 조립된 물리적 시스템에 맞추어 네트워크 구성을 다시 설정해야 한다.

이러한 동적 구성 기능(Dynamic Configuration Capability)은 WTB를 영구적으로 설치된 노드를 기반으로 설계된 네트워크와 구별하는 중요한 특징이다. 고정형 산업 기계(Fixed Industrial Machine)에서는 장치 주소와 네트워크 위치를 설계 단계에서 지정한 후 운용 기간 동안 변경하지 않는 경우가 많다. 그러나 철도 시스템에서는 항상 사전에 결정할 수 없는 다양한 차량 조합을 처리해야 한다. 따라서 자동 편성 인식은 토폴로지 관리를 오프라인 엔지니어링 활동(Offline Engineering Activity)에서 통신 시스템의 실제 운용 동작으로 확장한다.

편성 인식은 네트워크 관리(Network Management)와 애플리케이션 기능(Application Functionality) 사이의 중요한 경계도 형성한다. 열차 애플리케이션이 통신을 시작할 때마다 물리적 편성을 독립적으로 재구성해서는 안 된다. 대신 네트워크 인프라(Network Infrastructure)가 인식된 토폴로지를 기반으로 체계화된 통신 환경을 제공한다. 상위 수준 기능은 전체 백본 구조를 직접 발견하기 위한 기본 메커니즘을 각각 구현하지 않고도 이러한 환경을 활용하여 협조 운용(Coordinated Operation)을 수행할 수 있다.

WTB와 다기능 차량 버스(Multifunction Vehicle Bus, MVB)의 관계는 이러한 계층 구조를 더욱 명확하게 보여준다. MVB는 차량 또는 편성 내부의 장치 사이에서 통신을 제공할 수 있으며, WTB는 이러한 차량 수준 통신 영역을 열차 전체에 걸쳐 연결한다. 따라서 자동 편성 인식은 열차 백본 수준(Train-Backbone Level)에서 동작하여 더 큰 통신 단위들이 어떻게 구성되어 있는지를 결정하고, 내부 장치 네트워크는 자체적인 로컬 구조와 역할을 유지할 수 있다.

게이트웨이(Gateway)는 이러한 서로 다른 통신 범위 사이의 경계에서 중요한 역할을 수행한다. 차량 내부 네트워크의 장비에서 생성된 정보는 열차 수준 통신 아키텍처를 통해 열차의 다른 영역에 제공될 수 있다. 열차 토폴로지가 이미 구축되어 있기 때문에 게이트웨이와 애플리케이션은 항상 동일한 인접 편성이나 물리적 배열이 유지된다고 가정하지 않고, 현재 확인된 백본 구조를 기반으로 동작할 수 있다.

신뢰성(Reliability) 관점에서 자동 인식은 구성 변경에 체계적으로 대응할 수 있는 방법도 제공한다. 새롭게 연결된 통신 참여자는 단순히 전기적 신호가 감지되었다는 이유만으로 운용 중인 열차의 구성원으로 간주되어서는 안 된다. 변경된 편성을 기반으로 정상적인 열차 전체 통신을 수행하기 전에 네트워크는 일관성 있는 토폴로지(Coherent Topology)를 구축해야 한다. 이를 통해 네트워크 구성원과 물리적 조직에 대한 서로 다른 가정을 기반으로 시스템이 동작할 위험을 줄일 수 있다.

진단(Diagnostics) 기능 역시 인식된 열차 구조를 활용할 수 있다. 통신 문제를 현재 구성과 연관하여 해석할 수 있기 때문이다. 구축된 토폴로지 내부에 존재해야 하는 차량이나 통신 세그먼트(Communication Segment)가 사용할 수 없는 상태가 되면 진단 기능은 통신 장애(Communication Failure)와 의도적인 구성 변경(Intentional Configuration Change)을 보다 체계적으로 구분할 수 있다. 따라서 정확한 토폴로지 정보는 정상 운용뿐만 아니라 네트워크 상태에 대한 유지보수 중심의 해석에도 활용될 수 있다.

자동 열차 편성 인식(Automatic Train Consist Recognition)은 모듈형 로보틱스(Modular Robotics)와 피지컬 AI(Physical AI) 시스템에도 유용한 아키텍처적 유사성을 제공한다. 자율이동로봇(Autonomous Mobile Robot), 무인항공기(UAV), 매니퓰레이터(Manipulator), 탈착식 임무 모듈(Detachable Mission Module)은 동적으로 결합하여 일시적인 운용 시스템을 구성할 수 있다. 네트워크 연결 가능성(Network Reachability)만으로 발견된 모든 참여자가 즉시 협조 제어(Coordinated Control)에 참여할 수 있는 것은 아니다. 먼저 식별 정보(Identity), 위치(Position), 역할(Role), 방향(Orientation), 구성원 자격(Membership)을 확립해야 할 수 있다.

화물 무인항공기 플릿(Cargo UAV Fleet)에서도 이와 유사한 메커니즘을 통해 현재 협조 운용에 참여하는 항공기 또는 임무 모듈을 인식하고, 분산 임무 실행(Distributed Mission Execution)을 시작하기 전에 이들의 논리적 관계를 설정할 수 있다. 기반 통신 기술은 WTB가 아니라 이더넷(Ethernet), 무선 네트워크(Wireless Networking) 또는 다른 현대적 프로토콜일 수 있지만 시스템 원칙은 동일하다. 즉, 참여자를 발견하고, 토폴로지를 구축하고, 운용 관계를 할당한 후 협조 통신을 활성화하는 것이다.

보다 넓은 관점에서 얻을 수 있는 핵심 교훈은 동적인 물리적 구성(Dynamic Physical Composition)에는 동적인 통신 구성(Dynamic Communication Organization)이 필요하다는 것이다. 자동 열차 편성 인식은 새롭게 조립된 철도 차량 집합을 단순히 연결된 통신 인터페이스의 집합에서 논리적으로 구성된 열차 네트워크(Logically Organized Train Network)로 변환한다. WTB 열차 연결(WTB Train Coupling)과 함께 WTB 프레임 교환(WTB Frame Exchange) 및 상위 수준 열차 전체 기능이 동작할 수 있는 기반을 구축하며, 동시에 동적으로 구성되는 자율 시스템(Dynamically Composed Autonomous System)을 이해하기 위한 유용한 모델을 제공한다.

## 03.03. WTB Frame Structure

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

와이어 열차 버스(Wire Train Bus, WTB) 프레임 구조(Frame Structure)는 IEC 61375 열차 통신 네트워크(Train Communication Network, TCN)의 열차 수준 백본(Train-Level Backbone)에서 사용되는 체계적인 데이터 전송 메커니즘을 제공한다. 열차 연결(Train Coupling)과 자동 편성 인식(Automatic Consist Recognition)을 통해 현재 편성에 어떤 노드가 참여하는지 결정한 이후, WTB 통신에서는 차량 간 정보를 예측 가능한 방식으로 교환하기 위한 정의된 프레이밍 방식(Framing Method)이 필요하다. 따라서 프레임 구조는 동적인 열차 구성과 통제된 운용 통신을 연결한다.

WTB 통신은 여러 차량 또는 편성(Consist)이 하나의 공통 열차 백본(Common Train Backbone)을 공유하는 분산 철도 환경(Distributed Railway Environment)을 위해 설계되었다. 프레임(Frame)은 이러한 네트워크를 통해 프로토콜 정보와 애플리케이션 관련 데이터를 전달하는 구조화된 단위를 제공한다. 장치가 임의의 비트열(Bit Sequence)을 전송하도록 하는 대신 통신 시스템은 수신 노드가 일관성 있게 해석할 수 있도록 정의된 필드(Field)와 전송 규칙에 따라 정보를 구성한다.

통신 프레임의 구조는 여러 기능을 동시에 지원해야 한다. 수신기는 전송을 인식하고, 해당 정보가 자신과 관련되어 있는지 판단하며, 전달된 정보를 해석하고, 통신이 올바르게 수신되었는지를 검증할 수 있는 충분한 프로토콜 정보를 필요로 한다. 따라서 프레이밍(Framing)은 단순한 데이터 포장 기술이 아니다. 프레이밍은 분산된 열차 노드 사이의 결정론적 통신(Deterministic Communication)에 필요한 경계, 해석 규칙, 무결성 메커니즘(Integrity Mechanism)을 설정한다.

WTB는 물리적인 열차 구성이 변경될 수 있는 상황에서도 네트워크 동작을 예측 가능하게 유지해야 하는 통신 아키텍처에서 동작한다. 초기화(Inauguration)를 통해 유효한 논리 토폴로지(Logical Topology)가 구축되면 프레임 교환 메커니즘(Frame Exchange Mechanism)은 설정된 구성 내부에서 동작한다. 이러한 구분은 중요하다. 초기화는 어떤 노드가 존재하고 열차가 어떻게 구성되어 있는지를 결정하며, 프레임 통신은 인식된 참여자들이 운용 정보를 반복적으로 교환하는 메커니즘을 제공한다.

WTB 프레임을 개념적으로 이해하는 유용한 방법은 제어 중심의 프로토콜 정보(Control-Oriented Protocol Information)와 전송되는 페이로드(Payload)를 구분하는 것이다. 프로토콜 관련 필드는 통신 시스템이 전송을 관리하고 해석할 수 있도록 하며, 데이터 필드는 열차 기능에 필요한 정보를 전달한다. 무결성 관련 정보(Integrity-Related Information)는 수신기가 통신 오류를 감지할 수 있도록 한다. 이러한 요소들이 결합되어 백본의 물리적 비트 스트림(Bit Stream)을 의미 있고 검증 가능한 프로토콜 트랜잭션(Protocol Transaction)으로 변환한다.

주소 지정(Addressing)과 통신 관계는 인식된 열차 토폴로지와 밀접하게 연결되어 있다. 초기화 과정에서 노드가 구성된 이후 프레임 교환은 현재 편성에 대해 구축된 논리적 통신 구조(Logical Communication Structure)에 따라 참여자를 참조할 수 있다. 따라서 네트워크가 먼저 필요한 인식 및 구성 절차를 완료한다면 서로 다른 편성이 연결된 이후에도 동일한 통신 아키텍처를 적용하여 운용할 수 있다.

WTB 통신은 서로 다른 종류의 정보 교환도 처리해야 한다. 철도 네트워크에는 정기적으로 갱신해야 하는 주기적 프로세스 정보(Cyclic Process Information)가 존재하며, 이벤트(Event), 관리(Management), 진단(Diagnostics) 또는 기타 통신 요구와 관련하여 상대적으로 낮은 빈도로 전달되는 정보도 존재한다. 따라서 프로토콜 구조는 반복적인 운용 데이터와 특정 트랜잭션이나 조건이 요구할 때 전송되는 정보 모두에 적합한 통신 동작을 지원해야 한다.

주기적 프로세스 통신(Cyclic Process Communication)은 많은 운용 상태를 지속적으로 갱신해야 하므로 분산 열차 제어에서 특히 중요하다. 협조 차량 기능(Coordinated Vehicle Function)과 관련된 정보는 충분히 예측 가능한 타이밍으로 전달될 때 의미가 있다. 따라서 WTB는 제한 없는 네트워크 처리량(Network Throughput)을 최대화하는 것보다 전송 스케줄링(Transmission Scheduling), 제한된 통신 동작(Bounded Communication Behavior), 공유 매체에 대한 통제된 접근(Controlled Medium Access)이 더욱 중요한 결정론적 통신 시스템의 한 종류로 볼 수 있다.

마스터 제어 통신 원칙(Master-Controlled Communication Principle)은 전통적인 WTB 운용의 핵심 요소이다. 모든 노드가 열차 버스에 자유롭게 접근하기 위해 경쟁하도록 하는 대신, 통신은 제어된 프로토콜 동작에 따라 교환이 이루어지도록 조정된다. 이를 통해 버스 접근의 불확실성을 줄이고 결정론적 타이밍(Deterministic Timing)을 확보하는 데 기여한다. 따라서 프레임 구조는 개별 프로토콜 트랜잭션이 언제 발생하는지를 결정하는 매체 접근(Medium Access) 및 스케줄링 메커니즘과 함께 이해해야 한다.

이러한 통제된 교환에서는 하나의 전송이 통신 동작을 시작하거나 요청하고, 다른 전송이 이에 대응하는 응답을 제공할 수 있다. 따라서 개별 프레임의 의미는 프레임 내부의 필드뿐만 아니라 프로토콜 트랜잭션 내에서 해당 프레임이 차지하는 위치에 의해서도 결정된다. 이러한 트랜잭션 중심 해석(Transaction-Oriented Interpretation)은 결정론적 철도 통신에서 올바른 형식의 데이터뿐만 아니라 정확하게 조정된 통신 순서도 필요하기 때문에 중요하다.

철도 통신은 전기적·기계적으로 가혹한 환경에서 동작하기 때문에 프레임 무결성(Frame Integrity)이 매우 중요하다. 긴 차량 편성, 차량 간 커넥터(Inter-Vehicle Connector), 반복적인 연결 과정, 전자기적 교란(Electromagnetic Disturbance), 진동(Vibration)은 물리적 통신 경로에 영향을 줄 수 있다. 프레임 전송과 연계된 오류 검출 정보(Error-Detection Information)를 이용하면 수신 노드는 관찰된 모든 비트열을 유효한 데이터로 자동 수용하는 대신, 전송된 정보가 프로토콜의 무결성 검사를 만족하는지 판단할 수 있다.

유효하지 않은 프레임(Invalid Frame)을 검출했다고 해서 원래 정보를 자동으로 복원할 수 있는 것은 아니다. 대신 무결성 메커니즘은 손상된 통신을 거부하고 상위 프로토콜 동작, 반복되는 주기적 업데이트, 진단 또는 시스템 수준 고장 처리(System-Level Fault Handling)가 적절하게 대응할 수 있는 기반을 제공한다. 이러한 구분은 오류 검출(Error Detection), 오류 정정(Error Correction), 이중화(Redundancy), 기능 안전 메커니즘(Functional Safety Mechanism)이 서로 다른 보호 계층을 구성한다는 점에서 안전 관련 엔지니어링에 중요하다.

타이밍(Timing)은 시스템 수준에서 WTB 프레임을 해석하는 방법에도 영향을 준다. 프레임 자체의 구조가 올바르더라도 정보가 지나치게 늦게 도착하거나 더 이상 충분한 최신성(Freshness)을 갖지 못한다면 애플리케이션에 적합하지 않을 수 있다. 따라서 결정론적 통신은 데이터 무결성과 시간적 동작(Temporal Behavior)을 결합한다. 철도 애플리케이션은 메시지가 올바르게 수신되었는지만 확인하는 것이 아니라 분산 기능에서 가정한 시간 범위 내에 수신되었는지도 고려해야 한다.

WTB와 다기능 차량 버스(Multifunction Vehicle Bus, MVB)의 관계는 또 다른 중요한 아키텍처 관점을 제공한다. MVB는 차량 또는 편성 내부의 장치 간 통신을 구성할 수 있으며, WTB는 선택된 정보를 열차 수준 백본을 통해 전송한다. 따라서 이들 통신 영역 사이의 게이트웨이(Gateway)는 한쪽 통신 환경에서 정보를 수신하고 필요한 경우 이를 매핑(Mapping)하거나 처리한 후 다른 네트워크 영역에서 적절한 데이터를 사용할 수 있도록 제공할 수 있다.

이러한 계층형 아키텍처(Layered Architecture)를 통해 모든 로컬 장치가 열차 백본 프로토콜에 직접 참여할 필요가 없어진다. 센서(Sensor), 컨트롤러(Controller), 액추에이터(Actuator), 진단 장치(Diagnostic Device)는 차량 내부 네트워크를 통해 통신할 수 있으며, 게이트웨이 기능은 열차 수준에서 필요한 정보만 외부에 제공할 수 있다. 따라서 WTB 프레임은 개별 전자 장치 사이를 이동하는 독립적인 패킷이라기보다 분산된 차량 통신 영역을 연결하는 정보 계층(Information Hierarchy)의 일부로 이해할 수 있다.

진단(Diagnostics)과 네트워크 감시(Network Supervision) 역시 구조화된 통신 동작에 의존한다. 유효한 프레임은 정의된 프로토콜 규칙을 따르기 때문에 통신 장비는 누락된 교환(Missing Exchange), 잘못된 형식의 정보(Malformed Information), 무결성 실패(Integrity Failure), 예상하지 못한 네트워크 동작을 감지할 수 있다. 이러한 관찰 결과를 열차 초기화 과정에서 구축된 토폴로지와 결합하면 유지보수 시스템은 통신 이상을 특정 노드, 차량 관계 또는 열차 백본 구간과 연계할 수 있다.

WTB 프레이밍 개념(WTB Framing Concept)은 모듈형 로봇(Modular Robot), 자율주행 차량(Autonomous Vehicle), 무인항공기 플릿(UAV Fleet)에도 유용한 시사점을 제공한다. 현대 피지컬 AI(Physical AI) 시스템에서는 WTB 대신 이더넷(Ethernet), 데이터 분산 서비스(Data Distribution Service, DDS), 시간 민감형 네트워킹(Time-Sensitive Networking, TSN), CAN 또는 무선 링크(Wireless Link)를 사용할 수 있지만, 원시 연결성(Raw Connectivity)을 구조화된 통신으로 변환해야 한다는 아키텍처 요구는 동일하다. 신원(Identity), 메시지 유형(Message Type), 페이로드 해석(Payload Interpretation), 무결성, 타이밍, 통신 권한(Communication Authority)이 정의되어야 분산 기계가 신뢰성 있게 협조할 수 있다.

화물 무인항공기 플릿(Cargo UAV Fleet)에 적용할 수 있는 핵심 원칙은 협조 운용(Coordinated Operation)에 단순한 네트워크 연결 이상의 요소가 필요하다는 것이다. 플릿 구성원이 발견되고 운용 관계가 설정된 이후에는 임무 상태(Mission State), 항법 협조(Navigation Coordination), 상태 건전성 감시(Health Monitoring), 페이로드 상태(Payload Status), 고장 정보(Fault Information)를 전달하기 위해 명확하게 정의된 메시지 구조와 타이밍 규칙을 사용해야 한다. WTB는 토폴로지 관리와 결정론적 데이터 교환을 분리하면서도 시스템 수준에서는 긴밀하게 통합할 수 있음을 보여준다.

따라서 WTB 프레임 구조(WTB Frame Structure)는 인식된 열차 토폴로지와 분산 철도 기능 사이를 연결하는 운용 통신 계층(Operational Communication Layer)을 형성한다. 열차 연결은 물리적 연결성(Physical Connectivity)을 구축하고, 자동 편성 인식은 논리적 구성(Logical Organization)을 설정하며, 구조화된 프레임 교환(Structured Frame Exchange)은 이러한 구성 전체에 걸쳐 통제된 정보를 전달한다. 이러한 단계적 구조는 전체 열차 통신 네트워크(TCN) 아키텍처를 이해하고 철도의 결정론적 네트워킹 원칙을 협조형 자율 시스템(Coordinated Autonomous System)의 통신 아키텍처와 비교하기 위한 기반을 제공한다.

## 03.04. WTB UAV Swarm Analogy

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

와이어 열차 버스(Wire Train Bus, WTB)는 동적으로 구성되는 무인항공기 군집(UAV Swarm)의 통신을 이해하는 데 유용한 아키텍처적 유사성(Architectural Analogy)을 제공한다. IEC 61375 열차 통신 네트워크(Train Communication Network, TCN)에서 WTB는 연결(Coupling)과 분리(Uncoupling)를 통해 구성원과 배열이 변경될 수 있는 차량 편성(Consist)을 연결한다. UAV 군집 역시 항공기가 동적으로 참여하거나 이탈하고, 재구성되거나 새로운 역할을 맡으면서도 협조 운용(Coordinated Operation)을 지속해야 한다는 유사한 시스템 문제를 가진다.

이러한 유사성은 물리적 측면보다는 주로 아키텍처적 측면에 있다. 철도 차량은 유선 열차 백본(Wired Train Backbone)을 통해 통신하는 반면, UAV는 일반적으로 무선 데이터링크(Wireless Datalink)에 의존하며 직접 링크(Direct Link), 메시 네트워크(Mesh Network), 인프라(Infrastructure) 또는 이들을 조합한 방식으로 통신할 수 있다. 그러나 두 시스템 모두 독립적으로 운용되는 여러 플랫폼을 참여자와 상호 관계가 파악된 체계적인 통신 영역(Organized Communication Domain)으로 변환해야 한다.

WTB 열차 연결(WTB Train Coupling)은 개념적으로 군집 형성(Swarm Formation)에 대응한다. 철도 편성이 기계적·전기적으로 연결되면 통신 네트워크가 최종적인 열차 구성을 판단하기 전에 물리적 연결성이 먼저 형성된다. 마찬가지로 다른 UAV와 무선 링크가 감지되었다고 해서 해당 UAV가 자동으로 운용 군집의 구성원이 되는 것은 아니다. 새로운 참여자에게 협조 임무 기능을 의존하기 전에 발견(Discovery), 식별(Identification), 인증(Authentication), 역할 할당(Role Assignment), 구성(Configuration)이 이루어져야 한다.

자동 열차 편성 인식(Automatic Train Consist Recognition)은 특히 강력한 유사성을 제공한다. WTB는 현재 열차에 어떤 편성이 참여하는지 인식하고 이들의 상대적인 구성을 설정해야 한다. UAV 군집에서도 현재 어떤 항공기가 활성 상태인지, 어떤 항공기가 이탈하거나 고장 났는지, 어떤 항공기가 새롭게 참여했는지를 판단하기 위한 유사한 구성원 인식(Membership Awareness)이 필요하다. 이렇게 생성된 군집 표현(Swarm Representation)은 단순한 무선 연결성에 의존하지 않고 분산 협조(Distributed Coordination)를 수행하기 위한 논리적 기반이 된다.

철도의 토폴로지 인식(Topology Recognition) 개념은 UAV 군집의 공간적 관계(Spatial Relationship)로 확장할 수 있다. 열차 토폴로지는 연결된 차량의 순차적인 물리적 배열에 크게 제한되지만 UAV 군집은 동적인 2차원 또는 3차원 공간에서 운용된다. 따라서 군집 토폴로지(Swarm Topology)는 단순한 선형 차량 순서 대신 통신 이웃(Communication Neighbor), 상대 위치(Relative Position), 편대 위치(Formation Location), 임무 역할(Mission Role), 연결 품질(Connectivity Quality), 라우팅 관계(Routing Relationship)를 포함할 수 있다.

방향(Orientation)은 두 시스템의 또 다른 중요한 차이를 보여준다. WTB는 편성이 서로 다른 방향으로 연결될 수 있는 시스템에서 차량 간 관계를 인식한다. UAV는 기수 방향(Heading), 고도(Altitude), 속도(Velocity), 자세(Attitude), 상대 기하 관계(Relative Geometry)가 지속적으로 변할 수 있기 때문에 더욱 풍부한 표현이 필요하다. 여기서 적용할 수 있는 핵심 원칙은 철도의 특정 표현 방식 자체가 아니라 통신 구성이 협조 시스템 동작에 필요한 물리적 관계를 반영해야 한다는 점이다.

WTB 초기화(WTB Inauguration)는 동적으로 조립된 시스템이 정상 운용을 시작하기 전에 어떻게 유효한 논리 네트워크(Logical Network)를 구축할 수 있는지를 보여준다. UAV 군집에서도 이와 유사한 초기화(Initialization) 또는 참여 승인 과정(Admission Process)을 적용할 수 있다. 새롭게 발견된 항공기는 식별 정보와 능력 정보를 알리거나 교환하고, 통신 관계를 구축하며, 필수 상태를 동기화하고, 임무 역할을 부여받은 후 협조 임무 실행에 참여할 수 있는 승인된 구성원이 될 수 있다.

네트워크 구성원 자격(Network Membership)과 운용 승인(Operational Authorization)의 구분은 무선 자율 시스템에서 더욱 중요해진다. 무선 통신이 가능한 UAV라고 하더라도 다른 임무에 속해 있거나 필요한 기능을 갖추지 못했거나 협조 제어에 참여하도록 신뢰할 수 없는 대상일 수 있다. 따라서 WTB에서 영감을 얻은 아키텍처는 연결성(Connectivity), 발견, 식별, 구성원 자격, 역할 할당, 임무 중요 정보(Mission-Critical Information) 교환 권한을 명시적인 단계로 분리할 필요성을 제시한다.

WTB 프레임 통신(WTB Frame Communication)은 또 다른 적용 가능한 개념을 제공한다. 열차 토폴로지가 구축된 이후에는 구조화된 프로토콜 교환(Structured Protocol Exchange)을 통해 인식된 참여자 사이에서 운용 정보를 전달한다. UAV 군집에서도 위치(Position), 속도, 임무 상태(Mission State), 건전성 상태(Health Status), 페이로드 정보(Payload Information), 편대 명령(Formation Command), 충돌 회피(Collision Avoidance), 고장 보고(Fault Reporting)를 위한 명확하게 정의된 메시지 구조(Message Structure)가 필요하다. 연결성만으로는 분산 자율 플랫폼 사이의 예측 가능한 상호운용성(Interoperability)을 제공할 수 없다.

통신이 협조 움직임(Coordinated Motion)에 영향을 미치는 경우 결정론적 동작(Deterministic Behavior)은 특히 중요하다. 철도 네트워크는 분산 열차 기능이 제한된 정보 교환 시간에 의존하기 때문에 통제되고 예측 가능한 통신을 중요하게 다룬다. UAV 군집 네트워크는 가변적인 무선 지연(Variable Wireless Latency)과 패킷 손실(Packet Loss)이라는 서로 다른 물리적 제약을 갖지만, 제한된 타이밍 요구사항(Bounded Timing Requirement), 메시지 우선순위(Message Priority), 최신성 감시(Freshness Monitoring), 동기화(Synchronization), 지연되거나 누락된 정보에 대한 명시적인 처리에서 동일한 이점을 얻을 수 있다.

WTB의 마스터 제어 통신(Master-Controlled Communication) 개념은 중앙집중형(Centralized) 또는 리더 협조형(Leader-Coordinated) 군집 아키텍처와 비교할 수 있다. 지정된 군집 리더(Swarm Leader) 또는 임무 조정자(Mission Coordinator)가 활동을 스케줄링하고 명령을 배포하거나 공유 임무 상태(Shared Mission State)를 유지할 수 있다. 그러나 UAV 시스템은 영구적인 마스터가 존재하지 않는 분산형(Decentralized) 또는 분산 협조형(Distributed Coordination) 구조를 사용할 수도 있다. 따라서 이러한 유사성은 철도의 마스터 메커니즘을 그대로 재현해야 한다는 의미가 아니라 협조 기능(Coordination Function)의 필요성을 보여준다.

동적 재구성(Dynamic Reconfiguration)은 WTB와 UAV 군집 통신 사이에서 가장 강한 유사성을 갖는 요소 중 하나이다. 철도 편성이 추가되거나 제거되면 네트워크는 열차에 대한 현재의 인식을 갱신해야 한다. 마찬가지로 군집은 항공기가 새롭게 참여하거나 의도적으로 이탈하고, 통신이 끊기거나 고장이 발생하며, 편대를 유지할 수 없는 상태가 될 때 대응해야 한다. 기존 구성원에 대한 오래된 가정이 지속되지 않도록 논리적 군집 구조(Logical Swarm Structure)를 갱신해야 한다.

고장 격리(Fault Isolation) 역시 토폴로지 인식(Topology Awareness)의 이점을 활용할 수 있다. 특정 열차 차량과의 통신이 사라지면 WTB 관련 감시 기능은 기존에 구축된 열차 구성을 기준으로 해당 이벤트를 해석할 수 있다. UAV 군집에서도 참여자의 손실은 구성원 정보 갱신, 경로 변경(Route Change), 편대 조정(Formation Adjustment), 임무 재분배(Mission Redistribution), 성능 저하 운용 모드(Degraded Operating Mode)를 발생시킬 수 있다. 따라서 통신 감시는 자율 시스템의 회복탄력성(Resilience)과 직접적으로 연결된다.

MVB-WTB 계층 구조(MVB-to-WTB Hierarchy)는 UAV 내부 네트워크와 외부 네트워크의 관계에도 유용한 유사성을 제공한다. UAV 내부에는 항공전자장비(Avionics), 센서, 비행 제어기(Flight Controller), 페이로드 제어기(Payload Controller), 컴퓨팅 장치가 있으며 이들은 온보드 통신 네트워크(Onboard Communication Network)를 통해 연결된다. 이와 별도의 플릿 또는 군집 통신 계층(Fleet or Swarm Communication Layer)은 항공기 사이에서 선택된 정보를 교환한다. 따라서 게이트웨이(Gateway)는 고주파 내부 제어 트래픽과 군집 전체에 분산되어야 하는 정보를 분리한다.

이러한 분리는 확장 가능한 피지컬 AI(Physical AI) 시스템에서 특히 중요하다. 원시 카메라 스트림(Raw Camera Stream), 라이다 측정값(LiDAR Measurement), 모터 제어 루프(Motor-Control Loop), 고주파 액추에이터 데이터(High-Frequency Actuator Data)는 일반적으로 전체 플릿에 지속적으로 방송할 필요가 없다. 대신 온보드 처리(Onboard Processing)를 통해 로컬 관측을 압축된 상태(State), 의도(Intent), 궤적(Trajectory), 건전성(Health), 의미 정보(Semantic Information)로 변환할 수 있다. 이후 군집 네트워크는 개별 차량을 넘어 전체 시스템에 가치가 있는 정보를 전달한다.

화물 무인항공기 시스템(Cargo UAV System)은 개별 항공기가 서로 다른 페이로드를 운반하고, 서로 다른 에너지 잔량을 가지며, 서로 다른 임무 역할을 수행할 수 있기 때문에 실용적인 사례를 제공한다. 따라서 군집 구성원 정보에는 식별 정보와 위치뿐만 아니라 능력 기술 정보(Capability Descriptor)도 포함할 수 있다. 임무 조정자는 이러한 정보를 이용하여 현재 플릿 구성과 운용 상태에 따라 운송(Transport), 중계(Relay), 검사(Inspection), 호위(Escort), 비상 대응(Contingency) 기능을 할당할 수 있다.

UAV 그룹을 영구적으로 구성된 네트워크가 아니라 일시적인 사이버 물리 조직(Temporary Cyber-Physical Organization)으로 간주하면 이러한 유사성은 더욱 중요해진다. 항공기는 서로 다른 위치에서 출동하여 임무를 위해 집결하고, 여러 하위 그룹(Subgroup)으로 분리되며, 충전을 위해 복귀한 후 나중에 다른 편대에 참여할 수 있다. 따라서 통신 아키텍처는 시스템 수명 전체에 걸쳐 하나의 정적인 네트워크 구성(Static Network Configuration)을 가정하지 않고 반복적인 형성과 해체를 지원해야 한다.

보안(Security)은 기본적인 철도 유사성에서는 상대적으로 덜 드러나지만 UAV 군집에서는 필수적인 요구사항을 추가한다. 무선 연결은 승인되지 않은 참여자(Unauthorized Participant), 위조된 식별 정보(Spoofed Identity), 조작된 메시지(Manipulated Message), 통신 방해(Communication Disruption)의 가능성을 증가시킨다. 따라서 군집 참여 승인(Swarm Admission)은 토폴로지 발견과 함께 인증(Authentication), 권한 부여(Authorization), 메시지 무결성(Message Integrity), 안전한 식별 관리(Secure Identity Management)를 결합해야 한다. 동적 인식은 단순히 누가 존재하는 것처럼 보이는지를 판단하는 것이 아니라 누가 실제로 참여할 권한을 갖는지를 확립해야 한다.

따라서 WTB 유사성(WTB Analogy)을 철도 프로토콜 자체를 UAV 통신에 직접 적용하자는 제안으로 해석해서는 안 된다. WTB는 연결된 철도 차량과 유선 열차 백본의 특성을 위해 설계된 반면 UAV 군집은 매우 동적인 무선 환경에서 운용된다. WTB가 제공하는 가치는 동적 구성원 인식(Dynamic Membership Recognition), 논리 토폴로지 구축(Logical Topology Establishment), 구조화된 통신(Structured Communication), 결정론적 협조(Deterministic Coordination), 감시(Supervision), 재구성(Reconfiguration)이라는 시스템 원칙에 있다.

피지컬 AI(Physical AI)에서는 이러한 원칙을 UAV뿐만 아니라 자율이동로봇 플릿(AMR Fleet), 사족보행 로봇 팀(Quadruped Team), 자율주행 차량, 모바일 매니퓰레이터(Mobile Manipulator), 이기종 로봇 그룹(Heterogeneous Robot Group)으로 일반화할 수 있다. 각각의 개별 플랫폼은 자체적인 로컬 센싱(Local Sensing), 제어(Control), 지능(Intelligence)을 유지하면서 동적으로 구축되는 집단 통신 구조(Collective Communication Structure)에 참여할 수 있다. 이를 통해 개별 구성원의 운용 자율성을 제거하지 않으면서 전체 시스템이 분산된 동작을 협조할 수 있다.

따라서 WTB는 독립적으로 기능하는 기계들이 구성이 변경된 이후 어떻게 하나의 협조 시스템(Coordinated System)이 될 수 있는지를 보여주는 성숙한 철도 사례를 제공한다. UAV 군집 유사성에서는 열차 연결(Coupling)이 동적 구성원 자격(Dynamic Membership)으로, 편성 인식(Consist Recognition)이 군집 발견(Swarm Discovery)으로, 열차 토폴로지(Train Topology)가 플릿 구성(Fleet Organization)으로, WTB 프레임 교환(WTB Frame Exchange)이 구조화된 에이전트 간 메시징(Structured Inter-Agent Messaging)으로, 네트워크 재초기화(Network Re-Inauguration)가 군집 재구성(Swarm Reconfiguration)으로 대응된다. 이러한 대응 관계는 철도 통신 아키텍처에서 확장 가능한 피지컬 AI 협조(Scalable Physical AI Coordination)로 이어지는 개념적 연결고리를 제공한다.
