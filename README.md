# CLI

NAMA:SANGGA BEKTI WIJAYA

NIM:1002250035

TOOLS:CLI

KENDALA:ssh

SOLUSI: network pilih bridged adapter jangan pilih nat

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
2.DIRECTORY & FILE MANAGEMENT
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

3.TEXT PROCESSING & SEARCHING
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

7.DISTRO COMPARISON & UNDERSTANDING


Install package (contoh install package vim)
Debian-based: sudo apt update && sudo apt install vim
RHEL-based: sudo dnf install vim (atau sudo yum install vim di versi lama)

Start SSH service
Debian-based: sudo systemctl start ssh
RHEL-based: sudo systemctl start sshd

Check service status (contoh SSH)
Debian-based: sudo systemctl status ssh
RHEL-based: sudo systemctl status sshd

Add firewall rule (contoh allow port 22/SSH)
Debian-based (ufw): sudo ufw allow ssh lalu sudo ufw reload
RHEL-based (firewalld): sudo firewall-cmd --permanent --add-service=ssh lalu sudo firewall-cmd --reload

View system info
Debian-based: uname -a atau cat /etc/os-release atau lsb_release -a
RHEL-based: uname -a atau cat /etc/os-release atau hostnamectl

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

```
ip a 

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
       valid_lft 85259sec preferred_lft 85259sec
    inet6 fe80::a00:27ff:fe00:53e4/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
 ```      
netmask 
```/24 → artinya 255.255.255.0```

gateway
```
Gateway: 10.0.2.2
(Ini IP router/gateway default di mode NAT VirtualBox).
```

**ssh_config_explanation.txt**


Parameter Utama yang Sudah Dikonfigurasi

Port 22
SSH server mendengarkan di port standar 22.
Belum diubah. Untuk keamanan tambahan, banyak admin mengubahnya ke port lain (misal 2222) agar mengurangi serangan otomatis.

PermitRootLogin prohibit-password
User root tidak boleh login langsung menggunakan password.
Tapi masih boleh login jika pakai SSH key.
Ini setting yang cukup aman (lebih baik daripada yes). Rekomendasi terbaik: ubah jadi no supaya root sama sekali tidak bisa login langsung via SSH.

PasswordAuthentication yes
Login menggunakan password masih diizinkan.
Karena ini yes, user biasa (termasuk root, kalau PermitRootLogin allow) bisa login pakai password.
Kalau sudah pakai SSH key dan ingin lebih aman, ubah jadi no.

PubkeyAuthentication yes
Autentikasi menggunakan SSH key diizinkan (dan aktif).
Ini bagus dan aman. Pastikan kamu sudah setup public key di ~/.ssh/authorized_keys.

MaxAuthTries 6
Maksimal 6 kali percobaan login (password atau key) dalam satu sesi koneksi sebelum koneksi diputus.
Cukup standar. Untuk lebih ketat, bisa diturunkan jadi 3 atau 4 untuk mengurangi risiko brute-force.

MaxSessions 10
Maksimal 10 sesi SSH simultan dari satu koneksi.
Mencegah satu user membuka terlalu banyak session sekaligus (berguna untuk kontrol resource).


**equiv_commands.md**

Distro               Package Manager           Init System  SSH Service Name     Firewall            
──────────────────── ───────────────────────── ──────────── ──────────────────── ────────────────────
Ubuntu/Debian        apt (deb)                 systemd      ssh                  ufw / iptables      
Kali Linux           apt (deb)                 systemd      ssh                  ufw / iptables      
RedHat (RHEL)        dnf/yum (rpm)             systemd      sshd                 firewalld           
CentOS               dnf/yum (rpm)             systemd      sshd                 firewalld





-SSH enabled status 

 ```
 ssh.service - OpenBSD Secure Shell server
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
```
-SSH connection test hasil

izin saya connect nya make ubuntu bukan windows

```
java@nix:~$ ssh kali@192.168.1.4
kali@192.168.1.4's password: 
Linux sanggalab 6.17.10+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.17.10-1kali1 (2025-12-08) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Dec 25 09:57:11 2025 from 192.168.1.10
┏━(Message from Kali developers)
┃
┃ This is a minimal installation of Kali Linux, you likely
┃ want to install supplementary tools. Learn how:
┃ ⇒ https://www.kali.org/docs/troubleshooting/common-minimum-setup/
┃
┗━(Run: “touch ~/.hushlogin” to hide this message)


```
**screenshots**


1. uname_output.png dan hostname_change.png
![image alt](https://github.com/dowsxc/PR/blob/main/1.jpeg)

2.
