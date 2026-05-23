# Hướng dẫn thiết lập Google Apps Script Backend cho MOS Survey

Tài liệu này chứa mã nguồn Google Apps Script và hướng dẫn thiết lập Google Sheet để nhận kết quả khảo sát MOS tự động gửi từ trình duyệt người nghe.

---

## 1. Mã nguồn Google Apps Script (Paste-Ready)

Hãy sao chép toàn bộ mã nguồn bên dưới để dán vào trình biên tập Apps Script:

```javascript
function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    const sheet = SpreadsheetApp.getActive().getSheetByName('responses');

    // Ghi mỗi lượt đánh giá (listener, stimulus) thành 1 dòng trong sheet
    data.ratings.forEach(r => {
      sheet.appendRow([
        new Date(),
        data.listener_id,
        data.started_at,
        data.completed_at,
        r.stim_id,
        r.rating,
        r.played_count,
        r.time_to_rate_ms,
        r.comment || '',
        data.user_agent
      ]);
    });

    return ContentService
      .createTextOutput(JSON.stringify({status: "ok"}))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({status: "error", message: err.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// Chạy hàm này thủ công MỘT LẦN để thiết lập tiêu đề các cột
function setupSheet() {
  const sheet = SpreadsheetApp.getActive().getActiveSheet();
  sheet.setName('responses');
  sheet.getRange(1, 1, 1, 10).setValues([[
    'received_at', 'listener_id', 'started_at', 'completed_at',
    'stim_id', 'rating', 'played_count', 'time_to_rate_ms',
    'comment', 'user_agent'
  ]]);
  sheet.setFrozenRows(1);
}
```

---

## 2. Các bước thiết lập chi tiết (10-Step Checklist)

1. Vào [Google Sheets](https://sheets.google.com) → click vào nút **"+ Trống"** (hoặc Blank) để tạo một bảng tính Google Sheet mới, đặt tên bảng tính là **"MOS Survey Results"**.
2. Trong thanh menu của Google Sheet, chọn **Extensions** (Tiện ích mở rộng) → **Apps Script**.
3. Xóa toàn bộ đoạn code mẫu mặc định (`function myFunction() { ... }`), rồi dán toàn bộ đoạn code ở mục **1** ở trên vào.
4. Nhấn **Save** (Ctrl+S hoặc click biểu tượng đĩa mềm), đặt tên cho dự án là **"MOS Survey Backend"**.
5. Trên thanh công cụ Apps Script, chọn hàm **"setupSheet"** bên cạnh nút Run, rồi click **"Run"**. Một hộp thoại cấp quyền (Authorization Required) sẽ hiện lên:
   - Click **Review permissions** (Xem lại quyền).
   - Chọn tài khoản Google của bạn.
   - Nhấn chọn **Advanced** (Nâng cao) ở góc dưới → Click link **"Go to MOS Survey Backend (unsafe)"** (Đi tới MOS Survey Backend - không an toàn).
   - Click **Allow** (Cho phép) để cấp quyền truy cập bảng tính.
   - Kiểm tra tab Google Sheet lúc nãy, bạn sẽ thấy sheet được đổi tên thành `"responses"` và dòng đầu tiên xuất hiện 10 cột tiêu đề được in đậm, đóng băng (frozen row).
6. Quay lại trang Apps Script → Click nút **Deploy** (Triển khai) ở góc trên bên phải → Chọn **New deployment** (Triển khai mới).
   - Click biểu tượng bánh răng ở cạnh mục "Select type" → Chọn **Web app**.
   - Mục **Description**: Ghi `"MOS Survey v1"`.
   - Mục **Execute as**: Chọn **Me (your-email@gmail.com)**.
   - Mục **Who has access**: Chọn **Anyone** (Bất kỳ ai) ← *LƯU Ý QUAN TRỌNG: Phải chọn "Anyone" thay vì "Anyone with Google account" để người tham gia khảo sát không cần đăng nhập tài khoản Google vẫn gửi được kết quả.*
   - Click nút **Deploy**.
   - Cấp quyền một lần nữa nếu được yêu cầu.
   - Sau khi thành công, sao chép đường dẫn **Web app URL** được tạo ra (có dạng: `https://script.google.com/macros/s/AKfycb.../exec`).
7. Mở file `tts-audio-oke/survey/index.html` trong trình chỉnh sửa văn bản, thay thế chuỗi placeholder `"__APPS_SCRIPT_URL__"` bằng đường dẫn URL vừa copy ở bước 6 (đảm bảo đặt trong dấu nháy kép, ví dụ: `const APPS_SCRIPT_URL = "https://script.google.com/macros/s/.../exec";`).
8. Thực hiện commit và push file `index.html` đã cập nhật lên GitHub repository.
9. Đợi 1-2 phút để GitHub Pages cập nhật bản build mới.
10. Truy cập vào link khảo sát chính thức của bạn để kiểm tra: [https://nguyen220905.github.io/tts-audio-oke/survey/](https://nguyen220905.github.io/tts-audio-oke/survey/)
    - Thực hiện thử 1 lượt khảo sát đầy đủ và nhấn hoàn tất.
    - Quay lại Google Sheet kiểm tra xem các hàng kết quả mới đã xuất hiện trong bảng dữ liệu hay chưa.
