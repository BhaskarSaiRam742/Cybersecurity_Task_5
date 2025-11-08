# Cybersecurity_Task_5
README — DVWA Capstone
Purpose
Minimal scripts to demo DVWA pentest + incident response (recon → SQLi PoC → evidence → contain).

Safety
Only test on VMs you own or are authorized to test. Preserve evidence before containment.

Files

recon.sh — run ./recon.sh <target-ip>

evidence_collect.sh — run ./evidence_collect.sh (creates tar.gz + .sha256)

contain.sh — run sudo ./contain.sh <attacker-ip>


Quick commands

Install target prerequisites:
sudo apt update && sudo apt install -y apache2 php php-mysqli git curl mariadb-server

Install attacker tools:
sudo apt install -y nmap gobuster sqlmap tcpdump

PoC (browser): open http://<target-ip>/DVWA/ → SQLi page → enter ' OR '1'='1

Start capture (attacker):
sudo tcpdump -i eth0 host <target-ip> and host <attacker-ip> -w /tmp/attack_capture.pcap & echo $! > /tmp/tcpdump.pid

Stop capture: sudo kill $(cat /tmp/tcpdump.pid)

Collect evidence: ./evidence_collect.sh

Contain (after evidence): sudo ./contain.sh <attacker-ip>


Deliverables
Report PDF, evidence tar.gz + .sha256, scripts, ~12-min demo video.
