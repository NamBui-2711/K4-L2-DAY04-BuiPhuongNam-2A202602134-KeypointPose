# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 14.31 khớp có v > 0 mỗi người
- Tổng: v=2 348 | v=1 67 | v=0 78

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 2 | 5 | 7% |
| 1 | left_eye | 21 | 2 | 6 | 7% |
| 2 | right_eye | 23 | 2 | 4 | 7% |
| 3 | left_ear | 11 | 12 | 6 | 41% |
| 4 | right_ear | 19 | 9 | 1 | 31% |
| 5 | left_shoulder | 27 | 2 | 0 | 7% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 24 | 1 | 4 | 3% |
| 8 | right_elbow | 26 | 1 | 2 | 3% |
| 9 | left_wrist | 17 | 6 | 6 | 21% |
| 10 | right_wrist | 18 | 7 | 4 | 24% |
| 11 | left_hip | 18 | 7 | 4 | 24% |
| 12 | right_hip | 24 | 4 | 1 | 14% |
| 13 | left_knee | 17 | 4 | 8 | 14% |
| 14 | right_knee | 22 | 2 | 5 | 7% |
| 15 | left_ankle | 16 | 1 | 12 | 3% |
| 16 | right_ankle | 15 | 4 | 10 | 14% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
