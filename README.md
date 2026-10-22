# VenixScoreboard — Paper 26.2 (1.21.4)

Plugin hiển thị bảng thông tin (Sidebar Scoreboard) cao cấp dành riêng cho server Paper 26.2 (1.21.4), hỗ trợ mượt mà người chơi **Java Edition** và **Bedrock Edition (PE)** thông qua **Geyser**.

---

## ✦ Các cải tiến và tính năng mới nhất

1. **Khắc phục triệt để lỗi lặp chữ trên Bedrock (Anti-Duplication):**
   - Đã gỡ bỏ việc gán đồng thời `team.prefix` và `score.customName`. Plugin hiện sử dụng trực tiếp cơ chế native `score.customName` của Paper 1.20.3+/1.21.4. Geyser sẽ chuyển đổi trực tiếp sang Bedrock mà **không bao giờ bị nhân đôi chữ**.

2. **Lệnh bật/tắt bảng Scoreboard (`/vs toggle`):**
   - Người chơi (đặc biệt là người chơi PE trên điện thoại màn hình nhỏ) có thể tự do đóng hoặc mở bảng điểm bất cứ lúc nào bằng lệnh:
     ```
     /venix toggle  (hoặc /vs toggle)
     ```
   - Trạng thái bật/tắt của từng người chơi được **lưu vĩnh viễn vào SQLite database**, khi người chơi thoát game hoặc server restart thì cài đặt vẫn được ghi nhớ.

3. **Thiết kế gọn gàng, tối ưu cho PE:**
   - Chiều cao bảng điểm được tinh giản từ 14 dòng xuống còn 10 dòng (loại bỏ các đường viền gạch ngang và các dòng trống thừa làm che tầm nhìn vũ khí/tay người chơi).
   - Thanh tiến trình EXP rút gọn còn 8 khối ký tự `[████░░░░]`, vừa vặn với chiều ngang màn hình cảm ứng di động.

4. **Tô đậm và phối màu nổi bật cho Rank & EXP:**
   - **Rank:**
     * `No Le`: `&e&lNo Le` (Vàng sáng in đậm nổi bật)
     * `Vo San`: `&a&lVo San` (Xanh lá sáng in đậm)
     * `Tu San`: `&b&lTu San` (Xanh cyan sáng in đậm)
     * `Quy Toc`: `&d&lQuy Toc` (Tím hồng in đậm sang trọng)
     * `Vua`: `&6&l&n✦ Vua ✦` (Vàng kim in đậm có gạch chân đẳng cấp)
   - **EXP & Level:**
     * `Level: &a&l{level}`
     * `EXP: &e&l{exp_current}&7/&b&l{exp_next}`
     * Thanh tiến trình: khối xanh lá `&a&l█` trên nền xám tối `&8░` với % vàng sáng `&e&l{exp_percent}`.

---

## ✦ Danh sách lệnh & Quyền hạn (Permissions)

| Lệnh | Quyền hạn | Mô tả |
| :--- | :--- | :--- |
| `/venix toggle` hoặc `/vs toggle` | `venixscoreboard.use` | **Bật / Tắt bảng Scoreboard cá nhân (được lưu vào DB)** |
| `/venix help` | `venixscoreboard.use` | Hiển thị bảng trợ giúp lệnh |
| `/venix reload` | `venixscoreboard.reload` hoặc `.admin` | Tải lại cấu hình an toàn không mất dữ liệu |
| `/venix rank get [player]` | `venixscoreboard.use` | Xem rank của bản thân hoặc người chơi khác |
| `/venix rank set <player> <rank>` | `venixscoreboard.rank.set` hoặc `.admin` | Đặt rank cho người chơi (`no_le`, `vo_san`, ...) |
| `/venix exp get [player]` | `venixscoreboard.use` | Xem EXP và Level của người chơi |
| `/venix exp add <player> <amount>` | `venixscoreboard.admin` | Cộng thêm EXP cho người chơi |
| `/venix exp set <player> <amount>` | `venixscoreboard.admin` | Đặt số EXP chỉ định cho người chơi |
| `/venix exp reset <player>` | `venixscoreboard.admin` | Đặt lại EXP của người chơi về 0 |
| `/venix quest list` | `venixscoreboard.use` | Xem danh sách nhiệm vụ & trạng thái tiến trình |
| `/venix quest progress <player>` | `venixscoreboard.quest.admin` hoặc `.admin` | Xem chi tiết tiến trình nhiệm vụ của người chơi |

---

## ✦ Cài đặt & Cập nhật

1. Lấy file **[VenixScoreboard.jar](file:///c:/Plugin%20Minecraft/VenixScoreboard.jar)** và chép đè vào thư mục `plugins/` của server Paper.
2. Chạy `/vs reload` hoặc restart server.
3. Nếu muốn cập nhật giao diện màu sắc và dòng mới, bạn có thể xóa thư mục `plugins/VenixScoreboard/` (hoặc xóa các file `scoreboard.yml`, `ranks.yml`, `exp.yml`, `messages.yml`) để plugin tự tạo lại các file cấu hình tối ưu mới nhất!
