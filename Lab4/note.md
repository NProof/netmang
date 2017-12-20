
cd   ryu/ryu/app  
ryu-manager --verbose ryu.app.simple_switch_13  

** new terminal **  
mkdir lab4
cd lab4
sudo mn --custom=lab4.py --topo=mytopo --controller=remote,ip=127.0.0.1:16633 --link=tc,bw=10

[sh ovs-vsctl set bridge <Switch名稱> protocols=OpenFlow13]
sh ovs-vsctl set bridge s1 protocols=OpenFlow13
sh ovs-vsctl set bridge s2 protocols=OpenFlow13

[sh ovs-ofctl -O OpenFlow13 show <Switch名稱>]
sh ovs-ofctl -O OpenFlow13 show s1
sh ovs-ofctl -O OpenFlow13 show s2

[sh ovs-ofctl -O openflow13 add-flow s? in_port= ?,action=output=?
sh ovs-ofctl -O openflow13 add-flow s? in_port= ?,action=output=? ,output=?]

sh ovs-ofctl -O openflow13 add-flow s1 in_port= 1,action=output=3  
sh ovs-ofctl -O openflow13 add-flow s1 in_port= 2,action=output=3  
sh ovs-ofctl -O openflow13 add-flow s1 in_port= 3,action=output=1,output=2
sh ovs-ofctl -O openflow13 add-flow s2 in_port= 1,action=output=2  
sh ovs-ofctl -O openflow13 add-flow s2 in_port= 2,action=output=1  

[sh ovs-ofctl -O openflow13 dump-flows s?]

sh ovs-ofctl -O openflow13 dump-flows s?

[mininet cli 輸入]
sh ovs-vsctl set interface s1-eth1 ingress_policing_rate=2000
sh ovs-vsctl set interface s1-eth1 ingress_policing_burst=100
sh ovs-vsctl set interface s1-eth1 ingress_policing_rate=8000
sh ovs-vsctl set interface s1-eth1 ingress_policing_burst=100

iperf -s -u -f m -i 5 
iperf -c 10.0.0.3 -u -f 10m -i 5 

sh ovs-vsctl set interface s1-eth1 ingress_policing_rate=6000
sh ovs-vsctl set interface s1-eth1 ingress_policing_rate=4000

[]
sh ovs-vsctl clear Port s1-eth3 qos  
sh ovs-vsctl --all destroy qos  
sh ovs-vsctl --all destroy queue  
sh ovs-vsctl set Port s1-eth3 qos=@newqos -- --id=@newqos create qos type=linux-htb other-config:max-rate=10000000 queues:0=@q0,1=@q1 -- -- id=@q0 create queue other-config:min-rate=6000000 other-config:max-rate=6000000 --id=@q1 create queue other-config:min-rate=4000000 other-config:max-rate=4000000  
sh ovs-ofctl -O openflow13 add-flow s1 in_port= 1,action=output=set_queue:0,output:3  
sh ovs-ofctl -O openflow13 add-flow s1 in_port= 2,action=output=set_queue:1,output:3 
sh ovs-ofctl -O openflow13 add-flow s1 in_port= 3,action=output=output:1,output2  
sh ovs-ofctl -O openflow13 add-flow s2 in_port= 1,action=output=output2     
sh ovs-ofctl -O openflow13 add-flow s2 in_port= 2,action=output=output1  

sh ovs-vsctl list qos
sh ovs-vsctl list queue
