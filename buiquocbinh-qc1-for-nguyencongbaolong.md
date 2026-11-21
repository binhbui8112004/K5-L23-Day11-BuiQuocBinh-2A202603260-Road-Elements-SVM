# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Công Bảo Long - 2A202603297  
Người kiểm (học viên): Bùi Quốc Bình - 2A202603260  
Ngày: 2026-11-21  
Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `nguyencongbaolong-front.zip`; không có manifest trong file được gửi nên chưa xác minh được revision.  
Số ảnh kiểm: 6 (A01–A06)  
Số nhãn đã kiểm (shape + tag): 78

> Phạm vi: đối chiếu annotation trong `annotations.xml` với sáu ảnh cùng tên trong thư mục `data/`. Đây là QC thủ công theo ảnh và guideline, không có GT để đo chính xác ngưỡng lệch 5 px hoặc xác nhận toàn bộ độ bao phủ. Zip mở được và có XML; chưa đánh giá tính đầy đủ của bộ bàn giao front + fisheye hay manifest. `road_check lint` cũng được chạy như công cụ gợi ý; cảnh báo tự động được kiểm tra lại bằng ảnh, không tính máy móc thành lỗi.

## Tổng hợp theo mã

| Mã                                   | Loại lỗi                              | Số mục kiểm |                                              Số lỗi | Mức           |
| ------------------------------------ | ------------------------------------- | ----------: | --------------------------------------------------: | ------------- |
| QC1-01 tag camera                    | sai thuộc tính / bỏ sót               |           6 |                                                   0 | nặng          |
| QC1-02 đủ L1, R1                     | bỏ sót                                |           6 |                                                   1 | nặng          |
| QC1-03 position                      | sai thuộc tính / thừa                 |          13 |                                                   0 | nặng          |
| QC1-04 tâm vạch, chiều, điểm dừng    | sai phạm vi / bỏ sót                  |          13 |                                 0 lỗi xác nhận được | chính         |
| QC1-05 vạch đứt, che                 | sai phạm vi / sai thuộc tính          |          13 |                                 0 lỗi xác nhận được | chính         |
| QC1-06 style, color, kind            | sai thuộc tính                        |          13 |                                                   1 | chính         |
| QC1-07 vùng lái                      | sai phạm vi / bỏ sót / thừa           |          20 |                                 0 lỗi xác nhận được | chính         |
| QC1-08 đèn, màu                      | bỏ sót / sai phạm vi / sai thuộc tính |           8 |                                 0 lỗi xác nhận được | nặng / chính  |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính                        |          21 |                                 0 lỗi xác nhận được | chính         |
| QC1-10 hình in, đủ biển              | bỏ sót / sai phạm vi                  |          13 |                                 0 lỗi xác nhận được | chính         |
| QC1-11 fisheye                       | sai phạm vi / sai thuộc tính          |           0 |                                                   0 | không áp dụng |
| QC1-12 file                          | lỗi file                              |       1 zip | 0 lỗi đọc được; revision/gói bàn giao chưa xác minh | nhẹ / nặng    |

## Danh sách lỗi (mỗi lỗi một dòng)

| #   | Mã     | Ảnh | Nhãn (label, id)                                                     | Mức   | Mô tả ngắn                                                                                                                               |
| --- | ------ | --- | -------------------------------------------------------------------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | QC1-02 | A03 | `lane`, thiếu shape (không có ID)                                    | nặng  | Không thấy polyline `L1` trong XML, trong khi vạch đôi màu vàng ở bên trái làn xe đang đi nhìn thấy rõ. Bổ sung `L1` theo đúng tâm vạch. |
| 2   | QC1-06 | A04 | `lane`, `position=L1` (shape thứ 6 trong XML; XML không có ID shape) | chính | Vạch `L1` nhìn thấy là vạch đôi màu vàng nhưng thuộc tính đang là `color=white`. Đổi thành `yellow`; `kind=double` phù hợp.              |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead                                                                                                                                                                                                                                                      | Lời đáp (nếu có) |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| A01 | Lint báo hai polyline cùng `position=L2`. Ảnh cho thấy hai vạch trắng song song; xác nhận quy ước với vạch đôi là giữ cả hai polyline hay chỉ một polyline với `kind=double`? Chưa tính là lỗi vì ảnh cho thấy hai vệt riêng và guideline chưa nói rõ cách biểu diễn. | —                |
| A04 | Vùng `drivable=alternative` có bao gồm làn xe đạp ở sát lề hay chỉ là làn xe cơ giới cùng chiều? Chưa tính là lỗi vì cần xác nhận cách áp dụng guideline cho làn xe đạp.                                                                                              | —                |

## Quyết định

Lỗi nặng: 1  
Lỗi chính: 1 / 78 nhãn = 1.28%  
Lỗi nhẹ: 0  
Ca chờ lead: 2 (không làm thay đổi quyết định vì đã có lỗi nặng xác nhận được)  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có ít nhất một lỗi nặng (QC1-02 ở A03), nên lô cần Rework. Tỉ lệ lỗi chính 1.28% không vượt 5%, nhưng không thay đổi kết luận do lỗi nặng.

### Ghi chú đếm

- 78 nhãn gồm shape và tag: A01 14, A02 12, A03 15, A04 12, A05 7, A06 18.
- QC1-03–QC1-06 kiểm 13 polyline `lane`; QC1-07 kiểm 20 shape gồm drivable, crosswalk và road_curb.
- Lint cũng cảnh báo thiếu L1/R1 ở A05 và thiếu R1 ở A06. Khi xem ảnh, không thấy vạch lane rõ ở các phía đó nên không tính là lỗi theo ngoại lệ “bỏ qua nếu thật sự không thấy vạch”.
- Các mục ghi “0 lỗi xác nhận được” không đồng nghĩa đã đối chiếu GT; zip không có ảnh hoặc GT. Ảnh tham chiếu được lấy từ thư mục `data/` theo tên trong XML.
