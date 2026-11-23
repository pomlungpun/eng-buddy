# Eng Buddy · เว็บฝึกภาษาอังกฤษ + ล็อกอินด้วย Google

เว็บแอปฝึกภาษาอังกฤษ (คำศัพท์ 3,596 คำ A1–C1, 12 Tenses, Reading, Listening, Writing, Speaking และข้อสอบวัดระดับ)
ทุกคนล็อกอินด้วยบัญชี Google (Gmail) ของตัวเอง ความคืบหน้าเก็บบน Firebase แยกเป็นของแต่ละคน และเข้าจากเครื่องไหนก็ได้

ใช้เวลาตั้งค่าประมาณ 15–20 นาที ทุกอย่างใช้แพ็กเกจฟรี

---

## ไฟล์ในโฟลเดอร์นี้

| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `index.html` | ตัวแอป |
| `data.js`, `data2.js`, `vocab.json` | บทเรียน ข้อสอบ และคำศัพท์ |
| `firebase-config.js` | **ต้องแก้** ใส่ค่าจาก Firebase (ขั้นตอนที่ 2) |
| `firestore.rules` | กฎความปลอดภัยของฐานข้อมูล (ขั้นตอนที่ 4) |
| `.nojekyll` | ไฟล์ว่าง ช่วยให้ GitHub Pages แสดงเว็บตรงตามไฟล์ |

---

## ขั้นตอนที่ 1 · สร้างโปรเจกต์ Firebase

1. เข้า https://console.firebase.google.com แล้วล็อกอินด้วย Gmail ของคุณ
2. กด **Create a project / เพิ่มโปรเจกต์** ตั้งชื่อ เช่น `eng-buddy`
3. ขั้นตอน Google Analytics ปิดไว้ได้ แล้วกดสร้างโปรเจกต์

## ขั้นตอนที่ 2 · เพิ่มเว็บแอปและคัดลอกค่า config

1. ในหน้าโปรเจกต์ กดไอคอน **`</>`** (Web) เพื่อเพิ่มแอป
2. ตั้งชื่อเล่นแอป เช่น `eng-buddy-web` **ไม่ต้อง**ติ๊ก Firebase Hosting แล้วกด Register
3. จะเห็นโค้ดที่มี `const firebaseConfig = { apiKey: "...", authDomain: "...", ... }`
4. เปิดไฟล์ `firebase-config.js` ด้วย Notepad แล้วคัดลอกค่าทั้ง 6 ช่องไปใส่ให้ครบ เช่น

```js
window.FIREBASE_CONFIG = {
  apiKey: "AIzaSy...",
  authDomain: "eng-buddy-12345.firebaseapp.com",
  projectId: "eng-buddy-12345",
  storageBucket: "eng-buddy-12345.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abc123"
};
```

> ค่า `apiKey` ของ Firebase เปิดเผยในเว็บได้ตามปกติ ความปลอดภัยมาจากกฎในขั้นตอนที่ 4

## ขั้นตอนที่ 3 · เปิดการล็อกอินด้วย Google

1. เมนูซ้าย **Build › Authentication** แล้วกด **Get started**
2. แท็บ **Sign-in method** เลือก **Google** แล้วเปิด **Enable**
3. เลือกอีเมลสำหรับ support (อีเมลของคุณ) แล้วกด **Save**

## ขั้นตอนที่ 4 · สร้างฐานข้อมูล Firestore

1. เมนูซ้าย **Build › Firestore Database** แล้วกด **Create database**
2. เลือก location ใกล้ไทย เช่น `asia-southeast1 (Singapore)`
3. เลือก **Start in production mode** แล้วกดสร้าง
4. ไปที่แท็บ **Rules** ลบของเดิม แล้ววางเนื้อหาจากไฟล์ `firestore.rules` ทั้งหมด จากนั้นกด **Publish**

## ขั้นตอนที่ 5 · เอาเว็บขึ้น GitHub Pages

