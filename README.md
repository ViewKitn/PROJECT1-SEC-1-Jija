<div align="center">
  <h3 style="text-align:center;">Project</h3>
  <h1>"What is it?"<br>( เกมทายว่ามันคืออะไร จากภาพ )</h1>
</div>
<h3>สมาชิกกลุ่ม Jija</h3>
<table>
  <colgroup>
    <col>
    <col>
  </colgroup>
  <tr>
    <th>รหัสนักศึกษา</th>
    <th>ชื่อ</th>
    <th>หน้าที่รับผิดชอบ</th>
    <th>สัดส่วนงาน</th>
  </tr>
  <tr>
    <td>66130500007</td>
    <td>Kittikan Weelmek</td>
    <td>page: main-page<br>
        feature: นับคะแนน, รวมคะแนน, watch ( ทำการ tracking round เพื่อจะที่ทำการเปลี่ยนค่า page เป็น score ใช้ในการ show score page )
    </td>
    <td>23%</td>
  </tr>
  
  <tr>
    <td>66130500050</td>
    <td>Narisara Jampathong</td>
    <td>page: category-page<br>
        feature: จับเวลาและกำหนดเวลาในการเล่นเกมแต่ละรูป,  function เสียงเพลงขณะเล่นเกมและเสียงคลิกปุ่ม , function สุ่มคำชมเชยเมื่อตอบถูก
    </td>
    <td>23%</td>
  </tr>

  <tr>
    <td>66130500051</td>
    <td>Naruedom Srirukkaew</td>
    <td>page: playgame-page<br>
        feature: สุ่มคำตอบ, กับสุ่มช้อย, เช็คคำตอบเมื่อ user กดเลือกอันไหน
    </td>
    <td>31%</td>
  </tr>

  <tr>
    <td>66130500060</td>
    <td>Paveepat Thaitiemsing</td>
    <td>page: score-page<br>
        feature: ระบบจัดการ page(เมื่อกดปุ่ม play, back, home, play again จะสลับเปลี่ยน page เป็นหน้าใหม่ขึ้นมา), showtext (แสดงคะแนนเมื่อเข้าเงื่อนไขต่างๆ เช่น เมื่อได้ 12 คะแนนขึ้นไปจะแสดงข้อความ     
        Perfect), showModal / ModalContent (จะแสดงข้อความ correct / incorrect) , ปรับแต่ง UI all page เช่น พื้นหลังเป็นวิดีโอ
    </td>
    <td>23%</td>
  </tr>
</table>

  <h3>การใช้งานแอพลิเคชั่น</h3>
  <a href="https://github.com/user-attachments/files/18827254/default.pdf">คู่มือการใช้งานแอพลิเคชั่น</a>
  <br>
  
  <h3>รายการฟีเจอร์ความสามารถของแอปพลิเคชัน</h3>
  <ul>
     <li><b>feature audio</b>
          <ul>
               <li>playMusic [เปิด/ปิดเสียงเพลงประกอบเกม]</li>
               <li>playClickSound [เสียงขณะที่ user ทำการคลิกต่างๆในเกม]</li>
          </ul>
     </li>
     <li><b>feature timer</b>
          <ul>
               <li>startTimer [เริ่มจับเวลาโดยเวลาจะลดลงจาก 5 วินาทีไปเรื่อยๆ]</li>
               <li>stopTimer [หยุดเวลและเซ็ตเวลากลับไปเป็น 5 วินาที]</li>
          </ul>
     </li>
     <li><b>feature score</b>
          <ul>
               <li>addScore [เพิ่มค่าคะแนนให้ user ครั้งละ 1 คะแนน]</li>
               <li>resetScore [เซ็ตค่าคะแนนให้เป็น 0]</li>
          </ul>
     </li>
     <li><b>feature round</b>
          <ul>
               <li>increaseRound [เพิ่มรอบในการเล่น]</li>
               <li>resetRound [รีเซ็ตรอบในการเล่น]</li>
          </ul>
     </li>
     <li><b>feature trackRoundToScorePage</b>
       <ul>watch [เมื่อ user เล่นครบ 15 รอบจะทำการเปลี่ยนไปที่หน้า score page]</ul>
     </li>
     <li><b>feature choice</b>
          <ul>
               <li>randomChoice [สุ่มตัวเลือกในการตอบของแต่ละหมวด]</li>
               <li>resetChoiceList [รีเซ็ตตัวเลือกในการตอบ]</li>
          </ul>
     </li>
    <li><b>feature answer</b>
          <ul>
               <li>showCompliment [สุ่มคำชมมาแสดงใน หน้า showModel เมื่อ user ตอบถูก]</li>
               <li>randomAnswer [สุ่มคำตอบของแต่ละข้อ]</li>
               <li>checkAnswer [ตรวจคำตอบเมื่อถูกจะแสดง correct ผิดแสดง incorrect]</li>
               <li>resetAnswerList [รีเซ็ตรายการคำตอบ]</li>
               <li>resetAnswer [รีเซ็ตคำตอบ]</li>
          </ul>
     </li>
     <li><b>other feature</b>
          <ul>
               <li>getColorButton [ให้แสดงสีต่างๆในปุ่มรายการตัวเลือกตอบ]</li>
               <li>gameStart [สุ่มตัวเลือกตอบจากหมวดคำถามที่เลือก]</li>
               <li>nextRound [รีเช็ตคำถามและตัวเลือกตอบใหม่เมื่อไปข้อถัดไป]</li>
               <li>clearGame [รีเซ็ตค่าทุกอย่างเพื่อเริ่มเล่นเกมใหม่]</li>
               <li>showtext [แสดงคำชมตามระดับคะแนนในหน้า score page ]</li>
               <li>showmodal [แสดงหน้าต่างเฉลยคำตอบให้ user ในแต่ละข้อ]</li>
          </ul>
     </li>
  </ul>
  
  <h3>แหล่งข้อมูลอ้างอิงหรือเป็นแรงบันดาลใจในการพัฒนาแอปพลิเคชัน ให้ระบุให้ชัดเจนว่าแต่ละแหล่งอ้างอิงใช้ตรงส่วนใดของแอปพลิเคชัน </h3>
  
