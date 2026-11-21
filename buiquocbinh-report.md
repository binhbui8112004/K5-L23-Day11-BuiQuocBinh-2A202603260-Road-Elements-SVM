# Báo cáo cá nhân — Ngày 11

Họ tên: Bùi Quốc Bình Mã học viên: 2A202603260  
Phiên bản CVAT (Help → About): v2.82.0 _(kiểm tra lại trên tab Help → About của CVAT lớp)_  
Guideline: Road v1.0 Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 16:50 Số lần nộp lại sau Rework: 0

## 1. Kiểm project

| Mục                   | Đúng như guideline Road v1.0? | Ghi chú                                                                                                                                         |
| --------------------- | ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 6 label, đúng kiểu    | Đúng                          | `lane` (polyline), `road_curb` (polyline), `crosswalk` (polygon), `drivable` (polygon), `traffic_light` (rectangle), `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng                          | Đủ các thuộc tính `position`, `style`, `color`, `kind`, `area_type`, `type`, `facing`, `group`, `edge_zone`                                     |
| 4 tag ảnh             | Đúng                          | `camera`, `timeofday`, `weather`, `source` đều dùng thuộc tính select `value`                                                                   |

Cách kết thúc polyline trên bản CVAT này: Bấm phím **N** (hoặc double-click ở điểm cuối).  
Cách đặt tag ảnh trên bản CVAT này: Dùng công cụ **Tag** ở thanh công cụ trái đặt 4 tag (`camera`, `timeofday`, `weather`, `source`), sau đó mở **Details** trong bảng Objects bên phải để chọn đúng giá trị `value`.

## 2. Số lượng đã gán

_(Số liệu khớp với `buiquocbinh-manifest.json`)_

| Task                         | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| ---------------------------- | --: | ---: | --------: | --------: | -------: | ------------: | -----------: |
| front                        |  12 |   26 |         4 |         4 |       23 |            33 |           30 |
| front-extra (đã làm 0 / 4)   |   0 |    0 |         0 |         0 |        0 |             0 |            0 |
| fisheye                      |   8 |    8 |        13 |         9 |       10 |             4 |            3 |
| fisheye-extra (đã làm 0 / 4) |   0 |    0 |         0 |         0 |        0 |             0 |            0 |

## 3. Bảng ca khó

| Ảnh | Nhãn           | Phân vân giữa                                       | Đã chọn                                                 | Lý do                                                                                                           |
| --- | -------------- | --------------------------------------------------- | ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| A05 | `lane`         | Không vẽ `L1`/`R1` hay vẽ giả định theo mép xe      | Không vẽ `L1`/`R1`, chỉ vẽ `road_curb` bên phải         | Đoạn đường mặt nhựa tối không có vạch sơn L1/R1 nhìn thấy được; theo guideline không bịa vạch, được miễn QC1-02 |
| A06 | `lane`         | Vẽ `R1` hay bỏ qua                                  | Không vẽ `R1`, chỉ vẽ `L1` (vàng đôi)                   | Bên phải vướng cột trụ cầu vượt và bóng râm, không thấy vạch sơn R1 rõ ràng                                     |
| A07 | `lane`         | Vẽ `L1` sát dải bê tông hay chỉ vẽ `road_curb`      | Không vẽ `L1`, chỉ vẽ `road_curb` trái và `R1`, `R2`    | Sát bên trái làn xe mình là gờ chân dải phân cách bê tông, không có vạch sơn L1 rõ ràng                         |
| A08 | `lane`         | Có gán `L1` ở mép trái giao lộ hay không            | Không vẽ `L1`                                           | Giao lộ rộng, bên trái không có vạch sơn sát làn đang đi; chỉ có vạch ngang và `R1`/`R2` bên phải               |
| A12 | `lane`         | Vẽ `R1` hay bỏ qua                                  | Không vẽ `R1`, chỉ vẽ `L1` (giữa) và `L2` (trái)        | Nửa đường bên phải sau vạch ngựa vạn không có vạch sơn kẻ làn rõ ràng                                           |
| B01 | `lane`         | Vẽ `L1`/`R1` hay `road_curb`                        | Vẽ 2 `road_curb`, không vẽ `L1`/`R1`                    | Hai bên đường là gờ phân cách đường ray xe điện và mép vỉa làn xe đạp, không có vạch sơn làn                    |
| B03 | `traffic_sign` | Bật hay tắt `edge_zone` cho biển tròn xanh bên phải | Đặt `group=mandatory` và kiểm tra tâm theo bán kính 80% | Tâm hộp nằm sát ngưỡng ranh giới 80% bán kính (`~512 px`), được rà lại theo gợi ý `road_check lint`             |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: Nguyễn Công Bảo Long - 2A202603297 Quyết định nhận được: _(điền khi nhận lại phiếu từ bạn Long)_

| Mã lỗi                         | Số lỗi | Đồng ý? | Đã sửa? |
| ------------------------------ | -----: | ------- | ------- |
| _(Chờ phiếu QC 1 từ bạn Long)_ |        |         |         |

## 5. Kiểm file export

| File                      | Mở lại được?                                       | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML?                           |
| ------------------------- | -------------------------------------------------- | --------------------------- | --------------------------- | -------------------------------------------------- |
| `buiquocbinh-front.zip`   | Có (`road_check lint` OK, `contains_images=false`) | 9 / 9 (`A01`)               | 6 / 6 (`A02`)               | Có (`camera=front` trên đủ 12 ảnh)                 |
| `buiquocbinh-fisheye.zip` | Có (`road_check lint` OK, `contains_images=false`) | 5 / 5 (`B01`)               | 6 / 6 (`B02`)               | Có (`fisheye_front/rear/left/right` trên đủ 8 ảnh) |

## 6. Ảnh chụp màn hình

_(Toàn bộ 4 ảnh minh chứng đã được lưu trên Google Drive và bật quyền xem "Bất kỳ ai có đường liên kết")_

1. **Tab Labels của project** (`01-project-labels.png`): [Xem ảnh 1 trên Drive](https://drive.google.com/drive/folders/16B15-DknV2IkC22GILoU3NyDsoXxDrNV?usp=sharing)
2. **Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển)** (`02-front-a04.jpg`): [Xem ảnh 2 trên Drive](https://drive.google.com/drive/folders/16B15-DknV2IkC22GILoU3NyDsoXxDrNV?usp=sharing)
3. **Một ảnh fisheye đã gán, phóng to đoạn polyline cong** (`03-fisheye-zoom-curve.jpg`): [Xem ảnh 3 trên Drive](https://drive.google.com/drive/folders/16B15-DknV2IkC22GILoU3NyDsoXxDrNV?usp=sharing)
4. **Một đoạn XML có `<polyline label="lane">`** (`04-xml-polyline-lane.jpg`): [Xem ảnh 4 trên Drive](https://drive.google.com/drive/folders/16B15-DknV2IkC22GILoU3NyDsoXxDrNV?usp=sharing)

- **Link thư mục Google Drive chứa đủ 4 ảnh (dành cho Lab Coach đối chiếu nhanh):** https://drive.google.com/drive/folders/16B15-DknV2IkC22GILoU3NyDsoXxDrNV?usp=sharing

## 7. Tự đánh giá

Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:

- **QC1-01 (tag camera/ảnh)** ở bộ fisheye (quên gắn tag cho các ảnh sau B01 và để nhầm mặc định `front`) và **QC1-03 (`position` làn)** khi có lúc nhầm giữa `L1/L2` và `R1/R2` lúc đường lệch tâm. Cách tránh ở Ngày 20: luôn đặt **4 tag ngay bước đầu tiên** trên mọi frame trước khi vẽ shape, đồng thời chạy `road_check lint` tự kiểm ngay sau khi export lần đầu.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:

- Nhãn `lane` và `drivable` là ground truth để huấn luyện các mô hình nhận diện làn đường (như mô hình row-anchor cho LKA — Lane Keeping Assist) và phân vùng mặt đường đi được. Nếu gắn sai `position` (lỗi `QC1-03`, ví dụ gán nhầm vạch `R1` bên phải thành `L1` bên trái ở A07/A09), mô hình LKA sẽ học lệch tâm làn xe đang chạy sang làn bên cạnh, dẫn tới tính sai sai số lệch tâm và điều khiển đánh lái lệch làn nguy hiểm.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

_(Không bắt buộc — bỏ qua nếu không làm)_
