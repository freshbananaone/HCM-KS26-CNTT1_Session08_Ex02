# Bài 2: Chuẩn hóa tài liệu cài đặt cảm biến độ ẩm

*Tài liệu thực hành Markdown – Trang trại Lan*

> **Lưu ý:** Đây là tài liệu minh họa để học cách trình bày Markdown và kiểm tra logic điều khiển máy bơm. Đề bài chưa cung cấp model cảm biến, bộ điều khiển hoặc sơ đồ đấu dây, nên ví dụ Python chỉ **mô phỏng** thao tác bật/tắt, chưa điều khiển phần cứng thật.

## 1. Phân tích Input / Output (I/O)

- **Input:** Văn bản thô được viết bằng Markdown, gồm nội dung hướng dẫn, tên biến, câu lệnh Terminal, mã Python, bảng so sánh và danh sách kiểm tra.
- **Output:** Khi mở bằng StackEdit, nội dung được *Markdown Parser* chuyển thành giao diện dễ đọc: tiêu đề rõ ràng, đoạn code tách biệt và tô màu, bảng thẳng hàng, ô đánh dấu công việc.

Vì vậy, cùng một tài liệu vừa có thể lưu bằng file `.md`, vừa xem đẹp trên StackEdit mà không phải định dạng thủ công trong Word.

## 2. Các bước chuẩn bị và kiểm tra

1. **Kiểm tra thiết bị:** Xác định chính xác loại cảm biến, điện áp cấp nguồn, chân tín hiệu và bộ điều khiển đang sử dụng trước khi nối dây.
2. **Lắp cảm biến:** Đặt đầu đo vào vùng đất cần theo dõi; đấu nối theo sơ đồ của *đúng model* và ngắt nguồn điện khi thực hiện.
3. **Kiểm tra dữ liệu:** Đọc giá trị cảm biến trên bộ điều khiển, thử ở đất khô và đất ẩm để hiệu chuẩn.
4. **Thử logic máy bơm:** Chạy chương trình Python mô phỏng dưới đây trước. Chỉ triển khai bơm thật khi đã có mạch điều khiển phù hợp và biện pháp chống chạy khô, chống tràn.

Tên biến `do_am` là giá trị độ ẩm đo được, còn `NGUONG_BAT` là ngưỡng quyết định bật bơm. Lệnh ngắn `python3 --version` có thể đặt trong câu văn bằng **Inline Code**.

### Lệnh nhập trong Terminal

Hai dòng sau là **lệnh cần gõ vào Terminal**, không phải đoạn văn giải thích:

```bash
python3 --version
python3 dieu_khien_bom.py
```

> Trước khi chạy dòng thứ hai, hãy lưu đoạn code Python tại mục 3 thành file `dieu_khien_bom.py`.

## 3. Ví dụ Python kiểm tra logic điều khiển bơm

Đoạn code dùng ba giá trị đo mẫu và in trạng thái bơm. Ngưỡng `40` chỉ là ví dụ, không phải ngưỡng tiêu chuẩn cho mọi cây trồng hoặc cảm biến.

```python
NGUONG_BAT = 40  # Nguong minh hoa, can hieu chuan thuc te


def dieu_khien_bom(do_am):
    """Mo phong quyet dinh bat/tat bom dua tren do am (%)."""
    if not 0 <= do_am <= 100:
        raise ValueError("Do am phai nam trong khoang 0-100")

    if do_am < NGUONG_BAT:
        return "BAT BOM (mo phong)"
    return "TAT BOM"


for do_am in [55, 32, 47]:
    print(f"Do am {do_am}%: {dieu_khien_bom(do_am)}")
```

**Kết quả dự kiến:** Giá trị `55` và `47` cho trạng thái tắt bơm; giá trị `32` cho trạng thái bật bơm (mô phỏng). Muốn điều khiển máy bơm thật phải thay phần mô phỏng bằng mã dành riêng cho bộ điều khiển và kiểm tra an toàn.

## 4. So sánh hai loại cảm biến

Bảng dưới đây sử dụng hai nhóm thường gặp để minh họa khái niệm **cảm biến cũ** và **cảm biến mới**, không phải so sánh hai model cụ thể của trang trại.

| Tiêu chí | Loại cũ: cảm biến điện trở | Loại mới: cảm biến điện dung |
| :--- | :--- | :--- |
| Nguyên lý | Đo sự thay đổi điện trở qua đất | Đo sự thay đổi điện dung liên quan đến độ ẩm |
| Ưu điểm | Thường rẻ và dễ thử nghiệm | Đầu đo thường ít bị ăn mòn hơn khi dùng lâu |
| Hạn chế | Điện cực dễ bị ăn mòn theo thời gian | Cần hiệu chuẩn, giá tùy model có thể cao hơn |
| Phù hợp | Bài thực hành ngắn hạn | Theo dõi độ ẩm lâu dài nếu chọn đúng thiết bị |

## 5. Task List kiểm tra thiết bị

- [ ] Đã xác định model và điện áp của cảm biến.
- [ ] Đã kiểm tra nguồn cấp và mạch điều khiển bơm.
- [ ] Đã lắp, đấu nối theo đúng sơ đồ của nhà sản xuất.
- [ ] Đã thử cảm biến ở đất khô và đất ẩm, ghi lại giá trị.
- [ ] Đã chạy thử file Python mô phỏng trên Terminal.
- [ ] Đã kiểm tra biện pháp chống chạy khô/chống tràn trước khi dùng bơm thật.

## 6. Ghi nhớ ký tự Escape

Để hiển thị nguyên văn dấu \* hoặc dấu \# mà không tạo định dạng Markdown, cần viết dấu gạch chéo ngược `\` trước ký tự đặc biệt. Ví dụ: `\*` sẽ hiện thành dấu sao, còn `\#` sẽ hiện thành dấu thăng.

## 7. Kết luận

Theo mình, việc tách rõ **đoạn giải thích**, `tên biến`, lệnh Terminal và khối code giúp người mới đỡ nhầm khi làm theo hướng dẫn. Bảng so sánh và Task List cũng khiến việc kiểm tra thiết bị có thứ tự hơn, thay vì phải đọc một đoạn văn dài.
