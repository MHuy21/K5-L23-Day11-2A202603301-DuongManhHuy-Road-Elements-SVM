# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Phạm Minh Quân (phamminhquan) Người kiểm (học viên): Dương Mạnh Huy (duongmanhhuy)
Ngày: 2026-11-21 Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `phamminhquan-front.zip` (sha256 `1d2c8977692b…`), `phamminhquan-fisheye.zip` (sha256 `c60bf90e1d6a…`), revision 1
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng) Số nhãn đã kiểm (shape + tag): 53

Ảnh kiểm: A01 (11 nhãn), A03 (10), A07 (12), A09 (6), B02 (8), B07 (6). Chọn để phủ đủ: làn nhiều vạch (A01), checkpoint occluded/đèn nhỏ (A03), barrier + đèn (A07), giao lộ (A09), fisheye đèn rìa + edge_zone (B02), fisheye camera phải + crosswalk/road_curb (B07).

## Tổng hợp theo mã

| Mã                                   | Loại lỗi                              | Số mục kiểm | Số lỗi | Mức          |
| ------------------------------------ | ------------------------------------- | ----------: | -----: | ------------ |
| QC1-01 tag camera                    | sai thuộc tính / bỏ sót               |           6 |      0 | nặng         |
| QC1-02 đủ L1, R1                     | bỏ sót                                |           8 |      2 | nặng         |
| QC1-03 position                      | sai thuộc tính / thừa                 |           9 |      0 | nặng         |
| QC1-04 tâm vạch, chiều, điểm dừng    | sai phạm vi / bỏ sót                  |           9 |      1 | chính        |
| QC1-05 vạch đứt, che                 | sai phạm vi / sai thuộc tính          |           9 |      0 | chính        |
| QC1-06 style, color, kind            | sai thuộc tính                        |           9 |      0 | chính        |
| QC1-07 vùng lái                      | sai phạm vi / bỏ sót / thừa           |          11 |      6 | chính        |
| QC1-08 đèn, màu                      | bỏ sót / sai phạm vi / sai thuộc tính |          11 |      5 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính                        |          14 |      0 | chính        |
| QC1-10 hình in, đủ biển              | bỏ sót / sai phạm vi                  |           8 |      0 | chính        |
| QC1-11 fisheye                       | sai phạm vi / sai thuộc tính          |           6 |      0 | chính        |
| QC1-12 file                          | lỗi file                              |           2 |      0 | nhẹ / nặng   |

Cách đếm "Số mục kiểm": QC1-01 = số tag camera; QC1-02 = 4 ảnh front × 2 vị trí (L1, R1); QC1-03…06 = số polyline lane trong 6 ảnh; QC1-07 = 6 vùng (drivable/crosswalk/road_curb) có trong lô + 5 vùng phải có mà thiếu; QC1-08 = 6 đèn có trong lô + 5 đèn thiếu; QC1-09 = 6 đèn + 8 biển; QC1-10 = 8 biển; QC1-11 = 6 shape ở hai ảnh fisheye; QC1-12 = 2 file.

## Danh sách lỗi (mỗi lỗi một dòng)

