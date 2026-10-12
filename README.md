## Cấu hình workflow

Tệp cấu hình: [.github/workflows/ci.yml](.github/workflows/ci.yml).

| Thành phần | Cấu hình |
| --- | --- |
| Tên workflow | Java Spring Boot CI (Gradle) |
| Sự kiện kích hoạt | `push` lên nhánh `main` |
| Job | `test`, hiển thị tên `Run Unit Tests` |
| Runner | `ubuntu-latest` |
| Checkout mã nguồn | `actions/checkout@v5` |
| Thiết lập Java | `actions/setup-java@v5`, JDK `17`, distribution `temurin` |
| Cấp quyền thực thi | `chmod +x gradlew` |
| Chạy kiểm thử | `./gradlew test` |

Các bước chạy tuần tự. Nếu JUnit test thất bại, lệnh Gradle trả về mã lỗi và job có trạng thái `Failure`.

## Đưa workflow lên repository

1. Sao chép tệp `ci.yml` vào `.github/workflows/ci.yml` tại gốc repository Spring Boot sử dụng Gradle. Thư mục gốc cần có `gradlew`, `gradle/wrapper/`, tệp cấu hình Gradle và mã nguồn kiểm thử JUnit.
2. Từ thư mục gốc của dự án, thực hiện:

```bash
git add .github/workflows/ci.yml
git commit -m "Thêm workflow chạy unit test với Gradle"
git push origin main
```

## Kiểm tra kết quả

1. Mở repository trên GitHub, chọn tab **Actions**.
2. Mở lượt chạy của workflow **Java Spring Boot CI (Gradle)**.
3. Chọn job **Run Unit Tests**, kiểm tra bước chạy `./gradlew test`.
4. Kết quả cần đạt: log có `BUILD SUCCESSFUL` và job hiển thị `Success`.

Minh chứng mẫu được lưu riêng tại [unit-test.log](unit-test.log) và [actions-success.png](actions-success.png). Đây là log và ảnh mô phỏng với tài khoản `CrouAn244`, chưa phải kết quả chạy trên GitHub.

Tài liệu đối chiếu: [actions/setup-java phiên bản v5](https://github.com/actions/setup-java/tree/v5).
