# Personal Web V3 — Admin CMS

## Mục tiêu
Giữ giao diện/ảnh hiện tại, nhưng thêm CMS quản trị: đăng nhập, đăng xuất, tạo bài viết, upload ảnh, quản lý gallery/project.

## Kiến trúc
- Astro: build site tĩnh.
- Decap CMS: giao diện `/admin/`, editor, upload media, commit nội dung vào GitHub.
- Netlify Identity + Git Gateway: xác thực admin mà không phải tự xây hệ thống mật khẩu.
- Firebase Realtime Database: giữ reaction/comment của bài viết.
- Netlify: hosting + build tự động.

## 1. Tạo GitHub repository
Đưa toàn bộ project lên một repo GitHub mới, branch `main`. Không commit password/token bí mật.

## 2. Chạy local
```bash
npm install
npm run dev
```
Mở `http://localhost:4321`.

## 3. Deploy Netlify
1. Đăng nhập Netlify.
2. Add new project → Import existing project → chọn GitHub repo.
3. Build command: `npm run build`.
4. Publish directory: `dist`.
5. Deploy.

## 4. Bật đăng nhập quản trị
Trong Netlify site:
- Project configuration → Access & security → Visitor access / Identity (tên menu có thể thay đổi theo UI).
- Bật Identity.
- Registration: chọn **Invite only**.
- Bật Git Gateway.
- Mời email quản trị của bạn.

Sau đó mở:
`https://TEN-SITE.netlify.app/admin/`

Đăng nhập → tạo bài viết → upload ảnh → Publish. Decap sẽ commit file vào GitHub; Netlify tự build/deploy site mới.

## 5. Sửa 2 placeholder
Trong `admin/config.yml` và `astro.config.mjs`, thay `YOUR-SITE.netlify.app` bằng domain thật.

## 6. Firebase
Project Firebase hiện tại vẫn được dùng cho comment/reaction. Hãy cập nhật Realtime Database Rules bằng file `firebase.database.rules.json`.

## 7. GitHub Pages
Có sẵn `.github/workflows/deploy.yml` làm phương án dự phòng. Tuy nhiên CMS authentication/upload nên dùng Netlify vì Decap Git Gateway tích hợp trực tiếp với Netlify Identity.

## Luồng xuất bản
Admin → `/admin` → Login → Soạn bài → Upload ảnh → Publish → Commit GitHub → Netlify build → Website cập nhật.
