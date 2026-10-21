# Mhai - Portfolio

> ระบบจัดการและเผยแพร่ผลงานส่วนตัวสำหรับผู้ใช้หลายบัญชี (Multi-User Professional Portfolio Management System)

## ภาพรวมโครงการ

**Mhai - Portfolio** คือเว็บแอปพลิเคชันที่เปิดให้ผู้ใช้สมัครสมาชิกและสร้าง Portfolio ของตนเอง เพื่อรวบรวม จัดการ และเผยแพร่ผลงานทางวิชาชีพผ่านหน้าโปรไฟล์สาธารณะและลิงก์รายผลงาน โดยแต่ละบัญชีสามารถจัดการข้อมูลของตนเองได้เท่านั้น

ผู้เข้าชมสามารถเปิดดูผลงานที่เผยแพร่แล้วโดยไม่ต้องเข้าสู่ระบบ และ Search Engine สามารถค้นพบหน้า Portfolio สาธารณะได้ แต่ระบบจะไม่มี Public Feed, User Directory หรือระบบค้นหาผู้ใช้ภายในเว็บไซต์ใน MVP

### วัตถุประสงค์ของโครงการ

- พัฒนาระบบสมัครสมาชิก เข้าสู่ระบบ และจัดการสิทธิ์การเข้าถึงข้อมูลของแต่ละผู้ใช้
- ให้ผู้ใช้สร้าง แก้ไข ลบ และเผยแพร่ผลงานของตนเอง พร้อมรายละเอียด หมวดหมู่ เทคโนโลยี และรูปภาพประกอบ
- รองรับ Public Portfolio Profile และลิงก์แชร์ผลงาน โดยผู้ใช้สามารถตั้ง Custom URL ได้เมื่อพร้อม
- แสดงสถิติการเผยแพร่ผลงานและสัดส่วนหมวดหมู่ผ่าน Dashboard ส่วนตัว
- รองรับการแสดงผลหน้า Public Profile และ Public Project ให้ Search Engine ทำดัชนีได้

### สิ่งที่คาดหวังจากการพัฒนา

- เรียนรู้การพัฒนาเว็บแบบ Full Stack ด้วย Next.js และ NestJS
- เข้าใจการออกแบบ REST API การยืนยันตัวตน (Authentication) และการกำหนดสิทธิ์ (Authorization)
- ฝึกออกแบบและเชื่อมต่อฐานข้อมูลด้วย PostgreSQL และ Prisma ORM
- เรียนรู้การจัดการไฟล์รูปภาพ การจัดโครงสร้างระบบ และการแยกหน้าที่ของแต่ละส่วนให้ดูแลรักษาง่าย
- ฝึกใช้เครื่องมือสำหรับพัฒนา ทดสอบ และจัดการสภาพแวดล้อมของแอปพลิเคชัน

## Tech Stack

| ส่วนงาน | เทคโนโลยี | การใช้งานหลัก |
|---|---|---|
| Frontend | Next.js, daisyUI, Font Awesome, Chart.js | ส่วนติดต่อผู้ใช้ การแสดงผล และกราฟ Dashboard |
| Backend | NestJS, TypeScript, JWT, Argon2, Swagger | REST API, Authentication, Security และ API Documentation |
| Database | PostgreSQL, Prisma ORM | จัดเก็บข้อมูลและติดต่อฐานข้อมูล |
| Media Storage | Cloudinary | จัดเก็บ Avatar, Cover Image และ Project Gallery |
| Development Tools | Git, GitHub, Docker, Postman | Version Control, Environment และ API Testing |

## ฟีเจอร์หลักใน MVP

1. **Authentication:** สมัครสมาชิกและเข้าสู่ระบบด้วย Email/Password, Google หรือ Facebook
2. **Portfolio Management:** จัดการ Project พร้อมสถานะ Draft / Published, Category และ Technologies
3. **Profile & Sharing:** แสดงหน้า Public Profile และ Public Project พร้อม Temporary URL / Custom URL
4. **Media Management:** อัปโหลดภาพหน้าปกและ Gallery หลายรูปต่อ Project
5. **Dashboard:** ดูจำนวนผลงาน สถิติการเผยแพร่รายเดือน และสถิติหมวดหมู่
6. **SEO:** รองรับการทำดัชนีหน้า Public Profile และ Published Projects โดยไม่มี Public Feed หรือ User Search

### ตัวอย่างการใช้งาน

```text
เจ้าของผลงาน → Login → สร้าง Project → Publish → แชร์ URL → ผู้เข้าชมเปิดดูผลงาน
เจ้าของผลงาน → Login → Dashboard → ดูสถิติและกราฟผลงานของตนเอง
```

---

# Mhai - Portfolio

## Functional Requirements Specification (MVP)

**Project Type:** Multi-User Professional Portfolio Management System

**Architecture:** Next.js Frontend + NestJS REST API

**Sharing Model:** Public Profile + Custom URL + Temporary URL with Redirect

**Authentication:** Email/Password, Google, Facebook

**SEO Policy:** Public Portfolio Indexable

**Version:** 1.3 — MVP

**Document Status:** Requirements Baseline

---

## 1. Project Overview & User Roles

### 1.1 Project Objective

Mhai - Portfolio เป็นระบบที่ให้ผู้ใช้หลายบัญชีสามารถสร้าง จัดการ เผยแพร่ และแชร์ผลงานของตนเองผ่านเว็บไซต์ Portfolio ส่วนตัว โดยมุ่งเน้นการแสดงความสามารถและประสบการณ์ทางวิชาชีพ

ระบบรองรับการเข้าชมผลงานโดยไม่ต้องเข้าสู่ระบบ และอนุญาตให้ Search Engine ทำดัชนีหน้าผลงานสาธารณะได้ แต่ไม่มีระบบ Social Media, Public Feed หรือการค้นหาผู้ใช้ภายในเว็บไซต์

**วัตถุประสงค์หลัก**

1. ผู้ใช้สามารถสมัครสมาชิกและเข้าสู่ระบบได้
2. ผู้ใช้สามารถสร้างและจัดการผลงานของตนเองได้
3. ผู้ใช้แต่ละคนมี Public Portfolio Profile
4. ผู้ใช้สามารถกำหนด Custom URL Name ได้เพียงครั้งเดียว
5. ระบบสร้าง Temporary URL ให้ผู้ใช้ที่ยังไม่ได้กำหนดชื่อ URL
6. Temporary URL เดิมต้อง Redirect ไป Custom URL เมื่อผู้ใช้ตั้งชื่อสำเร็จ
7. Guest สามารถดู Public Profile และ Published Projects โดยไม่ต้อง Login
8. Search Engine สามารถทำดัชนี Public Profile และ Published Projects ได้
9. ผู้ใช้สามารถดูสถิติผลงานของตนเองผ่าน Dashboard
10. ระบบไม่มี Public Feed, User Directory หรือ User Search

### 1.2 User Roles

| Role | Description |
|---|---|
| Registered User | ผู้ใช้ที่มีบัญชี สามารถสร้าง แก้ไข ลบ เผยแพร่ผลงาน ตั้งค่า Profile และดู Dashboard ของตนเอง |
| Guest | ผู้ที่ไม่ได้เข้าสู่ระบบ สามารถดู Public Profile และ Published Projects ผ่าน URL ที่ถูกต้อง |

