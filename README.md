# คู่มือการใช้ Git แบบละเอียด

เอกสารนี้ออกแบบมาสำหรับผู้เริ่มต้นจนถึงคนที่ต้องการใช้งาน Git จริงในงานพัฒนาโปรแกรม, System Engineer, DevOps และงานร่วมทีม โดยเขียนในรูปแบบที่สามารถนำไปใช้เป็น `README.md` หรืออัปขึ้น GitHub ได้ทันที

---

## สารบัญ 

1. [Git คืออะไร](#git-คืออะไร)
2. [Git ทำงานอย่างไร](#git-ทำงานอย่างไร)
3. [คำศัพท์สำคัญที่ต้องรู้](#คำศัพท์สำคัญที่ต้องรู้)
4. [ติดตั้ง Git](#ติดตั้ง-git)
5. [ตั้งค่า Git ครั้งแรก](#ตั้งค่า-git-ครั้งแรก)
6. [เริ่มต้นสร้างโปรเจกต์ด้วย Git](#เริ่มต้นสร้างโปรเจกต์ด้วย-git)
7. [วงจรการทำงานพื้นฐานของ Git](#วงจรการทำงานพื้นฐานของ-git)
8. [คำสั่ง Git พื้นฐานที่ใช้บ่อย](#คำสั่ง-git-พื้นฐานที่ใช้บ่อย)
9. [การดูความเปลี่ยนแปลงของไฟล์](#การดูความเปลี่ยนแปลงของไฟล์)
10. [การย้อนกลับการเปลี่ยนแปลง](#การย้อนกลับการเปลี่ยนแปลง)
11. [Branch และการทำงานแยกส่วน](#branch-และการทำงานแยกส่วน)
12. [Merge และการรวมงาน](#merge-และการรวมงาน)
13. [Merge Conflict คืออะไร](#merge-conflict-คืออะไร)
14. [การใช้งาน .gitignore](#การใช้งาน-gitignore)
15. [การเชื่อม Git กับ GitHub](#การเชื่อม-git-กับ-github)
16. [Clone / Push / Pull](#clone--push--pull)
17. [Fetch vs Pull](#fetch-vs-pull)
18. [การใช้งานจริงแบบ Workflow](#การใช้งานจริงแบบ-workflow)
19. [Stash, Tag, Reset, Revert](#stash-tag-reset-revert)
20. [ตัวอย่างใช้งานจริงตั้งแต่ต้นจนจบ](#ตัวอย่างใช้งานจริงตั้งแต่ต้นจนจบ)
21. [ปัญหาที่พบบ่อย](#ปัญหาที่พบบ่อย)
22. [Best Practice สำหรับการใช้ Git](#best-practice-สำหรับการใช้-git)
23. [Cheat Sheet](#cheat-sheet)

---

## Git คืออะไร

Git คือระบบ **Version Control System (VCS)** สำหรับเก็บประวัติการเปลี่ยนแปลงของไฟล์ โดยเฉพาะไฟล์ในโปรเจกต์ เช่น source code, script, config, document หรือ infrastructure code

Git ช่วยให้คุณสามารถ:

- ดูว่าไฟล์ถูกแก้ไขอะไรไปบ้าง
- ย้อนกลับไปเวอร์ชันเก่าได้
- แยกงานออกเป็น branch
- รวมงานจากหลายคนเข้าด้วยกัน
- ทำงานร่วมกับ GitHub, GitLab, Bitbucket ได้

> สรุปง่าย ๆ  
> **Git** = เครื่องมือจัดการเวอร์ชัน  
> **GitHub** = เว็บไซต์สำหรับเก็บ Git repository และทำงานร่วมกัน

---

## Git ทำงานอย่างไร

Git มีพื้นที่สำคัญ 3 ส่วน

### 1. Working Directory
พื้นที่ที่คุณแก้ไขไฟล์จริงในเครื่อง

### 2. Staging Area
พื้นที่เตรียมไฟล์ก่อนบันทึกลงประวัติ

### 3. Repository
พื้นที่เก็บประวัติ commit

ลำดับการทำงานหลักคือ

```bash
แก้ไฟล์ -> git add -> git commit
```

ภาพจำง่าย ๆ

```text
Working Directory --> Staging Area --> Repository
```

---

## คำศัพท์สำคัญที่ต้องรู้

### Repository (Repo)
โฟลเดอร์โปรเจกต์ที่ Git ใช้ติดตามไฟล์

### Commit
การบันทึกสถานะของโปรเจกต์ ณ เวลาหนึ่ง

### Branch
เส้นทางการพัฒนาที่แยกออกจากกัน

### Merge
การรวม branch กลับเข้าด้วยกัน

### Clone
การคัดลอก repo จาก remote ลงมาในเครื่อง

### Push
การส่ง commit จากเครื่องเราไปยัง remote

### Pull
การดึงการเปลี่ยนแปลงจาก remote ลงมา

### Remote
repo ที่อยู่บน server เช่น GitHub

### HEAD
ตัวชี้ไปยัง commit ปัจจุบันที่เรากำลังอยู่

---

## ติดตั้ง Git

ตรวจสอบก่อนว่ามี Git แล้วหรือยัง

```bash
git --version
```

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install git -y
```

### CentOS / RHEL

```bash
sudo yum install git -y
```

### Fedora

```bash
sudo dnf install git -y
```

### macOS (ผ่าน Homebrew)

```bash
brew install git
```

### Windows

ติดตั้งผ่าน Git for Windows แล้วเปิดใช้งานผ่าน Git Bash หรือ Command Prompt / PowerShell

---

## ตั้งค่า Git ครั้งแรก

ตั้งชื่อและอีเมลสำหรับใช้กับ commit

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

ตรวจสอบค่าที่ตั้งไว้

```bash
git config --list
```

ตรวจเฉพาะค่าบางตัว

```bash
git config --global user.name
git config --global user.email
```

> `--global` หมายถึงใช้กับทุก repo ในเครื่องนี้  
> ถ้าไม่ใส่ `--global` จะมีผลเฉพาะ repo ปัจจุบัน

---

## เริ่มต้นสร้างโปรเจกต์ด้วย Git

สร้างโฟลเดอร์ใหม่และเริ่มต้น repo

```bash
mkdir myproject
cd myproject
git init
```

ตรวจสอบสถานะ

```bash
git status
```

ผลลัพธ์จะบอกว่า repo ถูกสร้างแล้ว และตอนนี้ยังไม่มี commit

---

## วงจรการทำงานพื้นฐานของ Git

### 1. สร้างไฟล์

```bash
echo "# My Project" > README.md
```

### 2. ดูสถานะไฟล์

```bash
git status
```

ไฟล์ใหม่จะอยู่ในสถานะ **untracked**

### 3. เพิ่มไฟล์เข้า staging

```bash
git add README.md
```

หรือเพิ่มทุกไฟล์

```bash
git add .
```

### 4. commit

```bash
git commit -m "Add README"
```

ตอนนี้ไฟล์ถูกบันทึกลงประวัติแล้ว

---

## คำสั่ง Git พื้นฐานที่ใช้บ่อย

### ดูสถานะ

```bash
git status
```

ใช้บ่อยที่สุด เพราะบอกว่า:

- branch ปัจจุบันคืออะไร
- มีไฟล์ใหม่ไหม
- มีไฟล์ไหนถูกแก้แต่ยังไม่ add
- มีไฟล์ไหน add แล้วแต่ยังไม่ commit

---

### ดูประวัติ commit

```bash
git log
```

แบบสั้น

```bash
git log --oneline
```

แบบมีกราฟ branch

```bash
git log --oneline --graph --all
```

---

### ดูไฟล์ที่ Git ติดตามอยู่

```bash
git ls-files
```

---

## การดูความเปลี่ยนแปลงของไฟล์

### ดูสิ่งที่แก้ไขแต่ยังไม่ add

```bash
git diff
```

### ดูสิ่งที่ add แล้ว แต่ยังไม่ commit

```bash
git diff --cached
```

### ดูความต่างระหว่าง commit

```bash
git diff <commit1> <commit2>
```

ตัวอย่าง

```bash
git diff HEAD~1 HEAD
```

---

## การย้อนกลับการเปลี่ยนแปลง

### 1. ยกเลิกการแก้ไขไฟล์ที่ยังไม่ add

```bash
git restore filename
```

ตัวอย่าง

```bash
git restore README.md
```

---

### 2. เอาไฟล์ออกจาก staging แต่ยังเก็บการแก้ไขไว้

```bash
git restore --staged filename
```

ตัวอย่าง

```bash
git restore --staged README.md
```

---

### 3. reset ย้อน commit

#### soft reset
ย้อน commit แต่เก็บไฟล์ไว้ใน staging

```bash
git reset --soft HEAD~1
```

#### mixed reset
ย้อน commit และเอาออกจาก staging แต่ยังเก็บไฟล์ใน working directory

```bash
git reset --mixed HEAD~1
```

#### hard reset
ย้อน commit และลบการแก้ไขออกจาก working directory

```bash
git reset --hard HEAD~1
```

> ระวัง `--hard` เพราะอาจทำให้ข้อมูลที่ยังไม่ได้เก็บหาย

---

### 4. revert
สร้าง commit ใหม่เพื่อยกเลิก commit เก่า

```bash
git revert <commit-id>
```

เหมาะกับ repo ที่ใช้งานร่วมกัน เพราะปลอดภัยกว่าการ reset commit ที่ push ไปแล้ว

---

## Branch และการทำงานแยกส่วน

Branch ใช้สำหรับแยกงาน เช่น

- `main`
- `develop`
- `feature/login`
- `fix/nginx-config`

### ดู branch

```bash
git branch
```

### สร้าง branch ใหม่

```bash
git branch feature-login
```

### สลับ branch

```bash
git switch feature-login
```

หรือแบบเก่า

```bash
git checkout feature-login
```

### สร้างและสลับทันที

```bash
git switch -c feature-login
```

---

## Merge และการรวมงาน

สมมติว่าคุณทำงานใน branch `feature-login` เสร็จแล้ว

### กลับไป branch หลัก

```bash
git switch main
```

### รวม branch

```bash
git merge feature-login
```

### ลบ branch ที่ไม่ใช้แล้ว

```bash
git branch -d feature-login
```

---

## Merge Conflict คืออะไร

เกิดเมื่อ Git ไม่สามารถรวมการเปลี่ยนแปลงให้อัตโนมัติได้ เช่น มีคนแก้บรรทัดเดียวกันคนละแบบ

ตัวอย่าง conflict

```text
<<<<<<< HEAD
Hello from main
=======
Hello from feature-login
>>>>>>> feature-login
```

วิธีแก้:

1. เปิดไฟล์
2. เลือกว่าต้องการเก็บข้อความส่วนไหน
3. ลบเครื่องหมาย conflict ออก
4. add ไฟล์
5. commit ใหม่

```bash
git add file.txt
git commit -m "Resolve merge conflict"
```

---

## การใช้งาน .gitignore

ไฟล์ `.gitignore` ใช้บอก Git ว่าไฟล์หรือโฟลเดอร์ไหน **ไม่ต้องติดตาม**

ตัวอย่าง

```gitignore
node_modules/
.env
*.log
__pycache__/
*.pyc
dist/
build/
.terraform/
*.tfstate
```

เหมาะกับ:

- ไฟล์ชั่วคราว
- ไฟล์ build
- cache
- log
- secret
- state file

> ถ้าไฟล์ถูก track ไปแล้ว `.gitignore` จะไม่ทำให้หายไปอัตโนมัติ ต้อง `git rm --cached` ก่อน

ตัวอย่าง

```bash
git rm --cached .env
git commit -m "Stop tracking .env"
```

---

## การเชื่อม Git กับ GitHub

### 1. สร้าง repo บน GitHub
เช่นชื่อ `myproject`

### 2. เพิ่ม remote

```bash
git remote add origin https://github.com/username/myproject.git
```

ตรวจสอบ remote

```bash
git remote -v
```

### 3. เปลี่ยนชื่อ branch เป็น main

```bash
git branch -M main
```

### 4. push ครั้งแรก

```bash
git push -u origin main
```

> `-u` ทำให้ Git จำ default upstream branch  
> ครั้งต่อไปใช้แค่ `git push` หรือ `git pull` ได้

---

## Clone / Push / Pull

### Clone repo

```bash
git clone https://github.com/username/myproject.git
cd myproject
```

### Push ขึ้น GitHub

```bash
git push
```

### Pull จาก GitHub

```bash
git pull
```

---

## Fetch vs Pull

### Fetch

```bash
git fetch
```

ดึงข้อมูลจาก remote มาไว้ในเครื่อง **แต่ยังไม่ merge**

### Pull

```bash
git pull
```

คือการทำ

```bash
git fetch
git merge
```

รวมกันในคำสั่งเดียว

> ถ้าต้องการดูก่อนว่ามีอะไรเปลี่ยน ควรใช้ `git fetch`

---

## การใช้งานจริงแบบ Workflow

## Workflow แบบทำงานคนเดียว

```bash
git pull
# แก้ไขไฟล์
git status
git add .
git commit -m "Update project"
git push
```

---

## Workflow แบบทำงานเป็นทีม

1. ดึง branch หลักล่าสุด
2. สร้าง branch ใหม่
3. พัฒนาใน branch ตัวเอง
4. commit
5. push branch ขึ้น GitHub
6. เปิด Pull Request
7. review
8. merge เข้า main

ตัวอย่าง

```bash
git switch main
git pull
git switch -c feature/dashboard
# แก้ไฟล์
git add .
git commit -m "Add dashboard page"
git push -u origin feature/dashboard
```

---

## Stash, Tag, Reset, Revert

## Stash

ใช้เก็บงานชั่วคราวโดยยังไม่ commit

### เก็บงานไว้ก่อน

```bash
git stash
```

### ดู stash

```bash
git stash list
```

### เอากลับมา

```bash
git stash pop
```

หรือ

```bash
git stash apply
```

---

## Tag

ใช้ติดเวอร์ชัน เช่น `v1.0.0`

### สร้าง tag

```bash
git tag v1.0.0
```

### push tag

```bash
git push origin v1.0.0
```

### ดู tag

```bash
git tag
```

---

## ตัวอย่างใช้งานจริงตั้งแต่ต้นจนจบ

### 1. สร้างโปรเจกต์

```bash
mkdir demo-git
cd demo-git
git init
```

### 2. สร้างไฟล์

```bash
echo "print('Hello Git')" > app.py
echo "# Demo Git" > README.md
```

### 3. เช็กสถานะ

```bash
git status
```

### 4. add ไฟล์

```bash
git add .
```

### 5. commit ครั้งแรก

```bash
git commit -m "Initial commit"
```

### 6. สร้าง branch ใหม่

```bash
git switch -c feature/update-message
```

### 7. แก้ไฟล์ `app.py`

```python
print("Hello Git Version 2")
```

### 8. add และ commit

```bash
git add app.py
git commit -m "Update greeting message"
```

### 9. กลับไป main

```bash
git switch main
```

### 10. merge branch

```bash
git merge feature/update-message
```

### 11. เชื่อมกับ GitHub

```bash
git remote add origin https://github.com/username/demo-git.git
git branch -M main
git push -u origin main
```

---

## ปัญหาที่พบบ่อย

## 1. commit ไม่ได้ เพราะยังไม่ได้ตั้งค่า user.name / user.email

แก้ด้วย

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## 2. push ไม่ได้ เพราะ authentication ไม่ผ่าน

สาเหตุที่พบบ่อย:

- URL repo ผิด
- ยังไม่ได้ล็อกอิน GitHub
- ใช้ HTTPS แต่ไม่มี token
- ใช้ SSH key ไม่ถูก
- ไม่มีสิทธิ์เข้าถึง repo

---

## 3. pull แล้ว conflict

แปลว่า local กับ remote มีการแก้ไฟล์ส่วนเดียวกัน  
ต้องแก้ conflict ก่อน แล้วจึง add และ commit

---

## 4. เผลอ add ไฟล์ลับ เช่น `.env`

ถ้ายังไม่ push:
- ลบออกจาก staging / commit
- ใส่ `.gitignore`

ถ้า push ไปแล้ว:
- ถือว่า secret รั่ว
- ต้องเปลี่ยน password / token / key ใหม่ทันที

---

## 5. ลบไฟล์ในเครื่องแล้ว Git ยังตามอยู่

ใช้

```bash
git rm filename
git commit -m "Remove file"
```

---

## 6. เปลี่ยนชื่อไฟล์

```bash
git mv oldname.txt newname.txt
git commit -m "Rename file"
```

---

## Best Practice สำหรับการใช้ Git

### 1. commit ให้บ่อย แต่แต่ละ commit ควรมีความหมาย
ตัวอย่างที่ดี

```bash
git commit -m "Add login validation"
git commit -m "Fix database connection timeout"
git commit -m "Update Docker deployment guide"
```

### 2. อย่า commit ทุกอย่างมั่วรวมกัน
แยกงานเป็นเรื่อง ๆ จะย้อนกลับง่ายกว่า

### 3. อย่า push secret ขึ้น repo
เช่น `.env`, private key, access token, cloud credentials

### 4. ใช้ branch สำหรับฟีเจอร์หรือการแก้ไข
เช่น

- `feature/login`
- `fix/nginx-port`
- `docs/update-readme`

### 5. ดึงของใหม่ก่อน push เสมอ
ช่วยลด conflict

```bash
git pull
git push
```

### 6. ใช้ `.gitignore` ตั้งแต่เริ่มโปรเจกต์
ลดความเสี่ยงเผลอ commit ไฟล์ไม่จำเป็น

### 7. ใช้ข้อความ commit ให้ชัดเจน
ไม่ควรใช้ข้อความแบบ

```bash
git commit -m "fix"
git commit -m "update"
git commit -m "work"
```

---

## Cheat Sheet

### ตั้งค่าเริ่มต้น

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --list
```

### เริ่ม repo

```bash
git init
git status
```

### เพิ่มไฟล์และ commit

```bash
git add .
git commit -m "Initial commit"
```

### ดูประวัติ

```bash
git log
git log --oneline
git log --oneline --graph --all
```

### ดูความต่าง

```bash
git diff
git diff --cached
```

### branch

```bash
git branch
git switch -c new-branch
git switch main
git merge new-branch
git branch -d new-branch
```

### remote / GitHub

```bash
git remote add origin https://github.com/username/repo.git
git remote -v
git push -u origin main
git pull
git clone https://github.com/username/repo.git
```

### ย้อนกลับ

```bash
git restore file.txt
git restore --staged file.txt
git reset --soft HEAD~1
git reset --hard HEAD~1
git revert <commit-id>
```

### stash / tag

```bash
git stash
git stash list
git stash pop
git tag v1.0.0
git push origin v1.0.0
```

---

## ตัวอย่างโครงสร้าง README สำหรับอัป GitHub

คุณสามารถใช้ไฟล์นี้เป็น `README.md` ได้ทันที โดยวางไว้ที่ root ของโปรเจกต์ เช่น

```text
myproject/
├─ README.md
├─ app.py
├─ .gitignore
└─ ...
```

จากนั้นอัปขึ้น GitHub ด้วยคำสั่ง

```bash
git add README.md
git commit -m "Add Git usage guide"
git push
```

---

## สรุป

Git เป็นเครื่องมือสำคัญมากสำหรับการทำงานสายไอที เพราะช่วยให้เราจัดการเวอร์ชันของงานได้อย่างเป็นระบบ  
หัวใจสำคัญของการใช้งาน Git มีอยู่ 4 เรื่องหลัก:

1. เข้าใจ `status`, `add`, `commit`
2. ใช้ `branch` และ `merge` ให้คล่อง
3. เชื่อมกับ GitHub ผ่าน `push`, `pull`, `clone`
4. ใช้งานอย่างมีวินัย เช่น เขียน commit message ให้ดี และไม่ push secret

เมื่อเข้าใจพื้นฐานเหล่านี้แล้ว คุณจะสามารถต่อยอดไปสู่เรื่องที่สูงขึ้นได้ เช่น

- Pull Request
- Rebase
- Cherry-pick
- GitHub Actions
- GitOps
- Infrastructure as Code workflow

---

## ภาคเสริม: ตัวอย่างข้อความ commit ที่ดี

```bash
git commit -m "Add Docker installation guide"
git commit -m "Fix typo in README"
git commit -m "Refactor nginx config structure"
git commit -m "Update Terraform variable naming"
git commit -m "Add Kubernetes deployment example"
```

---

## ภาคเสริม: คำสั่งที่เจอบ่อยในการทำงานจริง

### ดู remote branch ทั้งหมด

```bash
git branch -r
```

### ดู local + remote branch

```bash
git branch -a
```

### ลบ branch บน remote

```bash
git push origin --delete feature-login
```

### เปลี่ยนชื่อ branch

```bash
git branch -m old-name new-name
```

### ดูว่าไฟล์ไหนแก้ไปบ้างใน commit หนึ่ง

```bash
git show <commit-id>
```

### ดูสั้น ๆ ว่า commit ไหนแก้อะไร

```bash
git log --stat
```
