### Floorplan trực quan trên OpenRoad:  
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/81e81736-fe3e-4941-b5af-e6c790cac6b7" />  

FLOORPLAN ANALYSIS:  
=================
Trong report metrics.csv  trong thư mục reports:  
### 1. Core/Die Area:  
DIEAREA ( 0 0 ) ( 502460 513180 )  
Width ≈ 502.46 µm  
Height ≈ 513.18 µm  
Die area ≈ 257852 µm²  
=> diện tích này gần vuông  
"design__core__area": 240531   

### Ưu điểm  
routing cân bằng  
clock tree dễ distribute hơn  
wirelength trung bình thấp hơn  
congestion thường ít hơn rectangle quá dài  

### 2. Cell Utilization:  
"design__instance__utilization": 0.49522  
=> utilization ≈ 49.5%  
### Nhận xét:  
-utilization thấp → routing dễ hơn  
-congestion giảm  
-timing dễ optimize hơn  

=> 49% là khá an toàn.  