Registered User สามารถเข้าดู Public Portfolio ของผู้ใช้รายอื่นได้ โดยมีสิทธิ์เทียบเท่า Guest สำหรับข้อมูลที่ไม่ใช่ของตนเอง

### 1.3 Core Business Rules

- ผู้ใช้แต่ละคนจัดการเฉพาะข้อมูลของตนเอง
- ผู้ใช้หนึ่งบัญชีมี Public Portfolio Profile หนึ่งหน้า
- Public Profile แสดงผลงาน Published ทั้งหมดของเจ้าของ
- Guest สามารถเข้าชม Public Portfolio โดยไม่ต้อง Login
- Search Engine สามารถ Crawl และ Index หน้า Public Portfolio ที่เข้าเกณฑ์ได้
- Mhai ไม่มี Public Feed, User Directory หรือ Search ภายในระบบ
- ผู้ใช้สามารถกำหนด Custom URL Name ได้เพียงหนึ่งครั้ง
- Custom URL Name ต้องไม่ซ้ำกับบัญชีอื่น
- การกำหนด Custom URL Name ไม่ใช่ข้อบังคับหลังสมัครสมาชิก
- ผู้ใช้ที่ยังไม่ได้ตั้ง Custom URL ใช้ Temporary URL
- หลังตั้ง Custom URL แล้ว Temporary URL เดิมต้อง Redirect ไป URL ใหม่
- Dashboard, Draft Projects และข้อมูล Authentication เป็นข้อมูลส่วนตัว
- ผลงาน Draft ไม่สามารถเข้าถึงผ่าน Public URL

---

## 2. Authentication Module (AUTH)

จัดการการสมัครสมาชิก การเข้าสู่ระบบ และการยืนยันตัวตน

### 2.1 Email & Password Authentication

| ID | Functional Requirement |
|---|---|
| FR-AUTH-01 | ผู้ใช้สามารถสมัครสมาชิกด้วย Display Name, Email และ Password |
| FR-AUTH-02 | ระบบต้องตรวจสอบรูปแบบ Email และป้องกัน Email ซ้ำ |
| FR-AUTH-03 | ระบบต้อง Hash Password ด้วย Argon2 ก่อนบันทึกลง Database |
| FR-AUTH-04 | ผู้ใช้สามารถ Login ด้วย Email และ Password |
| FR-AUTH-05 | เมื่อ Login สำเร็จ ระบบต้องสร้าง Authentication Session ด้วย JWT |
| FR-AUTH-06 | ผู้ใช้สามารถ Logout โดยระบบต้องจัดการ Session หรือ Refresh Token ให้ไม่สามารถใช้งานต่อได้ตามกลไกที่กำหนด |
| FR-AUTH-07 | ระบบต้องตรวจสอบ JWT ก่อนอนุญาตให้เข้าถึง Private API |
| FR-AUTH-08 | ระบบต้องปฏิเสธ Request ที่ไม่ได้รับอนุญาต |
| FR-AUTH-09 | ระบบต้องตรวจสอบความถูกต้องของข้อมูล Register และ Login |

### 2.2 Social Authentication

| ID | Functional Requirement |
|---|---|
| FR-AUTH-10 | ผู้ใช้สามารถ Register หรือ Login ด้วย Google |
| FR-AUTH-11 | ผู้ใช้สามารถ Register หรือ Login ด้วย Facebook |
| FR-AUTH-12 | ระบบต้องใช้ OAuth/OIDC Flow ที่เหมาะสมกับแต่ละ Provider |
| FR-AUTH-13 | Backend ต้องตรวจสอบผล Authentication จาก Provider |
| FR-AUTH-14 | ระบบต้องสามารถสร้างบัญชีใหม่เมื่อเข้าสู่ระบบผ่าน Social Provider ครั้งแรก |
| FR-AUTH-15 | ระบบต้องจัดเก็บ Provider และ Provider User ID |
| FR-AUTH-16 | ระบบต้องรองรับบัญชีที่ไม่มี Password สำหรับ Social Login |
| FR-AUTH-17 | ระบบต้องป้องกันการเชื่อมบัญชีผิดคนเมื่อ Email ซ้ำ |
| FR-AUTH-18 | เมื่อ Social Login สำเร็จ ระบบต้องสร้าง Authentication Session ของ Mhai |

### 2.3 Authentication Business Rules

- Email ต้องไม่ซ้ำแบบ Case-insensitive
- ห้ามจัดเก็บ Plain Text Password
- บัญชี Social Login สามารถมี `passwordHash = NULL` ได้
- Social Provider Token ไม่สามารถใช้แทน JWT ของ Mhai โดยตรง
- ห้ามเชื่อมบัญชี Social กับบัญชีเดิมอัตโนมัติเพียงเพราะ Email ตรงกัน
- กรณีพบ Email ซ้ำกับบัญชีที่ยังไม่ได้เชื่อม Provider ระบบต้องไม่สร้างบัญชีซ้ำหรือยึดบัญชีเดิมโดยอัตโนมัติ
- Account Linking UI ยังไม่รวมใน MVP
- User ที่ Login สำเร็จสามารถเข้า Dashboard ได้ทันที แม้ยังไม่ได้กำหนด Custom URL

---

## 3. User Profile Module (USER)

จัดการข้อมูล Profile ของผู้ใช้และข้อมูลที่แสดงต่อสาธารณะ

| ID | Functional Requirement |
|---|---|
| FR-USER-01 | ผู้ใช้สามารถดูข้อมูล Profile ของตนเองได้ |
| FR-USER-02 | ผู้ใช้สามารถแก้ไข Display Name ได้ |
| FR-USER-03 | ผู้ใช้สามารถเพิ่มหรือแก้ไข Bio ได้ |
| FR-USER-04 | ผู้ใช้สามารถกำหนด Profile Image หรือ Avatar ได้ |
| FR-USER-05 | ผู้ใช้สามารถเพิ่มหรือแก้ไข GitHub, LinkedIn และ Website URL ได้ |
| FR-USER-06 | ระบบต้องแสดงข้อมูล Profile ที่อนุญาตให้เผยแพร่บน Public Portfolio |
| FR-USER-07 | ระบบต้องไม่เปิดเผย Email หรือข้อมูล Authentication บน Public Profile โดยอัตโนมัติ |
| FR-USER-08 | ผู้ใช้สามารถดูสถานะการกำหนด Custom URL Name ของตนเองได้ |
| FR-USER-09 | การแก้ไข Display Name ต้องไม่กระทบ Custom URL Name |

### 3.1 Profile Data

| Field | Public | Editable |
|---|---|---|
| Display Name | Yes | Yes |
| Bio | Yes | Yes |
| Avatar | Yes | Yes |
| GitHub URL | Yes | Yes |
| LinkedIn URL | Yes | Yes |
| Website URL | Yes | Yes |
| Email | No | No (MVP) |
| Custom URL Name | Yes (เมื่อกำหนดแล้ว) | ครั้งเดียว |
| Account Created At | No | No |

### 3.2 Business Rules

- Display Name สามารถซ้ำกันได้
- Custom URL Name ต้องไม่ซ้ำ
- Display Name เปลี่ยนแปลงได้
- Custom URL Name ไม่สามารถเปลี่ยนหรือลบได้หลังยืนยัน
- ระบบต้องรองรับกรณีผู้ใช้ยังไม่ได้กรอกข้อมูล Profile บางส่วน
- Public Profile ต้องใช้ข้อมูลที่เจ้าของอนุญาตให้เผยแพร่เท่านั้น

