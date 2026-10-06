# KruBlackAI Auto Gen Pilot

ระบบสร้างวิดีโออัตโนมัติครบวงจรสำหรับครีเอเตอร์ นักการตลาด ร้านค้าออนไลน์ และทีมผลิตสื่อ

> **KruBlackAI Auto Gen Pilot — พัฒนาโดย นายธวัชชัย แก่นจักร์**  
> **Copyright © 2026 นายธวัชชัย แก่นจักร์ — สงวนลิขสิทธิ์ทั้งหมด**

## สิ่งที่มีในเวอร์ชันนี้

- แดชบอร์ด Creative Control Center พร้อมสถิติและความคืบหน้า pipeline
- สร้างโปรเจกต์: ชื่อเรื่อง, รายละเอียด, ประเภทผลงาน 6 แบบ, อัตราส่วน 9:16 / 16:9 และสไตล์ภาพยนตร์
- Workflow 6 ขั้น: วิเคราะห์เนื้อหา → บทพูด → สตอรี่บอร์ด → พร้อมป์ AI → สร้างวิดีโอ → ตัดต่อ/ส่งออก
- แก้ไขบทพูดรายฉาก, อารมณ์, ชื่อฉาก, คำอธิบายช็อต และพร้อมป์ได้ภายหลัง
- มุมมอง storyboard พร้อม reference-image placeholder, render queue และ timeline preview
- สร้างเวอร์ชันใหม่โดยไม่ทับเวอร์ชันเดิม (UI flow พร้อมต่อยอด persistence)
- หน้าจัดการโปรเจกต์, การตั้งค่าผู้ให้บริการ/การส่งออก และคู่มือใน sidebar
- Responsive layout สำหรับมือถือ แท็บเล็ต และเดสก์ท็อป
- route manifest ที่ `public/manus-routes.json`

## เริ่มต้นใช้งาน

ต้องใช้ Node.js 18+ และ npm

```bash
npm install
npm run dev
# เปิด http://localhost:5173
```

สร้าง production build:

```bash
npm run build
npm run preview
```

## เชื่อมต่อบริการจริง

UI ในรอบนี้ทำงานด้วย demo data และ local state เพื่อให้ทดลอง flow ได้ทันที การต่อ backend ควรเพิ่ม API adapter แยกตาม provider โดยไม่ผูกกับ UI:

- วิเคราะห์ / สร้างบท / พร้อมป์: endpoint ที่คืน JSON ตาม P1–P5
- เสียงพูด: endpoint ตาม P6 พร้อม `voice_text`, `voice_character`, `emotion`, `speed`, `pitch`
- วิดีโอ: queue worker ตามสถานะ `รอ → กำลังสร้าง → เสร็จ → มีปัญหา`
- ตัดต่อ: FFmpeg worker สำหรับรวมคลิป, voice, music, SFX และท้ายเครดิต
- จัดเก็บโครงการ, scene, prompt, clip, voice และ export เป็น JSON/ฐานข้อมูล

อย่าเก็บ API key ในฝั่ง client ให้ใช้ environment variables ฝั่ง server เช่น `LLM_API_KEY`, `VIDEO_PROVIDER_API_KEY`, `TTS_API_KEY`, `STORAGE_BUCKET` และ `DATABASE_URL`

## โครงสร้างหลัก

```text
src/main.jsx       # React UI, state และ workflow screens
src/styles.css     # visual system และ responsive layout
public/manus-routes.json
index.html
```

© 2026 นายธวัชชัย แก่นจักร์ — KruBlackAI Auto Gen Pilot — สงวนลิขสิทธิ์ทั้งหมด
