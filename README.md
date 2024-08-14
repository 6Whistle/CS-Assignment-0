# 컴퓨터 구조 프로젝트 0 보고서

## 학번 : 2018202046

## 이름 : 이준휘

## 교수님 : 이성원

## 분반 : 월 3 , 수 4


## A. Result 2 - 1

### 1. What is the Transmission gate?

- Transmission gate란 n-MOS Transistor와 p-MOS Transistor의 양 끝을 결합하여 만든
    회로다.
    n-MOS Transistor는 G의 값이 0 일 때 D와 S 사이의 연결이 끊기고, G의 값이 1 일
    경우 전류가 흐른다. 다른 특징으로는 G의 값이 1 일 때(연결되어 있을 때) 0 을 잘
    통과시키고, 1 을 잘 통과시키지 못하는 특징이 있다.
    이와 반대로 p-MOS Transistor는 G의 값이 0 일 때 D와 S는 연결되고, G의 값이 0 일
    경우 끊긴다. 다른 특징도 n-MOS와 반대로 G의 값이 0 일 때(연결되어 있을 때) 0
    을 잘 통과시키지 못하고, 1 을 잘 통과시키는 특징이 있다.

```
이를 바탕으로 만든 Transmission gate는 외부의 신호 A에 의해서 전류를 흐르게
하거나 차단시키는 역할인 스위치의 역할을 할 수 있다.
```
```
Truth table INPUT : 0 INPUT : 1
A : 0 Z Z
A : 1 0 1
```
#### A가 1 일 경우 0 과 1 을 모두 잘 통과시키는 모습을 보인다. 해당 회로의 특이한

```
점을 본다면 A가 0 인 상태에서는 n-MOS와 p-MOS 모두 단선된 것과 같이
동작하여 Z상태를 가진다는 점이다. 이러한 이유로 인해 해당 회로는 MUX, BUS
등에서 다양하게 활용되고 있다.
```

### 2. Implement a MUX using Transmission gate

- MUX(Multiplexer)란 여러 개의 신호 중에서 하나의 신호를 선택해서 출력하는 회
    로를 말한다. MUX에 들어오는 INPUT의 개수를 n이라고 할 때 n개의 신호 중 1 개
    를 선택하기 위한 SELECT 신호의 비트의 수는 ⌈𝑙𝑜𝑔!𝑛⌉개로 표현할 수 있다.

```
MUX를 만드는 방법은 logic gate를 이용한 방법과 Transmission gate를 이용하는 방
법으로 나눌 수 있다. 이 중 Transmission gate를 활용한 설계는 아래와 같다.
```
```
일반적으로 많이 쓰이는 2 to 1 MUX의 경우에는 2 개의 Transmission gate를 위와 같
이 clk에 의해 선택할 수 있도록 만들 수 있다. 하나의 신호가 출력이면 다른 신
호는 Z상태이기 때문에 두 gate에서 나오는 신호를 합치더라도 X상태(두 값이 충
돌하여 값을 예측할 수 없는 상태)가 나오지 않는다. 위의 그림에서는 A에 연결
된 Transmission gate는 연결되고 B는 스위치가 off되어 있기 때문에 A의 결과가 출
력되는 모습을 보인다.
```
```
위의 그림은 clk의 값이 1 일 때이다. 이 경우에는 아까와는 반대로 A가 끊어지고
B가 연결된 것이기 때문에 B의 결과가 출력된다.
```
```
이를 Truth table로 나타내면 다음과 같다.
```

#### CLK A B D

#### 0 Q 1 Q 2 Q 1

#### 1 Q 1 Q 2 Q 2

### 3. Implement a Latch using MUXs

- Latch는 Sequential Circuit 중 하나로 이전 상태를 기억하는 회로다. Latch는 Clock의
    값이 1 일 때에는 새로운 값을 저장하고, 0 이 되었을 때 이전의 값을 유지하는 특
    성을 지니고 있다. Latch는 종류에 따라 R-S Latch, D Latch 등 다양하게 존재한다.