---

## 4. Custom URL Management Module (URL)

จัดการ Temporary URL, Custom URL Name และ URL Redirection

### 4.1 Temporary URL

| ID | Functional Requirement |
|---|---|
| FR-URL-01 | ระบบต้องสร้าง Random Public Token ให้ User ใหม่โดยอัตโนมัติ |
| FR-URL-02 | Token ต้องสุ่มอย่างปลอดภัย คาดเดาได้ยาก และมีความไม่แน่นอนอย่างน้อย 128 บิต |
| FR-URL-03 | ระบบต้องป้องกัน Token ซ้ำ |
| FR-URL-04 | ผู้ใช้ที่ยังไม่มี Custom URL Name ต้องมี Temporary Public Profile URL |
| FR-URL-05 | Guest สามารถเปิด Temporary URL ได้โดยไม่ต้อง Login |
| FR-URL-06 | ระบบต้องใช้ Temporary Token เดิมจนกว่าจะกำหนด Custom URL Name |
| FR-URL-07 | ระบบต้องไม่สร้าง Token ใหม่ทุกครั้งที่ Login |
| FR-URL-08 | ผู้ใช้สามารถคัดลอก Temporary URL เพื่อแชร์ได้ |

### 4.2 Custom URL Name

| ID | Functional Requirement |
|---|---|
| FR-URL-09 | ผู้ใช้สามารถกำหนด Custom URL Name ได้ |
| FR-URL-10 | การตั้ง Custom URL เป็น Optional |
| FR-URL-11 | ระบบต้องตรวจสอบรูปแบบ Custom URL Name |
| FR-URL-12 | ระบบต้องตรวจสอบชื่อไม่ให้ซ้ำกับผู้ใช้อื่น |
| FR-URL-13 | ระบบต้องป้องกัน Reserved Words |
| FR-URL-14 | ระบบต้องแสดง URL Preview ก่อนยืนยัน |
| FR-URL-15 | ระบบต้องแจ้งเตือนว่าชื่อ URL เปลี่ยนภายหลังไม่ได้ |
| FR-URL-16 | ผู้ใช้ต้องยืนยันก่อนบันทึก |
| FR-URL-17 | หลังบันทึกสำเร็จ ระบบต้องไม่อนุญาตให้เปลี่ยนหรือลบ Custom URL Name |
| FR-URL-18 | ระบบต้องจองและบันทึกชื่อแบบ Atomic เพื่อป้องกัน Concurrent Requests |
| FR-URL-19 | หากบันทึกล้มเหลว Temporary URL เดิมต้องยังใช้งานได้ |

### 4.3 URL Redirection

| ID | Functional Requirement |
|---|---|
| FR-URL-20 | เมื่อกำหนด Custom URL Name สำเร็จ ระบบต้องเปลี่ยน Public URL หลักเป็น Custom URL |
| FR-URL-21 | Temporary Profile URL เดิมต้อง Redirect ไป Custom Profile URL |
| FR-URL-22 | Temporary Project URL เดิมต้อง Redirect ไป Custom Project URL โดยคง Project Slug |
| FR-URL-23 | ระบบต้องเก็บ Temporary Token เดิมเพื่อใช้ Redirect |
| FR-URL-24 | ระบบต้องป้องกัน Redirect Loop |
| FR-URL-25 | Project ที่ไม่ได้ Published ต้องไม่เปิดเผยข้อมูลผ่าน Redirect |
| FR-URL-26 | Temporary Token ต้อง Redirect เฉพาะไปยังบัญชีเจ้าของเดิม |
| FR-URL-27 | เมื่อมี Custom URL แล้ว ระบบต้องแสดง URL ใหม่นี้เป็นลิงก์หลัก |
| FR-URL-28 | ระบบต้องใช้ HTTP 301 Redirect สำหรับ Temporary URL ที่เปลี่ยนเป็น Custom URL ถาวร |
| FR-URL-29 | ระบบต้องส่ง Search Engine ไปยัง Custom URL ที่เป็น URL หลัก |
| FR-URL-30 | ระบบต้องปรับ Canonical URL และ Sitemap หลังการกำหนด Custom URL สำเร็จ |

### 4.4 URL Formats

**Before Custom URL**

Profile:

`https://mhai.app/p/<random-token>`

Project:

`https://mhai.app/p/<random-token>/<project-slug>`

**After Custom URL**

Profile:

`https://mhai.app/<username>`

Project:

`https://mhai.app/<username>/<project-slug>`

**Redirect Example**

`mhai.app/p/A7kR9xT2`

301 Redirect →

`mhai.app/somchai`

`mhai.app/p/A7kR9xT2/ecommerce`

301 Redirect →

`mhai.app/somchai/ecommerce`

### 4.5 Custom URL Validation Rules

- ความยาว Username 3–30 ตัวอักษร
- อนุญาตเฉพาะ `a-z`, `0-9`, `-` และ `_`
- ไม่อนุญาตช่องว่าง
- ไม่อนุญาตขึ้นต้นหรือลงท้ายด้วย `-` หรือ `_`
- Username ถูก Normalize เป็นตัวพิมพ์เล็ก
- ตรวจสอบชื่อซ้ำแบบ Case-insensitive
- ต้องมี Database Unique Constraint
- ต้องป้องกัน Reserved Words เช่น `login`, `register`, `dashboard`, `api`, `p`, `settings`, `admin`

### 4.6 URL Business Rules

- ผู้ใช้สามารถใช้ Temporary URL ต่อไปได้โดยไม่ต้องตั้ง Custom URL
- Temporary Token ไม่ใช่ Authentication Token
- เมื่อมี Custom URL แล้ว Temporary Token จะทำหน้าที่เป็น Redirect Alias
- Temporary Token ต้องไม่ถูกนำกลับไปใช้กับบัญชีอื่น
- URL Redirect ต้องไม่เปิดเผย Draft Project
- หลัง Redirect แล้ว URL ใหม่จะเป็น Canonical URL
- Temporary URL เดิมต้องไม่อยู่ใน Sitemap หลังผู้ใช้ตั้ง Custom URL แล้ว
- Temporary URL ที่ยังใช้งานเป็น URL หลักอยู่ สามารถทำดัชนีได้ภายใต้นโยบาย SEO ของระบบ
- การ Redirect ต้องไม่ทำให้ผู้ใช้เข้าถึงเนื้อหาที่ไม่มีสิทธิ์ดู

---

## 5. Portfolio Management Module (PORTFOLIO)

จัดการการสร้าง แก้ไข ลบ และเผยแพร่ผลงาน

### 5.1 Portfolio CRUD

