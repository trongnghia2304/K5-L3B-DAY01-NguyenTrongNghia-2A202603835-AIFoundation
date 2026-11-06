# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603835
- **Họ và tên:** Nguyen Trong Nghia
- **SEED** (in ở ô đầu notebook): 3178

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☑ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☑ |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*

| Phương án | F1 (test) | F1 (SUB 40) | p95 ms/tin | USD / 1k tin |
| --- | ---: | ---: | ---: | ---: |
| 1. BoW + LogReg (tự code) | 0.862 | 0.923 | 0.084 | 0 |
| 2. BoW + MLP (deep learning) | 0.912 | 0.919 | 2.118 | 0 |
| 3a. Encoder (MiniLM) + kNN | 0.887 | 0.900 | 37.515 | 0 |
| 3b. Encoder (MiniLM) + LogReg | 0.958 | 0.950 | 30.330 | 0 |
| 3c. Encoder (MiniLM) + MLP head | 0.958 | 0.974 | 45.583 | 0 |
| 4a. LLM nhỏ zero-shot (groq · gpt-oss-20b) | — (chỉ đo SUB) | 0.909 | 2363.646 | 0 (Groq free tier) |
| 4b. LLM lớn zero-shot (groq · gpt-oss-120b) | — (chỉ đo SUB) | 0.857 | 2444.741 | 0 (Groq free tier) |
| 4c. LLM nhỏ few-shot (groq · gpt-oss-20b) | — (chỉ đo SUB) | 0.895 | 2668.145 | 0 (Groq free tier) |

Đường Pareto: 1, 3b, 3c. Cả 5 phương án 1–3c đều đạt SLA p95 < 50 ms; cả 3 phương án LLM (p95 ≈ 2.4–2.7 s) đều không đạt.

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*

| Phần | Hỏi AI gì | AI trả lời/viết gì | Mình đã sửa / kiểm chứng gì |
| --- | --- | --- | --- |
| Phần 1 | Giải thích công thức cập nhật w và lý do F1 thay cho accuracy | Hướng dẫn đạo hàm của BCE loss và ý nghĩa dữ liệu lệch lớp | Tự code kiểm chứng các hàm vectorize, sigmoid, train_logreg, metrics |
| Phần 2 | Nguyên lý hoạt động của ReLU và 5 dòng trong PyTorch training loop | Giải thích tính phi tuyến và cơ chế zero_grad, backward, step | Chạy kiểm chứng và theo dõi hiện tượng overfit trên biểu đồ val loss |
| Phần 3 | Bản chất của vector embedding và cách tính cosine đồng thời | Gợi ý chuẩn hoá L2 ma trận để nhân vô hướng | Tự code top_k_similar, knn_predict và kiểm tra trên tập test |
| Phần 4 (cấu hình provider) | Nhờ Claude tìm model phù hợp | AI đã trả lời gợi ý cho mình dùng Groq và cách vào trang để lấy api key free | Đã lấy api key free và chạy thành công so với tự kiếm key từ các model khác |
