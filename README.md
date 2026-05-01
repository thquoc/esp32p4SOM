#CHỌN MẠCH CHUYỂN NGUỒN CHO USB.
-
#1. Mạch nguồn ưu tiên sử dụng diode.
-  
-  Mạch nguồn ưu tiên sử dụng diode hoạt động dựa trên nguyên lý so sánh điện áp, tự động chọn nguồn có điện áp cao hơn để cấp cho tải. Mạch này thường ứng dụng để chuyển đổi nguồn pin và sạc.
<img width="512" height="156" alt="image" src="https://github.com/user-attachments/assets/c7ba12ef-588f-4c8a-9395-fe878a2e7f6e" />

-  Khi chúng ta cấp nguồn PIN(4V2) vào anode của diode D20, thì có sự chênh lệch điện áp giữa anode và cathode của diode này, nên diode D20 sẽ phân cực thuận. Khi đó V_LOAD = 3V7.
-  Đến khi có sạc usb được cấp vào thì ngay lập tức D21 sẽ được phân cực thuận(5-3,7>0.5V). Khi đó V_LOAD = 4V5. Lúc này diode D20 sẽ xảy ra hiện tượng phân cực ngược vì điện áp chân cathode cao hơn điện áp chân anode, đẩy D20 vào trạng thái phân cực ngược và đóng hoàn toàn. Nhờ đó, nguồn USB sẽ thay thế PIN cấp nguồn cho tải và chặn dòng ngược về phía PIN.
-  Ưu điểm: chuyển mạch nhanh, chi phí thấp, chặn dòng ngược.
-  Nhược điểm: sụt áp, công suất thấp.

#2. Mạch nguồn ưu tiên dùng "ideal diode".
-  
-  Mạch này vẫn hoạt động dựa trên nguyên lý so sánh điện áp, tự động chọn nguồn có điện áp cao hơn để cấp cho tải. Tuy nhiên, mạch này rất "nhạy" áp, khi có sự chênh lệch nhỏ chỉ 0.01V thôi thì mạch đã chuyển nguồn rồi.
<img width="510" height="133" alt="image" src="https://github.com/user-attachments/assets/00bdf0bb-1b38-4df3-95f5-097278489400" />

-  Trường hợp USB1_5V > USB_5V: Trong trường hợp này transistor pnp bên phải của Q11 và điện trở 51k sẽ kéo chân Gate của p-mosfet về mức điện áp thấp hơn điện áp USB_5V, lúc này p-mosfet dẫn(Vg < Vs).
-  Trường hợp USB1_5V < USB_5V:Trường hợp này transistor pnp bên phải của Q11 kéo chân Gate của p-mosfet Q8 lên mức điện áp xấp xỉ mức điện áp USB_5V, lúc này p-mosfet đóng(Vg ~Vs).
-  Ưu điểm: chuyển mạch nhanh, không sụt áp, công suất cao, chặn dòng ngược.
-  Nhược điểm: chi phí cao hơn diode, phụ thuộc vào sai số linh kiện, không kiểm soát được nguồn nào sẽ là nguồn ưu tiên.
Các nguồn có giá trị điện áp bằng nhau, trong thực tế các nguồn này không bằng nhau tuyệt đối vì chúng còn phụ thuộc vào sai số linh kiện, sụt áp tải dòng... Chính nhờ đặc điểm này nên tôi có thể dùng nguồn ưu tiên "ideal diode" để chuyển mạch cho các nguồn USB. Vậy tại sao tôi không dùng nguồn ưu tiên sử dụng diode?
  -  Mạch nguồn ưu tiên diode gây sụp áp lớn khoảng 0.5V, và điện áp logic của cổng usb laptop/pc thường hoạt động trong khoảng ~(4.75 đến 5V). Chính vì thế khi sử dụng mạch nguồn ưu tiên diode sẽ dẫn đến lỗi "không nhận diện được USB".




# esp32p4SOM
