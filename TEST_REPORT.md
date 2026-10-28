# TEST REPORT

ทดสอบเมื่อ 2026-10-28 โดยรันคำสั่งใน working directory ของโปรเจกต์

| รายการ | สถานะ | หลักฐาน/หมายเหตุ |
|---|---|---|
| JSON story parse | PASS | `story.json` โหลดด้วย JSON parser ใน validator |
| จำนวนตอน 200 | PASS | พบ 200 episodes |
| 20 บท บทละ 10 ตอน | PASS | ตรวจจำนวนตอนในแต่ละบท |
| รหัสตอนซ้ำ | PASS | ตรวจ ID episode และรูปแบบรหัส |
| ตัวเลือก/ปลายทาง | PASS | ตรวจว่าปลายทางที่ระบุอยู่ใน episode/endings |
| ตัวละครที่อ้างถึง | PASS | ตรวจ ID ใน `characters.json` |
| ฉากและไฟล์ภาพ | PASS | ตรวจ scene IDs และไฟล์ SVG ที่มีอยู่จริง |
| ตอนจบอย่างน้อย 5 แบบ | PASS | พบ 5 endings พร้อม title/text/condition |
| JavaScript syntax | PASS | `node --check game.js` |
| HTTP static-server smoke test | PASS | เปิด `index.html`, CSS, JS และ JSON ผ่าน local HTTP server ได้ status 200; JSON parse ได้ |
| ZIP integrity | PASS | `zipfile.testzip()` ไม่พบไฟล์เสีย และ ZIP มีโฟลเดอร์โปรเจกต์ชั้นเดียว |
| Browser runtime / UI interactions | NOT TESTED | ไม่มีการรันทดสอบ browser automation ในขั้นตอนนี้ |
| iOS Safari / iPadOS / Android จริง | NOT TESTED | ต้องทดสอบบนอุปกรณ์จริงก่อนเผยแพร่สาธารณะ |
| เซฟ/โหลด/รีเฟรช/เริ่มใหม่ end-to-end | NOT TESTED | มี implementation แต่ยังไม่ได้ทำ automated browser test |
| เส้นทางทั้ง 5 แบบครบตั้งแต่ต้นจนจบ | NOT TESTED | validator ตรวจโครงสร้าง ไม่ได้จำลอง playthrough 200 ตอน |
| ความยาวนิยาย 500–900 คำต่อ episode | NOT PASS / OUT OF SCOPE FOR THIS BUILD | ตอนมีเนื้อหากระชับกว่าข้อกำหนด; ต้องขยายเป็นฉบับเต็ม |

## ผล validator

```json
{
  "episodes": 200,
  "chapters": 20,
  "characters": 26,
  "sceneAssets": 25,
  "endings": 5,
  "errors": [],
  "warnings": []
}
```

## ข้อจำกัดที่ทราบ

1. เนื้อหา 200 ตอนมี beat เฉพาะและโครงเรื่องต่อเนื่อง แต่ยังสั้นกว่าเป้าหมาย 500–900 คำ/ตอนมาก
2. ภาพเป็น SVG กราฟิกแบบ stylized ไม่ใช่ภาพวาดกึ่งสมจริง/PNG โปร่งใสตามสเปกภาพเต็ม
3. ไม่มีเสียงประกอบจริง
4. ระบบความสัมพันธ์และตัวเลือกมีผลต่อค่าสถานะ/flags และตัวเลือกตอนจบ แต่ยังไม่ได้มี branching scenes จำนวนมากหรือ route-specific dialogue ครอบคลุมทุกตัวละคร
5. ยังไม่ได้ทดสอบ browser automation หรืออุปกรณ์จริง
