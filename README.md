# FP_Jaringan_Komputer

<img width="1405" height="559" alt="image" src="https://github.com/user-attachments/assets/9da71863-abd5-444d-a7ca-ed3331c12a32" />



## Konfigurasi

I. Konfigurasi Router Interface (IP Statis - Gateway)
Berikut adalah konfigurasi Command Line Interface (CLI) yang diterapkan pada masing-masing Router untuk mendefinisikan Gateway setiap subnet jaringan lokal.

1. Router_Gedung Utama Yayasan ARA
Code snippet

Router_Gedung_Utama# configure terminal
Router_Gedung_Utama(config)# hostname R-Gedung-Utama

interface FastEthernet0/0
 ip address 10.0.0.1 255.255.254.0
 no shutdown

interface FastEthernet1/0
 ip address 10.0.2.1 255.255.254.0
 no shutdown

interface FastEthernet9/0
 ip address 10.0.4.1 255.255.255.128
 no shutdown

interface FastEthernet8/0
 ip address 10.0.4.129 255.255.255.192
 no shutdown

interface FastEthernet7/0
 ip address 10.0.4.193 255.255.255.224
 no shutdown

interface FastEthernet6/0
 ip address 10.0.4.225 255.255.255.240
 no shutdown
 
end
2. Router_Lantai 2 (ARA Tech)
Code snippet

Router_Lt_2# configure terminal
Router_Lt_2(config)# hostname R-Lt2-ARA-Tech

interface FastEthernet0/0
 ip address 10.0.5.225 255.255.255.224
 no shutdown

interface FastEthernet1/0
 ip address 10.0.5.193 255.255.255.224
 no shutdown

interface FastEthernet9/0
 ip address 10.0.5.129 255.255.255.192
 no shutdown
 
end
3. Router_Lantai 4 (ARA Tech)
Code snippet

Router_Lt_4# configure terminal
Router_Lt_4(config)# hostname R-Lt4-ARA-Tech

interface FastEthernet0/0
 ip address 10.0.7.1 255.255.255.192
 no shutdown

interface FastEthernet1/0
 ip address 10.0.6.225 255.255.255.224
 no shutdown

interface FastEthernet9/0
 ip address 10.0.6.161 255.255.255.192
 no shutdown
 
end
4. Router_Lantai 5 (ARA Tech)
Code snippet

Router_Lt_5# configure terminal
Router_Lt_5(config)# hostname R-Lt5-ARA-Tech

interface FastEthernet0/0
 ip address 10.0.7.113 255.255.255.224
 no shutdown

interface FastEthernet1/0
 ip address 10.0.7.97 255.255.255.240
 no shutdown

interface FastEthernet9/0
 ip address 10.0.7.65 255.255.255.224
 no shutdown
 
end
II. Konfigurasi DHCP Pool (PC Klien)
Konfigurasi ini mendefinisikan DHCP Pool untuk PC Klien dan mengecualikan (excluded-address) semua IP Gateway dan IP yang dialokasikan untuk Server.

1. DHCP Pool - R-Gedung-Utama
Code snippet

Router_Gedung_Utama# configure terminal

! === Excluded Addresses: Gateway & Servers ===
ip dhcp excluded-address 10.0.0.1
ip dhcp excluded-address 10.0.2.1
ip dhcp excluded-address 10.0.4.1
ip dhcp excluded-address 10.0.4.129
ip dhcp excluded-address 10.0.4.193
ip dhcp excluded-address 10.0.4.225 
ip dhcp excluded-address 10.0.4.233 10.0.4.238 ! IT Pendidikan Servers (6 hosts)

! === DHCP Pools ===
ip dhcp pool POOL-OPS-YAYASAN
 network 10.0.0.0 255.255.254.0
 default-router 10.0.0.1

ip dhcp pool POOL-KURIKULUM
 network 10.0.2.0 255.255.254.0
 default-router 10.0.2.1

ip dhcp pool POOL-SDM
 network 10.0.4.0 255.255.255.128
 default-router 10.0.4.1

ip dhcp pool POOL-SARANA
 network 10.0.4.128 255.255.255.192
 default-router 10.0.4.129

ip dhcp pool POOL-PEMBINAAN
 network 10.0.4.192 255.255.255.224
 default-router 10.0.4.193

ip dhcp pool POOL-IT-PC
 network 10.0.4.224 255.255.255.240
 default-router 10.0.4.225

end
write memory
2. DHCP Pool - R-Lt2-ARA-Tech
Code snippet

Router_Lt_2# configure terminal

! === Excluded Addresses: Gateway & Servers ===
ip dhcp excluded-address 10.0.5.225
ip dhcp excluded-address 10.0.5.193
ip dhcp excluded-address 10.0.5.129
ip dhcp excluded-address 10.0.5.221 10.0.5.222 ! Cybersecurity Servers (2 hosts)
ip dhcp excluded-address 10.0.5.179 10.0.5.190 ! Data Center Servers (12 hosts)

! === DHCP Pools ===
ip dhcp pool POOL-L2-SUB-C
 network 10.0.5.224 255.255.255.224
 default-router 10.0.5.225

ip dhcp pool POOL-L2-SUB-B-PC
 network 10.0.5.192 255.255.255.224
 default-router 10.0.5.193

ip dhcp pool POOL-L2-SUB-A-PC
 network 10.0.5.128 255.255.255.192
 default-router 10.0.5.129

end
write memory
3. DHCP Pool - R-Lt4-ARA-Tech
Code snippet

Router_Lt_4# configure terminal

! === Excluded Addresses: Gateway & Servers ===
ip dhcp excluded-address 10.0.7.1
ip dhcp excluded-address 10.0.6.225
ip dhcp excluded-address 10.0.6.161
ip dhcp excluded-address 10.0.6.186 10.0.6.190 ! R&D Servers (5 hosts)

! === DHCP Pools ===
ip dhcp pool POOL-L4-SUB-F
 network 10.0.7.0 255.255.255.192
 default-router 10.0.7.1

ip dhcp pool POOL-L4-SUB-E
 network 10.0.6.224 255.255.255.224
 default-router 10.0.6.225

ip dhcp pool POOL-L4-SUB-D-PC
 network 10.0.6.128 255.255.255.192
 default-router 10.0.6.161

end
write memory
4. DHCP Pool - R-Lt5-ARA-Tech
Code snippet

Router_Lt_5# configure terminal

! === Excluded Addresses: Gateway (No Servers on this Router) ===
ip dhcp excluded-address 10.0.7.113
ip dhcp excluded-address 10.0.7.97
ip dhcp excluded-address 10.0.7.65

! === DHCP Pools ===
ip dhcp pool POOL-L5-SUB-I
 network 10.0.7.96 255.255.255.224
 default-router 10.0.7.113

ip dhcp pool POOL-L5-SUB-H
 network 10.0.7.96 255.255.255.240
 default-router 10.0.7.97

ip dhcp pool POOL-L5-SUB-G
 network 10.0.7.64 255.255.255.224
 default-router 10.0.7.65

end
write memory
