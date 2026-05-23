### Floorplan trực quan trên OpenRoad:  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/81e81736-fe3e-4941-b5af-e6c790cac6b7" />  

FLOORPLAN ANALYSIS:  
=================
Trích file metrics.csv  trong thư mục rún/reports:  
### 1. DIE AREA (diện tích chip):   
"DieArea" ≈ 257852 µm²  
=> diện tích này gần vuông  
Đây là tổng diện tích toàn chip, bao gồm:  
-core region  
-IO region  
-power ring  
-spacing/margin  
### CORE AREA (diện tích vùng core):  
"coreArea": 240531µm²   
Đây là vùng chứa:  
-standard cells  
-logic gates  
-flip-flops  

Core area chiếm phần lớn die area:  
257852/240531 ≈93.3%  
=> phần IO/margin không quá lớn  
chip sử dụng diện tích khá hiệu quả  
### Kết luận:  
Thiết kế có floorplan cân đối với die area 257852 µm² và core area 240531 µm².  
Bố cục gần vuông giúp routing và clock tree hiệu quả hơn.  
Core chiếm khoảng 93,3% diện tích die, cho thấy mức sử dụng diện tích tốt nhưng vẫn đủ không gian cho IO và routing.  

### 2. CELL UTILIZATION:  
"final_util": 0.49522  
=> utilization ≈ 49.5%  
### Nhận xét:  
-utilization thấp → routing dễ hơn  
-congestion giảm  
-timing dễ optimize hơn  

=> 49% là khá an toàn.  

### 3. ASPECT RATIO:  
tỉ lệ giữa chiều rộng và chiều cao của chip/core  
DIEAREA ( 0 0 ) ( 502460 513180 ) ;  
aspect ratio: Height/Weight = 513180/502460 = 1.02  

### Ý nghĩa của Aspect Ratio:  
≈ 1	gần vuông ✅
>> 1: kích thước chip	dài theo chiều dọc  
<< 1: kích thước chip	dài theo chiều ngang

### Vì sao gần vuông là tốt?  
###  Routing cân bằng hơn:  
Nếu chip quá dài:  

-một số net phải đi rất xa  
-wirelength tăng   
-delay tăng  

Chip gần vuông:  
-khoảng cách trung bình ngắn hơn  
-routing đều hơn  
###  Clock Tree tốt hơn  
CTS thích layout cân đối vì:  

-skew dễ control  
-insertion delay đồng đều hơn  

###  Giảm congestion hotspot  

-tập trung routing ở một vùng  
-tạo congestion cục bộ  

Với Aspect ratio như trên: 1.02
→ rất gần vuông.  
Đây là floorplan khá tốt.  

### 4. CELL COUNT:  
Cell count dùng để phân tích:  

-độ phức tạp của thiết kế  
-số lượng logic cells  
-overhead sau physical implementation  

### a. Số lượng logical cells sau synthesis  

Sau giai đoạn synthesis, trích trong file metrics.csv thiết kế có:  

### synth_cell_count = 8680  

Đây là số lượng logical standard cells được tạo ra từ RTL synthesis, bao gồm:  

-logic gates,  
-flip-flops,  
-multiplexers,  
-các khối combinational/arithmetic logic.  

### b. Physical Component Count  

Trong picorv32.def  

### COMPONENTS 12498 ;  

Đây là tổng số physical instances sau physical implementation.  

Ngoài logical cells ban đầu, backend flow đã thêm:  

-clock tree buffers,  
-optimization buffers,  
-inserted inverters,  
-physical support cells.  

### c. Physical Design Overhead  

Số lượng component tăng từ:  

- 8680→12498  

tương đương tăng thêm khoảng:  

3818 cells  

Điều này phản ánh physical overhead do:  

-Clock Tree Synthesis (CTS),  
-timing optimization,  
-routing optimization.  

### 5. WHITE SPACE:  
### a. White Space là gì?  

White space là phần diện tích còn trống trong vùng core sau khi placement standard cells.  

Nó được tính từ utilization:  
  WhiteSpace=100%−Utilization = 100%−49.5% ≈ 50.5%  

### b. Ý nghĩa của White Space  

Khoảng 50% diện tích core còn trống cho:  

-routing resources,  
-clock tree buffers,  
-timing optimization,  
-filler/tap insertion,  
-future ECO optimization.  

### c. Đánh giá White Space của thiết kế  

Mức white space khoảng 50% được xem là khá an toàn đối với standard-cell digital design.  

Điều này mang lại nhiều lợi ích:  

-giảm nguy cơ routing congestion,  
-giúp CTS dễ optimize clock tree hơn,  
-giảm khả năng xuất hiện hotspot routing,  
-tạo thêm không gian cho timing optimization buffers.  

### 6. ẢNH HƯỞNG ĐẾN ROUTING/TIMING:  
### a. Ảnh hưởng đến Routing  

Floorplan của thiết kế có:  

-utilization trung bình (~49.5%)  
-aspect ratio gần vuông (~1.02)  
-white space khoảng 50.5%  

Những yếu tố này giúp:  

-phân bố cell đồng đều hơn  
-tạo đủ không gian cho routing  
-giảm nguy cơ congestion cục bộ  
-hỗ trợ placement và routing hiệu quả hơn  

### b. Ảnh hưởng đến Clock Distribution

Shape gần vuông và utilization vừa phải hỗ trợ tốt cho Clock Tree Synthesis (CTS):  

clock tree phân bố cân bằng hơn  
clock insertion dễ optimize hơn  
giảm nguy cơ skew tăng mạnh do layout mất cân đối  

Ngoài ra, white space đủ lớn cho phép tool chèn:  

-clock buffers  
-optimization buffers  
-CTS cells  

### c. Ảnh hưởng đến Timing  

Mặc dù floorplan tương đối tốt, STA analysis vẫn cho thấy:  

-setup timing violations  
-negative setup slack  
-critical paths có combinational depth lớn  

Critical path analysis trước đó cho thấy:  

-nhiều tầng AND4 gates nối tiếp  
-data arrival time vượt clock period 10 ns  

### => Điều này cho thấy: timing bottleneck chủ yếu xuất phát từ logic depth và combinational path length.  

Thay vì:  

-floorplan congestion  
-thiếu routing resource  
-layout shape không hợp lý  

### KẾT LUẬN:  

Floorplan hiện tại được đánh giá là khá cân bằng nhờ:  

core utilization hợp lý  
aspect ratio gần vuông
lượng white space đủ lớn

Những đặc điểm này hỗ trợ tốt cho:

placement quality
routing feasibility
clock distribution

Tuy nhiên, timing violation vẫn tồn tại chủ yếu do kiến trúc logic và critical path depth, thay vì do hạn chế của floorplan