| ID | Functional Requirement |
|---|---|
| FR-PORT-01 | ผู้ใช้สามารถสร้าง Project ใหม่ได้ |
| FR-PORT-02 | ผู้ใช้สามารถกำหนด Title, Description, Category, Technologies และ External Project URL |
| FR-PORT-03 | ระบบต้องสร้าง Project Slug จาก Title โดยอัตโนมัติ และมีวิธีรองรับ Title ที่แปลงเป็น Slug ไม่ได้ |
| FR-PORT-04 | ผู้ใช้สามารถแก้ไข Project Slug ก่อน Publish ครั้งแรก |
| FR-PORT-05 | Project Slug ต้องไม่ซ้ำภายในบัญชีเดียวกัน |
| FR-PORT-06 | ผู้ใช้สามารถดูรายการผลงานทั้งหมดของตนเอง |
| FR-PORT-07 | ผู้ใช้สามารถดูรายละเอียด Project ของตนเอง |
| FR-PORT-08 | ผู้ใช้สามารถแก้ไข Project ของตนเอง |
| FR-PORT-09 | ผู้ใช้สามารถลบ Project ของตนเอง |
| FR-PORT-10 | ผู้ใช้สามารถกรอง Project ตาม Category และ Status |
| FR-PORT-11 | ผู้ใช้สามารถเรียง Project ตามวันที่ |
| FR-PORT-12 | ระบบต้องป้องกันการเข้าถึง Private Project ของบัญชีอื่น |

### 5.2 Portfolio Status

| ID | Functional Requirement |
|---|---|
| FR-PORT-13 | Project ใหม่ต้องมีสถานะ Draft |
| FR-PORT-14 | ผู้ใช้สามารถ Publish Project |
| FR-PORT-15 | ผู้ใช้สามารถเปลี่ยน Published กลับเป็น Draft |
| FR-PORT-16 | Published Project ต้องปรากฏบน Public Profile |
| FR-PORT-17 | Draft Project ต้องไม่ปรากฏบน Public Profile |
| FR-PORT-18 | Draft Project ต้องไม่สามารถเข้าถึงผ่าน Public URL |
| FR-PORT-19 | ระบบต้องบันทึก Created At, Updated At และ Published At |
| FR-PORT-20 | เมื่อ Publish ครั้งแรก ระบบต้องบันทึก Published At |
| FR-PORT-21 | การ Publish ซ้ำต้องไม่เปลี่ยน Published At เดิม |
| FR-PORT-22 | หลัง Publish ครั้งแรก ระบบต้องไม่เปลี่ยน Project Slug อัตโนมัติ |

### 5.3 Portfolio Data

| Field | Description |
|---|---|
| Title | ชื่อผลงาน |
| Slug | ชื่อสำหรับ URL |
| Description | รายละเอียดผลงาน |
| Category | หมวดหมู่หลัก |
| Technologies | เทคโนโลยีที่ใช้ |
| Cover Image | รูปหน้าปก |
| Gallery | รูปประกอบหลายรูป |
| Project URL | ลิงก์ไปยัง Demo |
| Status | Draft / Published |
| Created At | วันที่สร้าง |
| Updated At | วันที่แก้ไข |
| Published At | วันที่เผยแพร่ครั้งแรก |
| Owner ID | เจ้าของผลงาน |

### 5.4 Business Rules

- ผู้ใช้หนึ่งบัญชีมี Projects ได้หลายรายการ
- Project หนึ่งรายการมีเจ้าของหนึ่งบัญชี
- Project มี Category หลักหนึ่งหมวดหมู่
- Project สามารถมีหลาย Technologies
- Project Slug ต้องคงที่หลัง Publish ครั้งแรก
- Slug ที่เคยเผยแพร่ต้องไม่ถูกนำกลับไปใช้กับ Project อื่นภายในบัญชีเดียวกัน
- การลบ Project ต้องทำให้ Public URL ไม่สามารถเข้าถึงเนื้อหาได้อีก
- การ Unpublish ต้องทำให้เนื้อหาหยุดเผยแพร่และไม่ปรากฏบน Public Profile
- การเปลี่ยน Project Status ต้องส่งผลต่อ SEO Indexing Eligibility

---

## 6. Category Module (CATEGORY)

จัดการหมวดหมู่ผลงาน

| ID | Functional Requirement |
|---|---|
| FR-CAT-01 | ระบบต้องแสดง Category ที่กำหนดจากส่วนกลาง |
| FR-CAT-02 | ผู้ใช้สามารถเลือก Category หลักให้ Project |
| FR-CAT-03 | ระบบต้องใช้ Category สำหรับกรองผลงาน |
| FR-CAT-04 | ระบบต้องแสดง Category บน Public Project |
| FR-CAT-05 | ระบบต้องใช้ Category สำหรับ Dashboard Analytics |
| FR-CAT-06 | ผู้ใช้ทั่วไปต้องไม่สามารถแก้ไข Category ส่วนกลางผ่าน API |

### 6.1 Default Categories

- Frontend Development
- Backend Development
- Full Stack Development
- Mobile Development
- UI/UX Design
- Data Analytics
- DevOps

---

## 7. Media Management Module (MEDIA)

จัดการ Avatar, Cover Image และ Project Gallery ผ่าน Cloudinary

### 7.1 Cover Image

| ID | Functional Requirement |
|---|---|
| FR-MEDIA-01 | ผู้ใช้สามารถ Upload Cover Image |
| FR-MEDIA-02 | ผู้ใช้สามารถเปลี่ยน Cover Image |
| FR-MEDIA-03 | ผู้ใช้สามารถลบ Cover Image |
| FR-MEDIA-04 | ระบบต้องแสดง Cover Image บน Portfolio List และ Public Project |

### 7.2 Project Gallery

| ID | Functional Requirement |
|---|---|
| FR-MEDIA-05 | ผู้ใช้สามารถ Upload Gallery Images หลายรูปต่อ Project |
| FR-MEDIA-06 | ผู้ใช้สามารถเพิ่มรูปภาพใหม่ |
| FR-MEDIA-07 | ผู้ใช้สามารถลบรูปภาพเฉพาะรูป |
| FR-MEDIA-08 | ผู้ใช้สามารถจัดเรียงลำดับรูป |
| FR-MEDIA-09 | ระบบต้องบันทึกลำดับภาพ |
| FR-MEDIA-10 | Public Project ต้องแสดง Gallery ตามลำดับ |
| FR-MEDIA-11 | การลบรูปหนึ่งต้องไม่กระทบรูปอื่น |

### 7.3 File Upload & Cloudinary

| ID | Functional Requirement |
|---|---|
| FR-MEDIA-12 | ระบบต้องตรวจสอบ File Type |
| FR-MEDIA-13 | ระบบต้องตรวจสอบ File Size |
| FR-MEDIA-14 | ระบบต้อง Upload ภาพผ่าน Cloudinary |
| FR-MEDIA-15 | ระบบต้องจัดเก็บ Public ID, URL และข้อมูลอ้างอิงใน Database |
| FR-MEDIA-16 | ระบบต้องตรวจสอบ Ownership ก่อนแก้ไขหรือลบภาพ |
| FR-MEDIA-17 | ระบบต้องรองรับการลบไฟล์ที่ไม่ใช้งานและจัดการกรณีการลบ Cloudinary ล้มเหลว |
| FR-MEDIA-18 | ผู้ใช้สามารถ Upload และเปลี่ยน Profile Avatar |

### 7.4 Media Business Rules

- Project มี Cover Image ได้หนึ่งรูป
- Project มี Gallery Images ได้หลายรูป
- Gallery รองรับการจัดลำดับภาพ
- กำหนดค่าเริ่มต้น Gallery สูงสุด 10 รูปต่อ Project
- กำหนดค่าเริ่มต้น File Size สูงสุด 5 MB ต่อรูป
- จำนวนและขนาดไฟล์ปรับผ่าน Configuration ได้
- ต้องตรวจสอบสิทธิ์ก่อนจัดการ Media
- Public Project ต้องแสดงผลได้แม้ไม่มี Gallery Images

