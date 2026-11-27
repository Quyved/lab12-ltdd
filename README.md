# Lab 12 — Juice Tracker: Views trong Jetpack Compose

Bài thực hành theo [codelab Android Developers](https://developer.android.com/codelabs/basic-android-kotlin-compose-view-interop?hl=vi).
Mã nền lấy từ nhánh `compose-starter` của [Google Developer Training](https://github.com/google-developer-training/basic-android-kotlin-compose-training-juice-tracker).
Giữ nguyên giấy phép Apache 2.0 của dự án gốc.

## Chức năng

- Thêm, sửa và xóa nước ép; lưu dữ liệu cục bộ bằng Room.
- `ColorSpinnerRow`: nhúng Android `Spinner` bằng `AndroidView`, chọn một trong 7 màu và đồng bộ với trạng thái Compose.
- `RatingInputRow`: nhúng `RatingBar`, đánh giá từ 0 đến 5 sao với bước 1 sao.
- `AdBanner`: nhúng `AdView` ở đầu danh sách, dùng App ID và Ad Unit ID thử nghiệm của Google; tải một lần khi tạo View và giải phóng khi View rời Composition.

## Build và cài đặt

Cần JDK 17 trở lên, Android SDK Platform 35 và kết nối mạng để tải thư viện.

1. Mở dự án bằng Android Studio và chờ Gradle Sync hoàn tất.
2. Nếu build bằng dòng lệnh, cấu hình SDK trong `local.properties` (không commit file này), ví dụ `sdk.dir=C:/Users/YourName/AppData/Local/Android/Sdk`.
3. Chạy trên Windows:

```powershell
.\gradlew.bat assembleDebug lintDebug
```

APK tạo tại `app/build/outputs/apk/debug/app-debug.apk`, hỗ trợ Android 7.0 (API 24) trở lên.
Cài bằng Android Studio hoặc `adb install -r app/build/outputs/apk/debug/app-debug.apk`.
Đây là APK debug có chữ ký debug để cài thử/nộp bài.

## Kiểm tra chức năng trên thiết bị

1. Nhấn **+**, nhập tên và mô tả, chọn màu và số sao, rồi **Save**.
2. Chạm mục vừa lưu: màu và số sao phải khớp; sửa rồi lưu lại.
3. Đóng/mở ứng dụng: dữ liệu vẫn được giữ trong Room.
4. Xóa một mục và kiểm tra danh sách cập nhật.
5. Khi có mạng và dịch vụ quảng cáo khả dụng, banner hiển thị quảng cáo thử nghiệm của Google. Banner có thể trống khi ngoại tuyến hoặc dịch vụ không trả quảng cáo.

Không thay ID thử nghiệm bằng ID quảng cáo thật để nộp bài.

## Kết quả kiểm tra

- `assembleDebug lintDebug`: **BUILD SUCCESSFUL**.
- Android Lint: **0 errors, 25 warnings** (phiên bản thư viện/target SDK, tài nguyên, biểu tượng và nhãn trong mã nền).
- APK được xác minh bằng `apksigner verify --verbose`: hợp lệ, chữ ký APK Signature Scheme v2.
- Application ID: `com.example.juicetracker`; min SDK 24; target SDK 35.
- Chưa chạy thử trên thiết bị: tại thời điểm build, `adb devices` không có thiết bị kết nối.
