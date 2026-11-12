# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202604061
- Ngày / CVAT local: 11/11/2026
- Công cụ đã dùng: cvat, vscode

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: 
    Ảnh 000000181542.jpg; người phụ nữ mặc áo sáng màu gần giữa ảnh, đang băng qua đường; class person.
- Class và quy tắc tôi dùng để chọn biên: 
    Chọn class person. Vẽ theo đường viền nhìn thấy của người và quần áo; không lấy phần đường, xe máy hoặc người đi đường khác. Ở chỗ bị che khuất, chỉ đánh dấu phần nhìn thấy.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: 
    Gợi ý cho người đi bộ giúp xác định vùng đối tượng, nhưng cần kiểm tra kỹ tay/chân và các phần gần xe máy. Giữphần mask khớp với người; sửa hoặc bỏ phần mask lấn sang xe hay mặt đường vì đó không thuộc class person
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.
    Không dùng gợi ý; tôi tự vẽ mask cho người phụ nữ theo đường viền nhìn thấy, và không gộp xe máy hoặc mặt đường vào nhãn person

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Medium — 000000181542.jpg, vùng các người đi xe máy ở hai bên và người phụ nữ đang băng qua gần giữa ảnh.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Gộp-tách và biên
- Bằng chứng tôi nhìn thấy: Preview có nhiều khung và mask person chồng lấn quanh người đi xe máy; một số mask có vẻ lan sang xe máy hoặc phần người bên cạnh. Ảnh này có 30 annotation person, nên cần rà soát các vùng chồng lấn thay vì xem tất cả là đúng.
- Quy tắc và hành động sửa: Tách nhãn person khỏi motorcycle; chỉ giữ mask trên phần cơ thể nhìn thấy của người, không lấy thân xe hoặc người khác. Xóa mask trùng nếu nhiều annotation đang đánh dấu cùng một người.
- Sau sửa đã Save và export lại chưa? Chưa. Tôi mới kiểm tra preview/ZIP được tạo tự động, chưa sửa, Save hoặc export lại từ CVAT.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork:

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 000000181542.jpg — người phụ nữ gần giữa ảnh, cạnh xe máy | Mask người chỉ gồm phần cơ thể nhìn thấy; hoặc gồm cả phần bị xe/người khác che khuất | Chỉ có thể nhìn thấy đường biên của phần không bị che | Chỉ gán phần nhìn thấy; hỏi coach cách xử lý phần cơ thể bị che nếu công cụ đề xuất mask kéo dài vào xe |
| 000000373353.jpg — người đi bộ gần chiếc taxi vàng ở giữa ảnh | Pixel ở vùng chồng lấn thuộc person hay car | Người và xe sát/chồng lên nhau trong ảnh; vùng bị che không có biên quan sát được | Giữ biên theo phần nhìn thấy, không tự suy diễn pixel khuất |
| 000000458325.jpg — người đi ván trượt ở gần giữa ảnh | Gán phần ván trượt vào person, hoặc không gán vì không có class skateboard | Bộ nhãn Medium có person nhưng không có skateboard | Gán cơ thể vào person; hỏi coach xem ván trượt không có class riêng thì để nền hay xử lý theo quy tắc khác |

