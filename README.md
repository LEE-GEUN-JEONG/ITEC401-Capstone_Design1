# ITEC401 / 종합설계프로젝트1 / 2020년도 / 1학기 / 심재훈
## Cadence virtuoso tool을 사용하여 SRAM SYSTEM을 Full-Custom Design 하였음.
## 프로젝트를 위한 여러가지 디지털 및 아날로그 회로에 대한 자료와 최종 프로젝트를 정리하여 나열하였음.
## 본 프로젝트를 위해서는 openvpn으로 학내 서버에 접속한 뒤 mobaxterm으로 리눅스에 접속하였음.
## 본 프로젝트에서는 full custom design 뿐만 아니라 cadence virtuoso tool 내부의 calculator 사용을 위해 코딩도 진행하였음.
## 최종프로젝트 입력신호를 위한 pwl file을 첨부하였음.

### 프로젝트 제안서
![image](https://user-images.githubusercontent.com/58419421/99411334-d432bd80-2936-11eb-892d-51bff8774aae.png)
![image](https://user-images.githubusercontent.com/58419421/99411377-e14fac80-2936-11eb-98b7-32900eabbc6b.png)

#### 프로젝트 수행을 위한 과제 (파일 첨부하였음.)
##### 프로젝트 수행을 위한 과제는 양이 방대하여 일부만 나열하였음. (모든 내용은 파일에 첨부하였음.)

![image](https://user-images.githubusercontent.com/58419421/99411998-984c2800-2937-11eb-97e9-14ea1bfaf384.png)

![image](https://user-images.githubusercontent.com/58419421/99411805-591dd700-2937-11eb-89da-10b49b75029c.png)
![image](https://user-images.githubusercontent.com/58419421/99411846-64710280-2937-11eb-84bf-53dc4150e85d.png)
![image](https://user-images.githubusercontent.com/58419421/99412179-c7629980-2937-11eb-912c-ac57f1fa7949.png)

# 최종 프로젝트
Design Project
Spring, 2020
ITEC401011
Professor: Jae Hoon Shim
김동현, 김승현, 나경운, 이경민, 이근정
1. Abstract
본 설계의 특징은 다음과 같다. • 동기식 SRAM Array
Enable 신호에 Row Decoder를 동기화하여 Enable 신호가 인가될 때만 Word Line이 선택되고, Read, Write 동작이 발생하게 하였다. Enable 신호의 사용으로 설계가 간단해지고 동작 분석이 용이하였
다. 그리고 SRAM Cell의 Hold mode 동작을 보장할 수 있고, Gate delay문제 해결을 위한 setup time,
hold time 설정이 용이하였다. 하지만 Read와 Write 동작을 분리할 수 없기 때문에 최적의 Read cycle,
Write cycle을 만드는 데는 한계가 존재했다.
• Pre-Charge Circuit
BL과 BLB가 pre-charge에 의하여 충전될 때 균형적으로 충전될 수 있게 PFET을 BL과 BLB 사이에
연결하였다. 따라서 불균형하게 초기 전압 값을 가지고 있어도 Pre-charge 후에는 비슷한 Pre-charge
level을 가지도록 하였다.
• Row Decoder
Enable 신호에 Row Decoder를 동기화하여 입력인 Address 신호에 상관없이 Device를 on, off 할 수
있게 설계하였다. 그리고 2단 Partial Decoding으로 사용되는 TR의 개수를 줄여 전력 소모를 줄였다.
• Column Decoder
A[0] 신호를 입력으로 8words*8bit SRAM Array를 16words*4bits SRAM Array로 변환시켰다. A[0]
신호로 왼쪽 column(또는 왼쪽 페이지)을 선택하거나 오른쪽 column을 선택할 수 있게 하였다. 이로 인
해 사용되는 Sense Amplifier와 Write Driver의 개수를 줄여 전력 소모, 면적, cost를 줄일 수 있었다.
• CMOS Transmission Gate
SRAM Array에 사용되는 Pass TR을 CMOS Transmission Gate로 대체하여 Low signal과 High
signal 모두 잘 전달할 수 있게 하였다.
• Sense Amplifier
SA의 BL, BLB와 SA의 cross coupled inverter 사이에 CMOS Transmission Gate를 삽입하여 Write
동작과 Read 동작 시에 스위치 역할을 할 수 있게 하였다. 따라서 Latch type SA의 단점인 leakage 문
제를 해결하였다. 그리고 cross coupled inverter의 VDD, GND와 연결되는 TR의 게이트 입력에
control 신호를 인가하여 Read 동작이 일어나지 않을 때에는 전원을 off 시킬 수 있게 하였다. 따라서 전
력 소모를 줄일 수 있었다. 
• Write Driver
Write control 신호를 통하여 Write 동작이 일어나지 않을 때에는 Write Driver를 off 시켜 전력 소모
를 줄일 수 있었다. *참고사항
PRE : Pre-Charge Circuit의 Control Signal (Active Low)
EN : Common Enable Signal (Active Low)
A[3:1] : Row Decoder의 Address Signal 
A[0] : Column Decoder의 Left Page, Right Page 선택을 위한 Signal 
RWSEL : Read or Write operation을 선택해주는 Signal
(초기 16 cycle RWSEL=0 -> Write 동작, 후기 16 cycle RWSEL=1 -> Read 동작)
SAE : Sense Amplifier Control Signal (Active High)
WEN : Write Driver Control Signal (Active Low)
RDATA[3:0] : Sense Amplifier 를 통해 Read 한 data
WDATA[3:0] : Write Driver 를 통해 Write 할 data


![image](https://user-images.githubusercontent.com/58419421/99412427-0d1f6200-2938-11eb-90b3-4b57db8b37a5.png)
![image](https://user-images.githubusercontent.com/58419421/99412449-13add980-2938-11eb-891c-0ace6223c877.png)

BL과 BLB의 Pre-charging 충전량 및 속도를 증가시킬 수 있는 방법은 다음과 같다.
• Pre-charge circuit의 control signal인 PRE의 on time을 증가시킨다. 현재 Pre-charge circuit의 control signal인 PRE는 PFET을 이용한 active low input 이다. 따라서
PRE=0을 인가해주는 시간을 증가시킨다면 BL과 BLB의 Pre-charge level이 증가할 것이다.
• pre_pass를 증가시킨다. pre_pass가 증가하면 VDD와 연결된 PFET의 channel width가 증가하므로 pre-charging 통로의 폭
이 증가하게 된다. 따라서 동일 시간에 더 많은 양의 전하를 흘려보낼 수 있으므로 pre-charging 속도가
증가한다.


![image](https://user-images.githubusercontent.com/58419421/99412530-2cb68a80-2938-11eb-9624-2d156f8e6fd3.png)
4) Analysis of the circuits and design considerations (including sizing of
transistors)
Analysis of the circuits
본 설계의 Pre-charge circuit은 단순 통과 역할 하는 PFET 2개와 BL, BLB의 균형적 charging을 위
한 PFET 1개로 이루어져있다. 이 3개의 PFET 게이트 입력으로 Pre-charge circuit의 control signal인
PRE 신호가 입력된다. PFET을 이용하여 Pre-charge circuit을 구성하였으므로 Active Low 입력을 가진
다. 따라서 PRE=0이 입력되면 3개의 PFET이 turn on 되어 Pre-charge circuit이 ON 되게 된다. Pre-charge circuit이 ON되면 64bit SRAM의 전원인 VDD의 charge가 PFET을 통과하여 BL과 BLB
로 흐르게 된다. Read와 Write 동작을 위한 충분한 전압 값이 BL과 BLB에 전달된다면 PRE=1이 되어
Pre-charge circuit은 전체 회로와 분리되게 된다. Design Consideration
Write 동작을 위한 사전 Pre-charge 동작에서는 SRAM Cell과 직접적으로 연결된 BL과 BLB의 전압
레벨을 VDD 까지 증가시켜야 한다. 하지만 Read 동작을 위한 Pre-charge 동작에서는 SA와 직접적으로
연결된 BL과 BLB의 전압 레벨을 VDD 까지 증가시켜야 했다. 따라서 Read 동작을 위한 Pre-charge에서
는 Pre-charge 동작이 원활히 수행되지 못하였다.(SA에 direct로 연결된 BL과 BLB는 Pre-charge
circuit과 직접적으로 연결되어 있지 않고, 중간에 Column Decoder를 지나므로 Write 동작보다
pre-charge 속도가 느릴 수 밖에 없다.)
따라서 Read 동작 시에는 PRE control signal의 on time을 증가시키거나 pre_pass 변수를 증가시켜
Pre-charge 충전량을 인위적으로 증가시킬 수 있게 하였다. 그리고 read upset 방지를 위해
pre_balance 변수도 적절하게 증가시켜 read 동작이 일어나기 전 SA와 연결된 BL, BLB가 균등하게
Pre-charge가 되도록 하였다. 


![image](https://user-images.githubusercontent.com/58419421/99412576-3f30c400-2938-11eb-8444-bdf4d7c52c2b.png)
![image](https://user-images.githubusercontent.com/58419421/99412593-435ce180-2938-11eb-81cd-a83e9e761a84.png)
![image](https://user-images.githubusercontent.com/58419421/99412611-4788ff00-2938-11eb-8eff-3ab20fa30dfa.png)
![image](https://user-images.githubusercontent.com/58419421/99412628-4c4db300-2938-11eb-87fa-a1cbf09d4bf7.png)
![image](https://user-images.githubusercontent.com/58419421/99412653-52439400-2938-11eb-9fdd-6ca60570e314.png)
![image](https://user-images.githubusercontent.com/58419421/99412676-57084800-2938-11eb-94ed-76f39ba410ee.png)
![image](https://user-images.githubusercontent.com/58419421/99412702-5ec7ec80-2938-11eb-9ab8-1ae0d2bb0cbc.png)
![image](https://user-images.githubusercontent.com/58419421/99412717-62f40a00-2938-11eb-913d-9c9148b0cdad.png)
![image](https://user-images.githubusercontent.com/58419421/99412729-66879100-2938-11eb-9a42-1dc52ecd3424.png)
![image](https://user-images.githubusercontent.com/58419421/99412739-6ab3ae80-2938-11eb-9743-b41735a95973.png)
![image](https://user-images.githubusercontent.com/58419421/99412765-6edfcc00-2938-11eb-90c3-734afe2fe19d.png)
![image](https://user-images.githubusercontent.com/58419421/99412785-730be980-2938-11eb-9ab5-7b7e70d9be37.png)
![image](https://user-images.githubusercontent.com/58419421/99412796-7606da00-2938-11eb-9ac9-b4f7f2d81fff.png)
![image](https://user-images.githubusercontent.com/58419421/99412810-799a6100-2938-11eb-9d67-9ac41e978383.png)
![image](https://user-images.githubusercontent.com/58419421/99412832-7dc67e80-2938-11eb-8865-d12777d12b8d.png)
![image](https://user-images.githubusercontent.com/58419421/99412847-81f29c00-2938-11eb-83b4-6a487c990879.png)
![image](https://user-images.githubusercontent.com/58419421/99412855-85862300-2938-11eb-8c96-7b3c2fb216c4.png)
![image](https://user-images.githubusercontent.com/58419421/99412883-8b7c0400-2938-11eb-8726-9b662dcd7722.png)
![image](https://user-images.githubusercontent.com/58419421/99412944-9afb4d00-2938-11eb-8c08-312627e4cbf3.png)
2) the reasons you have chosen the particular structure
WEN(write contol signal) 신호로 write 동작을 하지 않을 때에는 확실하게 외부 회로와 WD 회로를
분리시킬 수 있고, 그리고 WDATA(입력 data) 신호로 BL 또는 BLB 한 곳을 확실히 discharging 시켜서
write 동작 수행 전 SRAM Cell의 BL과 BLB에 wdata를 Full swing한 값으로 준비시켜 안정적인 쓰기
동작이 가능한 장점이 있다.
![image](https://user-images.githubusercontent.com/58419421/99412986-a6e70f00-2938-11eb-8f80-3c6d367155d7.png)

![image](https://user-images.githubusercontent.com/58419421/99413039-b23a3a80-2938-11eb-9db4-0cb91ccebdb4.png)
![image](https://user-images.githubusercontent.com/58419421/99413065-b8c8b200-2938-11eb-9b0c-e94c520ea6b2.png)
![image](https://user-images.githubusercontent.com/58419421/99413079-bd8d6600-2938-11eb-9f61-74cffbaf2cdb.png)
![image](https://user-images.githubusercontent.com/58419421/99413091-c2521a00-2938-11eb-9b78-0068dea8c555.png)
![image](https://user-images.githubusercontent.com/58419421/99413110-c67e3780-2938-11eb-8bfd-c27d928aa249.png)
![image](https://user-images.githubusercontent.com/58419421/99413123-c9792800-2938-11eb-81a7-2077dd583b79.png)
![image](https://user-images.githubusercontent.com/58419421/99413133-ce3ddc00-2938-11eb-8cd2-4bf5e7f6fb6d.png)
![image](https://user-images.githubusercontent.com/58419421/99413147-d1d16300-2938-11eb-8b20-138936809a06.png)
![image](https://user-images.githubusercontent.com/58419421/99413162-d564ea00-2938-11eb-8d67-b0e1098e89da.png)
![image](https://user-images.githubusercontent.com/58419421/99413171-d8f87100-2938-11eb-814e-85d2e6063994.png)
![image](https://user-images.githubusercontent.com/58419421/99413186-dd248e80-2938-11eb-888c-ef2ef7e3ba88.png)
![image](https://user-images.githubusercontent.com/58419421/99413196-e150ac00-2938-11eb-9806-2b0c88874ca8.png)
![image](https://user-images.githubusercontent.com/58419421/99413215-e57cc980-2938-11eb-8a6a-083cc8fd4daf.png)




