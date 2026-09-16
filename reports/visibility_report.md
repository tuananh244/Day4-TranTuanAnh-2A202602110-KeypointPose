# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 14.9 khớp có v > 0 mỗi người
- Tổng: v=2 376 | v=1 56 | v=0 61

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 21 | 4 | 4 | 14% |
| 1 | left_eye | 19 | 3 | 7 | 10% |
| 2 | right_eye | 22 | 4 | 3 | 14% |
| 3 | left_ear | 21 | 4 | 4 | 14% |
| 4 | right_ear | 22 | 4 | 3 | 14% |
| 5 | left_shoulder | 27 | 1 | 1 | 3% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 23 | 5 | 1 | 17% |
| 8 | right_elbow | 26 | 2 | 1 | 7% |
| 9 | left_wrist | 22 | 6 | 1 | 21% |
| 10 | right_wrist | 22 | 5 | 2 | 17% |
| 11 | left_hip | 26 | 2 | 1 | 7% |
| 12 | right_hip | 27 | 1 | 1 | 3% |
| 13 | left_knee | 18 | 5 | 6 | 17% |
| 14 | right_knee | 21 | 2 | 6 | 7% |
| 15 | left_ankle | 15 | 4 | 10 | 14% |
| 16 | right_ankle | 16 | 3 | 10 | 10% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
