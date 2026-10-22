# ✦ RANK TIER PLUGIN — TÀI LIỆU HƯỚNG DẪN HOÀN CHỈNH ✦

**Phiên bản Plugin:** v2.0.0  
**Tương thích:** Paper 26.2 (Minecraft 1.21.4)  
**Hỗ trợ nền tảng:** Java Edition & Bedrock Edition (PE) thông qua Geyser  
**File thực thi:** `RankTier.jar` (14.3 MB - Đã tích hợp sẵn SQLite JDBC Driver)  

---

## 1. TỔNG QUAN HỆ THỐNG
**RankTier** là plugin quản lý Cấp độ vô hạn, Rank số La Mã, Bảng thông tin Sidebar Scoreboard, Nhiệm vụ ngẫu nhiên và Đấu trường Truy nã (Bounty Hunting Duel) dành cho máy chủ Paper 26.2.

Plugin được thiết kế tối ưu hiệu năng:
- **Paper 1.21.4 Adventure API & NumberFormat:** Không nhấp nháy, ẩn hoàn toàn các con số đỏ `1..10` bên phải scoreboard.
- **Geyser Bedrock Friendly:** Không bị lặp chữ tiếng Việt trên điện thoại, hỗ trợ lệnh bật/tắt bảng linh hoạt.
- **Async Database & Auto-Migration:** Toàn bộ dữ liệu SQLite/MySQL được lưu bất đồng bộ, tự động nâng cấp cấu trúc bảng từ bản cũ mà không mất dữ liệu người chơi.

---

## 2. HỆ THỐNG RANK LA MÃ VÀ TITLE HIỂN THỊ
Mỗi người chơi có một Cấp độ (Level) và một Rank tương ứng bằng **chữ số La Mã** (`Rank I`, `Rank II`, `Rank III`,...):
- Cấp 1 -> Rank I
- Cấp 2 -> Rank II
- Cấp 3 -> Rank III
- Cấp 10 -> Rank X
- Cấp 50 -> Rank L
- Cấp 100 -> Rank C

### Định dạng Danh hiệu (Prefix/Title):
> **Quy tắc:** Ngoài cùng là **Rank**, bên trong là **Level**:  
> `[Rank I] [Lv.1] PlayerName`

Danh hiệu này tự động đồng bộ trên:
1. **Nametag trên đầu:** Người chơi khác nhìn thấy `[Rank I] [Lv.1]` bay trên đầu nhân vật.
2. **Tab List:** Danh sách người chơi trong phím Tab hiện đầy đủ tiền tố màu sắc.
3. **Kênh Chat:** Định dạng chat chuẩn `[Rank I] [Lv.1] PlayerName: Nội dung tin nhắn`.

Màu sắc rank thay đổi theo các mốc cấp độ:
- Cấp 1 - 5: Màu vàng sáng `§e§lRank I`
- Cấp 6 - 10: Màu xanh lá `§a§lRank VI`
- Cấp 11 - 20: Màu xanh dương `§b§lRank XI`
- Cấp 21 - 50: Màu hồng tím `§d§lRank XXI`
- Cấp 51+: Màu cam hoàng gia gạch chân `§6§l§nRank LI`

---

## 3. CÔNG THỨC EXP VÀ CẤP ĐỘ VÔ HẠN (INFINITE LEVELS)
Hệ thống không giới hạn cấp độ tối đa.

### Công thức yêu cầu EXP lên cấp tiếp theo:
$$E_{\text{req}}(L) = 1000 + (L - 1) \times 110$$

- **Level 1 -> 2:** Cần `1,000 EXP` (Tổng tích luỹ: 1,000)
- **Level 2 -> 3:** Cần `1,110 EXP` (Tổng tích luỹ: 2,110)
- **Level 3 -> 4:** Cần `1,220 EXP` (Tổng tích luỹ: 3,330)
- **Level 4 -> 5:** Cần `1,330 EXP` (Tổng tích luỹ: 4,660)
- **Level 5 -> 6:** Cần `1,440 EXP` (Tổng tích luỹ: 6,100)

### Lễ thăng cấp hiếm (Level-Up Ceremony):
Khi người chơi đủ EXP thăng cấp:
1. **Hiệu ứng vòng xoay hạt EXP:** Hạt ngọc lục bảo xanh lá (`HAPPY_VILLAGER`) và hạt vàng hoàng kim (`TOTEM_OF_UNDYING`) xoay quanh thân nhân vật theo hình xoắn kép trong 3 giây.
2. **Hiệu ứng Phát sáng (Glowing):** Người chơi phát sáng toàn thân trong 3 giây.
3. **Âm thanh thành tựu:** Phát âm thanh `UI_TOAST_CHALLENGE_COMPLETE`.
4. **Thông báo toàn server:** Kênh chat chỉ broadcast thông báo thăng cấp danh giá:  
   `✦ PlayerName đã thăng cấp lên Rank II (Cấp 2)! ✦`

