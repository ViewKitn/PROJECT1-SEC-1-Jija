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
    <td>%</td>
  </tr>
  
  <tr>
    <td>66130500050</td>
    <td>Narisara Jampathong</td>
    <td>page: category-page<br>
        feature: จับเวลาและกำหนดเวลาในการเล่นเกมแต่ละรูป,  function เสียงเพลงขณะเล่นเกมและเสียงคลิกปุ่ม , function สุ่มคำชมเชยเมื่อตอบถูก
    </td>
    <td>%</td>
  </tr>

  <tr>
    <td>66130500051</td>
    <td>Naruedom Srirukkaew</td>
    <td>page: playgame-page<br>
        feature: สุ่มคำตอบ, กับสุ่มช้อย, เช็คคำตอบเมื่อ user กดเลือกอันไหน
    </td>
    <td>%</td>
  </tr>

  <tr>
    <td>66130500060</td>
    <td>Paveepat Thaitiemsing</td>
    <td>page: score-page<br>
        feature: ระบบจัดการ page(เมื่อกดปุ่ม play, back, home, play again จะสลับเปลี่ยน page เป็นหน้าใหม่ขึ้นมา), showtext (แสดงคะแนนเมื่อเข้าเงื่อนไขต่างๆ เช่น เมื่อได้ 12 คะแนนขึ้นไปจะแสดงข้อความ     
        Perfect), showModal / ModalContent (จะแสดงข้อความ correct / incorrect) , ปรับแต่ง UI all page เช่น พื้นหลังเป็นวิดีโอ
    </td>
    <td>%</td>
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
               <li>resetScor [เซ็ตค่าคะแนนให้เป็น 0]e</li>
          </ul>
     </li>
     <li><b>feature trackRoundToScorePage [เก็บค่าคะแนนทั้งหมดที่ user ทำได้ส่งไปแสดงผลหน้า score page]</b></li>
     <li><b>feature round</b>
          <ul>
               <li>increaseRound [เพิ่มรอบในการเล่น]</li>
               <li>resetRound [รีเซ็ตรอบในการเล่น]</li>
          </ul>
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
               <li>randomAnswer [สุ่มคำตอบมาแสดงให้ตรงกับคำถามตามข้อนั้นๆ]</li>
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








