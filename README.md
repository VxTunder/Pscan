This is a simple Port scanner with a few bugs that I do not know how to fix if you have any suggestions please let me knpw.
The code starts below this line

import socket
from IPy import IP

def scan(target):
    converted_ip = check_ip(target)
    print('\n' + '[-_0 Scanning Target]' + str(target))
    for port in range(1, 100):
        scan_port(converted_ip, port)

def check_ip(ip):
    try:
        IP(ip)
        return(ip)
    except ValueError:
        return socket.gethostbyname(ip)

# The banner is defined here
def get_banner(s):
        return s.recv(1024)

def scan_port(ipaddress, port):
    try:
        sock = socket.socket()
        sock.settimeout(1.5)
        sock.connect((ipaddress, port))

#this Gets a banner(name & version)
        try:
            banner = get_banner(sock)
        print('[+] Open port ' + str(port) + ' : ' + str(banner))
    except:
        print('[+] open port ' + str(port))
# The line above is not working idk why!


#enables multy targets (IP and or link)
targets = input('[+] Enter Target/s To Scan(slipt multiple Targets with ,): ')
if ',' in targets:
    for ip_add in targets.split(','):
        scan(ip_add.strip(' '))

    else:
        scan(targets)

