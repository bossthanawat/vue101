# VSCode Extensions

สำหรับ developer ที่ใช้ VSCode ในการพัฒนา Vue App นั้น เจ้าตัว VSCode เองก็จะมี extensions ต่างๆไว้ให้ใช้มากมาย
ซึ่งในหัวข้อนี้จะแนะนำ extensions ที่จะสามารถอำนวยความสะดวกแก่ developer ได้อีกมาก

...ไปลองดูกัน

### ติดตั้ง VSCode
จะใช้ VSCode extensions ก็แปลว่า เราจะต้องมี VSCode ก่อน ซึ่งถ้าหากใช้ Text editor เจ้าอื่นๆอยู่ ก็อาจจะมี extensions เป็นให้ใช้ด้วยเหมือนกัน แต่สำหรับ section นี้ ขอเชิญชวนมาใช้งาน VSCode กันดีกว่าครับ

[กด Download เลยสิครับ ของมันดี](https://code.visualstudio.com/download)


### หา Extensions ได้จากที่ไหน
วิธีอย่างเร็วๆก็คือ เมื่อเปิด VSCode ขึ้นมา จะพบเมนูด้านซ้าย จะมีปุ่มนี้ให้กด

![Extensions Button](https://code.visualstudio.com/assets/docs/editor/extension-gallery/extensions-view-icon.png)

มันคือปุ่มที่จะสามารถแสดง Extension View เพื่อค้นหาและติดตั้ง extension ผ่านทางแอพ VSCode ได้เลยนั่นเอง โดยเมื่อกดไปแล้วจะเจอหน้าตาแบบนี้

![Extensions Button](https://code.visualstudio.com/assets/docs/editor/extension-gallery/extensions-popular.png)

หรือ! อยากจะหาในเว็บเลยก็ได้ กดไปที่ [Visual Studio Marketplace](https://marketplace.visualstudio.com/)

### จะติดตั้ง Extensions ได้ยังไง
เมื่อเราเลือก extension ที่ต้องการได้แล้ว กดกดเลือก extension เลย จากนั้นข้อมูลจะมาแสดงอยู่ในหน้าต่างด้านขวาของ Extension View

![Extensions Button](https://code.visualstudio.com/assets/docs/editor/extension-gallery/extension-dependencies.png)

สังเกตเห็นว่าจะมีปุ่ม Install สีเขียวอยู่ ก็กดปุ่มเพื่อทำการติดตั้งได้เลย เมื่อเสร็จแล้ว VSCode อาจจะถามให้ reload (restart program) อีกทีนึง ก็กดไปตามลำดับครับ

### แนะนำ Extensions สำหรับโปรเจค Vue
เราสามารถเอาชื่อไป search หาใน extensions view ในแอพ VSCode ได้เลยนะ

#### 1. Prettier
เป็นตัวช่วยในการจัด format code ให้เป็นมาตราฐานตาม rule ที่ถูกเซ็ตไว้ จัดบรรทัดใหม่เต็มส่วนขาดหาย ลบส่วนที่ไม่จำเป็น ของ JavaScript , CSS ต่างๆ ซึ่งอันนี้เราสามารถกำหนด rule เองได้นะ  

#### 2. Vetur
เนื่องจากโปรเจค vue เนี่ย จะมีไฟล์บางส่วนที่มีสกุลเป็น .vue ซึ่งพก code formatter ทั่วไปอาจจะไม่สามารถเข้ามาทำงานได้เหมือนไฟล์ .js ดังนั้น Vetur จะเป็นตัวที่จะมาทำให้ไฟล์ .vue ของเราสามารถใช้งานกับ code formatter อย่างเช่น Prettier ได้

สำหรับ Vetur เนี่ย เราต้องไปเพิ่มการตั้งค่านิดหน่อย ที่ settings ของ VSCode ดังนี้
1. เลือกเมนู File > Preferences > Settings
2. เลือกปุ่ม Open Settings (JSON)
3. เพิ่มตั้งค่าต่างๆดังนี้
```JSON
{
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.css": "prettier",
  "vetur.format.defaultFormatter.js": "ชื่อของ_code-formatter_ที่จะใช้",
}
```

#### 3. ESLint
คือ extensions ที่ช่วยสำหรับช่วยให้ตรวจสไตล์การเขียนโค้ด Javascript ให้ตรงกับมาตรฐานกลางต่างๆ ซึ่งสามารถใช้งานร่วมกับ Prettier ได้ด้วย ซึ่งจะต้องตั้งค่าเพิ่มเติมตามใน [ESLint Document](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) นี้

