---
title: "Không Hoạt Động - Không Giá Trị"
subtitle: "Đừng nói \"không hoạt động\". Hãy đưa ra chi tiết."
date: 2022-11-30T12:18:43+07:00
authors: ["HSGamer"]
description: "Đừng nói \"không hoạt động\". Hãy đưa ra chi tiết."

tags:
- not work
categories:
- development

comment:
  enable: true
share:
  enable: true
---

# Tình huống

> Bạn đang có một ngày đẹp trời để làm việc với dự án cá nhân của bạn. Rồi tự nhiên có một người lạ nhắn với bạn và nói rằng dự án của bạn không hoạt động với máy của họ. Bạn sẽ làm gì?

Tình huống này đã xảy ra với tôi vài lần ở kênh hỗ trợ của tôi. Trong phần lớn lần đó, tôi thường kêu họ cung cấp thêm chi tiết về máy của họ đang sử dụng, cách họ cài đặt dự án của tôi, lỗi họ đã thấy, v.v. Rồi ngồi chờ họ trả lời.

Tuy nhiên, không chỉ dịch vụ của tôi, còn các dịch vụ của đồng nghiệp và nhà cung cấp dịch vụ mà tôi quen biết cũng gặp tình trạng tương tự. Cho nên, tôi tạo bài viết này như một đường dẫn tắt để dạy người dùng cách báo cáo lỗi.

# Đừng

```txt
00:00 - Người Dùng: Xin chào. Tính năng này không hoạt động đối với tôi. Có cách nào để sửa không?
05:00 - Hỗ Trợ: Hmmmm... Lạ thật đấy, tôi không thấy lỗi đó trên máy của tôi. Bạn có thể gửi tôi tệp cài đặt của bạn được không?
06:00 - Người Dùng: Đây là tệp cài đặt của tôi: config.yml
06:30 - Hỗ Trợ: Bạn quên chỉnh `enabled` thành `true`
07:00 - Người Dùng: Phải rồi ha. Tôi quên. Hoạt động được rồi. Cảm ơn nhé.
```

Vấn đề ở đây là **Hỗ Trợ** có thể đang ngoại tuyến hoặc không có trên kênh khi **Người Dùng** nhắn tin đầu tiên, và mất `5 tiếng` để thấy tin đó. Nhưng họ không biết **Người Dùng** làm gì với dự án mà làm cho tính năng `không hoạt động`, nên họ đoán **Người Dùng** đã làm gì sai ở tệp cài đặt và yêu cầu **Người Dùng** gửi họ tệp tin đó. Rồi họ phải chờ thêm `1 tiếng` nữa để nhận được tệp tin, chỉ để thấy rằng **Người Dùng** quên bật tính năng đó. Tóm lại, **Hỗ Trợ** mất `6 hours` chỉ để hiểu vấn đề của **Người Dùng**.

# Hãy

```txt
00:00 - Người Dùng: Xin chào. Tính năng này không hoạt động đối với tôi. Có cách nào để sửa không?
00:30 - Người Dùng: Đây là tệp cài đặt của tôi: config.yml, features.yml, data.json
05:00 - Hỗ Trợ: Bạn quên chỉnh `enabled` thành `true` ở tệp `config.yml`
06:00 - Người Dùng: Phải rồi ha. Tôi quên. Hoạt động được rồi. Cảm ơn nhé.
```

Giờ **Hỗ Trợ** chỉ mất `5 tiếng` để hiểu và đưa ra giải pháp cho **Người Dùng**. Thời gian đã không bị lãng phí.

# Thay thế

Có vài trường hợp mà **Người Dùng** không biết gửi tệp gì cho **Hỗ Trợ** bởi vì có quá nhiều tệp tin.

Đây là một số giải pháp để giải quyết vấn đề này triệt để:

* **Gửi Toàn Bộ**: Gửi hết tệp cài đặt, tệp báo cáo, tệp ghi hoạt động, ảnh chụp, video, hướng dẫn, v.v. Bất kì thứ gì liên quan đến dự án.
  * Nó có thể là một giải pháp tồi do **Người Dùng** phải gửi thông tin nhạy cảm như một phần của báo cáo.
  * Vì lí do bảo mật, đây chắc chắn là giải pháp nguy hiểm cho các dự án có cung cấp kênh hỗ trợ cho cộng đồng (diễn đàn, JIRA, Fanpage, v.v.). Tuy nhiên, nếu dự án của bạn không chứa hay lưu bất kì thông tin nhạy cảm, giải pháp này sẽ ổn.
* **Mẫu / Hướng Dẫn Báo Cáo**: Cung cấp các hình thức mẫu / đơn báo cáo hoặc tạo hướng dẫn để chỉ cho **Người Dùng** cách báo cáo.
  * Đây là giải pháp phổ biến hơn ở các dự án cộng đồng.
  * **Hỗ Trợ** có thể xác định tệp tin mà **Người Dùng** phải cung cấp, và có thể tránh thông tin nhạy cảm.
  * **Hỗ Trợ** có thể chỉ cho **Người Dùng** cách để xóa các thông tin nhạy cảm trong trường hợp một số phần của thông tin đó cần thiết để tìm hiểu nguyên nhân.

# Liên quan

* [no hello](https://nohello.net/)
* [The XY Problem](https://xyproblem.info/)