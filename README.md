# ACSC Detective Check List 2026 — Professional Edition

เว็บแอปสำหรับใช้ Checklist สืบสวนคดี 15 เคส 3 กลุ่ม (ออนไลน์/ฉ้อโกง, ทั่วไป, ร้ายแรง) พร้อมระบบบันทึก แก้ไข และส่งออกข้อมูล

> หมายเหตุ: เคสทั้งหมดเป็นตัวอย่างสมมติ ใช้เพื่อการฝึกอบรมเท่านั้น

## Features

- 15 เคสตัวอย่างพร้อม Scenario / Timeline / Evidence / Hypothesis / Action Log
- Checklist มาตรฐาน 10 ข้อ ติ๊กได้ พร้อมช่องบันทึกใต้แต่ละข้อ
- ทุกตารางแก้ไขได้ inline เพิ่ม/ลบแถวได้
- บันทึกอัตโนมัติลง `localStorage` ของเบราว์เซอร์
- Dashboard ภาพรวมความคืบหน้าทุกเคส
- ค้นหาเคสแบบ realtime
- Export/Import JSON (รายเคส และรวมทุกเคส)
- Export Action Log เป็น CSV (เปิดใน Excel ได้)
- โหมดสว่าง/มืด
- พิมพ์ / Save PDF ในรูปแบบที่จัดวางสวยงาม
- ใช้งานบนมือถือ/แท็บเล็ตได้

## Tech

- HTML + CSS + Vanilla JS ไฟล์เดียว
- ไม่ต้องติดตั้งอะไร ไม่มี build step ไม่มี backend
- ข้อมูลเก็บในเครื่องผู้ใช้ (localStorage) — แต่ละคนมีข้อมูลของตัวเอง

## Local

เปิดไฟล์ `index.html` ในเบราว์เซอร์ได้เลย หรือรันเซิร์ฟเวอร์ static เช่น

```bash
npx serve .
```

## Deploy

โปรเจกต์เป็น static site — รองรับ Vercel / Netlify / GitHub Pages / Cloudflare Pages ได้ทันที

### Vercel

1. push repo ขึ้น GitHub
2. ที่ Vercel เลือก **Add New → Project** แล้ว import repo
3. Framework Preset: **Other** (หรือ Static)
4. Build Command: เว้นว่าง / Output Directory: `.`
5. Deploy

ดูขั้นตอนละเอียดในไฟล์ [`DEPLOY.md`](DEPLOY.md)

## Keyboard Shortcuts

- `Ctrl/Cmd + K` โฟกัสช่องค้นหา
- `Ctrl/Cmd + P` พิมพ์ / Save PDF
- `Esc` ปิด sidebar (มือถือ)

## License

MIT — ใช้ส่วนตัว / องค์กรได้ตามต้องการ
