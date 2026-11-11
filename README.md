# Tài liệu chuẩn bị cho R2

Đây là cây thư mục làm việc trên máy, chưa phải corpus đã publish.

- `raw/chua-thien-mu/`: đặt tài liệu nguồn nguyên bản (HTML, PDF, TXT…). Không sửa bản nguồn; giữ URL, tiêu đề, tác giả/cơ quan và ngày thu thập trong hồ sơ nguồn.
- `curated/vi/hue/dia-diem/chua-thien-mu/`: các file TXT mẫu để biên soạn và review theo chủ đề. Lưu bằng UTF-8, thay các phần trong dấu `[...]` bằng nội dung thực và dẫn nguồn.
- `curated/vi/hue/nhan-vat/`: hồ sơ nhân vật, mỗi nhân vật có thư mục riêng.
- `curated/vi/hue/am-thuc/`: hồ sơ món ăn, mỗi món có thư mục riêng.

Các file mẫu chưa có tri thức thực, không được ingestion hoặc publish khi còn placeholder. Chỉ giữ chủ đề có tài liệu; không cần điền mọi chủ đề nếu chưa có nguồn.

## Ngữ cảnh tour

`curated/` vẫn là kho tri thức có nguồn. Ngữ cảnh lời thuyết minh theo tour
được đặt riêng trong `tour-context/`, không trộn vào corpus tri thức:

```text
tour-context/
└── vi/
    └── lang-tu-duc/
        ├── s0.md
        ├── s2.md
        ├── s3.md
        ├── s4.md
        └── s5.md
```

Chỉ tạo các cảnh đã được xác nhận trong tour; không tự thêm `s1` hoặc suy cảnh
từ tên file audio. Mỗi file cảnh dùng front matter:

```yaml
content_type: tour_script
heritage_slug: lang-tu-duc
active_area_id: khiem-lang
scene_id: <id-cảnh>
scene_key: s<chỉ-số-cảnh>
language: vi
```

Sau front matter là tiêu đề `# Kịch bản thuyết minh cảnh ...`, mục
`## Nội dung thuyết minh` và nguyên văn kịch bản thực tế, gồm cả câu chuyển ý.
`scene_id` là liên kết chính; tên file chỉ hỗ trợ biên tập. Kịch bản giúp hệ
thống hiểu câu hỏi nhưng không tự động là citation.

Luồng dự kiến: lấy kịch bản theo ID cảnh → hiểu câu hỏi → tìm tư liệu có nguồn
trong phạm vi địa điểm → trả lời. Việc thêm file không tự tích hợp hệ thống;
bộ đọc và luồng chat phải được nối riêng. Chỉ nhập cảnh khi đã có kịch bản
thực tế để kiểm chứng.

Tên file dễ đọc trên máy, ví dụ `lich-su.txt`, là bản làm việc. Khi upload theo contract trong `docs/chatbot.md`, công cụ cần tính hash nội dung và tạo object key bất biến, ví dụ:

```text
knowledge/curated/vi/hue/dia-diem/chua-thien-mu/lich-su/<content-hash>.txt
```

Upload không tự đồng bộ thư mục và không tự đưa tài liệu vào chatbot. Pipeline sẽ tạo `processed/corpus-vN/`, passage, manifest và search index rồi kiểm tra trước khi publish. Không tự tạo `processed/` bằng tay.
