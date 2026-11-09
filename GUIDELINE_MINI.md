# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Xe ô tô chở người, thường có 4 bánh, thiết kế thân xe kín. | Sedan, hatchback, SUV, taxi. |
| `truck` | Xe tải chuyên chở hàng hóa, thường có thùng hàng hoặc khoang chở hàng lớn. | Xe tải thùng, xe tải mui bạt, xe tải nhỏ. |
| `bus` |Xe khách có sức chứa nhiều người, thân xe dài và nhiều cửa sổ. | Xe buýt công cộng, xe khách, minibus. |
| `van` | Xe có khoang cabin và khoang chở hàng hoặc chở người liền thân, thường có thiết kế hình hộp.  | Minivan, xe van chở hàng, xe chở khách cỡ nhỏ. |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Bounding box phải bao quanh toàn bộ phần nhìn thấy của phương tiện, không lấy quá nhiều nền đường hoặc vật thể xung quanh.
- Vật thể bị che khuất: Chỉ vẽ box theo phần phương tiện nhìn thấy; không tự suy đoán phần bị che. Nếu vẫn nhận diện được phương tiện thì tiến hành gán nhãn.
- Vật thể bị cắt bởi rìa ảnh: Vẽ box đến sát rìa ảnh tại vị trí vật thể bị cắt. Không loại bỏ nếu vẫn nhận diện được loại xe.
- Vật thể rất nhỏ/mơ hồ: 	Chỉ gán nhãn khi có đủ đặc điểm để xác định lớp. Nếu không thể phân biệt thì bỏ qua, không đoán nhãn.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_001` | Xe màu trắng có hình dáng vuông, đỗ bên đường. | van | Có khoang xe liền thân, hình dáng đặc trưng của xe van, không có thùng hàng tách biệt. |
| `drive_004` | Xe màu đỏ ở phía dưới ảnh bị cắt một phần bởi rìa ảnh. | Gán nhãn nếu nhận diện được; box kéo đến rìa ảnh. | Vật thể bị cắt không phải lý do để loại bỏ nếu vẫn xác định được lớp. |
| `drive_006` | Xe màu trắng ở sát mép trái ảnh, chỉ nhìn thấy một phần. |car nếu đủ đặc điểm nhận diện.  | |
