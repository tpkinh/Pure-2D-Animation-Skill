# Workflow Chuyển Ảnh Sang Style Lock

## Cách kích hoạt

Khi người dùng đính kèm ảnh và yêu cầu **“chạy workflow cho ảnh này”** (hoặc câu tương đương), thực hiện toàn bộ quy trình trong file này. Không cần hỏi lại các thông tin đã thấy rõ trong ảnh. Ảnh đính kèm là **edit target**; giữ chủ thể, nội dung và bố cục cốt lõi trừ khi người dùng yêu cầu thay đổi.

## Điều kiện bắt buộc

1. Đọc toàn bộ [IMAGE_STYLE_LOCK.md](IMAGE_STYLE_LOCK.md) trước khi soạn prompt hay tạo ảnh.
2. Dùng ảnh người dùng cung cấp làm ảnh tham chiếu/chỉnh sửa. Nếu ảnh chỉ có đường dẫn local, phải xem ảnh trước khi chỉnh sửa.
3. Không thay đổi hoặc ghi đè ảnh gốc.
4. Chỉ xuất kết quả đã qua kiểm tra style. Mọi file xuất cuối cùng lưu trong thư mục [`outputs`](outputs/).
5. Nếu chưa có thư mục `outputs/`, tạo thư mục đó trước khi lưu kết quả.
6. Không thể chuyển đạt chuẩn chỉ bằng đổi màu hoặc lọc ảnh: phải tái minh họa bằng công cụ tạo/chỉnh sửa ảnh để thay thế toàn bộ ngôn ngữ đồ họa không phù hợp.

## Luồng xử lý tự động

### 1. Đọc và phân tích ảnh đầu vào

Trích xuất ngắn gọn:

- Chủ thể, số lượng nhân vật và các đặc điểm nhận diện cần giữ.
- Hành động/cảm xúc, trang phục, đạo cụ và yếu tố kể chuyện.
- Bố cục, góc nhìn, tỉ lệ khung hình và lớp background.
- Các yếu tố cần chuyển đổi vì trái style lock: shading mềm, texture chân thực, gradient, blur, phối cảnh/camera, 3D hoặc bán hiện thực.

### 2. Chọn phạm vi bảo toàn

Giữ nguyên, theo thứ tự ưu tiên: chủ thể → nhận diện nhân vật → hành động/cảm xúc → trang phục/đạo cụ → bố cục → tỉ lệ ảnh.

Chuyển đổi: toàn bộ cách thể hiện hình ảnh sang 2D animation theo style lock. Không sao chép texture, hiệu ứng camera hoặc mức độ hiện thực từ ảnh nguồn.

### 3. Soạn prompt chỉnh sửa

Prompt phải bao gồm cả ba phần:

1. **Nội dung cần giữ:** mô tả chính xác các thành phần đã phân tích.
2. **Mục tiêu style:** line art sạch, màu phẳng, cel-shading cứng 1–2 cấp, background 2D cùng hệ đồ họa.
3. **Ràng buộc loại trừ:** toàn bộ các điều cấm trong `IMAGE_STYLE_LOCK.md`.

Luôn dùng khung prompt sau, thay phần trong ngoặc vuông:

```text
Use case: style-transfer
Asset type: final project illustration
Input image: edit target; preserve its [subject, identity, action, costume/props,
composition, and aspect ratio].
Primary request: redraw the supplied image as a pure 2D animation illustration.
Subject and composition: [mô tả ảnh đầu vào].
Style/medium: clean consistent outlines, readable silhouette, flat color shapes,
hard-edge 1–2 level cel shading, stylized 2D face, hair, skin, clothing, and props.
Scene/backdrop: [mô tả background] redrawn in the same 2D line-art system, palette,
and simplified detail level. Create depth only through layering, scale, composition,
and reduced detail in distant layers.
Constraints: preserve [các bất biến đã xác định]; redraw every visual element to comply
with IMAGE_STYLE_LOCK.md.
Avoid: 3D render, 2.5D, CGI, semi-realism, digital painting, soft airbrush,
gradient-heavy shading, realistic skin or material texture, pores, volumetric light,
god rays, bloom, lens flare, depth of field, bokeh, motion blur, photographic camera
effects, realistic background, and watermark.
```

### 4. Tạo ảnh và kiểm tra

1. Tạo một bản chuyển style bằng công cụ chỉnh sửa ảnh.
2. Kiểm tra bản tạo theo checklist bên dưới.
3. Nếu có lỗi, chỉ tạo lại với prompt sửa tập trung vào lỗi đó; luôn lặp lại các bất biến cần giữ.
4. Lặp tối đa 2 lần sửa sau bản đầu. Nếu vẫn chưa đạt, báo rõ lỗi còn lại và chờ chỉ đạo thay vì xuất một ảnh không đạt chuẩn.

### 5. Xuất file

- Lưu **chỉ bản đã duyệt** vào `outputs/`.
- Tên file: `<ten-anh-goc>-2d-animation.png`.
- Nếu tên đã tồn tại, dùng phiên bản tăng dần: `<ten-anh-goc>-2d-animation-v2.png`, `-v3.png`, ...
- Không ghi đè output cũ nếu người dùng không yêu cầu.
- Sau khi hoàn thành, báo đường dẫn file output và xác nhận ảnh đã qua checklist.

## Checklist duyệt bắt buộc

- [ ] Chủ thể, nhận diện, hành động, trang phục/đạo cụ và bố cục cốt lõi được bảo toàn.
- [ ] Silhouette và nét viền rõ, sạch, đồng nhất.
- [ ] Màu phẳng; cel-shading cứng, tối đa 1–2 cấp.
- [ ] Khuôn mặt, tóc, da, vải và đạo cụ đều có ngôn ngữ đồ họa 2D.
- [ ] Background là minh họa 2D cùng line art, palette và mức độ giản lược với nhân vật.
- [ ] Chiều sâu chỉ dùng bố cục, chồng lớp, tỷ lệ và giảm chi tiết ở lớp xa.
- [ ] Không có gradient mềm, airbrush, texture hiện thực, DOF, bokeh, blur, bloom, lens flare, god rays hoặc ánh sáng thể tích.
- [ ] Không có dấu hiệu 3D, CGI, 2.5D hoặc bán hiện thực.

## Prompt sửa lỗi

Khi kiểm tra thấy lỗi, nối **một** đoạn phù hợp bên dưới vào prompt trước đó:

```text
Remove all soft gradients, airbrushed modeling, and realistic texture. Use only flat
color regions and one or two clearly separated hard-edge cel-shadow shapes per form.
```

```text
Redraw the face, skin, clothing, and props as simplified 2D animation graphic shapes;
remove pores, material shine, tiny wrinkles, and photorealistic facial modeling.
```

```text
Replace the backdrop with a simplified 2D illustrated background using the same clean
outline weight and flat palette as the character; remove photographic depth and blur.
```
