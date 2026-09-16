# Mini guideline - nhóm: ______  |  người gán: Phan Tấn Đạt  |  ngày: 16/9/2026

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
| Hông của người mặc quần áo dài |Vị trí vòng 2, vùng có chiều rộng tăng bất thường |vị trí này thường phình to do áo chồng quần (train_03.jpg) |
| Tai bị tóc hoặc mũ bảo hiểm che một phần |chọn 'bị che', vị trí 2 tai song song 2 mắt. khoảng cách tùy góc nghiêng của đầu |nguyên lý giải phẫu cơ thể người (train_04.jpg) |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) |Chỉ ghi nhận những bộ phận nhìn thấy |Không đoán vì kích thước cơ thể mỗi người khác nhau (không có sample) |
| Cổ tay nằm sau tay lái / sau thân mình |chọn 'bị che', lấy khoảng cách cổ tay-khuỷu tay ~ khuỷu tay-vai |nguyên lý giải phẫu cơ thể người (train_18.jpg) |
| Hai người chồng lên nhau |Chỉ đoán bộ phận 'bị che' cạnh bộ phận thấy được nếu có bằng chứng. Còn lại bỏ nếu không thấy |Không đoán vì kích thước cơ thể mỗi người khác nhau (train_03.jpg) |
| Người nhỏ đến mức nào thì không gán nữa |Khi kích thước < 100 px |Quá mờ và bé để có thể phân biệt bộ phận cơ thể (không có sample) |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_03.jpg`, người thứ `2`, khớp `Left_Elbow`

- Mơ hồ ở chỗ nào: Không rõ vị trí ở sau người thứ 1
- Bạn quyết thế nào: sample từ khớp 'Right_Elbow', chiếu giải phẫu + POV và đặt khớp `Left_Elbow`
- Vì sao: Giải phẫu cơ thể người
- Nếu người khác quyết ngược lại thì model học sai cái gì: vị trí của khớp `Left_Elbow` sẽ nằm lung tung không xác định.

### Ca 2 - ảnh `train02.jpg`, người thứ `1`, khớp `3 khớp mắt + mũi`

- Mơ hồ ở chỗ nào: Người quay lưng lại với camera
- Bạn quyết thế nào: Đặt ra ngoài mép ảnh (v=0), không đoán
- Vì sao: Không có cơ sở để đoán
- Nếu người khác quyết ngược lại thì model học sai cái gì: Các khớp sẽ nằm lung tung không xác định.

### Ca 3 - ảnh `train13.jpg`, người thứ `2`, khớp `Các khớp bên trái cơ thể trừ thuộc phần đầu`

- Mơ hồ ở chỗ nào: Ảnh mờ, 1 phần cơ thể bị che bởi người thứ 1
- Bạn quyết thế nào: Đặt ra ngoài mép ảnh (v=0), không đoán
- Vì sao: Không có cơ sở để đoán
- Nếu người khác quyết ngược lại thì model học sai cái gì: Các khớp sẽ nằm lung tung không xác định.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_ear` (bạn `38%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: guideline chưa rõ
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Tình huống 2
