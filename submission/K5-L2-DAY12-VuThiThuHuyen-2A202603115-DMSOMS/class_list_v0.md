# Danh sách lớp v0 — Vũ Thị Thu Huyền · G12

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`, `seatbelt`) | `seat`: driver; `seatbelt`: not_worn / unknown | Xác định người đang ngồi ở ghế lái và hỗ trợ phát hiện trường hợp tài xế chưa thắt dây an toàn để đưa ra cảnh báo | Có thể quan sát tư thế người và dây an toàn; tuy nhiên dây có thể bị che bởi quần áo, tay hoặc vùng tối |
| 2 | `face` và `glasses` | Box khuôn mặt; `glasses`: unknown / none / clear / sun | Xác định vị trí khuôn mặt để phục vụ phân tích mắt, hướng nhìn và tư thế đầu; nhận diện kính nhằm đánh giá các yếu tố có thể gây nhiễu khi quan sát mắt | Có thể nhận diện khuôn mặt; kính có thể xuất hiện phản xạ hoặc che khuất vùng mắt trên ảnh NIR |
| 3 | `eye_left`, `eye_right` | open / closed / unknown | Theo dõi trạng thái từng mắt để phát hiện nhắm mắt kéo dài, dấu hiệu mệt mỏi hoặc buồn ngủ khi lái xe | Có thể quan sát trên IR, nhưng độ chính xác giảm khi mắt bị kính phản xạ, góc mặt hoặc vật thể che khuất |
| 4 | `gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Xác định khu vực tài xế đang nhìn để phát hiện hành vi mất tập trung, chẳng hạn nhìn xuống đùi hoặc nhìn màn hình trung tâm quá lâu | Có thể ước lượng từ hướng đầu và vùng mắt; khó xác định khi mắt bị kính hoặc phản xạ che |
| 5 | `face13` | 13 điểm mốc khuôn mặt; cờ `occluded` / `outside` | Cung cấp các điểm đặc trưng để phân tích hướng xoay đầu, tư thế khuôn mặt và những biểu hiện liên quan đến mệt mỏi như nhắm mắt hoặc ngáp | Có thể quan sát khi khuôn mặt đủ rõ; cần chú ý điều kiện kích thước khuôn mặt và các điểm bị che khuất |
| 6 | `hand` (`whose`, `side`, `on_wheel`) | `whose`: driver / passenger; `side`: left / right; `on_wheel`: yes / no / unknown | Xác định bàn tay thuộc về tài xế hay hành khách, đồng thời kiểm tra tay tài xế có tiếp xúc với vô lăng hay không | Có thể nhận diện hình dạng và vị trí bàn tay, nhưng khó xác định khi tay bị vô lăng hoặc vật thể khác che |
| 7 | `phone` (`state`) | held / mounted / lap | Phát hiện điện thoại được cầm trên tay, đặt trên giá đỡ hoặc để trên đùi nhằm hỗ trợ nhận diện hành vi sử dụng điện thoại gây mất tập trung | Có thể nhận biết qua hình dạng và vị trí tương đối của thiết bị; chi tiết màn hình không phải lúc nào cũng quan sát được trên IR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`) | rear_left / rear_middle / rear_right (theo chiều xe) | Xác định số lượng hành khách và vị trí từng người ở hàng ghế sau, hỗ trợ giám sát tình trạng sử dụng ghế và an toàn cabin | Có thể quan sát hình dạng và vị trí cơ thể trên từng ghế |
| 2 | `person.seatbelt` | not_worn / unknown | Phát hiện hành khách chưa thắt dây an toàn hoặc trường hợp không đủ bằng chứng để xác định trạng thái dây | Có thể quan sát dải dây an toàn, nhưng cần giữ unknown khi dây bị che hoặc không đủ rõ |
| 3 | `face` (OMS) | Rectangle (chỉ vẽ box) | Xác định vị trí vùng đầu và khuôn mặt của hành khách, hỗ trợ đánh giá tư thế ngồi và tình trạng hành khách trong cabin | Có thể nhận diện vùng mặt khi đủ sáng IR; khó quan sát khi người quay mặt đi hoặc cúi thấp |
| 4 | `child_seat` (`occupied`) | `seat`; `occupied`: no / unknown | Nhận diện ghế trẻ em và xác định tình trạng có thể quan sát được bên trong ghế, hỗ trợ hệ thống giám sát an toàn trẻ em | Có thể nhận diện hình dạng ghế và lòng ghế; IR có thể giúp quan sát chi tiết khi ảnh RGB thiếu sáng |
| 5 | `infant_seat` (`facing`) | `seat`; `facing`: rear / front | Nhận diện nôi hoặc ghế dành cho trẻ nhỏ và hướng lắp đặt, hỗ trợ kiểm tra cấu hình ghế và an toàn túi khí | Có thể quan sát hình dáng tổng thể và hướng đặt ghế, nhưng cần đủ bằng chứng để xác định |
| 6 | `object` (`type`) | `seat`; `type`: bag / box / cup / other | Phân biệt các vật dụng trên ghế với hành khách hoặc ghế trẻ em, giúp giảm nhầm lẫn khi hệ thống phân tích tình trạng cabin | Có thể nhận diện hình dạng vật thể trên IR, nhưng không có đầy đủ thông tin màu sắc như RGB |
| 7 | `frame_meta` | `modality`: rgb / ir; `light`: day / night / unknown; `camera_blocked`: yes / no | Ghi nhận đặc điểm của khung hình và tình trạng camera, hỗ trợ kiểm soát chất lượng dữ liệu đầu vào cho hệ thống OMS | Có thể nhận biết modality và một số dấu hiệu camera bị che; thông tin ánh sáng cần dựa trên quy tắc metadata của dataset |

## 2 câu hỏi leo thang

**1. Câu hỏi:** Trong trường hợp có trẻ em ngồi bên trong `child_seat`, schema của dự án sẽ biểu diễn trẻ bằng thuộc tính `occupied` của ghế hay cần tạo thêm một box `person` riêng cho trẻ? Nếu có, quy tắc nào quyết định cách gán nhãn?

- **Khung ví dụ:** `S05_rgb.png`, `S05_ir.png` và `S02_rgb.png`.
- **Bạn tạm gán thế nào và vì sao:** Với `S05_rgb.png`, lòng ghế bị vùng tối che khuất nên mình giữ `occupied=unknown`. Trên ảnh `S05_ir.png`, lòng ghế quan sát rõ và không có trẻ bên trong nên có thể xác định `occupied=no`. Mình không sử dụng thông tin từ ảnh IR để suy diễn ngược sang ảnh RGB, đồng thời không tự thêm box `person` nếu chưa có quy định xác nhận.

**2. Câu hỏi:** Khi một điểm mốc `face13` bị che khuất bởi cấu trúc khuôn mặt hoặc góc quay đầu nhưng vẫn nằm trong khung hình, cần dựa vào tiêu chí nào để phân biệt `occluded` và `outside`? Làm thế nào để áp dụng nhất quán giữa các ảnh NIR có góc chụp khác nhau?

- **Khung ví dụ:** `D01.png` – điểm `mouth_right`; `D02.png` – điểm `left_eye_outer`.
- **Bạn tạm gán thế nào và vì sao:** Sau khi đối chiếu guideline và review chéo, mình sử dụng cờ `occluded` cho các điểm bị che khuất nhưng vẫn có thể xác định vị trí tương đối theo cấu trúc khuôn mặt. Không sử dụng `outside` chỉ vì điểm mốc không nhìn thấy rõ, khi chưa có căn cứ cho thấy điểm nằm ngoài phạm vi ảnh.