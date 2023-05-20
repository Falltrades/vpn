# openvpn

Put your openvpn configuration file.ovpn in /etc/openvpn/. You can add this line in /etc/openvpn/file.ovpn (in the first section) to authenticate your username automatically :
```
auth-user-pass /etc/openvpn/login
```

```
echo "<username>" > /etc/openvpn/login 
```

Start your VPN.
```
sudo openvpn --config /etc/openvpn/file.ovpn
```

Recommended to add in /etc/sudoers.d/user
```
%user ALL=NOPASSWD: /usr/sbin/openvpn
```

# anyconnect

Follow https://its.gmu.edu/knowledge-base/how-to-install-cisco-anyconnect-on-linux/ for installation.

Use this script if you prefer the use of command line over GUI to run VPN.
```
cat << EOF > anyconnect.sh
#!/bin/bash
user=xxxxx
precode=xxxx
otp=${1}
vpn=vpn.xxx.xx

printf "${user}\n${precode}${otp}\ny\n" | /opt/cisco/anyconnect/bin/vpn -s connect $vpn
EOF

cat << EOF > anydisconnect.sh
#!/bin/bash
/opt/cisco/anyconnect/bin/vpn -s disconnect
EOF

chmod +x anyconnect.sh

```

To start VPN script with OTP code.
```
./anyconnect.sh xxxxxx
```

To disconnect.
```
./anydisconnect.sh
```

