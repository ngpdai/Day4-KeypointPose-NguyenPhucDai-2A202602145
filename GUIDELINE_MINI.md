# Mini guideline - nhóm: ______  |  người gán: Nguyen Phuc Dai  |  ngày: 16/09/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài |Ước lượng vị trí khớp hông dựa trên cấu trúc xương chậu và vị trí nối giữa thắt lưng với đùi, gắn cờ |Khớp hông nằm dưới quần áo không có bề mặt nhìn thấy trực tiếp; bắt buộc ước lượng giải phẫu để giữ đủ 17 điểm cho model. (Kèm ảnh screenshot CVAT vị trí 2 khớp hông v=1 trên áo dài/quần rộng). |
| Tai bị tóc hoặc mũ bảo hiểm che một phần |Nếu vẫn nhìn thấy gốc tai hoặc đoán chắc chắn vị trí qua phom đầu -> gắn v = 2 (visible). Nếu bị che hoàn toàn -> đặt chấm ước lượng và gắn v = 1 (occluded). |Tai bị che nhẹ vẫn còn điểm mốc thị giác rõ ràng; phân biệt rõ để tránh gán nhầm cờ v = 0 làm mất thông tin OKS. (Kèm ảnh screenshot CVAT tai dưới vệt tóc). |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) |Các khớp từ hông trở lên gán bình thường (v = 2 hoặc v = 1). Các khớp bị cắt ra ngoài khung ảnh (đầu gối, cổ chân) -> tick Outside (v = 0) và không đặt chấm. |Khớp ngoài khung hình thuộc quy tắc v = 0 chuẩn của COCO; không đặt toạ độ bừa bãi ra ngoài ảnh. (Kèm ảnh screenshot CVAT người bị cắt nửa thân dưới). |
| Cổ tay nằm sau tay lái / sau thân mình |Đặt chấm ước lượng tại vị trí khớp cổ tay dựa theo hướng cẳng tay và bàn tay, tick Occluded (v = 1).|Khớp vẫn còn nằm trong khung hình nhưng bị vật thể (tay lái/thân mình) che khuất. (Kèm ảnh screenshot CVAT cổ tay bị vô-lăng che). |
| Hai người chồng lên nhau |Gán hoàn chỉnh 17 điểm cho từng người một. Điểm người này bị người kia che -> đặt chấm ước lượng và tick |Tránh lỗi "nhầm người" (kéo đường nối từ người này sang người khác). (Kèm ảnh screenshot CVAT 2 skeleton tách biệt khi đứng đè lên nhau). |
| Người nhỏ đến mức nào thì không gán nữa |Gán tất cả người trong khung hình mà mắt thường xác định được phom thân và có ít nhất 3 khớp còn trong khung. |Bộ ảnh cabin/giao thông đã được lọc chuẩn; gán triệt để để tránh bỏ sót person. (Kèm ảnh screenshot CVAT người ở background xa).   |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_03.jpg`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào:Cổ tay trái của tài xế bị vô-lăng che khuất hoàn toàn, chỉ thấy cẳng tay hướng về phía tay lái.
- Bạn quyết thế nào:Đặt chấm tại vị trí ước lượng nối tiếp cẳng tay chạm vô-lăng, đánh cờ
- Vì sao:Người vẫn nằm trong khung hình, tay không bị cắt qua mép ảnh.
- Nếu người khác quyết ngược lại thì model học sai cái gì:Model sẽ học sai rằng cổ tay biến mất khi cầm vô-lăng, làm sụt giảm khả năng dự đoán tư thế lái xe (DMS).

### Ca 2 - ảnh `rain_07.jpg`, người thứ `2`, khớp `right_shoulder & right_elbow`

- Mơ hồ ở chỗ nào:Người ngồi ghế phụ xoay lưng lại camera, không rõ vai phải hay vai trái bị vặn.
- Bạn quyết thế nào:Đứng từ góc độ cơ thể của nhân vật để xác định bên phải/bên trái, gán right_shoulder bên phải cơ thể nhân vật và tick v = 1 do bị quai balo che.
- Vì sao:Quy tắc cốt lõi là trái/phải tính theo cơ thể người, không tính theo góc nhìn bức ảnh.
- Nếu người khác quyết ngược lại thì model học sai cái gì:Xương vai sẽ bị cắt chéo qua thân (lỗi dao_trai_phai), khiến model khi lật ảnh (augmentation fliplr) bị học sai vĩnh viễn.

### Ca 3 - ảnh `train_12.jpg`, người thứ `1`, khớp `left_ankle`

- Mơ hồ ở chỗ nào:Người trong ảnh đứng ở mép dưới, bàn chân trái bị cắt ngang đúng qua cổ chân bởi viền ảnh.
- Bạn quyết thế nào:Tick Outside (v = 0) cho left_ankle và không đặt chấm toạ độ.
- Vì sao:Khớp đã bị rơi ra ngoài rìa khung ảnh, tuân thủ đúng luật v = 0.
- Nếu người khác quyết ngược lại thì model học sai cái gì:Model bị nhiễu toạ độ biên và tính sai chỉ số OKS khi huấn luyện.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_hip` (bạn `45%` / họ `15%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:Một bên coi hông mặc quần dài/áo rộng là che hoàn toàn nên tick v = 1, bên còn lại nhầm lẫn gán v = 2 hoặc dùng Outside (v = 0) khi không nhìn thấy bề mặt.
- Luật mới bổ sung vào mục 2 sau khi thống nhất:ất cả khớp hông bị che bởi quần áo đều bắt buộc tick v = 1 và đặt chấm ước lượng giải phẫu, không được gán v = 0 ngoại trừ trường hợp bị mép ảnh cắt mất hẳn.
