xterm h1 h4 h6  
ipconfig ( 記錄h1,h4,h6的ip )  
證明 H1 送出封包的 Link 設定為 3Mbps，目的地 H4、H6:
iperf -s -u -f m -i 5 &(in h4 h6)  
iperf -c [h4's ip] -u -f m -b 10m -i 5 (in h1)  
iperf -c [h6's ip] -u -f m -b 10m -i 5 (in h1)  
  
證明 H1 能 ping 通 H4、H6 :
ping [h4's ip] –c 1000 (in h1)  
ping [h6's ip] –c 1000 (in h1)  
ping [h1's ip] –c 1000 (in h4)  
ping [h1's ip] –c 1000 (in h6)  

p.s. 
  ping 是雙向的，所以來回都要。
