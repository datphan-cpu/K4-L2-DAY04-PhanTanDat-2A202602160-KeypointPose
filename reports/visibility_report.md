# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 13.97 khớp có v > 0 mỗi người
- Tổng: v=2 326 | v=1 79 | v=0 88

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 23 | 0 | 6 | 0% |
| 1 | left_eye | 21 | 2 | 6 | 7% |
| 2 | right_eye | 21 | 1 | 7 | 3% |
| 3 | left_ear | 13 | 11 | 5 | 38% |
| 4 | right_ear | 17 | 9 | 3 | 31% |
| 5 | left_shoulder | 25 | 3 | 1 | 10% |
| 6 | right_shoulder | 28 | 1 | 0 | 3% |
| 7 | left_elbow | 24 | 3 | 2 | 10% |
| 8 | right_elbow | 24 | 4 | 1 | 14% |
| 9 | left_wrist | 18 | 6 | 5 | 21% |
| 10 | right_wrist | 20 | 6 | 3 | 21% |
| 11 | left_hip | 19 | 5 | 5 | 17% |
| 12 | right_hip | 20 | 6 | 3 | 21% |
| 13 | left_knee | 14 | 5 | 10 | 17% |
| 14 | right_knee | 14 | 6 | 9 | 21% |
| 15 | left_ankle | 14 | 4 | 11 | 14% |
| 16 | right_ankle | 11 | 7 | 11 | 24% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