```
현재 과제에서 제작하는 Latch는 MUX를 이용한 것으로 설계는 다음과 같다.
```
```
설계 방식은 MUX의 입력 신호 1 개와 출력 신호를 연결하여 Cycle이 돌도록 하여
기존의 값을 유지하는 방식이다. 해당 회로는 아직 초기화를 하지 않은 Latch를
보이고 있다. Clk이 0 일 때에는 이전 값을 유지하는 모습이다.
```
```
위의 그림들에서 볼 수 있다시피 clk의 값이 1 이 된 경우에는 D에서 출력하고 있
는 값을 그대로 가져와 출력하는 모습을 보인다.
```

```
위의 그림은 이전 그림의 상태에서 다시 clk이 0 일 때를 보인 그림이다. 해당 그
림에서는 D의 값을 바꾸었지만 기존의 값을 유지하는 모습을 보인다. 이를 통해
회로가 정상적으로 설계되었음을 확인할 수 있다.
```
```
해당 Latch의 Truth Table은 다음과 같다.
CLK D Q
0 Qn Qn- 1
1 Qn Qn
```
### 4. Implement D-FF using Latches

- FlipFlop이란 Clock이 rising 또는 falling edge를 가질 때만 값이 저장되는 Sequential
    Curcuit을 말한다. 이 중 이번 과제에서 만드는 Flipflop은 D-FF으로, D-Latch 2개를
    사용하여 제작할 수 있다. 해당 회로의 설계는 다음과 같다.

```
위의 그림을 살펴보면 이전의 제작했던 Latch 2개가 이어져 있는 모습이고, 특히
한 쪽은 clk’의 값을 받는 것을 볼 수 있다. 이는 보통 Flipflop을 구성하는데 이
때 앞쪽을 master, 뒤 쪽의 latch를 slave라 말한다. 필자가 제작한 D-FF은 falling
edge에서 동작한다. 현재 위의 그림에서는 아직 초기화하지 않은 상태의 FlipFlop
을 볼 수 있다.
```

```
위의 사진은 아까 전의 상태에서 clk의 값을 1 로 바꾼 것이다. 해당 상태에서 D의
데이터는 master latch에 전달되어 저장이 된다. 그리고 slave의 latch는 아직 기존
값을 유지하고 있다.
```
```
위의 사진은 아까 전의 상황에서 clk을 0 으로 바꾼 후 D의 값을 바꿔본 모습이다.
이를 보았을 때 master에서 저장하고 있던 값 0 이 slave에도 저장되어 출력되는
것으로 바뀐 모습을 볼 수 있다. 이처럼 두 latch간의 전달 과정을 통해 falling
edge에서만 데이터를 저장하는 회로를 구성할 수 있었다.
```
```
해당 D-FF의 Truth table은 다음과 같다.
CLK D Q
Down Qn Qn
else Qn Qn- 1
```
### 5. Implement Synchronous Up/Down Counter using D-FFs and adders

- Counter란 값을 일정하게 누적하거나 빼는 회로를 말한다. 해당 회로를 구성하는
    방법으로는 Synchronous한 회로를 만드는 방법과 Asynchronous한 회로(Ripple
    counter)를 구성하는 방법으로 나눌 수 있다. 해당 과제에서 진행하는 counter는
    adder를 이용한 Sychronous Up/Down Counter이다. 해당 설계는 다음과 같다.


해당 회로를 살펴보면 4bits data를 저장하기 위한 D-FF이 존재하고 해당 회로에는
Reset과 Set 신호가 연결되어 있어 초기화를 할 수 있다. 해당 선들은 4bits adder
의 피연산자로 들어가고 있다. 다른 피연산자는 덧셈인지 뺄셈인지에 따라 0001
또는 FFFF 값을 넘기는 MUX와 연결되어 있다. 만약 up상태일 경우 0001 을 D-FF의
데이터와 더하여 다시 저장하고, down상태일 경우에는 FFFF(-1)을 D-FF의 데이터와
더하여 저장한다.

