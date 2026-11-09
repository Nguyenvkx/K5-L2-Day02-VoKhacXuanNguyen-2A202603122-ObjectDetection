# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Võ Khắc Xuân Nguyên   
- MSSV: 2A202603122
- Email: vokhacxuannguyen165@gmail.com
- Lớp: L2A
- Link repo bài làm: https://github.com/Nguyenvkx/K5-L2-Day02-VoKhacXuanNguyen-2A202603122-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/drive/1SFTuqNYedrXcYCrfO2hQx6TJUkMMH5WA?hl=vi#scrollTo=AXC8f8IoXzTC

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý:
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: 
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu: 

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 463 | |
| FP | 490 | |
| FN | 190 |  |
| Precision | 0.4858 |  |
| Recall | 0.709 | |
| F1 | 0.5766 | |
| mean_iou_of_matches | 0.8222 | |
| passed | | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.411 |
| Recall | 0.23 |
| mAP50 | 0.272 |
| mAP50–95 | 0.201 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
    Lớp có recall thấp nhất là bus (0.00). Trong ảnh drive.052.jpg.
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
    Cần kiểm tra lại vấn đề của bounding box, khung bao quanh quá rộng hoặc quá hẹp, bị lệch tạo độ, so với viền thực tế của đối tượng.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
    Lỗi nhầm lẫn giữa van /  car ( Recall của van chỉ đạt 8.33%)
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
    Không dùng 10 ảnh eval để train để tránh rò rỉ dữ liệu vì tập eval đóng vai trò làm dữ liệu độc lập để đánh giá khả năng tổng quát hoá thực tế của mô hình. 
    Vai trò của validation là dùng để kiểm tra, chấm điểm và đánh giá chính xác chất lượng của mô hình và cơ sở chọn checkpoint tốt nhất
## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Huấn luyện mô hình | Chỉ số Recall của lớp bus đạt $0.00$ ($0\%$) và lớp van rất thấp ($8.33\%$). | Kiểm tra lại tập nhãn train, đối chiếu các ảnh eval có chứa xe lớn/xe khách/xe van. | Mô hình bị nhầm lẫn giữa các lớp tương đồng giữa bus/ truckm  van / car / truck do gán nhãn chưa đồng nhất. |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.
    - Hoàn thành và định dạng YOLO (hoàn thành).
    - Đầy đủ vật thể ( hoàn thành).
    - Độ bám sát và hình học box (hoàn thành không lấn nền và gộp vật thể).
    - Phân lớp nhất quán ( hoàn thành phân lớp nhất quán không gán vật thể ngoài car/ truck/ bus/ van).
    - Mini guideline và quyết định mơ hồ (hoàn thành).
    - Gold-set annotation QC (f1 chỉ được 0.58, IoU = 0.8222).
    - Pipeline YOLO và phân tích ( hoàn thành)
## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
    CVAT để gán nhãn data.
    Google Colab để cấu hình môi trường và huấn luyện mô hình.