# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Đặng Hồng Anh   Nhóm: Solo   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.
ss
## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán |20 ảnh |
| Số skeleton |28 skeleton |
| v=2 / v=1 / v=0 | v=2 332 | v=1 109 | v=0 35 |
| Thời gian trung bình mỗi ảnh | 15.75 |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1.right_ear
2.left_ear
3.left_hip

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.
Đúng, bị che thì chỉ là phần đó bị che và dựa vào các khớp liền kề vẫn có thể xác định được vị trí của khớp bị che đó , còn khó xác định vị trí giải phẫu là khớp bị che toàn phần và những khớp gần nó có thể cũng bị che hoàn toàn bởi vật thể lớn.
<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình |0.9265 |0.921 |
| OKS@0.50 |0.9655 |1.0 |
| OKS@0.75 |0.9655 |1.0 |
| Lỗi `dao_trai_phai` |0| 0 |
| Lỗi `nham_nguoi` |2|1 |
| Lỗi `xoa_khop_bi_che` |0|0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- sửa ảnh train 013 do thiếu một người chưa đc gán nhãn
- Train 03 chỉnh lại vị trí hông của 2 người

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

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
| pose_mAP50 |0.845 |0.845 |0.0 |
| pose_mAP50-95 |0.6853 | 0.6908|0.0055 |
| pose_precision |0.9734 |0.9792 |0.0058 |
| pose_recall |0.8462 |0.8462 |0.0 |
| box_mAP50-95 |0.8119 |0.8041 | -0.0078|

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
Mức thay đổi: Tăng +0.0055 (từ 0.6853 lên 0.6908).

Phân tích: pose_mAP50-95 không giảm mà cải thiện nhẹ. Điều này chứng tỏ 20 ảnh fine-tune đã giúp mô hình định vị khớp chính xác hơn ở các ngưỡng OKS cao. Ngược lại, chỉ số box_mAP50-95 lại giảm nhẹ (-0.0078), cho thấy việc học tập trung vào keypoint của dữ liệu mới có thể làm giảm nhẹ khả năng bao quát khung thân (bounding box) trên toàn bộ tập test COCO.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

Mức chênh lệch: 0.1133 (tương đương 11.33%), trong đó box_mAP50-95 (0.8041) cao hơn pose_mAP50-95 (0.6908).

Khả năng dự đoán: Mô hình tìm người (bounding box) dễ hơn tìm khớp (keypoints).

Lý do:

Bounding box dựa vào thông tin ngữ cảnh tổng thể (global structure) của cơ thể người, kích thước lớn và dễ phát hiện.

Keypoint đòi hỏi độ chính xác tuyệt đối ở cấp độ pixel cho từng điểm nhỏ (khuỷu tay, cổ chân,...), vốn dễ bị che khuất (occlusion), biến dạng theo tư thế phức tạp hoặc bị mờ.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

ảnh test 0_2 đánh lệch tay trái.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

ảnh train013 OKS thấp vì tôi gán 2 người trong khi model gán 3 người. model đúng vì ảnh đó người vẫn rõ chỉ là các bộ phận bị mờ

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

Trường hợp trùng nhau (Có): Bức ảnh đó thuộc nhóm Hard Example (dữ liệu cực khó). Tình trạng mờ, thiếu ánh sáng, góc khuất nghiêm trọng hoặc tư thế quá phức tạp làm cho cả con người lẫn AI đều khó nhận diện đúng mốc giải phẫu.

Trường hợp không trùng nhau (Không): Cho thấy ảnh bạn gán tệ là do lỗi thao tác chủ quan của con người (Human Error), hoặc ảnh mô hình đoán tệ là do hiện tượng mô hình chưa tổng quát hóa tốt các trường hợp đặc biệt (Out-of-distribution).

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
Ảnh train_04 người thứ 2, hông của người đó mấp mé ở đáy ảnh, quyết định để outside vì nhận thấy phần thân người phải dài hơn chút nữa.