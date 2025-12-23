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
Tanggal installation:
Status (success/failed + notes)



**network_info.txt**
IP address, netmask, gateway
SSH enabled status
SSH connection test hasil

**screenshots**