| #   | Mã     | Ảnh | Nhãn (label, id)                            | Mức   | Mô tả ngắn                                                                                                                                 |
| --- | ------ | --- | ------------------------------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | QC1-02 | A07 | lane, thiếu L1                              | nặng  | Bỏ sót L1: vạch trắng liền chạy dọc chân barrier bên trái (khoảng (180,455) → (440,362)) thấy rõ nhưng không gán                           |
| 2   | QC1-02 | A09 | lane, thiếu L1                              | nặng  | Ảnh không có lane nào; vạch trắng đứt giữa ảnh (khoảng (533,643) → (668,432)) thấy rõ, phải là L1                                          |
| 3   | QC1-04 | A01 | lane#4@(0,595) L2                           | chính | L2 bị kéo lệch lên trên khỏi vạch trắng mép trái (lệch ~20 px quanh x = 200), quá ngưỡng 5 px                                              |
| 4   | QC1-07 | A01 | drivable, thiếu `direct`                    | chính | Bỏ sót vùng lái làn đang đi giữa L1 và R1; chỉ có polygon `alternative`                                                                    |
| 5   | QC1-07 | A01 | drivable, thiếu `alternative` phải          | chính | Bỏ sót làn cùng chiều bên phải giữa R1 và R2 (vạch vàng mép)                                                                               |
| 6   | QC1-07 | A03 | drivable, thiếu `alternative`               | chính | Bỏ sót làn cùng chiều bên phải giữa R1 và R2                                                                                               |
| 7   | QC1-07 | A07 | drivable#1@(0,522) direct                   | chính | Polygon `direct` khoét quanh xe phía trước (dừng ở đuôi xe ~y 365); guideline: gán "đi được nếu đường trống", không khoét lỗ quanh xe khác |
| 8   | QC1-07 | A07 | drivable, thiếu `alternative`               | chính | Bỏ sót làn cùng chiều bên phải giữa R1 và R2                                                                                               |
| 9   | QC1-07 | A09 | drivable, thiếu                             | chính | Ảnh không có vùng lái nào                                                                                                                  |
| 10  | QC1-08 | A03 | traffic_light, thiếu (~(628,302)–(638,320)) | chính | Bỏ sót đèn xe đang xanh, cao ~18 px (≥ 8 px phải gán)                                                                                      |
| 11  | QC1-08 | A03 | traffic_light, thiếu (~(704,307)–(716,326)) | chính | Bỏ sót đèn xe đang xanh, cao ~19 px                                                                                                        |
| 12  | QC1-08 | A09 | traffic_light, thiếu (~(420,295)–(431,343)) | chính | Bỏ sót cụm đèn quay lưng (`facing = back`), cao ~48 px                                                                                     |
| 13  | QC1-08 | B02 | traffic_light, thiếu (~(107,75)–(160,218))  | chính | Bỏ sót cụm đèn góc trên trái (mặt sau, `edge_zone = true`)                                                                                 |
| 14  | QC1-08 | B02 | traffic_light, thiếu (~(262,348)–(278,373)) | chính | Bỏ sót đèn nhỏ bên trái giao lộ, cao ~25 px                                                                                                |

Ảnh không lỗi: **B07** — tag `camera = fisheye_right` đúng; crosswalk#0@(210,720) bao đủ 5 vạch, không lấn thân xe; road_curb#1@(165,470) theo cung, 12 điểm; đủ nhóm nhãn theo kế hoạch ảnh (crosswalk + road_curb).

Ghi nhận không tính lỗi: A07 traffic_light#3@(703,244) cao dưới 8 px (lint QC1-08 nhẹ; box nhỏ như vậy không bắt buộc, không phải lỗi chấm).

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead                                                                                                                                              | Lời đáp (nếu có) |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| A03 | Checkpoint yêu cầu A03 có `occluded`; lô không có lane nào bật occluded. Đoạn vạch nào trong A03 được coi là bị che (nếu chỉ R2 sát xe đỗ thì có tính không)? |                  |
| A03 | Tag `weather = overcast`: trời nhiều mây lúc chạng vạng, đường khô — `overcast` hay `clear`?                                                                  |                  |
| A09 | Bên phải làn đi đang trong bóng râm, không thấy R1 rõ: có được miễn QC1-02 cho R1 không? (Chưa tính lỗi R1)                                                   |                  |

## Quyết định

Lỗi nặng: 2 Lỗi chính: 12 / 53 nhãn = 22,6 % Lỗi nhẹ: 0 Ca chờ lead: 3
Quyết định (Release / Hold / Rework): **Rework**
Lý do (theo luật của phiếu): Còn 2 lỗi nặng (QC1-02 thiếu L1 ở A07 và A09) → Rework theo luật 1. Ngoài ra tỉ lệ lỗi chính 12/53 = 22,6 % > 5 % cũng dẫn tới Rework theo luật 2. Ba ca mơ hồ không đổi kết luận nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
