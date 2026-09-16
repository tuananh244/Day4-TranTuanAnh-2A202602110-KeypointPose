# Mini guideline - nhóm: unknown  |  người gán: Trần Tuấn Anh  |  ngày: 16/09/2026

> Điền foile này **trng lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao | Screenshot |
| --- | --- | --- | --- |
| Hông của người mặc quần áo dài | Vẫn giữ nguyên, không chọn Occluded | Mặc dù bị che nhưng vẫn là phần thấy rõ, không cần thiết phải chọn Occluded | ![anh_bi_che2](.\screenshot\anh_bi_che2.png) |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Nếu chỉ  bị che một phần nhưng vẫn rõ mặt thì tiến hành dự đoán và để ở mức `Occluded` nếu ảnh quá mờ hoặc quá xa, còn nếu rõ ràng như `ảnh 1` thì gán như bình thường | Ảnh rõ ràng, dễ dự đoán theo tỉ lệ khuôn mặt và hình ảnh. | ![anh_bi_che2](.\screenshot\anh_bi_che2.png) | 
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Bỏ đi các thông tin dưới hông | Vẫn thể hiện được đây là `person`, không cần phải vẽ toàn bộ trong phần ảnh bị thiết dẫn đến model nhận sai. | ![anh_bi_che2](.\screenshot\anh_bi_che2.png)|
| Cổ tay nằm sau tay lái / sau thân mình | Dự đoán phần cổ tay và để ở mode `Occluded` | Phần cổ tay khá dễ đoán (như trong ảnh) nên tiến hành dự đoán và đặt ở phần `Occluded` để sau dữ liệu train đầy đủ hơn | [anh_bi_che3](.\screenshot\anh_bi_che3.png) |
| Hai người chồng lên nhau | Nếu người bị che bị mất đi quá nhiều thông tin hình ảnh, tiến hành `outside` các node tương ứng | Bởi các thông tin bị mơ hồ nên không tiến hành gán để tránh việc mô hình train sai sót | ![anh_bi_che](.\screenshot\anh_bi_che.png) |
| Người nhỏ đến mức nào thì không gán nữa | Như trong ảnh thì có thể tồn tại người ở phía đối diện bờ sông nhưng hình ảnh quá nhỏ nên tiến hành bỏ qua | Quá nhỏ để có thể gán và để mô hình `train` một cách chính xác | ![anh_bi_che4](.\screenshot\anh_bi_che4.png) |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_01`, người thứ  `1`, khớp `phần tay trái bị che khuất bởi bánh pizza`

- Mơ hồ ở chỗ nào: Phần tay không thể xác định rõ ràng đang nằm ở vị trí nào
- Bạn quyết thế nào: Dự đoán cách cầm ở phần rìa trên bánh, dùng Occluded thể hiện vật thể bị che kbuaast.
- Vì sao: Vì đây là phần có thể dự đoán được nên không cần tiến hành outside
- Nếu người khác quyết ngược lại thì model học sai cái gì: Modal có thể bị nhầm lẫn hoặc không ảnh hưởng quá lớn vì có nhiều yếu tố quyết định phần tay này (nhiều ảnh có tay)

### Ca 2 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 3 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