1. เข้า https://github.com แล้วล็อกอิน (ยังไม่มีบัญชีก็สมัครฟรี)
2. กด **+ › New repository** ตั้งชื่อ `eng-buddy` เลือก **Public** แล้วกด **Create repository**
3. ในหน้า repo กดลิงก์ **uploading an existing file**
4. ลากไฟล์ **ทั้งหมด** ในโฟลเดอร์นี้ไปวาง (รวม `firebase-config.js` ที่แก้แล้ว) แล้วกด **Commit changes**
   - ถ้า Windows ซ่อนไฟล์ `.nojekyll` ไว้ ไม่ต้องกังวล เว็บยังใช้งานได้
5. ไปที่ **Settings › Pages**
6. ในหัวข้อ **Build and deployment** ตั้งค่า Source เป็น **Deploy from a branch** แล้วเลือก Branch เป็น **main** และโฟลเดอร์ **/ (root)** จากนั้นกด **Save**
7. รอ 1–3 นาที แล้วรีเฟรชหน้านั้น จะเห็นลิงก์เว็บ เช่น `https://ชื่อผู้ใช้.github.io/eng-buddy/`

## ขั้นตอนที่ 6 · อนุญาตโดเมนของเว็บใน Firebase

1. กลับไปที่ Firebase › **Authentication › Settings › Authorized domains**
2. กด **Add domain** แล้วใส่ `ชื่อผู้ใช้.github.io` ใส่แค่ส่วนนี้ ไม่ต้องใส่ `https://` และไม่ต้องใส่ `/eng-buddy`
3. กด **Add**

## ขั้นตอนที่ 7 · ทดลองใช้

เปิดลิงก์เว็บ แล้วกด **เข้าสู่ระบบด้วย Google** ถ้าเข้าได้และเห็นชื่อคุณมุมซ้ายล่าง แสดงว่าตั้งค่าเสร็จแล้ว ส่งลิงก์ให้เพื่อนใช้ได้เลย ทุกคนจะมีข้อมูลแยกของตัวเอง

---

## ฟีเจอร์ AI ในเวอร์ชันเว็บ

เวอร์ชันนี้ไม่ได้เปิดใน Claude จึงใช้ “Claude ในแอปนี้” ไม่ได้ ให้แต่ละคนไปที่เมนู **ตั้งค่า AI** แล้วเลือกผู้ให้บริการ (OpenAI, Anthropic, Gemini, OpenRouter หรือ OpenAI-compatible) พร้อมใส่ API key ของตัวเอง
API key เก็บไว้ในเบราว์เซอร์ของเครื่องนั้นเท่านั้น ไม่ได้อัปโหลดขึ้น Firebase ส่วนบทเรียน คำศัพท์ แบบฝึกหัด และข้อสอบ Core Skills ใช้ได้โดยไม่ต้องมี AI

ไมโครโฟนสำหรับฝึกพูดใช้ได้บน Chrome และ Edge (เบราว์เซอร์จะขออนุญาตครั้งแรก)

## ถ้ามีปัญหา

| อาการ | วิธีแก้ |
|---|---|
| ขึ้นว่า `auth/unauthorized-domain` | ยังไม่ได้ทำขั้นตอนที่ 6 หรือพิมพ์โดเมนผิด |
| กดปุ่ม Google แล้วไม่มีอะไรเกิดขึ้น | เบราว์เซอร์บล็อกป๊อปอัป ให้อนุญาตป๊อปอัปสำหรับเว็บนี้ แล้วลองใหม่ |
| ขึ้นหน้าเลือกโปรไฟล์ในเครื่องแทนปุ่ม Google | ใส่ค่าใน `firebase-config.js` ไม่ครบ หรือยังไม่ได้อัปโหลดไฟล์ที่แก้แล้ว |
| ล็อกอินได้แต่ความคืบหน้าไม่ถูกบันทึก | ยังไม่ได้วาง Rules และกด Publish ในขั้นตอนที่ 4 |
| เปิดไฟล์ `index.html` ในเครื่องโดยตรงแล้วล็อกอินไม่ได้ | ปกติ Google ไม่ให้ล็อกอินจากไฟล์ในเครื่อง ต้องเปิดผ่านลิงก์ GitHub Pages |

## แก้ไข/อัปเดตเว็บภายหลัง

ใน GitHub repo กด **Add file › Upload files** แล้วอัปโหลดไฟล์ใหม่ทับไฟล์เดิม เว็บจะอัปเดตเองภายใน 1–3 นาที
