# RK3588 미디어 및 가속

## 출처 (Sources)

- `reference/rknn-toolkit2/rknpu2/examples/3rdparty/mpp/`
- `reference/rknn-toolkit2/rknpu2/examples/3rdparty/rga/`
- `reference/ubuntu-rockchip/README.md`

---

## RKMPP (Rockchip Media Process Platform)

### 지원 코덱

| 코덱 | 디코딩 | 인코딩 | 최대 해상도 |
|------|--------|--------|-----------|
| H.264/AVC | O | O | 8K@60fps / 4K@60fps |
| H.265/HEVC | O | O | 8K@60fps / 4K@30fps |
| VP9 | O | X | 4K@60fps |
| AV1 | O | X | 4K@60fps |

### 주요 API

```c
MppCtx mpp_ctx;
mpp_create(&mpp_ctx, &mpp_mpi);
mpp_init(mpp_ctx, MPP_CTX_DEC, MPP_VIDEO_CodingHEVC);
mpp_mpi->decode(mpp_ctx, packet, &frame);
```

---

## Mali-G610 GPU

### 사양

- **모델**: Mali-G610 MP4
- **최대 클럭**: 1000MHz
- **API**: OpenGL ES 3.2, Vulkan 1.2, OpenCL 2.2

### 드라이버 설치

```bash
add-apt-repository ppa:jjriek/panfork-mesa
apt-get install mali-g610-firmware libmali-g610-x11
```

### 지원 기능

- Wayland GNOME 데스크톱
- 4K YouTube (Chromium)
- 4K 비디오 (MPV)

---

## RGA (2D 가속)

### 기능

- 이미지 포맷 변환 (YUV ↔ RGB)
- 크기 조정, 회전, 자르기
- 블렌딩, 합성

### 라이브러리

```bash
export LD_LIBRARY_PATH=./lib:<LOCATION_LIBRGA.SO>
```

---

## FFmpeg 통합

### RKMPP 코덱

- `h264_rkmpp`: H.264 하드웨어 인코딩/디코딩
- `hevc_rkmpp`: H.265 하드웨어 인코딩/디코딩

### 사용 예시

```bash
ffmpeg -i input.mp4 -c:v h264_rkmpp -b:v 5M output.h264
```

---

## 버퍼 요구사항

- **64바이트 정렬**: MPP 필수
- **IOMMU 지원**: 메모리 관리 최적화

---

## 참고

- [RKMPP GitHub](https://github.com/rockchip-linux/mpp)
- [librga GitHub](https://github.com/airockchip/librga)
