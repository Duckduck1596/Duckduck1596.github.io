# Cisco IOS와 네트워크 기본 개념 정리

## 1. Cisco IOS 기본 개념
- **Cisco IOS (Internetwork Operating System)**  
  : 시스코 장비(라우터, 스위치 등)에 탑재된 운영체제.  
  CLI(Command Line Interface) 기반으로 장비 설정, 관리, 트러블슈팅을 수행한다.  

### ✅ 기본 IOS 모드
```bash
Router>             # User EXEC 모드
Router#             # Privileged EXEC 모드
Router(config)#     # Global Configuration 모드
Router(config-if)#  # Interface 설정 모드
```

---

## 2. 스위치의 MAC Address Table

### (1) MAC Address Table 개념
- 스위치는 **MAC 주소 테이블**을 통해 프레임의 목적지 포트를 결정한다.
- `source MAC + ingress port` 정보를 학습(learning) 후 테이블에 기록한다.

### (2) 주요 동작
- **Auto Negotiation**: 속도(10/100/1000Mbps)와 Duplex(half/full) 자동 협상  
- **Fast Ethernet**: 100Mbps 속도 지원 표준  
- **Learning**: 출발지 MAC 기록  
- **Flooding**: 모르는 MAC → 전체 포트로 전송  
- **Forward/Filter**: 목적지 MAC 확인 후 전달 or 필터링  

### (3) MAC Table 관련 CLI
```bash
Switch# show mac address-table
Switch# clear mac address-table dynamic
```

---

## 3. ARP 동작 방식

1. **ARP Cache 확인**  
   목적지 IP → MAC 매핑 확인  
2. **Network 비교**  
   같은 네트워크인지 확인  
3. **ARP 절차**  
   - Request: 브로드캐스트 전송  
   - Reply: 유니캐스트 응답  
   - Cache에 저장  

### ✅ ARP CLI 예시
```bash
Router# show arp
Router# clear arp-cache
```

---

## 4. L2 Switch Looping과 STP
- **문제**: 스위치 간 루프 발생 시 **브로드캐스트 스톰**  
- **해결**: STP(Spanning Tree Protocol)  
  - **BPDU** 교환  
  - 루트 브리지 선택 후 필요 없는 포트 차단  

### ✅ STP CLI 예시
```bash
Switch(config)# spanning-tree mode pvst
Switch# show spanning-tree
```

---

## 5. Broadcast Domain
- 브로드캐스트가 전달되는 네트워크의 범위  
- VLAN 단위로 분리됨  
- 라우터(L3) 통과 시 분리  

---

## 6. VLAN (Virtual LAN)

### (1) VLAN 기본 설정
```bash
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config)# interface fastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

### (2) Trunk 설정
```bash
Switch(config)# interface fastEthernet0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
```

### (3) Inter-VLAN Routing (Router on a Stick)
```bash
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
```

---

## 7. EtherChannel
- 여러 링크를 하나로 묶어 대역폭 확장 & 장애 대비  
- **PAgP(Cisco 전용)** / **LACP(표준)**  

### ✅ EtherChannel CLI 예시
```bash
Switch(config)# interface range g0/1 - 2
Switch(config-if-range)# channel-group 1 mode active    # LACP
Switch(config-if-range)# channel-group 1 mode desirable # PAgP
Switch# show etherchannel summary
```

---

## 8. Routing 기본 개념

### (1) 주요 라우팅 방식
- **Destination Based Routing**: 목적지 주소 기준  
- **Unicast Routing**: 단일 목적지로 전달  
- **Network Based Routing**: 네트워크 주소 단위 라우팅  
- **Hop-by-Hop Routing**: 각 라우터가 다음 홉 결정  

### (2) Routing CLI
```bash
Router(config)# ip route 0.0.0.0 0.0.0.0 192.168.1.1   # 기본 라우트
Router# show ip route
```

---

# 📌 오늘 학습 요약
- Cisco IOS: 장비 운영체제, CLI 기반 설정  
- MAC Table: Learning, Flooding, Forward/Filter  
- ARP: Request/Reply 과정 후 Cache 저장  
- STP: 루프 방지, BPDU 사용  
- VLAN: 네트워크 논리 분리, Trunk & Inter-VLAN Routing  
- EtherChannel: 링크 묶음, LACP/PAgP 사용  
- Routing: 목적지 기반 경로 결정  
