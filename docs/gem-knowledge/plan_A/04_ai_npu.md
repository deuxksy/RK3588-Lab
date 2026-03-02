# RK3588 AI/NPU 개발 가이드

## 출처 (Sources)

- `reference/rknn-toolkit2/README.md` (81줄)
- `reference/rknn-toolkit2/CHANGELOG.md`

---

## RKNN 소프트웨어 스택

```
Applications (Python/C++)
    ↓
RKNN-Toolkit-Lite2 / RKNN Runtime
    ↓
RKNPU Kernel Driver
    ↓
NPU Hardware (6 TOPS)
```

---

## 지원 플랫폼

- RK3566 / RK3568
- **RK3588** (3-core NPU, 6 TOPS)
- RK3562
- RV1103 / RV1106

---

## 설치

### 지원 환경

- Ubuntu 18.04: Python 3.6/3.7
- Ubuntu 20.04: Python 3.8/3.9
- Ubuntu 22.04: Python 3.10/3.11

### 설치 명령

```bash
pip install rknn-toolkit2
```

---

## 모델 변환

### 기본 프로세스

```python
from rknn.api import RKNN

rknn = RKNN()
rknn.config(
    mean_values=[[0, 0, 0]],
    quantized_dtype='asymmetric_quantized-8',
    target_platform='rk3588'
)
rknn.load_onnx(model='model.onnx')
rknn.build(do_quantization=True, dataset='dataset.txt')
rknn.export_rknn('model.rknn')
```

### 지원 모델 포맷

- ONNX (Opset 12~19)
- PyTorch (> 1.6.0)
- TensorFlow (1.12-1.15, 2.3-2.5)
- TFLite
- Caffe
- Darknet

---

## 양자화

### 옵션

- `normal` (기본값)
- `mmse` (최소 평균 제곱 오차)

### 혼합 양자화 (INT8 + FP16)

```python
rknn.config(
    quantized_dtype='asymmetric_quantized-8',
    hybrid_quantization_file='./quantization.json'
)
```

---

## 주요 오퍼레이터

### ONNX 지원

- Conv, ConvTranspose, MaxPool, AvgPool
- BatchNormalization, Relu, Sigmoid, Tanh
- Reshape, Transpose, Concat, Split
- LSTM, GRU, MatMul, Softmax

---

## 연결 보드 설정

### Linux

```bash
adb push Linux/rknn_server/aarch64/usr/bin/* /usr/bin/
adb push Linux/librknn_api/aarch64/librknnrt.so /usr/lib/
chmod +x /usr/bin/rknn_server
restart_rknn.sh
```

---

## 버전 1.6.0 주요 변경사항

- ONNX Opset 12~19 지원
- 사용자 정의 오퍼레이터 지원
- Transformer 지원 개선
- RK3588 INT4*INT4->INT16 지원
- 동적 가중치 합성곱, Layernorm, RoiAlign 최적화

---

## 참고 자료

- [RKNN-Toolkit2 GitHub](https://github.com/airockchip/rknn-toolkit2)
- [RKNN Model Zoo](https://github.com/airockchip/rknn_model_zoo)
- [RGA GitHub](https://github.com/airockchip/librga)