해당 그림은 위의 상태에서 clk을 1 cycle 움직인 것이다. 그림을 보면 D0의 위치에
1 이 저장되어 현재 0001(1)로 값이 표현되는 것을 알 수 있다.


```
다음과 그 다음 cycle에서도 값이 1 씩 더해져 0010 - > 0011로 변해가는 것을 볼 수
있다.
```
```
해당 그림은 0011 이 저장된 이전 상황에서 Down으로 모드를 전환한 뒤 clk을 2
cycle이 바꾸었다. 그림에서 이전과 다르게 0011 - > 0010 ->0001로 값이 1 씩 빼지는
것을 확인할 수 있다. 이를 통해 우리는 회로가 정상적으로 설계되었음을 알 수
있다.
```
```
해당 회로의 Truth table은 다음과 같다.
CLK Up/Down Dn[4:0] Dn+1[4:0]
Down 0 N N+
else 1 N N- 1
```
### 6. Compare Synchronous counter and Asynchronous counter such as a

### ripple counter

- Synchronous Counter의 동작은 위의 설명에서 보다시피 모든 D-FF이 같은 clk을 받
    기 때문에 동시에 동작하는 것을 알 수 있다. 우리는 이것을 Synchronous한 circuit
    이라 말한다. 이와 반대로 Asynchronous한 회로는 D-FF이 같은 cycle에서 동작하지
    않는다.


```
다음 회로도는 ripple counter를 나타낸 것이다. 해당 회로에서 볼 수 있는 것으로
는 이전의 설계한 counter와 달리 adder가 사용되지 않았고, D-FF에서 나온 Q’의
값이 D에 직접적으로 연결되며 Q의 값은 다음 D-FF의 CLK에 연결된다는 것이다.
```
```
해당 방법이 작동하는 방식은 다음과 같다.
각각의 D-FF은 Q’과 D값이 연결되어 있기 때문에 매 cycle마다 0 과 1 의 값이 반전
되며 값을 출력한다. 하지만 각각의 D-FF은 다른 주기를 가지면서 동작을 한다.
앞쪽에 연결된 D-FF이 1 cycle을 돌았을 때 다음 D-FF은 rising edge 또는 falling edge
하나를 가지는 것이다. 때문에 다음 위치의 D-FF은 앞쪽보다 2 배의 cycle을 가지
게 된다.
```
```
해당 방식을 사용할 경우 가장 큰 장점은 회로를 적게 사용하여 counter를 구성
할 수 있다는 점이다. 이전 방식에서는 4 bits adder를 사용하였기 때문에 해당 회
로 안에서 사용하는 gate가 많을 수밖에 없다. 하지만 ripple counter는 숫자를 가
산하는데 4 개의 D-FF 이외의 다른 회로를 요구하지 않는다. 이로 인해 낮은 cost
로 회로를 제작할 수 있으며, 회로가 큰 공간을 요구하지 않는다.
```
### 7. What makes that Asynchronous counter is rarely used

#### - 위에서 말했던 장점이 단순한 설계와 이로 인한 가격이었지만 해당 회로에는 단

```
점이 존재한다. 이는 모든 register가 동시에 동작하는 것, 즉 Asynchronous하다는
문제다.
```
```
현실에서는 Delay라는 것이 존재한다. 전선을 통과하는 빛의 속도의 한계, gate 등
을 지날 때 capacitor를 충전하는데 소요되는 Delay 등이 존재한다. Synchronous
counter의 경우 모든 D-FF이 같은 CLK에 의해 연결되어 동작하기 때문에 동시에
동작할 수 있다. 하지만 Ripple counter의 경우에는 다르다. 해당 회로에서, 뒤쪽의
D-FF 값의 변화는 앞쪽의 D-FF에 의해 결정된다. 뒤쪽의 D-FF에서 gate를 통과하기
때문에 Delay는 필연적으로 발생한다.
```
```
물론 이는 단순한 회로를 제작하는데 크게 문제가 되지 않는다. 하지만 기기의
size가 커질 수록, 즉 회로가 복잡해질수록 해당 문제는 크게 나타난다. 모든 동작
에 일정한 cycle에 의해 동작하도록 되어있지 않으면 Asynchronous한 값의 출력으
로 인해 이전의 값이 계산되거나, 값이 0 도 1 도 아닌 값이 입력되는 것, 즉
```

