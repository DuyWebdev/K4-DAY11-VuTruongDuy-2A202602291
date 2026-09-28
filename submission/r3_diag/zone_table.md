# Zone table — B4-center

## IoU 0.50 — L (locked annotation)

| zone | matched | missing | spurious |
|---|---:|---:|---:|
| center | 9 | 3 | 4 |
| mid | 2 | 3 | 2 |
| edge | 1 | 2 | 0 |

## IoU 0.50 — M (reference/model side)

| zone | matched | missing | spurious |
|---|---:|---:|---:|
| center | 8 | 4 | 7 |
| mid | 3 | 2 | 4 |
| edge | 2 | 1 | 1 |

## Nhận xét

- Ở IoU 0.50, zone center có nhiều đối tượng nhất ở cả hai phía.
- L side có matched: 9 center, 2 mid, 1 edge.
- M side có matched: 8 center, 3 mid, 2 edge.
- Kết quả IoU thay đổi theo ngưỡng 0.30 / 0.50 / 0.70; khi tăng ngưỡng, số matched giảm ở một số zone và số missing/spurious tăng.
- Bảng trên được lấy trực tiếp từ kết quả `iou-sweep` của B4-center.