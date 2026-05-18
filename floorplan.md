### Floorplan trực quan trên OpenRoad:  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/81e81736-fe3e-4941-b5af-e6c790cac6b7" />  

FLOORPLAN ANALYSIS:  
=================
Trích file metrics.csv  trong thư mục rún/reports:  
### 1. Die Area (diện tích chip):   
"DieArea" ≈ 257852 µm²  
=> diện tích này gần vuông  
Đây là tổng diện tích toàn chip, bao gồm:  
-core region  
-IO region  
-power ring  
-spacing/margin  
### Core Area (diện tích vùng core):  
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

### 2. Cell Utilization:  
"final_util": 0.49522  
=> utilization ≈ 49.5%  
### Nhận xét:  
-utilization thấp → routing dễ hơn  
-congestion giảm  
-timing dễ optimize hơn  

=> 49% là khá an toàn.  




