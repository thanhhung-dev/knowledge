# Tài liệu chuẩn bị cho R2

Đây là cây thư mục làm việc trên máy, chưa phải corpus đã publish.

- `raw/chua-thien-mu/`: đặt tài liệu nguồn nguyên bản (HTML, PDF, TXT…). Không sửa bản nguồn; giữ URL, tiêu đề, tác giả/cơ quan và ngày thu thập trong hồ sơ nguồn.
- `curated/vi/hue/dia-diem/chua-thien-mu/`: các file TXT mẫu để biên soạn và review theo chủ đề. Lưu bằng UTF-8, thay các phần trong dấu `[...]` bằng nội dung thực và dẫn nguồn.
- `curated/vi/hue/nhan-vat/`: hồ sơ nhân vật, mỗi nhân vật có thư mục riêng.
- `curated/vi/hue/am-thuc/`: hồ sơ món ăn, mỗi món có thư mục riêng.

Các file mẫu chưa có tri thức thực, không được ingestion hoặc publish khi còn placeholder. Chỉ giữ chủ đề có tài liệu; không cần điền mọi chủ đề nếu chưa có nguồn.

Tên file dễ đọc trên máy, ví dụ `lich-su.txt`, là bản làm việc. Khi upload theo contract trong `docs/chatbot.md`, công cụ cần tính hash nội dung và tạo object key bất biến, ví dụ:

```text
knowledge/curated/vi/hue/dia-diem/chua-thien-mu/lich-su/<content-hash>.txt
```

Upload không tự đồng bộ thư mục và không tự đưa tài liệu vào chatbot. Pipeline sẽ tạo `processed/corpus-vN/`, passage, manifest và search index rồi kiểm tra trước khi publish. Không tự tạo `processed/` bằng tay.
