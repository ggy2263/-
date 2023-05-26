# -3D 당구게임 개발 프로젝트

1.1. 연구배경

 참신하고 재미있는 게임을 생각해보던 중 기존의 당구 게임을 3D 공간으로 확장하면 현실세계의 물리 법칙의 구현을 가상 현실에 옮김으로써 도전과 재미를 모두 함께 할 수 있다고 생각함. 또한 기존의 물리 시뮬레이터를 활용하는 대신 직접 현실의 물리 법칙을 구현하는 것은 큰 도전이 될 것.
 
 2. 관련연구

![image](https://github.com/ggy2263/-/assets/81802704/0bfbd6df-bd3b-42aa-addc-d87b0c7d198d)

3.제안 연구의 중요성/독창성

기존의 물리 엔진이 아닌 독자적인 구현으로 기존의 엔진과 달리 독자적으로 수정 가능한 물리 시스템 구현 가능, 이를 통해 좀 더 현실적인 물리 시스템으로 발전 시킬 수 있음.

2.2. 기존 연구의 문제점 및 해결 방안
2.2.1. 연구의 문제점 
기존 당구 게임은 현실의 물리 법칙의 구현이 엔진의 한계로 잘 구현 되어 있지 않으며 공간 역시 2D 공간이라는 한계가 있음.
2.5.2. 해결 방안

직접 개발한 물리 시스템으로 당구 게임을 구현하여 좀 더 현실적인 움직임을 구현. 구체적으로는 일차적으로 당구 게임을 구현한다. 이후 구현한 당구게임을 3D공간으로 확장한다. 게임의 형식으로 동작 할 수 있어야 한다. 현실의 당구 게임의 법칙을 이용해 플레이 할 수 있어야 한다. 현실의 물리 법칙과 최대한 유사하게 동작한다. 이를 위해서 첫번째로 해결해야 하는 문제는 구체 형태의 당구공 오브젝트에 실제 당구처럼 길다란 막대기 형태의 충돌이 줄 수 있는 특정한 점에서 방향과 세기를 가진 힘을 가해 특정한 회전과 이동을 구현하는 것이다. 이후 이를 3D 공간으로 확장하는 것을 통해서 3D 당구게임의 구현이 가능하다.
이때 기존 엔진에서는 이러한 것들을 이용하여 마찰과 회전 충돌을 구현했다.
.
선형 댐핑(Linear Damping)	가해지면 선형 이동을 줄이는 '항력'입니다.
각 댐핑(Angular Damping)	가해지면 각 이동을 줄이는 '항력'입니다.
안정화 한계치 배수(Stabilization Threshold Multiplier)	피직스 안정화 기능이 활성화된 경우 이 바디에 적용되는 안정화 지수입니다. 숫자가 클수록 바디가 더욱 적극적으로 안정화되지만, 저속에서 운동량이 줄어들 수 있습니다. 값이 0이면 이 바디가 안정화되지 않습니다.
관성 텐서 스케일(Inertia Tensor Scale)	인스턴스별 관성 스케일링입니다. 값이 클수록 회전이 어렵습니다.


이후 제작되는 게임에서는 power라고 하는 변수를 이용해 x,y,z의 운동량에 해당하는
값을 주었다. 이때 감쇠를 위해 일정한 틱마다 값이 줄어들게 하였으며 충돌시에는 3차원에서의 충돌을 예상하여 적용한다. 이후 회전 값 역시 동일하게 구현하며 회전은 선 이동에 영향을 줄 수 있도록한다.
 
3. 프로젝트 내용
3.1. 시나리오
3.1.1 선형 움직임 구현

Power 변수를 설정하고 매 프레임마다 power 변수의 값이 일정한 비율로 줄어들게 하여 감쇠를 구현한다. 또한 power변수에 비례한 수치만큼 이동하도록 하여 선형 움직임을 구현한다.

3.1.2 선형 충돌 

.선형 충돌에서는 3차원 공간에서의 탄성 충돌의 구현을 위해 다음과 유사한 방식으로 동작한다

.
 [1]

이를 위해 3차원 공간에서 충돌하는 두 물체의 중심을 이용하여 두 물체의 충돌면의 법선 벡터를 구하고 충돌면을 기준으로 두 물체의 운동량을 교환하는 과정을 통해서 물체의 충돌을 구현하였다.

3.1.3 각운동량

 spin이라는 값을 통해서 x,y,z축을 기준으로 한 각 운동량을 설정해 주었으며 이는 선 운동량과
마찬가지로 매 프레임마다 조금씩 감쇠한다. 또한 각 운동량은 선 운동에 영향을 끼치도록 설정되었다.

3.2. 요구사항
 게임의 형식으로 동작 할 수 있어야 한다. 현실의 당구 게임의 법칙을 이용해 플레이 할 수 있어야 한다. 현실의 물리 법칙과 최대한 유사하게 동작한다.

이를 위해서 선 운동과 각 운동 그리고 충돌이 제대로 구현되어야 한다.
. 
3.3. 구현
 
시작시 초기값 할당
 
충돌시 시나리오 
 
평상시 회전과 이동