---

## 8. Public Portfolio & Sharing Module (SHARE)

จัดการหน้า Public Profile และ Public Project

### 8.1 Public Profile

| ID | Functional Requirement |
|---|---|
| FR-SHARE-01 | ระบบต้องมี Public Profile สำหรับ User แต่ละบัญชี |
| FR-SHARE-02 | Guest สามารถเปิด Public Profile ได้โดยไม่ต้อง Login |
| FR-SHARE-03 | Public Profile ต้องแสดง Display Name, Bio, Avatar และ Social Links |
| FR-SHARE-04 | Public Profile ต้องแสดง Published Projects ทั้งหมด |
| FR-SHARE-05 | Guest สามารถเลือก Project เพื่อดูรายละเอียด |
| FR-SHARE-06 | หากไม่มี Published Projects ต้องแสดง Empty State |
| FR-SHARE-07 | Public Profile ต้องไม่แสดง Draft Projects |
| FR-SHARE-08 | Public Profile ต้องไม่เปิดเผยข้อมูล Authentication |

### 8.2 Public Project

| ID | Functional Requirement |
|---|---|
| FR-SHARE-09 | Guest สามารถดู Published Project ผ่าน URL |
| FR-SHARE-10 | Public Project ต้องแสดง Title, Description, Category และ Technologies |
| FR-SHARE-11 | Public Project ต้องแสดง Cover และ Gallery |
| FR-SHARE-12 | Public Project ต้องแสดง External Project URL หากมี |
| FR-SHARE-13 | Guest ต้องไม่สามารถแก้ไขหรือลบ Project |
| FR-SHARE-14 | ระบบต้องตรวจสอบ Published Status ก่อนเปิดเผย Project |

### 8.3 Sharing & URL

| ID | Functional Requirement |
|---|---|
| FR-SHARE-15 | ผู้ใช้สามารถ Copy Public Profile URL |
| FR-SHARE-16 | ผู้ใช้สามารถ Copy Public Project URL |
| FR-SHARE-17 | หากยังไม่มี Custom URL ต้องใช้ Temporary URL |
| FR-SHARE-18 | หากมี Custom URL ต้องใช้ Custom URL เป็น Primary URL |
| FR-SHARE-19 | Temporary Profile URL เดิมต้อง Redirect ไป Custom Profile URL |
| FR-SHARE-20 | Temporary Project URL เดิมต้อง Redirect ไป Custom Project URL |
| FR-SHARE-21 | Project ที่ถูกลบหรือเปลี่ยนเป็น Draft ต้องไม่สามารถเปิดดูผ่าน Public URL |
| FR-SHARE-22 | URL ที่ไม่ถูกต้องหรือไม่มีข้อมูล Public ต้องแสดง Not Found |
| FR-SHARE-23 | ระบบต้องไม่มี Public Feed, User Directory หรือ User Search |
| FR-SHARE-24 | Public Profile และ Published Projects ต้องอนุญาตให้ Search Engine ทำดัชนีได้ ตาม SEO Policy ของระบบ |
| FR-SHARE-25 | Public API ต้องไม่เปิดเผยข้อมูล Authentication หรือข้อมูลส่วนตัว |

### 8.4 Sharing Business Rules

- Guest ไม่ต้อง Login เพื่อดู Public Portfolio
- Public Profile แสดง Published Projects ทั้งหมด
- URL สามารถส่งต่อได้
- Temporary Token ไม่ใช่ Password หรือ Authentication Token
- หลังมี Custom URL แล้ว Temporary URL ต้อง Redirect ไป URL ใหม่
- การซ่อน Project จากสาธารณะให้เปลี่ยนกลับเป็น Draft
- ไม่มีการกำหนด Permission ของ Guest รายบุคคล
- Public Portfolio ที่เปิดให้ Search Engine ทำดัชนีอาจค้นพบได้ แม้เจ้าของไม่ได้ส่งลิงก์ให้ผู้ค้นหาโดยตรง

---

## 9. Search Engine Optimization Module (SEO)

จัดการให้ Public Profile และ Published Projects สามารถค้นพบและทำดัชนีผ่าน Search Engine เช่น Google และ Bing ได้

### 9.1 Search Engine Indexing

| ID | Functional Requirement |
|---|---|
| FR-SEO-01 | ระบบต้องอนุญาตให้ Search Engine Crawl และ Index Public Profile ที่มีอยู่และเปิดเผยได้ |
| FR-SEO-02 | ระบบต้องอนุญาตให้ Search Engine Crawl และ Index Published Projects |
| FR-SEO-03 | Draft Projects ต้องไม่สามารถถูก Index เป็นเนื้อหาสาธารณะได้ |
| FR-SEO-04 | Private Pages เช่น Dashboard และ Settings ต้องไม่เผยแพร่เนื้อหาให้ Search Engine ทำดัชนี |
| FR-SEO-05 | Public Pages ที่อนุญาตให้ Index ต้องไม่ส่ง `noindex` โดยค่าเริ่มต้น |
| FR-SEO-06 | Public Pages ต้องส่ง HTTP Status Code ที่สอดคล้องกับสถานะของข้อมูล |
| FR-SEO-07 | Project ที่ถูกลบหรือ Unpublish ต้องตอบกลับ 404 หรือ 410 ตามนโยบายการลบ โดยไม่เปิดเผยเนื้อหาผลงานเดิม |

### 9.2 SEO Metadata

| ID | Functional Requirement |
|---|---|
| FR-SEO-08 | Public Profile ต้องมี HTML Title และ Meta Description ที่เหมาะสม |
| FR-SEO-09 | Public Project ต้องมี HTML Title และ Meta Description ที่เหมาะสมกับเนื้อหาผลงาน |
| FR-SEO-10 | ระบบต้องรองรับ Canonical URL สำหรับ Public Profile และ Public Project |
| FR-SEO-11 | เมื่อเปลี่ยน Temporary URL เป็น Custom URL ระบบต้องกำหนด Custom URL เป็น Canonical URL |
| FR-SEO-12 | ระบบต้องรองรับ Open Graph Metadata สำหรับการแชร์หน้า Portfolio และ Project |
| FR-SEO-13 | ระบบต้องสร้าง Metadata จากข้อมูลจริงของ User หรือ Project |
| FR-SEO-14 | Metadata ต้องไม่เปิดเผยข้อมูลส่วนตัวหรือข้อมูลของ Draft Projects |

### 9.3 Sitemap & Robots