```
metastability가 발생할 확률이 증가하게 된다. 이러한 문제를 막기 위해 최근에는
Asynchronous한 회로의 사용을 줄이고 Synchronous한 회로를 사용하도록 권장하고
있다.
```
## B. MU

### 1. With the given data, write assembly code and predict how it operates

- 현재 주어진 binary를 MU0 assembly code로 변환하고 해석할 경우 다음과 같다.
    address Binary code MU0 Assembly code
       000 0400 LDA 400 //ACC=[ 400 ]= 0020
       001 2400 ADD 400 //ACC=ACC+[ 400 ]= 0020 + 0020 = 0040
       002 1800 STO 800 //Store ACC( 0040 ) at 800
       003 0401 LDA 401 //ACC=[ 401 ]= 5555
       004 2402 ADD 402 //ACC=ACC+[ 402 ]= 5555 +00AA=55FF
       005 3403 SUB 403 //ACC=ACC-[ 403 ]=55FF-0055=55AA
       006 1801 STO 801 //Store ACC(55AA) at 801
       007 4010 JMP 010 //PC= 010
       008 7000 STP
       009 0600 LDA 600 //ACC=[ 600 ]= 1234
0 0A 3600 SUB 600 //ACC=ACC-[ 600 ]=1234-1234=
00 B 0616 LDA 616 //ACC=[ 616 ]=
00 C 2600 ADD 600 //ACC=ACC+[ 600 ]=0000+1234=
00 D 1803 STO 803 //Store ACC( 1234 ) at 8 03
00 E 6000 JNE 000 //if(ACC!=0) PC=000 -> Operate
0 0F 7000 STP
010 0500 LDA 500 //ACC=[ 500 ]=7FFF
011 2501 ADD 501 //ACC=ACC+[ 501 ]=7FFF+0001=
012 5008 JGE 008 //if(ACC>= 0 ) PC=0 08 - > Don’t operate
013 3501 SUB 501 //ACC=ACC-[501]= 8000 - 0001 =7FFF
014 1802 STO 802 //Store ACC( 7 FFF) at 8 02
015 5009 JGE 009 //if(ACC>=0) PC=009 -> Operate
016 7000 STP
//data
400 0020
401 5555
402 00 AA
403 0055

```
500 7 FFF
501 0001
600 1234
601 0000
616 0000
```
```
800 0000 //store
801 0000
802 0000
803 0000
```

#### 위의 표를 살펴보면 MU0는 000 부터 007 까지의 동작을 수행한 후 010 으로 넘어

#### 가 015 까지 동작을 수행한다. 이후 009 로 넘어가 00 E까지의 동작을 마치고 다시

```
000 으로 넘어가는 Cycle을 가지게 된다.
```
```
데이터는 800 ~ 803 까지 각각 0040 55AA 7FFF 1234가 저장된다.
```
### 2. Complete the design by connecting all wires labeled as w1 ~ w

#### - 설계된 선을 연결한 회로는 다음과 같다.

