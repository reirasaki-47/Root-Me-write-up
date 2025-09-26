# FIND THE CAT (25 points)

## Description
"Con mèo của tổng thống đã bị quân ly khai bắt cóc. Một nghi phạm mang theo USB đã bị bắt giữ. Berthier, một lần 
nữa anh phải cứu nền Cộng hòa! Phân tích chiếc USB này và tìm ra con mèo đang bị giam giữ ở thành phố nào!"

Key của challenge là tên của thành phố viết thường.

## Difficulty: Medium (3rd level)

## Tools:
  - Arsernal Image Mounter
  - Autospy
  - [Pic2Map](https://www.pic2map.com/)

## Solution:
- Tải file challenge được file nén có tên là ch9.gz, giải nén ta thu được file chall9.
  
     <img width="606" height="38" alt="Screenshot 2025-09-26 173837" src="https://github.com/user-attachments/assets/27057f2a-9af4-4689-a1cb-43db00afb7a4" />
     <img width="606" height="38" alt="image" src="https://github.com/user-attachments/assets/d053a8c0-394e-4030-b144-23b90f006368" />

- Kiểm tra file, phần này chắc mình không phải giải thích nhiều vì phần mô tả cũng có nói rõ nó là một cái usb :v
- Ngoài ra ta còn biết ID=0xb -> định dạng FAT32, kích thước của usb ~127MB (260096 sectors x 512 byte)

     <img width="764" height="70" alt="image" src="https://github.com/user-attachments/assets/cdf4608d-04d1-4bc7-9622-4d50a2d1b222" />

- Tiếp đến mình dùng Autospy để mở file. Có thể thấy có khá nhiều folder trong phân vùng, trong đó những folder có tiền tố $ thì hoặc là chứa file cũ, đã xóa,
hoặc là file không có metadata, hoặc là file có metadata nhưng không trỏ tới thư mục gốc. Hiểu đại khái nó là những dữ liệu mà ta không thể nhìn thấy trong
Window Explorer. 

  <img width="737" height="539" alt="image" src="https://github.com/user-attachments/assets/a381ae33-f9ab-4ed6-8ade-8d4226409c22" />

- Thực ra ban đầu mình mount nó ra một ổ đĩa riêng để kiểm tra cho dễ (dùng Arsernal Image Mounter) chứ không dùng ngay Autospy.

  <img width="492" height="200" alt="image" src="https://github.com/user-attachments/assets/50eed1d8-28b4-44da-8320-39ace7e230a4" />

- Kết quả là, mấy cái file trong này phần lớn dùng tiếng Pháp (đớn, t/a còn chưa sõi mà phải đọc t/p :(( ).

  <img width="220" height="auto" alt="image" src="https://github.com/user-attachments/assets/9b642836-77ba-4f57-b789-10f957d60387" /><img width="200" height="auto" alt="image" src="https://github.com/user-attachments/assets/9087d371-1d0d-4581-8a46-e9e5aba805eb" /><img width="220" height="auto" alt="image" src="https://github.com/user-attachments/assets/ea2bc631-2b76-4ad6-9542-c5264e84b669" />

- Mình loay hoay mất gần 30 phút để đọc qua những file trong này. Theo mô tả đề bài, ta biết là có một con mèo bị bắt cóc và
đề hỏi là thành phố nơi nó bị giam giữ. Do đó mình lùng sục khắp các file để tìm các từ có tên liên quan đến thành phố thì mình biết được
mấy file này nói khá nhiều về vùng Alsace-Lorraine trong lịch sử tranh chấp của Pháp với Đức. Thế là mình tra gpt để hỏi về các thành phố, vùng,
tỉnh có liên quan trong cuộc tranh chấp này và tổng hợp được: Alsace, Lorraine, Mulhouse, Strasbourg, Metz, Nancy, Meurthe-et-Moselle.
- Tuy chưa có đầu mối về việc con mèo bị bắt cóc liên quan đến những thành phố này, nhưng biết đâu được :3. Và không ngoài dự đoán, không cái tên nào trong
này là đáp án đúng cả =)).
- Mặt khác, mình cũng phát hiện 1 file trông có vẻ khả nghi trong folder ```Files``` tên là ```DataSanitizationTutorial.odt```
.Đây là dạng file OpenDocument Text có thể chứa dữ liệu nén, do đó mình đổi tên file thành .zip và giải nén. 

   <img width="669" height="249" alt="image" src="https://github.com/user-attachments/assets/37ff5efe-10ef-4219-a3cd-037c272d9068" />

   <img width="838" height="561" alt="image" src="https://github.com/user-attachments/assets/aaad1640-3620-4928-8717-93da5c7c3200" />


- Tuy nhiên kiểm tra một hồi vẫn không có phát hiện gì mới nên mình đành phải bật Autospy để phân tích thêm. Đích đến chính là những file
đã bị xóa.

  <img width="1563" height="278" alt="image" src="https://github.com/user-attachments/assets/a06a7eb9-d49c-4f6a-8e52-471b6c3b1c61" />

- Và... *cảnh tượng này, ta đã nhìn thấy nó ở đâu rồi...* Ngay trong folder ```Files``` vẫn còn tồn tại 1 file nữa - file đã bị xóa tên là
```revendications.odt``` 

  <img width="1418" height="804" alt="image" src="https://github.com/user-attachments/assets/58c28027-7ec6-46f3-96a4-3679b7f4f47f" />
  <img width="589" height="317" alt="image" src="https://github.com/user-attachments/assets/14c20876-bce1-4f2c-87c1-e49269fb1288" />

Đoạn text dùng tiếng Pháp
```
RENDEZ L'AUTONOMIE À L'ALSACE        
SINON NOUS TUERONS LE CHAT!!!
```
dịch ra là
```
Hãy trao cho Alsace quyền tự chủ
Hoặc chúng ta sẽ giết con mèo!!!
```
- Đây chính xác là thứ mà chúng ta cần tìm. Mình nhanh chóng ```Extract File``` về và mở lên.

   <img width="831" height="808" alt="image" src="https://github.com/user-attachments/assets/0b567fb1-e6c2-4aad-a924-9d2c5b61490c" />

- Trông không có vẻ gì là nó sẽ bị thịt cả :))))))). Đến đây ta còn có thể nắm được một thông tin quan trọng: kẻ uy hiếp chính là
kẻ đã chụp bức ảnh này, và bức ảnh có thể có chứa vị trí đã chụp, nói đúng hơn là nơi mà con mèo bị bắt cóc. Mình lại tiếp tục đổi
tên file thành .zip để giải nén và thu được file ảnh gốc.

   <img width="537" height="325" alt="image" src="https://github.com/user-attachments/assets/d0f84f4f-b529-47a4-9d85-67b878c13864" />

- Ném ảnh lên [Pic2Map](https://www.pic2map.com/)

   <img width="828" height="451" alt="image" src="https://github.com/user-attachments/assets/3a9f542a-5242-4d0c-9d02-2d4eed6eaa03" />

---> Flag:  helfrantzkirch
