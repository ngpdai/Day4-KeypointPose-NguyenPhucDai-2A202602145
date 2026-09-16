# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên:Nguyen Phuc Dai  Nhóm: ______   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán |20 |
| Số skeleton |32 |
| v=2 / v=1 / v=0 |384 / 112 / 48 |
| Thời gian trung bình mỗi ảnh |4.2p |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1.left_hip: 45%
2.right_hip: 42%
3.left_wrist: 38%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.
Các khớp hông đúng là vị trí khó gán nhất do hoàn toàn bị che lấp bởi quần áo và ghế ngồi cabin. Khớp cổ tay cũng thường xuyên bị che lấp bởi vô-lăng và các thao tác điều khiển.
<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình |0.74 |0.88 |
| OKS@0.50 |0.82 |0.94 |
| OKS@0.75 |0.68   |0.85   |
| Lỗi `dao_trai_phai` |2 |0 |
| Lỗi `nham_nguoi` |1 | 0|
| Lỗi `xoa_khop_bi_che` | 3| 0|

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->
 
-train_07.jpg, người thứ 2, khớp right_shoulder & right_elbow: Sửa lỗi đảo trái/phải. Đã xoay lại đúng hệ cơ thể nhân vật.
-train_14.jpg, người thứ 1, khớp left_wrist: Sửa lỗi nhầm người sang tay nhân vật ngồi cạnh.
-train_03.jpg, người thứ 1, 3 khớp thân dưới: Gán lại từ v=0 (xoá/không chấm) sang v=1 và ước lượng toạ độ do còn trong khung hình.  

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?
Đây là một ảnh dễ, nhưng sai sót phát sinh do chủ quan thao tác nhanh và nhìn theo góc nhìn màn hình thay vì tưởng tượng góc nhìn từ chính cơ thể người trong ảnh.
<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 |0.845 |0.845 |0.000 |
| pose_mAP50-95 |0.685 |0.703 | +0.018|
| pose_precision | 0.975|0.981 |+0.006 |
| pose_recall |0.846 |0.846 |0.000 |
| box_mAP50-95 |0.811 |0.807 |-0.004 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
Tăng nhẹ +0.018 (từ 0.685 lên 0.703). 20 ảnh cabin bổ sung tập trung dạy model tinh chỉnh lại dung sai vị trí các khớp hay bị che khuất trong không gian hẹp (như cổ tay cầm vô-lăng hay hông bị ghế che).
2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
box_mAP50-95 (0.807) cao hơn pose_mAP50-95 (0.703) khoảng 0.104. Model nhận diện khung thân người (box) dễ hơn nhiều so với việc định vị chính xác 17 điểm khớp.
3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
Ảnh test_04.jpg bị lỗi lệch nhẹ (Float) ở khớp cổ tay và nhầm người ở vùng 2 hành khách ngồi sát nhau.  
4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
Ảnh test_09.jpg có OKS = 0.62. Nhãn người gán đúng hơn vì dựa trên việc kéo zoom 200% để phát hiện khớp khuỷu tay bị che khuất một phần dưới bóng râm, trong khi model bị trượt điểm ra ngoài mép áo.
5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
Ảnh train_18.jpg trùng khớp ở cả 2 danh mục. Điều này phản ánh bức ảnh có chất lượng nguồn kém (bị mờ nhoè và che lấp phức tạp), làm giảm độ chính xác của cả người gán nhãn lẫn mô hình.  
## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.
Tại ảnh train_05.jpg, nhân vật người lái xe có cổ tay phải (right_wrist) bị phần vô-lăng che khuất khoảng 80%. Quan sát thực tế cho thấy cẳng tay phải kéo dài hướng thẳng về viền trên của vô-lăng và ngón tay lấp hé ra phía sau. Do phần khớp vẫn hoàn toàn nằm bên trong khung hình (không bị mép ảnh cắt ngang), tôi quyết định chọn trạng thái v = 1 (Occluded) thay vì v = 0 (Outside). Vị trí chấm được đặt tại điểm ước lượng giao nhau giữa trục cẳng tay và vành vô-lăng để đảm bảo đủ 17 điểm keypoint cho model học tập.
<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
