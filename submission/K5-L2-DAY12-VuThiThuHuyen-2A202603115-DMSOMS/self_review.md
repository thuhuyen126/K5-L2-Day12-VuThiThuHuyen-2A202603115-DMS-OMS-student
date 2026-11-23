# Tự đánh giá — Vũ Thị Thu Huyền · G12

## 1. Tự rà soát 4 cảnh

Sau khi hoàn thành gán nhãn, mình kiểm tra lại 4 ảnh gồm 2 ảnh S## và 2 ảnh D## để rà soát bounding box, thuộc tính đối tượng và trạng thái các điểm mốc.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S02_rgb.png` | `child_seat` | `ok` | Lòng ghế bị vùng tối che khuất, không đủ bằng chứng xác định có trẻ bên trong nên giữ `occupied=unknown`; không suy diễn từ ảnh IR | Không cần sửa |
| `S05_ir.png` | `child_seat` | `wrong_class` | Lòng ghế có thể quan sát rõ và đang trống nhưng thuộc tính `occupied` ban đầu chưa được cập nhật phù hợp | Đã sửa |
| `D01.png` | `face13` (`mouth_right`) | `flag` | Ban đầu nhầm lẫn giữa `occluded` và `outside` đối với khóe miệng phải bị che khuất | Đã sửa |
| `D02.png` | `face13` (`left_eye_outer`) | `flag` | Điểm mốc khóe ngoài mắt trái bị che khuất một phần nhưng ban đầu thiếu cờ `occluded` | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

**Lỗi:** Sai hoặc thiếu cờ trạng thái cho các điểm mốc `face13`, đặc biệt là phân biệt `occluded` và `outside`.

**Vì sao mình mắc:** Khi xử lý ảnh NIR có góc chụp nghiêng và các điểm mốc bị che khuất, mình chưa phân biệt đầy đủ giữa điểm vẫn xác định được vị trí tương đối nhưng bị che và điểm nằm ngoài phạm vi quan sát. Việc kiểm tra lại từng thuộc tính trong panel Objects cũng chưa được thực hiện kỹ.

**Lần sau tránh bằng cách:** Sau khi hoàn thành 13 điểm `face13`, kiểm tra lần lượt từng điểm trong panel Objects, đối chiếu mục 4.6 của guideline và xác nhận các cờ trạng thái trước khi lưu annotation.

## 3. Ghi chú về disagreement_log

Qua review chéo với Trần Đức Hoà, mình nhận thấy có hai trường hợp bạn góp ý đúng và mình cần điều chỉnh:

- **`S05_ir.png` – `child_seat.occupied`:** Ban đầu mình gán `unknown`, trong khi bạn gán `no`. Qua đối chiếu, mình hiểu rằng thao tác copy box từ ảnh RGB sang IR giúp tiết kiệm thời gian nhưng vẫn phải rà soát lại thuộc tính sau khi copy, vì ảnh IR có thể cung cấp bằng chứng rõ hơn để xác định trạng thái `occupied`.

- **`D01.png` – `face13.mouth_right.occluded`:** Ban đầu mình đánh dấu `outside` thay vì `occluded`. Qua trường hợp này, mình học được cách phân biệt điểm mốc bị che khuất nhưng vẫn xác định được vị trí tương đối với điểm nằm ngoài phạm vi quan sát, nhằm giữ lại thông tin về điểm mốc giải phẫu bị che khuất thay vì loại bỏ điểm đó khỏi dữ liệu huấn luyện.

Hai trường hợp trên giúp mình rút ra bài học rằng cần kiểm tra độc lập từng kênh ảnh, rà soát thuộc tính sau khi copy box và áp dụng nhất quán quy tắc gán cờ keypoint theo guideline.
