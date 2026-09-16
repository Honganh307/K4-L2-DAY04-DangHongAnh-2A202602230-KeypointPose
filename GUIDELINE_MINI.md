# Mini guideline - nhóm: SOLO  |  người gán: DangHongAnh  |  ngày: 16/9/2026

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
| Hông của người mặc quần áo dài |vẫn gán điền point nhưng để bị che | vẫn có thể ước lượng hông của ng đó |
| Tai bị tóc hoặc mũ bảo hiểm che một phần |vẫn gán điền point nhưng để bị che| vẫn có thể ước lượng vị trí tai người đó |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) |phần chân sẽ để outside | vật thể ra khỏi khung hình |
| Cổ tay nằm sau tay lái / sau thân mình |gán point và để bị che | vật vẫn trong khung hình |
| Hai người chồng lên nhau |người đứng trước sẽ điền đầy đủ, phần che của người sau thì để nhãn bị che |vật thể đứng trước sẽ là nhìn thấy vật thể đứng sau là bị che |
| Người nhỏ đến mức nào thì không gán nữa | khi các khớp bằng mắt thường đã thấy k tách biệt | gán nhãn cho vật nhỏ đó chỉ gây nhiễu cho mô hình |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `002`, người thứ `1`, khớp `mặt`

- Mơ hồ ở chỗ nào: mặt người đó quay đi và không thấy
- Bạn quyết thế nào: ước tính tư thế mặt và gán để point bị che
- Vì sao: vật thể vẫn trong khung hình
- Nếu người khác quyết ngược lại thì model học sai cái gì: model sẽ coi như mặt người đó ở ngoài khung khiến hình dạng người méo mó

### Ca 2 - ảnh `004`, người thứ `2`, khớp `tai`

- Mơ hồ ở chỗ nào: tai bị mũ bảo hiểm che hoàn toàn
- Bạn quyết thế nào:ước lượng vị trí tai và gán bình thường, để chú thích bị che
- Vì sao: vật thể vẫn trong khung
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 3 - ảnh `002`, người thứ `1`, khớp `tai và vai`

- Mơ hồ ở chỗ nào: người đó quay đầu nhưng thân vẫn ở bên ngang khiên tai và vai bị chéo
- Bạn quyết thế nào: vẫn gán đúng thứ tự
- Vì sao: vẫn đúng bản chất của vật thể
- Nếu người khác quyết ngược lại thì model học sai cái gì: khi gán ngược lại hình dạng người sẽ không đúng

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `right_ear` (bạn `54%%` / họ `30%%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: guideline chưa rõ
- Luật mới bổ sung vào mục 2 sau khi thống nhất: vật thể trong khung thù vẫn phải gán
