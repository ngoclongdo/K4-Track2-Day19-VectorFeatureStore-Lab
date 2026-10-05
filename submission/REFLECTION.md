# Reflection — Lab 19

**Tên:** _Đỗ Nguyễn Ngọc long_
**Cohort:** _2A202602390_
**Path đã chạy:** _lite_

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **Exact (BM25 = 96.7% | Hybrid = 96.7%):** BM25 tối ưu do bắt đúng từ khóa chuyên môn verbatim (TF-IDF cao). Hybrid bảo toàn được độ chính xác nhờ RRF dung hòa rank.
- **Paraphrase (BM25 = 33.3% | Hybrid = 32.0% | Vector = 24.0%):** Do bge-small-en-v1.5 train trên tiếng Anh nên biểu diễn câu dài tiếng Việt hạn chế. Đổi sang `bge-m3` đa ngữ sẽ giúp pure Vector thắng vượt trội.
- **Mixed (Hybrid = 100.0% vs BM25 = 97.0%, Vector = 98.5%):** Hybrid thắng áp đảo vì người dùng thực tế vừa dùng từ khóa cụ thể vừa kèm diễn giải ngữ nghĩa, RRF cộng hưởng tín hiệu từ cả hai phía.

**Khi nào KHÔNG dùng Hybrid:**
1. **Pure BM25:** Khi truy vấn mang tính định danh chính xác (mã SKU, model, tên biến/hàm, số CMND/CCCD, log error code), hoặc tài nguyên máy chủ bị giới hạn không đủ RAM/CPU chạy embedding inference.
2. **Pure Vector:** Khi tìm kiếm đa phương thức (cross-modal image/text) hoặc dữ liệu hoàn toàn không đồng nhất về từ vựng (ngôn ngữ tự nhiên phức tạp, đa ngôn ngữ dịch nghĩa) mà từ khóa không có giá trị phân biệt.

---

## Điều ngạc nhiên nhất khi làm lab này

RRF với công thức đơn giản $1/(60 + \text{rank})$ giải quyết hoàn hảo bài toán khác biệt thang đo điểm (sparse score vs cosine similarity) mà không cần chuẩn hóa phân phối hay học trọng số.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