```
LDA 명령어는 w 1 과 연결되었다. 이유는 ACC에 값이 저장되기 위해서는 ACC의
WE 신호가 동작해야 한다. 또한 ACC = load data + 0를 해야 Load된 데이터가 변하
지 않고 저장되기 때문에 0000 을 더하도록 도우는 MUX와 연결되어야 한다. 때문
에 해당하는 w1을 연결하였다.
```
```
STO 명령은 w8에 연결하였다. Store이 진행되기 위해서는 Ram의 WE 신호가 1 이
되어야 한다. 그러기 위해서는 이전의 3 - input AND gate가 동작해야 하기 때문에
w8에 연결되어야 한다.
```
```
ADD 명령은 w 3 와 연결되었다. Add 명령이 진행되기 위해서는 ACC의 WE 신호가
동작해야한다. 그리고 더하는 인자의 경우 Not gate를 통과한 인자를 더해서는 안
된다. 때문에 해당 신호는 w3에 연결되었다.
```
```
SUB 명령은 w 2 에 연결하였다. 이유는 뺄셈이 진행되어서 ACC에 값이 저장되어야
```

```
하기 때문에 ACC의 WE의 신호가 있어야 하고, 가져온 인자는 2 ’s complement로
변환되어야 하기 때문에 해당 변환과 관련한 MUX가 연결되어있는 w2에 연결하
였다.
```
```
JMP 명령은 w 6 에 연결하였다. Jump를 수행할 경우 PC의 값을 주어진 값으로 바
꾸어야 한다. 이를 위해서는 PC 이전의 MUX에서 가져오는 주소를 사용해야 하며
PC의 WE은 동작해야 한다. 때문에 이와 관련한 w6를 선택하였다.
```
```
JGE 명령은 w 4 에 연결되었다. Jump great equal을 수행하기 위해서는 ACC의 값을 0
과 Compare하여 나온 신호들을 보아야 한다. 특히 이 중 Great과 Equal의 신호가
OR 연산 되어있는 w 4 신호가 해당 명령어에 연결하는 것이 적합하다.
```
```
JNE 명령은 w5에 연결하였다. Jump not equal을 수행하기 위에서는 JGE와 마찬가지
로 Compare가 필요하다. 또한 Equal의 신호를 Not gate를 통해 반전하여 연결한
w 5 가 해당 명령어와 연결하는 것이 옳다.
```
```
STP를 포함한 Forbidden된 명령어들은 w 7 에 연결하였다. 해당 명령어들은 NOR
gate를 통과하였기 때문에 하나의 신호라도 들어올 경우 0 을 출력하고, 이외의 경
우에는 1 을 출력한다. w 7 은 and gate를 지나치고 PC의 WE 신호에 들어가기 때문
에 w 7 이 0 일 경우 PC의 값은 최신화할 수 없다. 때문에 Processor의 동작은 정지
된다.
```
### 3. Operate MU


#### 초기화가 되기 전 MU0의 모습이다.

#### RST을 이용해 초기화를 진행하고 RAM에 데이터를 전달하였다.


#### ACC에 0020 이 저장된 것을 볼 수 있다. 즉 LDA 명령어가 제대로 동작한다.


#### ACC의 값과 400 번지의 0020 값이 더해져 0040 이 되었다. 이는 ADD 명령어가 정상

#### 적으로 동작함을 알 수 있다.


#### 800 번지에 0040 값이 저장된 것을 볼 수 있다. 이는 즉 STO 명령어가 정상적으로

#### 동작하는 것으로 생각할 수 있다.


#### 위의 그림은 데이터를 다시 ACC로 가져와서 다른 덧셈 연산을 한 결과를 나타낸

#### 것이다.


#### 5 5FF – 0055 = 55AA 뺄셈 연산이 정상적으로 동작하는 모습을 보여준다.


#### 값 55 AA가 801 번지에 정확히 저장되는 것을 볼 수 있고 그 후에 JMP를 통해 010

#### 으로 PC값을 바꾸는 모습이다. 해당 명령 또한 제대로 동작하는 것을 알 수 있

#### 다.

#### 010 ~ 011에서는 7 FFF와 0001 을 가져와 더하는 코드다. 해당 과정이 예측과 같게

#### 동작하였다.


#### 해당 과정은 JGE 명령을 사용한 것을 나타낸다. 해당 명령을 사용하였을 때 ACC

