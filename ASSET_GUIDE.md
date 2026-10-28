# ASSET GUIDE

## สถานะ assets

- `assets/characters/*.svg`: การ์ดตัวละครกราฟิกแบบ stylized SVG ที่สร้างขึ้นในโปรเจกต์ มีชื่อ/สีประจำตัวและภาพสัญลักษณ์ ไม่ใช่ภาพตัวละครกึ่งสมจริงหรือภาพ PNG โปร่งใส
- `assets/scenes/*.svg`: ฉากหลังเวกเตอร์ต้นฉบับ 25 ฉากในโทนจีนโบราณ ใช้เป็นภาพบรรยากาศเชิงกราฟิก ไม่ใช่ภาพวาดรายละเอียดระดับ cinematic realism
- `assets/scenes/catalog.json`: mapping scene ID ไปยัง path ที่เกมใช้
- `assets/audio/`, `assets/ui/`, `assets/icons/`, `assets/fonts/`: โฟลเดอร์เตรียมไว้ ยังไม่มีไฟล์เสียง/ฟอนต์/ไอคอนภายนอกที่อ้างสิทธิ์

## เปลี่ยนภาพตัวละคร

1. เพิ่มภาพใน `assets/characters/` เช่น `shen_yuening.png`
2. เปลี่ยน `portrait` ของตัวละครที่ตรงกันใน `characters.json`
3. ตรวจว่า path ใช้ `/` และตัวพิมพ์ตรงกันทุกตัว
4. รัน `node tools/validate_story.js`

## เปลี่ยนฉากหลัง

1. เพิ่มไฟล์ภาพใน `assets/scenes/`
2. เพิ่ม `{ "id": "scene_id", "name": "ชื่อฉาก", "path": "assets/scenes/scene_id.png" }` ใน `assets/scenes/catalog.json`
3. กำหนด `background: "scene_id"` ใน episode ที่ต้องการ
4. รัน validator

## เสียง

เวอร์ชันนี้ไม่มีไฟล์เสียงจริง จึงไม่กล่าวอ้างว่ามี BGM/SFX พร้อมใช้งาน หากเพิ่มเสียงในอนาคต ให้ใช้เฉพาะไฟล์ที่สร้างเองหรือมีใบอนุญาตชัดเจน และเพิ่มการจัดการ volume/mute จริงก่อนเปิดใช้ใน UI
