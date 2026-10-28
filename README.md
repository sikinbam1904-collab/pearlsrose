# วังหลัง: ลิขิตหงส์เหนือบัลลังก์

เกม Visual Novel ภาษาไทยแนวจีนโบราณ สืบสวนคดีเงินหลวง การเมือง และความสัมพันธ์ สร้างด้วย HTML/CSS/Vanilla JavaScript และ JSON สำหรับเผยแพร่เป็น Static Site บน GitHub Pages

## สถานะของเวอร์ชัน

- มีข้อมูลเนื้อเรื่อง **200 ตอนจริง (20 บท × 10 ตอน)**, 26 ตัวละคร, 25 ฉาก SVG และ 5 ตอนจบ
- เนื้อเรื่องเป็นฉบับเล่นได้แบบกระชับ ไม่ถึงเป้าหมาย 500–900 คำต่อ episode ทุกตอน จึงยังไม่ใช่ฉบับนิยายเกมเต็มความยาว
- ภาพตัวละครและฉากเป็นภาพประกอบ SVG แบบกราฟิกที่สร้างขึ้นสำหรับโปรเจกต์ ไม่ใช่ภาพวาดกึ่งสมจริง/PNG โปร่งใส
- ยังไม่มีไฟล์เสียงประกอบจริง; ตั้งค่าเสียงเป็นเพียงส่วน UI/placeholder และเกมไม่จำเป็นต้องมีเสียงเพื่อเล่น
- เซฟใน localStorage, ส่งออก/นำเข้าไฟล์เซฟ, คลังหลักฐาน, สารบัญตัวละคร, ประวัติการตัดสินใจ, เลือกบทและโหมดทดสอบมีให้ใช้งาน

## วิธีเล่น

1. เปิดเว็บไซต์และเลือก **เริ่มเรื่องใหม่** หรือ **เล่นต่อ**
2. อ่านคำบรรยายและบทสนทนา กด **ต่อไป** จนถึงหน้าตัวเลือก
3. เลือกทางเลือกที่ต้องการ ผลคะแนนและธงเส้นทางจะบันทึกไว้ในเครื่อง
4. ใช้ปุ่ม **คลังหลักฐาน**, **ตัวละคร** และ **ประวัติข้อความ** ระหว่างเล่น
5. ปิดเว็บแล้วกลับมาใหม่ได้ผ่านปุ่ม **เล่นต่อ** บนเบราว์เซอร์/อุปกรณ์เดิม
6. ในหน้า **ตั้งค่า** สามารถส่งออกเซฟเป็น JSON หรือนำเข้าเซฟเดิมได้

## ทดสอบในเครื่อง

`story.json` ถูกโหลดด้วย `fetch()` จึงควรเปิดผ่าน HTTP server แทนการดับเบิลคลิก `index.html`:

```bash
python3 -m http.server 8000
```

จากนั้นเปิด `http://localhost:8000` ในเบราว์เซอร์

ตรวจสอบโครงเรื่องและไฟล์อ้างอิงด้วย:

```bash
node tools/validate_story.js
node --check game.js
```

## เผยแพร่ผ่าน GitHub Pages

1. ดาวน์โหลด ZIP และแตกไฟล์
2. สร้าง repository ใหม่บน GitHub
3. อัปโหลด **เนื้อหาภายในโฟลเดอร์ `wanglang-palace-game`** ไปไว้ที่ root ของ repository ให้ `index.html` อยู่ระดับบนสุด
4. เปิด **Settings** ของ repository
5. เลือก **Pages**
6. ใน Build and deployment เลือก **Deploy from a branch**
7. เลือก branch `main` และโฟลเดอร์ `/(root)`
8. กด **Save** แล้วรอการเผยแพร่
9. เปิด URL ที่ GitHub Pages แสดงและทดสอบเริ่มเกม/บันทึก/โหลด/ตัวเลือก
10. เมื่อแก้ไขไฟล์ ให้อัปโหลดทับและรอ deployment รอบใหม่

