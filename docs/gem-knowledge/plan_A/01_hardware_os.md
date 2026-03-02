# RK3588 하드웨어 및 OS 가이드

## 출처 (Sources)

- `reference/ubuntu-rockchip/README.md` (48줄)
- `reference/OrangePi5Plus/User Manual/reference/OrangePi5Plus/User Manual/OrangePi_5_RK3588S_User Manual_v2.2.pdf`
- `reference/OrangePi5Plus/Datasheet/*.pdf`
- `reference/rk3588-TRM-and-Datasheet/*.pdf`
- `reference/OrangePi5Plus/Benchmarks/*.txt`

---

## RK3588 SoC 사양

### 프로세서 (CPU)

- **아키텍처**: ARM big.LITTLE
- **Big Cores**: 4x Cortex-A76 @ 2.4GHz (실측 2.256GHz)
- **Little Cores**: 4x Cortex-A55 @ 1.8GHz (실측 1.800GHz)
- **공정**: 8nm
- **클러스터**: 3개 (A55 x4, A76 x2, A76 x2)

### GPU

- **모델**: ARM Mali-G610 MP4
- **최대 클럭**: 1000MHz
- **API**: OpenGL ES 3.2, Vulkan 1.2, OpenCL 2.2

### NPU

- **성능**: 6 TOPS
- **코어**: 3-core
- **최대 클럭**: 1000MHz

### VPU (비디오)

- **디코딩**: H.264/H.265 8K@60fps, VP9/AV1 4K@60fps
- **인코딩**: H.264/H.265 4K@60fps

### 메모리

- **타입**: LPDDR4/LPDDR4X/LPDDR5
- **최대**: 16GB
- **클럭**: 최대 2112MHz

---

## Orange Pi 5 Plus 보드

### 메모리 옵션

- 4GB / 8GB / 16GB LPDDR4X

### 스토리지

- eMMC (모델별 상이)
- microSD 카드
- M.2 NVMe SSD (PCIe 3.0 x4)

### 네트워크

- **이더넷**: Realtek RTL8125 2.5GbE x2
- **WiFi/BT**: Realtek 8822BU (옵션)

### 전원

- DC 12V/2A
- USB-C PD (5V~20V)

---

## Ubuntu Rockchip OS

### 지원 버전

- **Ubuntu 22.04 LTS** (Rockchip Linux 5.10)
- **Ubuntu 24.04 LTS** (Rockchip Linux 6.1)

### 주요 특징

- apt 패키지 관리
- 3D 하드웨어 가속 (Panfork Mesa)
- GNOME 데스크톱 (Wayland)
- 4K 비디오 재생 지원

### 설치

1. [이미지 다운로드](https://github.com/Joshua-Riek/ubuntu-rockchip/releases)
2. [USBimager](https://bztsrc.gitlab.io/usbimager/) 또는 [balenaEtcher](https://www.balena.io/etcher)로 SD 카드에 굽기
3. 부팅 (첫 부팅 2분까지 소요)

### 로그인

- **사용자**: ubuntu
- **비밀번호**: ubuntu

---

## 성능 벤치마크

### CPU 성능

| 항목 | 값 |
|------|------|
| 7-Zip MIPS | 16,610 |
| 싱글 스레드 | 3,121 |
| A76 memcpy | 12,340 MB/s |
| A76 memset | 29,542 MB/s |

### 암호화 (AES-256-CBC)

| 코어 | 성능 |
|------|------|
| A55 | 846,812 kB/s |
| A76 | 1,285,368 kB/s |

### 네트워크

- Realtek RTL8125 2.5GbE x2 (PCIe 2.0 x1)

### 온도

- 아이들: 54.5°C
- 부하 후: 56.4°C
- 스로틀링: 없음

---

## 참고 링크

- [Ubuntu Rockchip](https://github.com/Joshua-Riek/ubuntu-rockchip)
- [Orange Pi 공식](https://www.orangepi.org/)
- [sbc-bench](https://github.com/ThomasKaiser/sbc-bench)
