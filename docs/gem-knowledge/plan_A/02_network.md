# RK3588 네트워크 구성

## 출처 (Sources)

- `reference/OrangePi5Plus/Benchmarks/*.txt`

---

## 하드웨어 사양

### 듀얼 2.5G 이더넷

- **컨트롤러**: Realtek RTL8125B x2
- **PCIe**: 2.0 x1 lane (5GT/s) 각각
- **드라이버**: r8169 (in-kernel)
- **ASPM**: Disabled (안정성)

### PCIe 토폴로지

```
PCIe3x4 (NVMe)     - 8GT/s, x4
PCIe2x1l1 (Eth#1)  - 5GT/s, x1
PCIe2x1l2 (Eth#2)  - 5GT/s, x1
```

---

## 기본 설정

### Netplan (기본값)

```yaml
network:
  version: 2
  ethernets:
    zz-all-en:
      match: {name: "en*"}
      dhcp4: true
      optional: true
    zz-all-eth:
      match: {name: "eth*"}
      dhcp4: true
      optional: true
```

### 인터페이스 네이밍

- systemd: `en*` (예: `enP4p65s0`)
- 전통적: `eth0`, `eth1`

---

## 네트워크 성능

| 항목 | 값 |
|------|------|
| 컨트롤러 | RTL8125 2.5GbE |
| 속도 | 10M / 100M / 1G / 2.5G auto-negotiation |
| PCIe | 5GT/s, x1 |

---

## 활용 방안

### 라우터 구성 (OpenWrt)

- `eth0`: WAN
- `eth1`: LAN (브리지)

### MacVLAN 격리

```yaml
services:
  isolated-service:
    network_mode: macvlan
    macvlan:
      parent: eth1
      mode: bridge
```
