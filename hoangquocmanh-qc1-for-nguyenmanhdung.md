# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Mạnh Dũng — nguyenmanhdung (file `front_nmd.zip`)        Người kiểm (học viên): Hoàng Quốc Mạnh — hoangquocmanh  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `front_nmd.zip` (CVAT task 25 "front", export 21/11/2026 02:27 UTC; không kèm manifest)  
Số ảnh kiểm: 6 (A04, A06, A09, A10, A11, A12) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 104  

> Ghi chú cho coach: lô này dùng chung task CVAT với lô của người kiểm (máy người kiểm hỏng, mượn máy bạn). Khoảng 90 % shape trùng tọa độ với lô `hoangquocmanh-front.zip` (A01–A08 trùng 100 %). Coach đã đồng ý cho kiểm lô này. Mẫu được chọn nghiêng về A09–A12, nơi hai lô khác nhau nhiều nhất.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 (+1 nhẹ: weather) | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 19 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 29 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 19 | 4 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 19 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 15 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 18 | 1 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 32 | 2 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 14 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 (lô front, không áp dụng) | 0 | chính |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng |

Cách đếm số mục: QC1-01 = số ảnh; QC1-02 = 2 vạch × 6 ảnh; QC1-03/05/06 = 19 lane; QC1-04 = 19 lane + 10 road_curb; QC1-07 = 15 polygon drivable; QC1-08 = 18 đèn; QC1-09 = 18 đèn + 14 biển; QC1-10 = 14 biển; QC1-12 = 1 file.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A10 | lane #4 | nặng | Vạch (1189,664)→(934,503) nằm bên phải xe nhưng gán `position = L1`; đúng là R1. Vì vậy ảnh có hai L1 và thiếu R1. |
| 2 | QC1-05 | A04 | lane #3, #4 | chính | Vạch vàng đôi bị vẽ thành 2 polyline (mỗi nét một đường). Cần một polyline `kind = double`. |
| 3 | QC1-05 | A06 | lane #7, #13 | chính | Vạch vàng đôi tách 2 polyline, hai đường còn mâu thuẫn `style` (dashed / solid). |
| 4 | QC1-05 | A09 | lane #4, #8 | chính | Vạch trắng đôi tách 2 polyline cùng L2, mâu thuẫn `kind` (double / single). |
| 5 | QC1-05 | A11 | lane #6, #7 | chính | Vạch đôi tách 2 polyline cùng L1. |
| 6 | QC1-09 | A06 | traffic_sign #0 | chính | Biển ONE WAY gán `group = information`; theo bảng nhóm biển là `mandatory`. |
| 7 | QC1-09 | A12 | traffic_sign #10 | chính | Biển ONE WAY (mũi tên trắng) gán `information`; đúng là `mandatory`. |
| 8 | QC1-07 | A12 | drivable #7 | chính | Polygon `direct` kéo sang tận vạch L2 (#13) ở mép trái ảnh, gồm cả làn bên trái giữa L1 và L2 (phần đó là `alternative`). |
| 9 | QC1-08 | A06 | (thiếu) | chính | Bỏ sót cụm đèn vỏ vàng ở góc trên trái (khoảng x 30–95, y 25–65), nhìn nghiêng; cao trên 8 px. |
| 10 | QC1-01 | A10 | tag weather | nhẹ | `weather = overcast` nhưng mặt đường ướt rõ, có phản chiếu; theo guideline là `rain`. |

Ảnh không lỗi: không có ảnh nào trong 6 ảnh mẫu hoàn toàn không lỗi. Ảnh ít lỗi nhất: A11 (1 lỗi chính QC1-05; tag, đèn, crosswalk, road_curb đúng).

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A09 | Đèn #2 (258,215) gán `red / facing front`, nhưng ảnh không cho thấy rõ ô đèn nào đang sáng. Có nên đổi thành `unknown`? Nếu thật sự sai màu thì đây là lỗi nặng. | |
| A10 | Đèn #16 (743,185) gán `red / front`; phóng to thấy màu hổ phách. Là red hay yellow? | |
| A06, A12 | Đèn đi bộ A06 #11 và A12 #5 đang sáng hình người đi bộ màu trắng nhưng gán `off`. Road v1.0 không có giá trị cho tín hiệu "walk" trắng: chọn `green`, `unknown` hay giữ `off`? | |
| A06 | Lint báo thiếu R1. Sau vạch ngựa vằn có các vệt trắng đứt ngắn: có tính là R1 "thấy được" không? | |
| A06 | drivable #2 (`alternative`) nằm bên trái vạch vàng đôi: là làn cùng chiều hay làn ngược chiều? | |
| A10, A11 | drivable A10 #12 (dọc lề trái) và A11 #8 (bên phải) có xe đỗ dọc lề: là dải đỗ (không gán) hay làn `alternative`? | |
| A04 | Lane #5 (R1) gán `solid`; ở gần xe trông như vạch đứt. Cần xem lại ở độ phóng to cao. | |
| A11 | Vạch đôi #6, #7 gán `white`; ảnh chạng vạng, khó phân biệt trắng hay vàng. | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 8 / 104 nhãn = 7,7 %   Lỗi nhẹ: 1   Ca chờ lead: 8  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có 1 lỗi nặng (QC1-03, A10 lane #4 gán L1 cho vạch bên phải), chỉ một lỗi này đã đủ để Rework. Ngoài ra, tỉ lệ lỗi chính 7,7 % > 5 %. Các ca chờ lead không đổi được kết luận nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
