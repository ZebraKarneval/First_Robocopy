### Anleitung
##### 1) Festplatten bestimmen die kopiert werden müssen
Beispiel Stuttgart: s-ln-01
https://confluence.kzvbw.local/display/DOM/Domino+Migration+2022

<table>
<tr>
<td><b>VMWare</b></td>
<td><b>Festplatten Nr.</b></td>
<td><b>Größe</b></td>
<td><b>Lauwerksbuchstabe</b></td>
<td><b>Bemerkung</b></td>
</tr>
<tr>
<td>s-ln-01/s-ln-01.vmdk</td>
<td>6</td>
<td>150 GB</td>
<td>G</td>
<td>Volume</td>
</tr>
<tr>
<td>s-ln-01/s-ln-01_1.vmdk</td>
<td>2</td>
<td>100 GB (dynamisch)</td>
<td>K</td>
<td>Data_Local</td>
</tr>
<tr>
<td>s-ln-01/s-ln-01_2.vmdk</td>
<td>1</td>
<td>60 GB</td>
<td>C</td>
<td>Betriebssystem</td>
</tr>
<tr>
<td><b>s-ln-01/s-ln-01_3.vmdk</td>
<td>3</td>
<td>1024 GB (dynamisch)</td>
<td>E</td>
<td>Data</td>
</tr>
<tr>
<td><b>s-ln-01/s-ln-01_4.vmdk</td>
<td>4</td>
<td>50 GB (dynamisch)</td>
<td>D</td>
<td>Domino</td>
</tr>
<tr>
<td><b>s-ln-01/s-ln-01_5.vmdk</td>
<td>5</td>
<td>5 GB (dynamisch)</td>
<td>F</td>
<td>Transaktion</td>
</tr>
</table>

##### 2) Benötigte Verzeichnisse auf den Festplatten
<b>s-ln-01/s-ln-01_4.vmdk:</b>
D:\ibm\domino\data
<b>s-ln-01/s-ln-01_3.vmdk:</b>
E:\
<b>s-ln-01/s-ln-01_5.vmdk:</b>
F:\

##### 3) VM: "s-ln-01" runterfahren

##### 4) Die besagten Platten von "s-ln-01" in VMware an "s-ln-02" anhängen, und die Maschine hochfahren

##### 5) Datenträger in der "Datenträgerverwaltung" anbinden 
Achtung: bei Dynamischen Datenrägern kann es sein, dass man den Fremden Datenträger importieren muss. Also "Rechts Klick" → "Fremden Datenträger importieren" → "ok" → "ok"

Hintergund: Bei dynamischer Partitionierung weiß nur das Betriebssystem, wie die Partitionierung funktioniert. Auf eine Partition können mehrer Sektoren unterschiedlicher Länge sein. Neues Betriebssystem weiß natürlich nicht wo der "Meta-File-Table" also da wo die Information dafür drinstehen sich befindet. Diese Informationen steht in der "System-Partition", daher muss diese ggf. angebunden werden, damit die anderen Daten träger erkannt werden.Aus irgend einem Grund hat es in diesem Fall, auch so funktioniert.

##### 6) Robocopy
Von Laufwerk: j:\ → f:\
Befehl:
robocopy j:\ f:\ /E /DCOPY:DA /COPY:DAT /PURGE /MIR /R:2 /W:5 /NP /LOG:C:\temp\f_robocopy.txt

asgeg
awgewa


