# PR
CLI

NAMA:SANGGA BEKTI WIJAYA

NIM:1002250035

TOOLS:CLI

KENDALA:Saya kurang paham yang no 3

SOLUSI: saya minta bantuan ai grok

**Perubahan_hostname.txt**

hostname lama:luufy_lab
hostname baru:sangga_lab
command yang di gunakan:

```
hostname
sudo nano hostname      (habis tu ctrl+o ,klik enter dan ctrl+x)
hostnamectl

uname -a
```

**command.txt

Semua commands yang dijalankan:
Penjelasan masing-masing:
```
2.
mkdir  ~/security_lab/scans/results  (buat direktori)
touch report.txt, targets.txt, notes.md (buat file)
nano report.txt, targets.txt, notes.md (buat isi file)
cp report.txt report_backup.txt (copy file)
mv  report.txt report_backup.txt ( rename)
mv  report_backup.txt /archive (move operations)

cat repor_backup.txt (buat liat isi file nya)
head -l lab_targets.txt   (Menampilkan baris awal file
tail -f targets.txt (Menampilkan baris akhir file)
wc -l lab_targets.txt (Menghitung (Word Count) isi file)

3.
grep "security" lab_targets.txt
grep -i "Security" lab_targets.txt     # ignore case
grep -v "closed" lab_targets.txt       # exclude baris dengan "closed"
grep -n "open" lab_targets.txt         # tampilkan nomor baris
-CUT & AWK
Isi lab_targets.txt contoh:
192.168.1.1:22:open
192.168.1.10:80:open
10.0.0.5:43:closed
-Extract IP:
cut -d: -f1 lab_targets.txt            # pakai delimiter :
awk -F: '{print $1}' SORT & UNIQ
-Buat file duplicates.txt dengan IP duplikat, lalu:lab_targets.txt   # sama, pakai awk
sort duplicates.txt | uniq
sort duplicates.txt | uniq | wc -l     # hitung unique IP
-PIPELINE
cat lab_targets.txt | grep "open" | sort | uniq
Jelaskan: cat → tampilkan isi → grep cari "open" → sort urutkan → uniq hapus duplikat.
4.. PACKAGE INSTALLATION & VERIFICATION
-Update system
sudo apt update && sudo apt upgrade -y
buat update dan upgrade
-Install tools
sudo apt install nmap wireshark tcpdump aircrack-ng burpsuite -y
-Verify version
nmap --version
wireshark --version
tcpdump --version
which aircrack-ng
which burpsuite
apt list --installed | grep nmap
-installation_log.txt
touch installation_log.txt  (buat file)
nano installation_log.txt (isi file)
5.NETWORK & CONNECTIVITY SETUP
-Network info
ip addr show atau ip a
# atau ifconfig  (kalau sudah install net-tools)
Catat IP, netmask, gateway (lihat di enp0s3 atau interface aktif).
-Listening ports
sudo netstat -tuln | grep LISTEN
# atau
sudo ss -tuln
-SSH setup & test
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh

saya ssh home server saya
ssh nix@192.168.0.100

6.LINUX CONFIGURATION & SERVICES
-systemctl
systemctl status ssh
systemctl is-enabled ssh
systemctl list-units --type=service

-SSHD config
cat /etc/ssh/sshd_config | grep -v "^#"
Parameter penting:
Port → port SSH (default 22)
PermitRootLogin → boleh login root? (biasa prohibit-password)
PasswordAuthentication → boleh login pakai password?
PubkeyAuthentication → boleh pakai SSH key?
MaxAuthTries → maksimal berapa kali salah password

-/etc/hosts
sudo nano /etc/hostsTambah:
127.0.0.1       localhost
192.168.1.100   kali-lab
192.168.1.101   ubuntu-target
Test: ping kali-lab
-Network config
cat /etc/netplan/*.yaml
ip addr show
ip route show
cat /etc/resolv.conf

-Firewall (UFW)

sudo ufw status
sudo ufw enable
sudo ufw allow 22/tcp
sudo ufw show added
```
**installation_log.txt**
Daftar tools & version:

nmap :7.98

wireshark:4.6.0

tcpdump:4.99.5

aircrack-ng:1.7

burpsuite :2025.11.4-43766

Tanggal installation:21 dec

Status (success/failed + notes) succes



**network_info.txt**
IP address, netmask, gateway
ip a 

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 85259sec preferred_lft 85259sec
    inet6 fe80::a00:27ff:fe00:53e4/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
       
netmask 
/24 → artinya 255.255.255.0

gateway

Gateway: 10.0.2.2
(Ini IP router/gateway default di mode NAT VirtualBox).

SSH enabled status 
● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: disabled)
   Active: active (running) since Mon 2025-12-22 15:10:59 WIB; 4min 16s ago
     Docs: man:sshd(8)
          man:sshd_config(5)
 Main PID: 625 (sshd)
    Tasks: 1 (limit: 5053)
   Memory: 2.2M (peak: 3.2M)
      CPU: 44ms
   CGroup: /system.slice/ssh.service
           └─625 "sshd: /usr/sbin/sshd -D [listener] 0 of 
SSH connection test hasil

```
kali@sanggalab:~ $ ssh nix@192.168.0.100
The authenticity of host '192.168.0.100 (192.168.0.100)' can't be established.
ED25519 key fingerprint is SHA256:9YYS6pPdpS3bYP5DJT0Q79ZlOpb7bAe9mi1MJY4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.0.100' (ED25519) to the list of known hosts.
nix@192.168.0.100's password: 

Welcome to Ubuntu 22.04.5 LTS (GNU/Linux 5.15.0-161-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:         https://ubuntu.com/pro

System information as of Mon Dec  1 11:29:31 PM UTC 2025

  System load:  3.92                   Temperature:         43.0 °C
  Usage of /:   31.5% of 97.87GB       Processes:          158
  Memory usage: 8%                    Users logged in:    0
  Swap usage:   0%                    IPv4 address for enp1s0: 192.168.0.100

Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
just raised the bar for easy, resilient and secure K8s cluster deployment.

https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

11 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm

The list of available updates is more than a week old.
To check for new updates run: sudo apt update

```
**screenshots**




