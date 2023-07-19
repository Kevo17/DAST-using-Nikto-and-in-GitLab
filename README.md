<h1>DAST using Nikto and in GitLab</h1>


<h2>Description</h2>
This lab focuses on leveraging Nikto, a popular Dynamic Application Security Testing (DAST) tool, to enhance the security of web applications. Nikto performs comprehensive scans on web servers, identifying potential vulnerabilities and security weaknesses.

During this hands-on lab, participants will gain practical experience in using Nikto to conduct DAST scans and improve the security of web applications.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Nikto</b>
- <b>JSON</b>
- <b>GitLab</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Linux</b> 

<h2>Program walk-through:</h2>

Let’s install Nikto to perform Dynamic Analysis: <br/>
```
apt install -y libnet-ssleay-perl
git clone https://github.com/sullo/nikto
cd nikto/program
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/WFKFIJw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

We have successfully installed the Nikto scanner. Let’s explore the functionality it provides us: <br/>
```
./nikto.pl -Help
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/yasoqoP.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Let’s run the Nikto with the following options: <br/>
```
./nikto.pl -output nikto_output.xml -h prod-rcgsg0ei
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/0QLRmSz.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Now, executing cat command on the output file will show the nikto result in XML format: <br/>
```
cat nikto_output.xml
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/2amTZ3m.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

List available plugins and run the headers plugin to perform a scan against prod-rcgsg0ei in Nikto: <br/>
```
./nikto.pl -list-plugins
./nikto.pl -h prod-rcgsg0ei -Plugins headers
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/n7yrRGe.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Configure Nikto (nikto.conf) in /nikto/program/ directory to remove the ports that would never be scanned and save output to CSV format: <br/>
```
cat >/nikto/program/nikto.conf<<EOF
SKIPPORTS=21 22 111
CLIOPTS=-output result.csv -Format csv
EOF
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/loroeK3.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

Re-run the nikto command: <br/>
```
./nikto.pl -h prod-rcgsg0ei -config nikto.conf
```
<br/>
 
<p align="center">
<img src="https://i.imgur.com/bxyzfrj.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<img src="https://i.imgur.com/we1FJqK.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
<img src="https://i.imgur.com/9fkl8Uv.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
