# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 28 skeleton, trung bình 15.96 khớp có v > 0 mỗi người
- Tổng: v=2 364 | v=1 83 | v=0 29

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 22 | 6 | 0 | 21% |
| 1 | left_eye | 21 | 7 | 0 | 25% |
| 2 | right_eye | 20 | 8 | 0 | 29% |
| 3 | left_ear | 12 | 16 | 0 | 57% |
| 4 | right_ear | 15 | 13 | 0 | 46% |
| 5 | left_shoulder | 28 | 0 | 0 | 0% |
| 6 | right_shoulder | 28 | 0 | 0 | 0% |
| 7 | left_elbow | 24 | 4 | 0 | 14% |
| 8 | right_elbow | 25 | 3 | 0 | 11% |
| 9 | left_wrist | 25 | 3 | 0 | 11% |
| 10 | right_wrist | 23 | 4 | 1 | 14% |
| 11 | left_hip | 21 | 5 | 2 | 18% |
| 12 | right_hip | 24 | 2 | 2 | 7% |
| 13 | left_knee | 21 | 4 | 3 | 14% |
| 14 | right_knee | 21 | 4 | 3 | 14% |
| 15 | left_ankle | 18 | 1 | 9 | 4% |
| 16 | right_ankle | 16 | 3 | 9 | 11% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