## แก้ปัญหา

- **หน้าเว็บว่าง:** เปิด Developer Console ดู error; ตรวจ `game.js` และ JSON
- **JSON โหลดไม่สำเร็จ:** ตรวจว่า `story.json`, `characters.json`, `chapters.json` อยู่ root และเปิดผ่าน HTTP/HTTPS ไม่ใช่ `file://`
- **ภาพไม่แสดง:** ตรวจชื่อไฟล์ตัวพิมพ์เล็ก/ใหญ่และ path ใน `characters.json`/scene catalog; เกมมี fallback บางส่วนเมื่อฉากไม่พบ
- **CSS ไม่ทำงาน:** ตรวจว่า `style.css` อยู่ root และ link เป็น relative path
- **เซฟไม่ถูกบันทึก:** ตรวจโหมด Private Browsing/การตั้งค่า storage; ส่งออกเซฟจากหน้า Settings เป็นทางสำรอง
- **ตัวเลือกไม่ไปต่อ:** ต้องอ่านข้อความในฉากจนถึงตัวเลือก; ตัวเลือกที่ถูกล็อกแสดงเหตุผลเบื้องต้น
- **GitHub Pages 404:** ตรวจ Settings → Pages, branch `main`, `/(root)` และให้ `index.html` อยู่ root
- **ภาษาไทยผิดเพี้ยน:** ตรวจ `<meta charset="utf-8">`; ฟอนต์ภายนอกเป็น optional และมี fallback

## วิธีปรับแต่ง

- **เปลี่ยนภาพตัวละคร:** วางไฟล์ SVG/PNG ใหม่ใน `assets/characters/` แล้วแก้ `portrait` ใน `characters.json` ให้ตรง path
- **เปลี่ยนฉากหลัง:** วางภาพใน `assets/scenes/`, เพิ่มรายการใน `assets/scenes/catalog.json`, แล้วใช้ `background` ID ใน `story.json`
- **แก้เนื้อเรื่อง:** แก้ `narration`, `dialogue`, `title`, `choices`, `evidenceGained` ใน `story.json` โดยคง ID และรูปแบบข้อมูล
- **เพิ่มตอน:** เพิ่ม episode พร้อม ID ที่ไม่ซ้ำ ปรับ `chapters.json` และปลายทาง `next`/`choices` แล้วรัน validator
- **เพิ่มตัวละคร:** เพิ่ม record ใน `characters.json`, เพิ่มภาพใน assets และใช้ ID เดียวกันใน `story.json`
- **เพิ่มตอนจบ:** เพิ่มรายการใน `endings` ของ `story.json` แล้วเพิ่มตัวเลือกปลายทาง `ENDING_...` ในตอนสุดท้าย

## ไฟล์หลัก

- `index.html` — หน้าเว็บไซต์
- `style.css` — UI และ responsive layout
- `game.js` — engine, choices, save/load, journal, character index, endings
- `story.json` — 200 ตอน, 5 endings และ evidence catalog
- `characters.json` — 26 ตัวละคร
- `chapters.json` — 20 บท
- `STORY_BIBLE.md`, `STORY_GUIDE.md` — worldbuilding และ continuity
- `ASSET_GUIDE.md` — แหล่งที่มาและวิธีเปลี่ยน assets
- `TEST_REPORT.md` — ผลตรวจสอบที่รันจริง

## เครดิต

เนื้อเรื่อง โค้ด และ SVG ที่อยู่ในแพ็กเกจนี้สร้างขึ้นสำหรับโปรเจกต์นี้ ไม่มีการนำภาพบุคคลหรือไฟล์เสียงจากแหล่งภายนอกมาใช้ ฟอนต์ Noto Serif Thai ถูกเรียกจาก Google Fonts แบบ optional; หากไม่โหลดจะใช้ fallback serif ของระบบ
