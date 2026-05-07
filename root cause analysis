ROOT CAUSE ANALYSIS  
==============  
### A. Dựa trên report:  
1. Setup timing fail:  
   Worst slack ≈ -4.13 ns  
3. Hold timing: OK  
4. Congestion OK :  
   route__drc_errors = 0 , utilization ≈ 49.5%  
5. Clock skew có nhưng không quá lớn:  
   skew ≈ 0.56 ns

### B. Vậy root cause là gì?  
Nhìn vào critical pat:  
FF → and4 → and4 → and4 → and4 → ... → FF
-> có rất nhiều and4 nối liên tiếp   
👉 nghĩa là:  
-logic depth quá sâu    
mỗi gate thêm:  
-gate delay  
-transition degradation  
-RC delay  

👉 tổng cộng:

data arrival time ≈ 16 ns

trong khi:

clock period = 10 ns

→ fail setup nặng.  

### C. Vì sao không phải congestion?  
Nếu congestion là nguyên nhân chính thì thường sẽ thấy:  

-wire delay cực lớn   
-utilization cao (~80–90%)  
-routing overflow  
-DRC nhiều  

Nhưng trong design này:  
-utilization chỉ ~50%  
-DRC = 0  
→ routing ổn. 

### D. Vì sao không phải clock?   
- Nếu clock là nguyên nhân chính:  

skew phải rất lớn (~1ns+)  

- Nhưng design này:    

skew ≈ 0.56 ns  

→ chỉ ảnh hưởng nhỏ.  
