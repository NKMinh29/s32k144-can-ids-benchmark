# Hồ sơ artifact cần nhập

Trạng thái 30/09/2026: đã đọc bản thảo gần nhất; chưa nhập các artifact thực nghiệm vào starter này.

| Artifact | Nguồn cần đối chiếu | Điều cần xác nhận |
|---|---|---|
| Firmware source | Project dùng tạo ELF cuối | Commit/snapshot, flags, model arrays |
| ELF + MAP | Đúng bản flash cho 18 run | SHA-256, section sizes, toolchain |
| Clock evidence | Runtime API/register audit | 48 MHz; xử lý bản cũ 80 MHz riêng |
| Raw logs | 18 run đo thật | 128 record/run, raw checksum |
| Logger structs | C header/source tương ứng | Alignment, packing, endianness, offsets |
| Offline notebook | Model và split trong bài | Dataset source/hash, split, seed, dependencies |
| Host parity evidence | Python integer vs C | 30.000 signed scores theo bản thảo |
| Hardware probes | Bốn input trong bài | Input, output, build, capture |
| Figures | Script và input | Tái tạo từ CSV cuối |

## Ma trận run cần khớp

| Model | Input | LPIT | Số run | Record/run |
|---|---|---|---:|---:|
| D3 | Normal | OFF | 3 | 128 |
| D3 | Attack | OFF | 3 | 128 |
| D3 | Normal | ON | 3 | 128 |
| D4 | Normal | OFF | 3 | 128 |
| D4 | Attack | OFF | 3 | 128 |
| D4 | Normal | ON | 3 | 128 |

Không điền checksum, tên raw file, acceptance, DOI hoặc kết quả tái chạy bằng giá trị đoán.
Manifest CSV kèm theo chỉ có header; điền từ file thực trước khi phân tích.

## Run protocol cần viết lại từ setup thật

1. Toolchain, board revision, wiring, CAN settings và project snapshot.
2. Xác nhận flash đúng ELF/hash và clock.
3. Chọn model/LPIT ở start gate; ghi capture metadata.
4. Chạy đúng traffic input cho tới khi logger seal.
5. Export log; ghi ngay run_id, config, hash và lỗi quan sát.
6. Validate trước khi aggregate; giữ cả run thất bại và lý do loại.

Không tự suy ra binary offsets chỉ từ tổng kích thước metadata/record. Cần định nghĩa cấu trúc và kiểm tra với file thật.
