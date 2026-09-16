# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Trần Tuấn Anh  Nhóm: None   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | v=2 376 | v=1 56 | v=0 61 |
| Thời gian trung bình mỗi ảnh | 6 phút|

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `left_wrist`
2. `right_wrist`
3. `left_knee`

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

Không, bởi hầu hết các ảnh đều lộ rõ phần bên trái hoặc các phần này khá dễ để dự đoán. Trong khi các phần bên phải lại bị che khuất và khó để "giải phẫu" và đưa ra skeleton chính xác.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.9189  |  0.9355 |
| OKS@0.50 | 1.0 | 1.0 |
| OKS@0.75 | 1.0 | 1.0 |
| Lỗi `dao_trai_phai` | 0 | 0 |
| Lỗi `nham_nguoi` | 1 | 0 |
| Lỗi `xoa_khop_bi_che` | 2 | 1 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- `train_02.jpg`, `người #1`, khớp `left_ear`: trước đó bị bỏ trống (v=0) nên tính 0 điểm (thieu_khop), sau đó đã gán lại v=1 với vị trí ước lượng.
- `train_04.jpg`, `người #1`, khớp `left_wrist`: trước đó bị gán lànham_nguoi - chấm đặt gần cổ tay của người khác trong ảnh, sau đó tiến hành gán lại cho hợp lý.
- `train_06.jpg`, `người #1`, khớp `left_ear`: trước đó là `thieu_khop (v=0)`, sau đó xem xét và tiến hành gán lại v=1 với vị trí ước lượng. 

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->
Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.

## 3. Kiểm chéo

Bạn cùng nhóm: NONE

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

- Phần này làm solo nên không có rule mới.

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.845 |0.845 | 0.0 |
| pose_mAP50-95 |0.6853 | 0.6908 | 0.0055 |
| pose_precision | 0.9734 | 0.9792 | 0.0058 |
| pose_recall | 0.8462 | 0.8462 | 0.0 |
| box_mAP50-95 | 0.8119 | 0.8041 | 0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

Phần `pose_mAP50-95` tăng khoảng 0.0055 nên nếu giảm thì có thể là do bản thân đang đánh sai ảnh hoặc là do lượng ảnh đưa vào chưa đủ nhiều.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

Bài làm có chênh trước Fine-tuned là 0.9785 − 0.845 = 0.1335 và sau Fine-tuned: 0.96 − 0.845 = 0.115. Model tìm người (box) dễ hơn tìm khớp nhiều - vì box mAP chỉ cần khoanh đúng vùng chứa người (dung sai IoU rộng), còn pose mAP (OKS) đòi hỏi từng điểm khớp rơi đúng vị trí trong bán kính rất nhỏ, dễ sai khi khớp bị che.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

`train_03`: model tìm ra 4 người trong khi bản thân chỉ gán 2 người. Nhưng `train_03` chỉ có 2 người và có thêm vài cái ngoài như búp bê, xe đạp... (Có thể modal bị nhầm do trong hình ảnh gán có những thứ bị che bởi xe)

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

`train_13, OKS = 0.629` (thấp nhất trong toàn bộ danh sách). Xếp sau là `train_15 (0.652)` và cũng `train_13` ở một người khác trong cùng ảnh `(0.679)` - tức train_13 có 2 trong 3 người bị model đoán lệch nặng. Em nghĩ cả hai đều không đúng hoàn toàn, chủ yếu là do phần ảnh mờ và có vấn đề trong việc gán.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

Có, cả 2 gần như khớp

| Xếp hạng	| Tự làm vs Gold | Model vs Tự làm |
| --- | --- | --- | 
|Tệ nhất | `train_15 (OKS 0.8435)` | `train_13 (OKS 0.629)` |
| Nhì |	`train_13 (OKS 0.8441)` |`train_15 (OKS 0.652)` |

Hai ảnh tệ nhất giống hệt nhau ở cả hai bảng xếp hạng, chỉ đổi chỗ thứ 1-2. Điều này nói lên: `train_13` và `train_15` là hai tấm ảnh khá khó (phần bị che khá nhiều và lượng thông tin để đoán khá ít).

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

Bên `train_13`, em quyết định xài `v=1` cho người thứ 3 (ở xa và mờ nhất) bởi vẫn thấy người đó nhưng vì quá mờ nên quyết định gái `v=1` thay vì `v=0`. Lý do chọn cũng vì thông tin, và người đó đang trong phạm vi có thể gán nhãn chứ không phải ở quá xa hoặc quá mờ.