---

## 4. CƠ CHẾ NHẬN KINH NGHIỆM (EXP)
EXP được tính tự động thông qua các hành động trong game:
- **Đặt block:** `+1 EXP / lần`
- **Phá block:** `+1 EXP / lần`
- **Tiêu diệt động vật (Mob thiện):** `+2 EXP / con` (Bò, cừu, gà, lợn, ngựa,...)
- **Tiêu diệt quái vật (Mob ác):** `+5 EXP / con` (Zombie, Skeleton, Creeper, Spider, Ghast, Slime,...)
- **Tiêu diệt Boss thế giới:** `+1000 EXP / con` (Warden, Ender Dragon, Wither)

---

## 5. HỆ THỐNG NHIỆM VỤ NGẪU NHIÊN (`quests.yml`)
Người chơi nhận nhiệm vụ tuần hoàn tự động để kiếm thêm EXP:
- **Bốc ngẫu nhiên:** Hệ thống tự gán một nhiệm vụ ngẫu nhiên từ file cấu hình.
- **Thời gian nghỉ ngơi:** Sau khi hoàn thành, người chơi nghỉ ngơi `30 giây` trước khi nhận nhiệm vụ mới.
- **Tự động làm mới:** Nếu người chơi không hoàn thành nhiệm vụ trong vòng `5 phút`, hệ thống sẽ tự hủy và đổi sang nhiệm vụ mới.
- **Dễ dàng cấu hình:** Quản trị viên có thể thêm bớt nhiệm vụ trong file `quests.yml`:
  ```yaml
  quests:
    break_5_blocks:
      display-name: "Phá 5 Block"
      type: BREAK_BLOCK
      amount: 5
      reward-exp: 100

    place_5_blocks:
      display-name: "Đặt 5 Block"
      type: PLACE_BLOCK
      amount: 5
      reward-exp: 100

    kill_5_mobs:
      display-name: "Giết 5 Quái vật"
      type: KILL_MOB
      amount: 5
      reward-exp: 100
  ```

---

## 6. ĐẤU TRƯỜNG TRUY NÃ & BOUNTY PULL (`/rankt wanted`)
Cơ chế PvP độc quyền kích thích giao chiến giữa các cao thủ:

1. **Phát lệnh truy nã:**  
   Người đi săn gõ: `/rankt wanted <tên_người_bị_săn>`
   - Cooldown: **1 tiếng (60 phút)** mỗi lần phát lệnh.
   - Thông báo toàn server:  
     `⚔ [TRUY NÃ] Hunter đang phát lệnh truy nã và săn lùng Target!`

2. **Đếm ngược kịch tính 5 giây:**  
   - Màn hình người bị truy nã xuất hiện **Title cảnh báo lớn**:  
     `⚔ BỊ TRUY NÃ! ⚔`  
     `Hunter sẽ tới sau 5s!`
   - Mỗi giây trôi qua đi kèm tiếng gõ chuông `BLOCK_NOTE_BLOCK_PLING` tăng dần cao độ.
   - Thanh ActionBar của thợ săn đếm lùi thời gian teleport.

3. **Dịch chuyển và Xuất hiện:**  
   - Hết 5 giây, thợ săn được dịch chuyển tức thì đến ngay vị trí nạn nhân.
   - Vụ nổ hạt khói `EXPLOSION` xuất hiện.
   - Đồng thời vang lên âm thanh hùng hồn của **Wither Spawn** và **Tù và cướp bóc Raid Horn**.

4. **Kết quả phân định thắng bại:**
   - **Người chiến thắng:**  
     - Tăng ngay **+1 Level** (bỏ qua lượng EXP cần cày của cấp hiện tại).
     - Nhận thêm **+500 Bounty**.
     - Cướp sạch toàn bộ điểm Bounty của người thua chuyển thành **EXP thưởng trực tiếp**.
     - Âm thanh vinh quang `UI_TOAST_CHALLENGE_COMPLETE`.
   - **Người thất bại:**  
     - Bị trừ **-1 Level** (tối thiểu Level 1).
     - Toàn bộ Bounty bị reset về 0.
     - Âm thanh thất bại `ENTITY_VILLAGER_NO`.
   - **Thông báo kết quả:** Broadcast toàn bộ máy chủ về kết quả cuộc đối đầu.

---

## 7. GIAO DIỆN SIDEBAR SCOREBOARD
Scoreboard hiển thị gọn gàng ở góc phải màn hình:

```text
       ✦ RANK TIER ✦
foggy.pikamc.vn:25058
Ngày: 22/10/2026 | Day: 127
 
Rank: Rank I
Cấp độ: Level 1 (250/1000 EXP)
Xếp hạng: #1 / 25
Bounty: 500 ✪
Nhiệm vụ: Phá 5 Block (2/5)
```

