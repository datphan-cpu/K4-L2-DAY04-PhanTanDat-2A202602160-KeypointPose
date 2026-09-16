# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Phan Tấn Đạt   Nhóm: ______   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán |20 |
| Số skeleton |29 |
| v=2 / v=1 / v=0 |326 / 79 / 88 |
| Thời gian trung bình mỗi ảnh |3 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear
2. right_ear
3. left_wrist

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->
1. left_ear và right_ear khá khó để xác định chính xác vị trí cho dù đã sử dụng kiến thức giải phẫu vì phần lớn ảnh là người được gán nhãn quay đầu ngược lại camera => không thế xác định rõ khuôn mặt.
2. left_wrist và các khớp bằng điểm không khó vì luôn gán nhãn theo kiến thức giải phẫu. Sai số chỉ xảy ra vì thời gian gán nhãn ngắn => ít chỉnh sửa kỹ.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình |0.9226 |0.9226 |
| OKS@0.50 |1.0 |1.0 |
| OKS@0.75 |0.9655 |0.9655 |
| Lỗi `dao_trai_phai` |0 |0 |
| Lỗi `nham_nguoi` |1 |1 |
| Lỗi `xoa_khop_bi_che` |11 |11 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- Sau khi check vs golđ => không sửa đổi thay đổi gì
-
-

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->
“Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.”

## 3. Kiểm chéo

Bạn cùng nhóm: Không có

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
| pose_mAP50 |0.845 |0.845 |0.0 |
| pose_mAP50-95 |0.6853 |0.6908 |0.0055 |
| pose_precision |0.9734 |0.9792 |0.0058 |
| pose_recall |0.8462 |0.8462 |-0.0185 |
| box_mAP50-95 |0.8119 |0.8041 |-0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
- tăng 0.55 điểm phần trăm (khoảng +0.8% tương đối). => Không giảm, mà tăng rất nhẹ.

20 ảnh đã dạy model, việc pose_mAP50-95 tăng nhưng rất ít cho thấy:
   - 20 ảnh giúp model tinh chỉnh vị trí khớp người một chút, nhưng đồng thời làm giảm tính tổng quát của head phát hiện người (bounding box), dẫn đến box mAP giảm.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm *khớp* dễ hơn? Vì sao?
- Dùng kết quả sau fine-tune: 0.9600 - 0.8450 = 0.115
- Kết luận: Model tìm người dễ hơn tìm khớp.
- Lý do:
  - Bounding box chỉ cần xác định vùng chứa người.
  - Pose estimation phải xác định chính xác từng keypoint (vai, khuỷu tay, cổ tay, đầu gối...).
  - Chỉ cần vài điểm lệch là OKS giảm mạnh.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
- Ảnh test_02 - lỗi 'nhầm người'

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
- Ảnh train_13 - Model (0.639) vs ban (0.934)
- Ai đúng? Không thể kết luận ai đúng.
- Vì: OKS chỉ đo: Mức độ giống nhau giữa model và nhãn của bạn. Không đo ai gần ground truth hơn
- Nếu nhìn bằng mắt để xác định: em chuẩn xác hơn vì làm theo guideline có sẵn.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
- Ảnh train_13: 
   - đông người 
   - 2 người bị mờ, khó phân định vị trí các khớp
   - 1 người bị che 1 nửa

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người, khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

- Train_03 + người thứ 2 + các keypoint mang tag 'Left' về chân
- Vẫn nhìn thấy 1 số phần tách biệt của các bộ phận cơ thể => theo Luật 5: Hai người chồng lên nhau => đánh nhãn v=1 cho các khớp đó.
