# PointNet2-for-3D-Detection

Dự án này là một cài đặt của **PointNet++ Mở Rộng** cho bài toán phát hiện vật thể 3D trên dữ liệu point cloud, theo định dạng dataset KITTI.

---

## 1. Tải dữ liệu

Chúng ta sử dụng bộ dữ liệu KITTI (Velodyne point clouds và nhãn).  
Tải về từ Kaggle:  
👉 [KITTI Dataset trên Kaggle](https://www.kaggle.com/datasets/klemenko/kitti-dataset)

Sau khi tải, tổ chức dữ liệu theo cấu trúc sau:

```
PointNet2-for-3D-detection/
│
├── data/
│   ├── kitti/
│   │   ├── training/
│   │   │   ├── velodyne/        # file .bin chứa point clouds
│   │   │   ├── label_2/         # file .txt chứa nhãn
│   │   │   └── calib/           # file hiệu chỉnh (calibration)
│   │   └── testing/
│   │       └── velodyne/        # file .bin dùng cho test
```

---

## 2. Cài đặt môi trường

Clone repo:
```bash
git clone https://github.com/GitPi888/PointNet2-for-3D-detection.git
cd PointNet2-for-3D-detection
```

Cài đặt các thư viện cần thiết:
```bash
pip install -r requirements.txt
```

---

## 3. Tiền xử lý dữ liệu

Sử dụng script có sẵn để tiền xử lý dữ liệu KITTI thành định dạng phù hợp:

```bash
cd preprocess
python preprocess_kitti.py --data_path ../data/kitti/training
```

---

## 4. Huấn luyện mô hình

Huấn luyện mô hình với file cấu hình mặc định:
```bash
cd models
python train.py --config ../configs/config.yaml
```

Checkpoint của mô hình sẽ được lưu trong thư mục `checkpoints/`.

---

## 5. Đánh giá & Dự đoán

Chạy đánh giá trên tập validation/test:
```bash
python eval.py --config ../configs/config.yaml --checkpoint ../checkpoints/model.pth
```

Chạy dự đoán trên một point cloud cụ thể:
```bash
python inference.py --pointcloud ../data/kitti/testing/velodyne/000000.bin                     --checkpoint ../checkpoints/model.pth
```

---

## 6. Trực quan hóa

Dự án cung cấp công cụ để hiển thị point cloud và bounding box dự đoán.

Chạy notebook demo:
```bash
jupyter notebook demo_viz.ipynb
```

---

## 7. Cấu trúc dự án

```
PointNet2-for-3D-detection/
├── configs/         # File cấu hình
├── data/            # Dữ liệu KITTI (sau khi tải)
├── models/          # Mô hình và script huấn luyện
├── preprocess/      # Script tiền xử lý dữ liệu
├── visualizer/      # Công cụ trực quan hóa
├── checkpoints/     # Mô hình đã huấn luyện
└── README.md        # Tài liệu dự án
```

---

## 8. Tham khảo

- [PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space (Qi et al.)](https://arxiv.org/abs/1706.02413)  
- [KITTI Vision Benchmark Suite](http://www.cvlibs.net/datasets/kitti/)  