### Các tính năng đặc biệt của bảng:
- **Không số đỏ:** Ẩn hoàn toàn cột số đếm bên phải trên bản Java nhờ Paper NumberFormat.
- **Không thanh tiến trình:** Giao diện tối giản, tập trung vào số liệu thực tế.
- **Xếp hạng máy chủ:** Dòng `Xếp hạng: #{rank_num} / {total_players}` cập nhật vị trí của người chơi dựa trên tổng EXP so với toàn bộ người chơi trong cơ sở dữ liệu.
- **Bật/Tắt cá nhân:** Người chơi PE (điện thoại) hoặc người chơi muốn thoáng màn hình có thể gõ `/rankt toggle` để ẩn hoặc mở lại bảng bất kỳ lúc nào.

---

## 8. HỆ THỐNG THÔNG BÁO KHI VÀO SERVER (JOIN MESSAGE)
Hỗ trợ thông báo chào mừng tùy chỉnh trong `config.yml`:

```yaml
join-message:
  enabled: true

  # Tin nhắn riêng gửi cho người chơi khi họ kết nối
  personal:
    - ""
    - "&6&l━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
    - "&e&l  ✦ CHÀO MỪNG TRỞ LẠI! ✦"
    - ""
    - "&f  Xin chào, &a&l{player}&f!"
    - "&f  Rank: {rank_colored}"
    - "&f  Level: &a&l{level}"
    - ""
    - "&7  Gõ &e/rankt help &7để xem lệnh."
    - "&7  Gõ &e/rankt toggle &7để ẩn/hiện bảng."
    - "&6&l━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
    - ""

  # Tin nhắn broadcast toàn server khi có người vào
  broadcast:
    - "&8[&6&l✦&8] {rank_colored} &f{player} &7đã tham gia server!"

  # Tin nhắn broadcast toàn server khi có người thoát
  quit-broadcast:
    - "&8[&c&l✦&8] &f{player} &7đã rời server."
```

**Biến hỗ trợ (Placeholders):**
- `{player}`: Tên người chơi
- `{rank}`: Tên rank dạng text không màu (VD: `Rank I`)
- `{rank_colored}`: Tên rank có màu sắc nổi bật (VD: `§e§lRank I`)
- `{level}`: Cấp độ hiện tại
- `{prefix}`: Toàn bộ tiền tố danh hiệu `[Rank I] [Lv.1]`

---

## 9. DANH SÁCH LỆNH VÀ QUYỀN HẠN (COMMANDS & PERMISSIONS)

Lệnh chính: `/rankt` (các bí danh lệnh tương đương: `/rt`, `/ranktier`)

| Câu lệnh | Quyền hạn (Permission) | Mô tả |
| :--- | :--- | :--- |
| `/rankt wanted <player>` | `ranktier.wanted` | Phát lệnh truy nã và săn lùng đối thủ (cooldown 1h). |
| `/rankt toggle` | `ranktier.use` | Đóng hoặc mở bảng Scoreboard bên phải màn hình. |
| `/rankt top` | `ranktier.use` | Xem bảng xếp hạng Top người chơi có Level cao nhất. |
| `/rankt help` | `ranktier.use` | Hiển thị bảng menu trợ giúp các lệnh. |
| `/rankt exp get <player>` | `ranktier.admin` | Xem tổng EXP và Level của người chơi chỉ định. |
| `/rankt exp add <player> <amount>` | `ranktier.admin` | Cộng thêm EXP cho người chơi. |
| `/rankt exp set <player> <amount>` | `ranktier.admin` | Thiết lập trực tiếp lượng EXP của người chơi. |
| `/rankt exp reset <player>` | `ranktier.admin` | Reset toàn bộ EXP của người chơi về 0. |
| `/rankt reload` | `ranktier.reload` | Tải lại toàn bộ các file cấu hình `yml` mà không cần reload server. |

---

## 10. HƯỚNG DẪN DÀNH CHO BEDROCK / GEYSER (PE)
Để người chơi trên điện thoại / Bedrock Edition có trải nghiệm hoàn hảo nhất:

1. **Khắc phục trùng lặp chữ:** Plugin đã được tối ưu hóa chỉ ghi nội dung vào `score.customName()`, loại bỏ triệt để hiện tượng lặp chữ khi Geyser chuyển tiếp gói tin sang Bedrock.
2. **Ẩn các con số màu đỏ trên Bedrock Client:**  
   Bedrock client mặc định tự sinh số thứ tự nếu Geyser không can thiệp. Để ẩn hoàn toàn các con số này trên Bedrock, mở file `config.yml` của plugin **Geyser-Spigot** và đổi cấu hình sau:
   ```yaml
   scoreboard:
     show-scoreboard-scores: false
   ```
   Sau đó gõ `/geyser reload`. Toàn bộ số đỏ trên điện thoại sẽ biến mất hoàn toàn!