### 1. เกมที่มีแนวคิดคล้ายกัน
- **4 Pics 1 Word**
- **Guess the Picture**
- **Who Am I?**

#### 🛠 การนำไปใช้ในแอป:
- `randomChoice` - สุ่มตัวเลือกคำตอบ
- `randomAnswer` - สุ่มคำถามตามหมวดหมู่
- `showmodal` - แสดงเฉลยคำตอบเมื่อจบแต่ละรอบ

---

### 2. หลักการออกแบบ UX/UI และ Gamification
- **"Game UX: Designing for Engagement"** - Celia Hodent
- หลักการ Gamification เช่น **ระบบคะแนน, คำชม, การจับเวลา**

#### 🛠 การนำไปใช้ในแอป:
- `addScore` / `resetScore` - ระบบคะแนน
- `showCompliment` - สุ่มคำชมให้ผู้เล่น
- `startTimer` / `stopTimer` - ระบบจับเวลา

---

### 3. แหล่งอ้างอิงด้านเสียงและเอฟเฟกต์
- **Freesound.org** และ **Zapsplat.com** (แหล่งเสียงฟรี)
#### 🛠 การนำไปใช้ในแอป:
- `playMusic` - เปิด/ปิดเสียงเพลง
- `playClickSound` - เสียงขณะกดปุ่ม

---

### 4. การพัฒนาระบบสุ่มและตรวจคำตอบ
- **Randomization Algorithm** สำหรับสุ่มตัวเลือก
- การใช้ **Math.random() และ Fisher-Yates Shuffle**

#### 🛠 การนำไปใช้ในแอป:
- `randomChoice` / `randomAnswer` - สุ่มตัวเลือกและคำตอบ
- `checkAnswer` - ตรวจสอบว่าคำตอบถูกต้องหรือไม่

---

### 5. หลักการพัฒนา Web Game
- **Phaser.js**, **Unity**, **HTML5 Canvas API**
- การพัฒนาเกมด้วย **Vue.js**

#### 🛠 การนำไปใช้ในแอป:
- `gameStart` - เริ่มเกมโดยสุ่มคำถามจากหมวดหมู่
- `nextRound` - รีเซ็ตคำถามและตัวเลือกเมื่อเปลี่ยนรอบ
- `clearGame` - รีเซ็ตค่าทุกอย่างเพื่อเริ่มเกมใหม่

---

### 6. การออกแบบระบบสี และ UI
- **Material Design Guidelines** จาก Google
- การใช้ **CSS Variables** หรือ **TailwindCSS**

#### 🛠 การนำไปใช้ในแอป:
- `getColorButton` - กำหนดสีของปุ่มตัวเลือก

---



https://github.com/user-attachments/assets/bad9b4d4-b13f-4e20-81fa-945db457c241