| ID | Functional Requirement |
|---|---|
| FR-SEO-15 | ระบบต้องมี `sitemap.xml` |
| FR-SEO-16 | Sitemap ต้องประกอบด้วย URL หลักของ Public Profiles และ Published Projects ที่เข้าเกณฑ์ |
| FR-SEO-17 | Sitemap ต้องไม่ประกอบด้วย Draft Projects, Dashboard หรือ Private URLs |
| FR-SEO-18 | ระบบต้องมี `robots.txt` เพื่อระบุนโยบายการเข้าถึงสำหรับ Search Engine Crawlers |
| FR-SEO-19 | `robots.txt` ต้องไม่ปิดกั้นการ Crawl Public Profile และ Published Projects ที่ต้องการให้ Index |
| FR-SEO-20 | ระบบต้องปรับข้อมูล Sitemap เมื่อ Project ถูก Publish, Unpublish, Delete หรือเมื่อ Custom URL Name ถูกกำหนด |
| FR-SEO-21 | เมื่อมี Custom URL แล้ว Sitemap ต้องใช้ Custom URL ไม่ใช่ Temporary URL เดิม |
| FR-SEO-22 | เมื่อยังไม่มี Custom URL ระบบสามารถใช้ Temporary Public URL ที่กำลังใช้งานเป็น URL หลักใน Sitemap ได้ |

### 9.4 SEO Rendering & Accessibility

| ID | Functional Requirement |
|---|---|
| FR-SEO-23 | หน้า Public Profile และ Public Project ต้องมีเนื้อหาหลักใน HTML ที่ Search Engine อ่านได้ โดยใช้ความสามารถ Server Rendering ของ Next.js |
| FR-SEO-24 | ระบบต้องสร้าง SEO Metadata แบบ Dynamic ตาม User หรือ Project |
| FR-SEO-25 | Public Project ต้องมี Link ที่ Search Engine สามารถติดตามได้จาก Public Profile |
| FR-SEO-26 | รูปภาพสำคัญที่แสดงบน Public Pages ต้องรองรับข้อความ Alt ที่เหมาะสม |

### 9.5 SEO Business Rules

**Indexable Pages**

- Public Profile ที่เป็น URL ปัจจุบันของผู้ใช้
- Published Project Pages
- Temporary Public Profile หรือ Project URL ที่ยังเป็น URL หลักก่อนตั้ง Custom URL

**Non-Indexable / Non-Public Content**

- Draft Project Content
- Dashboard
- Settings
- Private Portfolio Management
- Authentication Session Data
- Private API Responses

**Canonical Rules**

- ก่อนตั้ง Custom URL: Temporary URL เป็น Canonical URL ของหน้าสาธารณะนั้น
- หลังตั้ง Custom URL: Custom URL เป็น Canonical URL
- Temporary URL เดิมทำ 301 Redirect ไป Custom URL ใหม่
- ไม่ใส่ Redirect Alias ที่ไม่ใช่ URL หลักไว้ใน Sitemap
- ไม่ควรมี Canonical URL หลายค่าที่ขัดแย้งกันในหน้าเดียว

**SEO Restrictions**

- การอนุญาตให้ Index ไม่ได้หมายความว่า Google จะทำดัชนีทุกหน้าเสมอไป
- Sitemap และ Canonical เป็นสัญญาณช่วย Search Engine ไม่ใช่การรับประกันการแสดงผล
- Search Engine อาจใช้เวลาในการค้นพบหรืออัปเดต URL
- การลบหรือ Unpublish Project ไม่ได้ทำให้ข้อมูลที่เคยปรากฏใน Search Engine หายไปทันที
- ระบบยังคงไม่มี Feed หรือ User Search แม้ Google สามารถค้นพบ Public Portfolio ได้

---

## 10. Dashboard & Analytics Module (DASHBOARD)

แสดงสถิติผลงานของผู้ใช้ที่ Login

| ID | Functional Requirement |
|---|---|
| FR-DASH-01 | ระบบต้องแสดงจำนวนผลงานทั้งหมด |
| FR-DASH-02 | ระบบต้องแสดงจำนวน Published Projects |
| FR-DASH-03 | ระบบต้องแสดงจำนวน Draft Projects |
| FR-DASH-04 | ระบบต้องแสดงจำนวนผลงานที่ Publish ครั้งแรกในเดือนปัจจุบัน |
| FR-DASH-05 | ระบบต้องแสดงกราฟจำนวนผลงานที่ Publish ครั้งแรกแยกตามเดือน |
| FR-DASH-06 | ระบบต้องแสดงจำนวน Project แยกตาม Category |
| FR-DASH-07 | ระบบต้องแสดง Category ที่มี Project มากที่สุด |
| FR-DASH-08 | ระบบต้องคำนวณสถิติจาก Database |
| FR-DASH-09 | Dashboard ต้องแสดงข้อมูลของผู้ใช้ที่ Login เท่านั้น |
| FR-DASH-10 | หากไม่มีผลงานต้องแสดง Empty State |
| FR-DASH-11 | ต้องไม่สามารถเข้าดู Dashboard ของ User อื่นได้ |

### 10.1 Dashboard Metrics

| Metric | Description |
|---|---|
| Total Projects | จำนวน Project ทั้งหมด |
| Published Projects | จำนวน Project ที่เผยแพร่อยู่ |
| Draft Projects | จำนวน Project ที่ยังไม่เผยแพร่ |
| Published This Month | จำนวน Project ที่เผยแพร่ครั้งแรกในเดือนนี้ |
| Monthly Publishing Activity | กราฟการเผยแพร่ครั้งแรกแยกเดือน |
| Projects by Category | จำนวน Project แยก Category |
| Top Category | Category ที่มีจำนวน Project มากที่สุด |

### 10.2 Dashboard Business Rules

- Dashboard ต้อง Login ก่อนใช้งาน
- Backend ต้องใช้ User ID จาก Authentication Context
- ข้อมูลของผู้ใช้คนหนึ่งต้องไม่ปะปนกับอีกคน
- `publishedAt` หมายถึงวันที่ Publish ครั้งแรก
- การ Publish ซ้ำไม่เพิ่มจำนวนการเผยแพร่ครั้งแรก
- ผลงานที่เคย Published แต่กลับเป็น Draft ยังอยู่ในสถิติประวัติการเผยแพร่ครั้งแรกตราบใดที่ยังมีข้อมูล Project
- Project ที่ถูกลบแล้วไม่อยู่ในสถิติจากข้อมูล Project ปัจจุบัน
- ยังไม่มี View Counter หรือ Visitor Analytics

---

## 11. Access Control Matrix

| Feature | Owner | Other User | Guest |
|---|---|---|---|
| Register / Login | Yes | Yes | Yes |
| Set Custom URL | Yes (ครั้งเดียว) | เฉพาะของตนเอง | No |
| Edit Owner's Profile | Yes | No | No |
| Create Portfolio | Yes | เฉพาะของตนเอง | No |
| Edit/Delete Owner's Project | Yes | No | No |
| Publish / Unpublish Owner's Project | Yes | No | No |
| Manage Owner's Media | Yes | No | No |
| View Owner's Private Projects | Yes | No | No |
| View Owner's Dashboard | Yes | No | No |
| View Public Profile | Yes | Yes | Yes |
| View Published Projects | Yes | Yes | Yes |
| Follow Public URL Redirect | Yes | Yes | Yes |
| View Owner's Draft Projects | Yes | No | No |

**Authorization Rules**

- Private API ต้องตรวจสอบ Authentication
- Project และ Media Management ต้องตรวจสอบ Ownership
- Public API เปิดเผยเฉพาะ Public Data
- การรู้ URL ไม่ทำให้ได้สิทธิ์แก้ไขข้อมูล
- Search Engine Crawlers มีสิทธิ์เข้าถึงเพียงข้อมูล Public เช่นเดียวกับ Guest

---

## 12. Main User Flows

### Flow A: Register & Login with Email

