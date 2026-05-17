# คู่มือ Deploy ขึ้น Vercel ผ่าน GitHub

ทำตามขั้นตอน 3 ส่วนนี้ ใช้เวลาไม่เกิน 10 นาที

---

## ส่วนที่ 1: เตรียม Git ในเครื่อง

ตรวจว่ามี Git ก่อน:

```powershell
git --version
```

ถ้ายังไม่มี ติดตั้งจาก https://git-scm.com/download/win แล้วเปิด terminal ใหม่

ตั้งชื่อ/อีเมลให้ Git (ครั้งเดียวพอ ข้ามได้ถ้าตั้งแล้ว):

```powershell
git config --global user.name "ชื่อคุณ"
git config --global user.email "email@example.com"
```

ใน folder โปรเจกต์ ให้รัน:

```powershell
git init
git add .
git commit -m "Initial commit: ACSC Detective Check List"
```

---

## ส่วนที่ 2: สร้าง Repo บน GitHub แล้ว push

### วิธี A — ใช้ GitHub CLI (เร็วที่สุด)

ติดตั้ง GitHub CLI: https://cli.github.com/ แล้วรัน:

```powershell
gh auth login
gh repo create acsc-checklist --public --source=. --remote=origin --push
```

เสร็จ — repo ขึ้น GitHub แล้ว ข้ามไปส่วนที่ 3

### วิธี B — ผ่านเว็บ GitHub

1. เข้า https://github.com/new
2. Repository name: `acsc-checklist` (หรือชื่อที่ต้องการ)
3. เลือก **Public** หรือ **Private** ตามต้องการ
4. **อย่าติ๊ก** "Add a README" / .gitignore / license (เรามีอยู่แล้ว)
5. กด **Create repository**
6. หน้าถัดไปจะเห็นคำสั่ง copy มาวางใน terminal:

```powershell
git remote add origin https://github.com/<your-username>/acsc-checklist.git
git branch -M main
git push -u origin main
```

ครั้งแรก GitHub จะถามให้ login ผ่าน browser หรือใช้ Personal Access Token (https://github.com/settings/tokens)

---

## ส่วนที่ 3: Deploy บน Vercel

### วิธี A — ผ่านเว็บ Vercel (แนะนำ)

1. เข้า https://vercel.com/new
2. กด **Import Git Repository** เลือก repo `acsc-checklist`
   - ถ้าเป็นครั้งแรก จะต้องอนุญาตให้ Vercel เข้าถึง GitHub ของคุณ
3. ตั้งค่า:
   - **Project Name**: ตามต้องการ (จะกลายเป็น URL เช่น `acsc-checklist.vercel.app`)
   - **Framework Preset**: Other
   - **Root Directory**: `./` (default)
   - **Build Command**: เว้นว่าง
   - **Output Directory**: เว้นว่าง (หรือใส่ `.`)
   - **Install Command**: เว้นว่าง
4. กด **Deploy**
5. รอประมาณ 30 วินาที จะได้ URL ใช้งานทันที เช่น `https://acsc-checklist.vercel.app`

### วิธี B — Vercel CLI

```powershell
npm i -g vercel
vercel login
vercel --prod
```

ตอบคำถาม:
- Set up and deploy? **Y**
- Which scope? เลือก account ของคุณ
- Link to existing project? **N**
- Project name? `acsc-checklist`
- Directory? `./`
- Override settings? **N**

จบ — จะได้ URL production มา

---

## หลัง Deploy

### Custom Domain (ถ้ามี)

1. ใน Vercel project → **Settings → Domains**
2. ใส่ domain ของคุณ เช่น `checklist.yourdomain.com`
3. ทำตามขั้นตอนตั้ง DNS (CNAME) ที่ผู้ให้บริการ domain

### อัปเดตเว็บ

แค่แก้ไฟล์ → push ขึ้น GitHub Vercel จะ auto-deploy ให้:

```powershell
git add .
git commit -m "อัปเดตเคส C01"
git push
```

ภายใน 1 นาที เว็บจะอัปเดต

### ส่งให้คนอื่นใช้

- ส่ง URL Vercel ให้ได้เลย
- **ข้อมูลเก็บใน localStorage ของเบราว์เซอร์แต่ละคน** ใครเปิดในเครื่องตัวเองจะมีข้อมูลของตัวเอง ไม่ปนกัน
- ถ้าอยากแชร์ข้อมูลระหว่างทีม ใช้ปุ่ม **Export JSON** ส่งไฟล์ให้กัน แล้วฝั่งรับใช้ **Import** เข้ามา

---

## Troubleshooting

**Push แล้วเจอ "Permission denied"**
ใช้ Personal Access Token (Settings → Developer settings → Personal access tokens) แทน password ตอน push

**Vercel deploy แล้วเปิดแล้วขึ้น 404**
- ตรวจว่ามีไฟล์ `index.html` อยู่ที่ root
- ใน project settings ตั้ง Output Directory เป็น `.` หรือเว้นว่าง

**ฟอนต์ไทยไม่โหลด**
ตรวจว่าเครื่องของผู้ใช้เชื่อมเน็ตได้ ฟอนต์โหลดจาก Google Fonts ระหว่างใช้งาน

**ข้อมูลหายเมื่อเปลี่ยนเครื่อง/เบราว์เซอร์**
นี่เป็นพฤติกรรมปกติของ localStorage ใช้ Export/Import เพื่อย้ายข้อมูล หรือถ้าต้องการ sync ข้ามเครื่อง ต้องเพิ่ม backend (เช่น Supabase / Firebase)

---

## ต้องการเก็บข้อมูลแบบ shared ระหว่างทีม?

ถ้าในอนาคตอยากให้ทีมหลายคนเห็นข้อมูลเดียวกัน บอกผมได้ ผมต่อ backend ให้ได้หลายแบบ:

- **Supabase** (ฟรี Postgres + Auth) เพิ่ม cloud sync ใช้เวลาไม่นาน
- **Vercel KV / Postgres** ใช้คู่กับ Vercel ตรงๆ
- **Firebase Firestore** เหมาะถ้าต้องการ realtime
