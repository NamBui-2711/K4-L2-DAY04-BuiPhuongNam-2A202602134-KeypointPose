# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: __Bùi Phương Nam____   Nhóm: ______   Ngày: __16/09/2026____

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.
   
## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 28 |
| v=2 / v=1 / v=0 | v=2 336 v=1 48 v=0 92|
| Thời gian trung bình mỗi ảnh | 4 |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`): 

1.left_ear
2.right_ear
3.right_wrist

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích. 
Không hoàn toàn đúng. Khi gán có những ảnh mà nhân vật sẽ quay lưng lại với camera làm cho khó xác định được các vị trí chính xác trên khuân mặt ( ví dụ như ảnh train_06)

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.891 | 0.914 |
| OKS@0.50 | 0.966 | 1.000 |
| OKS@0.75 | 0.897 | 0.966 |
| Lỗi `dao_trai_phai` | 0 | 0 |
| Lỗi `nham_nguoi` | 1 | 0 |
| Lỗi `xoa_khop_bi_che` | 17 | 9 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_15.jpg người #1: thêm khớp(right_eye), thêm khớp(left_hip), bật lại khớp(left_knee) và cho occluded, bật lại khớp(left_ankle) và cho occluded
- train_13.jpg người #2: bật lại khớp(left_shoulder) và cho occluded, bật lại khớp(left_hip), bật lại khớp(left_knee)
- train_06.jpg người #1: thêm khớp(right_ear), bật lại khớp(right_hip)
- train_11.jpg người #1: bật lại khớp và cho occluded(left_hip), bật lại khớp và cho occluded(right_hip)
- train_09.jpg người #1: thêm khớp(left_wrist)
- train_04.jpg người #1: kéo lại khớp về đúng người(left_wrist)
- train_12.jpg người #1:bật lại khớp và cho occluded(left_knee), bật lại khớp và cho occluded(left_ankle)
- train_08.jpg người #1: bật lại khớp và cho occluded(left_knee), bật lại khớp và cho occluded(left_ankle)

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?
Không có lỗi đảo trái phải trong toàn bộ 20 ảnh
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
| pose_mAP50 | 0.845 | 0.845 | 0.0 |
| pose_mAP50-95 | 0.6853 | 0.6908 | 0.0055 |
| pose_precision | 0.9734 | 0.9792 | 0.0058 |
| pose_recall | 0.8462 | 0.8462 | 0.0 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
   Tăng 0.055 (từ 0.6853 lên 0.6908). Mức tăng nhỏ, chưa đủ kết luận model “giỏi hơn hẳn”; chỉ cho thấy nhãn của tôi không phá hỏng hoàn toàn kiến thức gốc.


2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
   Sau fine-tune box_mAP50-95 = 0.8041 và pose_mAP50-95 = 0.6908 tăng 0.1133.
   Model tìm người (box_mAP) dễ hơn rất nhiều so với việc định vị chính xác các khớp (pose_mAP).
   Vì bài toán phát hiện khung bao người (box) chỉ yêu cầu xác định ranh giới vùng chứa đối tượng (coi người là một khối tổng thể), trong khi dự đoán tư thế (pose) đòi hỏi độ chính xác đến từng pixel của 17 điểm khớp nhỏ trên cơ thể. Bất kỳ sai lệch nhỏ nào về góc khuất, trang phục che lấp hay khớp bị khuất tầm nhìn cũng sẽ làm OKS giảm và tính điểm sai ở pose_mAP. 

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
   Theo e thì hình test_02 person 0.31 đó là con chim nhưng mô hình gán đó là người và đây là lỗi trượt hẳn. Khi mà mô hình đã xác định sai đối tượng.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
   Ảnh train_06 có OKS = 0.605 thấp nhất. Annotator đúng, căn cứ vào luật nhóm đã thống nhất và thực tế hình ảnh (như trường hợp người ngồi ngược hướng camera hoặc bị khuất góc nhìn ở ảnh train_06), vị trí các khớp trên cơ thể đối tượng không thể quan sát hoặc xác định rõ ràng bằng mắt thường từ góc máy đó.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
   ảnh em train tệ nhất: train_15 = 0.6702
   ảnh model tệ nhất: train_06 = 0.605

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

ảnh train_06 khớp nose. Phần mũi bị ngược lại với hướng camera chụp nhưng theo cấu trúc cơ thể người thì có thể đoán được vị trí. chọn v=1 không Outside. Nếu để v=0, khớp này bị loại khỏi điểm OKS và model sẽ học rằng “ khuất góc nhìn = không có khớp mũi trên mặt người”.
<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
