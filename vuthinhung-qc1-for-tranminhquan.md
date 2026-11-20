# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): `tranminhquan`        Người kiểm (học viên): Vũ Thị Nhung (`vuthinhung` - 2A202603156)  
Ngày: 20/11/2026                         Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `tranminhquan-front.zip`, `tranminhquan-fisheye.zip` (`revision: 1` trong `tranminhquan-manifest.json`)  
Số ảnh kiểm: 6 (+ 2 ảnh thêm `A13`, `B09`, ghi riêng: 18 nhãn)   Số nhãn đã kiểm (shape + tag): 64  

> **Danh sách 6 ảnh bắt buộc lấy mẫu kiểm:** `A01`, `A03`, `A04`, `A08` (Set A - camera trước) và `B02`, `B06` (Set B - camera fisheye). Ảnh `A01` được kiểm tra kỹ toàn bộ 12 nhãn (4 tag + 4 lane + 3 drivable + 1 traffic_sign) và xác nhận **không có lỗi**.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 1 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 11 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 15 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 15 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 15 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 15 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 14 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 7 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 12 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 5 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 11 | 1 | chính |
| QC1-12 file | lỗi file | 64 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-05 | A03 | `lane#1@(695,466)` | chính | Vạch đứt bên phải (`R1`) vẽ nối xuyên qua phần đầu xe đỗ ven đường nhưng quên bật cờ `occluded=true` |
| 2 | QC1-06 | A04 | `lane#0@(28,562)` | chính | Vạch vàng đôi chia hai chiều xe chạy (`L1`) để giá trị mặc định `kind=single` thay vì `kind=double` |
| 3 | QC1-07 | A04 | `drivable#4@(724,542)` | chính | Vùng lái `drivable` (`area_type=alternative`) kéo tràn sang cả làn xe đạp sơn xanh và dải đỗ xe sát vỉa hè bên phải |
| 4 | QC1-01 | A08 | `tag:weather` | nhẹ | Ảnh trời nhiều mây âm u nhưng mặt đường khô (`overcast`), bạn quên sửa nên vẫn để giá trị mặc định đầu danh sách là `clear` |
| 5 | QC1-09 | A08 | `traffic_sign#12@(778,35)` | chính | Biển phụ chữ nhật nhỏ `"PASSENGER CARS ONLY"` gắn trên biển chỉ dẫn xanh lá nhưng gán `group=information` thay vì `supplementary` |
| 6 | QC1-04 | B02 | `lane#1@(685,398)` | chính | Polyline `R1` vẽ ngược chiều từ xa về gần xe (điểm đầu ở `(685,398)` cao hơn điểm cuối `(1140,675)`) |
| 7 | QC1-11 | B02 | `traffic_light#4@(82,102)` | chính | Cụm đèn tín hiệu bên trái có tâm hộp nằm ngoài 80% bán kính ảnh fisheye nhưng chưa tích chọn ô `edge_zone=true` |
| 8 | QC1-03 | B06 | `lane#0@(245,178)` | nặng | Ảnh camera bên trái (`B06_04068_MVL.png`, `camera=fisheye_left`) nhưng vạch `lane` để mặc định `position=L1` thay vì bắt buộc `position=other` |

*(Ghi chú riêng 2 ảnh thưởng `A13` và `B09`: `A13` gán đủ 4 tag với `weather=rain`, đủ 3 vạch làn và vùng lái; `B09` đủ 4 tag `camera=fisheye_front`, vạch đi theo cung cong, không phát hiện lỗi nặng).*

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04 | Phần làn xe đạp sơn màu xanh lá bên phải vạch trắng liền có được gộp vào `drivable` (`alternative`) khi không có xe đạp không? | Lead/Coach xác nhận: Không gộp; làn dành riêng cho xe đạp và dải đỗ xe sát lề không phải làn cơ giới cùng chiều nên không tính vào `drivable`. |
| B02 | Biển nhỏ gắn trên thân cột đèn sọc đen trắng ở rìa trái (`(74,324)`) bị méo nặng do thấu kính fisheye không đọc được ký hiệu thì xếp `group` nào? | Lead/Coach xác nhận: Chọn `group=other` (hoặc nhóm gần nhất) và bật `edge_zone=true`, ghi chú vào bảng ca khó thì không bị trừ điểm. |

## Quyết định
Lỗi nặng: **1**   Lỗi chính: **6** / **64** nhãn = **9,4 %**   Lỗi nhẹ: **1**   Ca chờ lead: **0**  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô còn **1 lỗi nặng** (`QC1-03` ở ảnh `B06` để `position=L1` trên camera ngang `fisheye_left`) **và** tỉ lệ lỗi chính là `6 / 64 = 9,38%` (vượt ngưỡng cho phép `5%` số nhãn đã kiểm). Theo đúng luật quyết định của Phiếu QC 1, lô bắt buộc phải trả về **Rework** để bạn sửa lỗi `position` ở camera hai bên, đảo lại chiều polyline ở `B02`, bật `edge_zone`, bật cờ `occluded` ở `A03` và chỉnh lại các thuộc tính bị dính mặc định của CVAT trước khi export bản `revision 2`.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
