# Metadata Management System (NBTC)

ฟอร์มลงทะเบียนรายการบัญชีข้อมูล เป็นเว็บแบบ static ไฟล์เดียว (`index.html`) ไม่ต้อง build เปิดใช้งานผ่าน GitHub Pages ได้ทันที

## เปิดใช้งานบน GitHub Pages
1. สร้าง repository ใหม่บน GitHub แล้วอัปโหลดไฟล์ `index.html`, `.nojekyll` และ `README.md` ไว้ที่ root
2. ไปที่ **Settings → Pages**
3. ที่ **Build and deployment** เลือก **Source: Deploy from a branch**
4. เลือก branch `main` และโฟลเดอร์ `/ (root)` แล้วกด **Save**
5. รอ 1-2 นาที เว็บจะอยู่ที่ `https://<ชื่อผู้ใช้>.github.io/<ชื่อ-repo>/`

## ตั้งค่า Webhook
แก้บรรทัด `const WEBHOOK_URL = ...` ใน `index.html` เป็น URL จริง (ต้องเป็น `https://`)
ถ้ายังไม่แก้ เมื่อกดบันทึกจะขึ้นข้อความ "ยังไม่สามารถส่งข้อมูลได้"

Webhook ต้องเปิด CORS ให้โดเมน `https://<ชื่อผู้ใช้>.github.io` และรองรับ request แบบ `POST` ที่ `Content-Type: application/json` (ถ้าใช้ n8n ให้ตั้ง Allowed Origins ที่ Webhook node)

## ข้อควรระวัง
- GitHub Pages เป็นเว็บสาธารณะ ใครมี URL ก็เปิดได้ และ `WEBHOOK_URL` มองเห็นได้จากซอร์สโค้ด หน้า "Internal Use Only" จึงไม่ได้ถูกจำกัดสิทธิ์จริง ควรให้ webhook มีการยืนยันตัวตนหรือจำกัดโดเมน หรือใช้ repository แบบ private ร่วมกับ GitHub Enterprise Cloud
- ไฟล์นี้โหลด Tailwind CSS (CDN) และฟอนต์ Sarabun (Google Fonts) ต้องเชื่อมต่ออินเทอร์เน็ต ถ้าใช้ในเครือข่ายปิดควรโฮสต์ไฟล์เหล่านี้เอง
- ไฟล์ตั้งค่า `noindex` ไว้เพื่อไม่ให้เครื่องมือค้นหาจัดทำดัชนี

## ทดสอบในเครื่อง
เปิด `index.html` ในเบราว์เซอร์ได้โดยตรง หรือรัน `python3 -m http.server 8000` แล้วเปิด http://localhost:8000