1. User เปิดหน้า Register
2. กรอก Display Name, Email และ Password
3. ระบบตรวจสอบข้อมูลและ Email ซ้ำ
4. ระบบ Hash Password ด้วย Argon2
5. ระบบสร้าง User Account
6. ระบบสร้าง Random Public Token
7. User Login
8. ระบบสร้าง Session
9. User เข้าสู่ Dashboard
10. ระบบแสดง Temporary URL และตัวเลือก Set Custom URL

### Flow B: Register / Login with Google or Facebook

1. User เลือก Social Provider
2. ระบบเริ่ม OAuth/OIDC Flow
3. User ยืนยันตัวตนกับ Provider
4. Backend ตรวจสอบข้อมูล Authentication
5. ระบบค้นหาบัญชีจาก Provider User ID
6. หากพบบัญชีที่เชื่อมถูกต้อง ให้ Login
7. หากไม่พบ ให้ตรวจสอบเงื่อนไขสร้างบัญชีใหม่และ Email ซ้ำ
8. เมื่อสร้างบัญชีใหม่ ระบบสร้าง Temporary Token
9. ระบบสร้าง Session ของ Mhai
10. User เข้าสู่ Dashboard

### Flow C: Set Custom URL Name

1. User Login
2. เปิด Profile Settings
3. ระบบตรวจสอบว่าเคยกำหนด Custom URL แล้วหรือไม่
4. User กรอก Custom URL Name
5. ระบบตรวจสอบรูปแบบและชื่อซ้ำ
6. ระบบแสดง URL Preview
7. ระบบแจ้งเตือนว่าเปลี่ยนชื่อภายหลังไม่ได้
8. User ยืนยัน
9. Backend ตรวจสอบและบันทึกแบบ Atomic
10. ระบบเก็บ Temporary Token เดิมสำหรับ Redirect
11. ระบบเปลี่ยน Primary URL เป็น Custom URL
12. ระบบอัปเดต Canonical URL และ Sitemap
13. Temporary URL เดิม Redirect ไป URL ใหม่

### Flow D: Create & Publish Portfolio

1. User Login
2. เปิด My Portfolios
3. Create Portfolio
4. กรอกข้อมูล Project
5. เลือก Category และ Technologies
6. Upload Cover Image
7. Upload Gallery Images
8. จัดลำดับ Gallery
9. กำหนด Project Slug
10. บันทึกเป็น Draft
11. ตรวจสอบและกด Publish
12. Backend บันทึก Published Status และ Published At
13. Project ปรากฏบน Public Profile
14. Project มีสิทธิ์ถูกเพิ่มลง Sitemap และทำดัชนี

### Flow E: Share Public Profile

1. User เปิดหน้า Profile
2. เลือก Copy Public URL
3. ระบบเลือก Temporary หรือ Custom URL
4. User ส่ง URL ให้ Guest
5. Guest เปิด URL
6. Backend ตรวจสอบ Public Profile
7. Frontend แสดง Profile และ Published Projects
8. Guest สามารถเลือก Project เพื่ออ่านรายละเอียด

### Flow F: Share Individual Project

1. User เลือก Published Project
2. กด Copy Project Link
3. ระบบสร้าง URL จาก Primary Public URL
4. User แชร์ URL
5. Guest เปิด URL
6. Backend ตรวจสอบ Project และ Published Status
7. ระบบแสดงรายละเอียด Project, Cover และ Gallery

### Flow G: Redirect Old Temporary URL

1. Guest หรือ Search Engine เปิด Temporary URL เดิม
2. Backend ค้นหา User จาก Temporary Token
3. ระบบตรวจพบ Custom URL Name
4. ระบบสร้าง Destination URL
5. หากเป็น Project ต้องคง Project Slug
6. ระบบตอบกลับ HTTP 301 Redirect
7. Browser หรือ Search Engine ไปยัง Custom URL
8. Backend ตรวจสอบข้อมูลปลายทาง
9. แสดง Public Content หรือ Not Found

### Flow H: Unpublish Project

1. User Login
2. เลือก Published Project
3. กด Unpublish
4. Backend ตรวจสอบ Ownership
5. ระบบเปลี่ยนสถานะเป็น Draft
6. Project หายจาก Public Profile
7. Public Project URL ไม่แสดงเนื้อหาอีกต่อไป
8. Project ถูกนำออกจาก Sitemap
9. Search Engine จะได้รับสถานะที่เหมาะสมเมื่อ Crawl URL อีกครั้ง

### Flow I: Dashboard

1. User Login
2. เปิด Dashboard
3. Frontend เรียก Dashboard API
4. Backend ตรวจสอบ Authentication
5. Backend ดึงข้อมูล Project ของ User
6. Backend คำนวณสถิติ
7. Frontend แสดงกราฟด้วย Chart.js

### Flow J: Search Engine Crawling & Indexing

1. Search Engine เข้าถึง `robots.txt`
2. Search Engine ค้นพบ Public URLs ผ่าน `sitemap.xml` หรือ Links
3. Search Engine ส่ง Request ไป Public Profile หรือ Published Project
4. ระบบตอบกลับ HTML พร้อมข้อมูล Public และ SEO Metadata
5. Search Engine อ่าน Title, Description และ Canonical URL
6. Search Engine ประเมินเนื้อหาว่าควรทำดัชนีหรือไม่
7. เมื่อมีการเปลี่ยน URL ระบบใช้ Redirect และอัปเดต Sitemap
8. เมื่อ Unpublish หรือ Delete เนื้อหา ระบบหยุดให้เข้าถึง Public Content และส่งสถานะ HTTP ที่เหมาะสม

---

## 13. Features Not Included in MVP

### Authentication

- Forgot Password / Reset Password
- Email Verification
- GitHub Login
- Account Linking UI
- Two-Factor Authentication

### Portfolio

- เปลี่ยน Custom URL หลังยืนยันแล้ว
- ลบบัญชีด้วยตนเอง
- หลาย Public Profiles ต่อบัญชี
- Custom Portfolio Themes
- Portfolio Template Builder
- Custom Categories

### Social & Discovery

- Public Feed
- User Directory
- Internal User Search
- Internal Project Search ของผู้ใช้อื่น
- Like, Comment, Follow
- Notifications

### Sharing

- Password-Protected Projects
- Invite-only Projects
- Secret Share Links รายผลงาน
- Share Link Expiration
- Custom Domain

### Analytics

- Profile View Counter
- Project View Counter
- Visitor Tracking
- Search Ranking Dashboard
- Google Search Console Integration ภายใน Mhai
- Advanced SEO Analytics

### Administration

- Admin Dashboard
- User Moderation Tools
- Advanced Content Reporting

---

## 14. MVP Acceptance Criteria

### Authentication

- [ ] Register และ Login ด้วย Email/Password ได้
- [ ] Google Login ใช้งานได้
- [ ] Facebook Login ใช้งานได้
- [ ] Logout ใช้งานได้
- [ ] Private API ตรวจสอบ Authentication และ Authorization

### User Profile

- [ ] ผู้ใช้แก้ไข Display Name และ Bio ได้
- [ ] ผู้ใช้จัดการ Avatar และ Social Links ได้
- [ ] Public Profile ไม่แสดงข้อมูลส่วนตัว

### Custom URL

