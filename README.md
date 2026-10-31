# เว็บประกาศผลคะแนน (Python + GitHub Actions)

โปรเจกต์ตัวอย่าง CI/CD สำหรับอ่านคะแนนจาก `data/scores.csv` คำนวณเกรดและค่าเฉลี่ย แล้วสร้างเว็บไซต์ที่ `_site/index.html`

## วิธีรันบน Windows (PowerShell)

```powershell
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements-dev.txt
ruff check .
pytest --cov=grades --cov=build_site --cov-report=term-missing --cov-fail-under=80
python build_site.py
```

เปิดไฟล์ `_site/index.html` ด้วยเว็บเบราว์เซอร์เพื่อดูผลลัพธ์

## อัปโหลดขึ้น GitHub

1. สร้าง Repository ชื่อ `hello-python` บน GitHub เลือก Public และติ๊ก Add a README file
2. เปิดโฟลเดอร์โปรเจกต์นี้ใน VS Code
3. เปิด Terminal แล้วตั้งค่า remote (แทน `YOUR-USERNAME` ด้วยชื่อบัญชี GitHub)

```bash
git init
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/hello-python.git
git add .
git commit -m "Initial CI/CD project"
git push -u origin main
```

ถ้าโฟลเดอร์นี้ clone มาจาก repo อยู่แล้ว ไม่ต้องใช้ `git init` หรือ `git remote add origin` ซ้ำ ให้ใช้ `git add .`, `git commit` และ `git push` ตามปกติ

## เปิด GitHub Pages

1. เข้า Repository บน GitHub
2. เลือก Settings > Pages
3. ที่ Build and deployment > Source เลือก **GitHub Actions**
4. ไปที่แท็บ Actions รอ workflow `CI/CD` ทำงานจน `test` และ `deploy` ผ่าน
5. เว็บไซต์จะอยู่ที่ `https://YOUR-USERNAME.github.io/hello-python/`

## ทดลอง CI/CD

แก้ไขคะแนนใน `data/scores.csv` แล้ว commit และ push อีกครั้ง GitHub จะรัน lint และ test ก่อน หากผ่านจึงสร้างและ deploy เว็บไซต์ให้อัตโนมัติ หาก test ไม่ผ่าน จะไม่ deploy

## โครงสร้างไฟล์

- `grades.py` คำนวณเกรดและค่าเฉลี่ย
- `build_site.py` อ่าน CSV และสร้าง HTML
- `tests/` ชุดทดสอบด้วย pytest
- `.github/workflows/ci.yml` ตั้งค่า GitHub Actions สำหรับ CI/CD
- `data/scores.csv` ข้อมูลคะแนน