의 값은 2 ’s Complement로 음수를 나타내기 때문에 해당 신호가 0 으로 나오게 된
다. 이에 해당 jump 과정은 무시되고 기존의 PC값을 그대로 사용하게 된다. JGE에
서 통과하는 case가 정확히 동작하고 있다.


#### 014 까지의 명령을 통해 8000 에서 1 을 뺀 값이 802 주소에 저장되었다. 그리고

JGE를 통해 다시 해당 값과 0 을 비교하였다. 이 때 7 FFF > 0 임으로 해당 Jump가
진행되어 009 으로 PC값이 바뀌었다. 이를 통해 JGE가 두 경우에서 모두 작동함으
로 정상적으로 제작되었음을 알 수 있다.


#### 0 09 ~ 00D의 과정을 살펴보면 ACC에 1234 값을 불러와서 ACC = 1234 - 1234 = 0 연산

#### 을 진행한다. 그 후 616 주소에서 0000 을 불러와 1234 와 덧셈을 진행한 후 이를

#### 803 주소에 저장한다. 해당 값은 정상적으로 저장되었고, 그 후의 동작으로 JNE를

#### 진행한다. 현재 ACC에 있는 값이 1234 임으로 0 이 아니기 때문에 JUMP가 동작하

#### 여 000 주소로 이동하는 모습을 볼 수 있다.


## C. Consideration

### 1. Consideration

- 해당 과제를 통해 2 학년 디지털논리회로 과정에서 학습하였던 Transmission Gate를
    비롯해 Mux, Latch, D-FF, Counter에 대해 복습을 할 수 있었다. 또한 MUX와 Latch의
    경우 기존과 다른 방법을 통해 회로를 설계해보면서 하나의 회로도 다양하게 설
    계할 수 있다라는 식견을 갖게 해주었다. Synchronous counter와 Asynchronous
    counter를 직접 비교해보고 각각의 특징을 이해할 수 있었다. MU0 과제에서는 2
    학년 때 추상적인 level로 알아보았던 MU0를 직접 그려보면서 해당 프로세서가
    어떻게 동작할지 고민하는 과정을 통해 회로를 이해하는 능력을 향상시켜주었다.
    또한 주어진 binary Code를 직접 해석하여 Assembly Code로 번역하는 과정을 통해
    Assembly language의 동작 과정을 이해할 수 있었다.

### 2. Problem & Solution

- 주어진 binary code를 해석하였을 때 기존 코드를 통해서는 LDA, STO, ADD, SUB,
    JMP, JGE의 동작을 전부 검증할 수 있다. 하지만 JNE의 동작의 경우 Jump를 하지
    않는 case를 검증할 수 없고, 해당 코드는 000 번지로 돌아가 다시 작업을 수행하
    기 때문에 STP의 동작이 작동하는지 확인할 수 없다. 이를 확인하기 위해서는 해
    당 작업을 추가해야 할 필요성이 있다. 이를 위해 마지막 JNE 동작에서 이동하는
    위치를 017 번지로 바꾸고 017 번지에서는 LDA를 통해 0000 값을 ACC에 불러온다.
    그리고 JNE 000을 통해 0 이 아닐 경우 000 번지로 이동하고 0 일 경우 다음 작업을
    수행하도록 코드를 작성한다. 해당 과정이 정상 작동할 경우 다음 작업을 수행할
    것이다. 그리고 다음 주소에는 STP를 작성하여 프로그램이 정상적으로 멈추는지
    확인한다. 이를 통해 모든 과정을 검증할 수 있다.
-

## D. Reference

- Transistor image :

### https://m.blog.naver.com/paval777/221577915620

- Transmission Gate image :

### https://en.m.wikipedia.org/wiki/File:CMOS_transmission_gate.PN

### G

- 4 bit Ripple counter image :

### https://www.researchgate.net/figure/A- 4 - bit-ripple-counter-

### circuit-The-output-of-one-flip-flop-clocks-the-next-one-

### hence_fig6_238687766

### -