- [ ] ระบบสร้าง Temporary Token ให้บัญชีใหม่
- [ ] Temporary URL ใช้งานได้
- [ ] ตั้ง Custom URL เมื่อไหร่ก็ได้
- [ ] Custom URL Name ไม่ซ้ำ
- [ ] Reserved Words ถูกปฏิเสธ
- [ ] Custom URL Name ตั้งได้ครั้งเดียว
- [ ] URL เก่า Redirect ไป URL ใหม่
- [ ] Redirect ทำงานสำหรับ Profile และ Project
- [ ] ระบบอัปเดต Canonical URL และ Sitemap

### Portfolio

- [ ] Create, Read, Update, Delete ใช้งานได้
- [ ] Category และ Technologies ใช้งานได้
- [ ] Draft / Published ใช้งานได้
- [ ] Project Slug ไม่ซ้ำภายในบัญชี
- [ ] Draft ไม่เข้าถึงผ่าน Public URL
- [ ] Authorization แยกข้อมูลเจ้าของถูกต้อง

### Media

- [ ] Upload Cover Image ได้
- [ ] Upload Gallery หลายรูปได้
- [ ] จัดลำดับ Gallery ได้
- [ ] ลบหรือเปลี่ยนรูปภาพได้
- [ ] Cloudinary ทำงานร่วมกับ Database ถูกต้อง

### Public Portfolio

- [ ] Guest เปิด Public Profile ได้
- [ ] Guest เห็น Published Projects ทั้งหมด
- [ ] Guest เปิด Project Detail ได้
- [ ] Guest ไม่เห็น Draft Projects
- [ ] Public API ไม่เปิดเผย Private Data
- [ ] ไม่มี Public Feed หรือ User Search

### SEO

- [ ] Public Profile ที่เข้าเกณฑ์ไม่มี `noindex` และไม่ถูกปิดกั้นการ Crawl
- [ ] Published Project ที่เข้าเกณฑ์ไม่มี `noindex` และไม่ถูกปิดกั้นการ Crawl
- [ ] Public Pages มี Title และ Meta Description
- [ ] Public Pages มี Canonical URL ที่ถูกต้อง
- [ ] Public Pages มี Open Graph Metadata
- [ ] ระบบมี `sitemap.xml` ที่แสดง Public URLs ปัจจุบัน
- [ ] ระบบมี `robots.txt` ที่กำหนด Crawl Policy ถูกต้อง
- [ ] Sitemap ไม่แสดง Draft หรือ Private URLs
- [ ] ระบบนำ Unpublished / Deleted Projects ออกจาก Sitemap
- [ ] Temporary URL Redirect ไป Custom URL ด้วย HTTP 301 เมื่อมี Custom URL แล้ว
- [ ] Public Page มีเนื้อหาหลักที่ Crawler อ่านได้จาก HTML Response
- [ ] Dashboard และ Private Content ไม่ถูกเปิดเผยเป็น Public Content

**หมายเหตุ:** Acceptance Criteria ด้าน SEO หมายถึงการเตรียมเว็บไซต์ให้ Search Engine ทำดัชนีได้อย่างถูกต้อง ไม่ใช่การรับประกันว่า Google ต้องแสดงเว็บไซต์ในผลการค้นหาทันที

### Dashboard

- [ ] แสดง Total Projects
- [ ] แสดง Published / Draft Projects
- [ ] แสดง Monthly Publishing Activity
- [ ] แสดง Projects by Category
- [ ] แสดง Top Category
- [ ] แยกข้อมูลสถิติของแต่ละ User
- [ ] ไม่มี View Counter ใน MVP

---

## 15. System Constraints & Implementation Notes

### Database

- Email, Username และ Temporary Token ต้องมี Unique Constraint
- Custom URL Name เป็น Nullable
- ต้องป้องกัน Concurrent Username Registration
- User หนึ่งบัญชีมีหลาย Projects ได้
- Project หนึ่งรายการมี Gallery Images หลายรูปได้
- Temporary Token ต้องเก็บไว้รองรับ Redirect
- Project Slug ต้องไม่ซ้ำในบัญชีเดียวกัน

### Security

- Private API ต้องตรวจสอบ JWT
- Project และ Media Management ต้องตรวจสอบ Ownership
- Social Login ต้องตรวจสอบผล Authentication จาก Provider
- ห้ามเปิดเผย Authentication Secrets
- Public API ต้องส่งเฉพาะ Public Data
- `robots.txt` และ `noindex` ไม่สามารถทดแทน Authentication และ Authorization ได้

### SEO

- ใช้ Next.js Metadata API สำหรับ Dynamic SEO Metadata
- ใช้ Next.js Server Rendering สำหรับ Public Content ที่ Search Engine ต้องอ่าน
- ใช้ `sitemap.ts` หรือวิธีเทียบเท่าเพื่อสร้าง Sitemap จากข้อมูลจริง
- ใช้ `robots.ts` หรือวิธีเทียบเท่าเพื่อกำหนด Crawl Policy
- Sitemap ต้องแสดงเฉพาะ Canonical Public URLs ปัจจุบัน
- ต้องรองรับการอัปเดตหรือทำให้ Cache ของ Sitemap หมดอายุเมื่อข้อมูลเปลี่ยน
- การเปลี่ยน URL ต้องใช้ Redirect ที่ถูกต้อง
- Public Content ที่ถูก Unpublish หรือ Delete ต้องไม่เปิดเผยผ่าน URL เก่า
- หน้า Private ต้องไม่เปิดเผยข้อมูลโดยไม่ผ่าน Authentication

### Analytics

- สถิติดึงจาก Database
- การเผยแพร่ครั้งแรกใช้ Published At
- ยังไม่ต้องมี Analytics Table
- ยังไม่มี Profile Views หรือ Project Views
- ต้องรองรับ Empty State

---

## 16. Requirements Traceability

| Module | Prefix | Responsibility |
|---|---|---|
| Authentication | AUTH | Register, Login, OAuth, JWT |
| User Profile | USER | Profile Management |
| Custom URL | URL | Temporary URL, Username, Redirect |
| Portfolio | PORT | CRUD, Draft, Publish |
| Category | CAT | Categories |
| Media | MEDIA | Cover, Gallery, Cloudinary |
| Sharing | SHARE | Public Profile & Project |
| SEO | SEO | Indexing, Metadata, Sitemap, Robots |
| Dashboard | DASH | Statistics & Charts |

---

## 17. Final MVP Scope

Mhai - Portfolio MVP ต้องสามารถรองรับผู้ใช้หลายบัญชีที่สมัครสมาชิกและสร้าง Professional Portfolio ของตนเองได้ พร้อม Custom URL ที่กำหนดได้ครั้งเดียว ระบบแชร์ผลงานแบบสาธารณะ และ Dashboard สำหรับดูสถิติส่วนตัว

ผู้ใช้สามารถนำลิงก์ Portfolio ไปใช้สมัครงาน ส่งให้ลูกค้า หรือเผยแพร่บนแพลตฟอร์มอื่น โดย Public Profile และ Published Projects มีความพร้อมสำหรับ Search Engine Indexing

ระบบยังคงไม่มี Public Feed, User Directory, Internal User Search หรือ Social Interactions

**Version:** 1.3 — MVP

**Status:** Requirements Baseline

**Next Phase:** Use Case Diagram → ER Diagram → API Design → UI/Wireframe → Project Structure
