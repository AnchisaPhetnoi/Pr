## lnternet

![451422145_1224687125203738_8498569189999753310_n](https://github.com/user-attachments/assets/76763b22-2d3c-48be-9727-18aff7ce207e)


![451441724_1049285763296091_1651136581644992249_n](https://github.com/user-attachments/assets/cb2f3cf6-90bc-4353-b183-f7b0f4deb104)


![449820386_518361827215236_9153207559269475400_n](https://github.com/user-attachments/assets/f919864c-99fa-4635-944e-818b14581138)

![452606136_1137072250738168_6154999550015225625_n](https://github.com/user-attachments/assets/00b050b6-0d66-4ce1-8aa8-7ece7377f5ef)

## การดูตัวอย่างโครงงาน เปิด-ปิดไฟ เบื้องต้น เพราะใช้การเชื่อมต่อ อินเตอร์เน็ตเหมือนกัน


![451450632_1009265103980193_6252494825828883293_n](https://github.com/user-attachments/assets/d598b49b-d1fd-4f85-988c-d91dc895bfc9)


![451441736_1191195105338224_3997875858568048924_n](https://github.com/user-attachments/assets/a7e1cd1e-3c76-4953-bd68-7b28a63bf909)


![451622259_369056789544862_7451973126471486584_n](https://github.com/user-attachments/assets/6d82618b-d5dd-43ba-9f96-1dc798004011)


![452246788_1962014040909753_4027006177212838324_n](https://github.com/user-attachments/assets/e47d2297-9430-4811-bd65-fa3b97216c1c)


##  โค้กศึกษา อะดูโน่ ในการเชื่อมต่อ อินเตอร์เน็ต
```cmd
#include <ESP8266WiFi.h>

const char* ssid     = "yourwifi";
const char* password = "12345678";
const char* host = "www.yourwebsite.com";
String url2 = "/button_proc.php";
String url = url2;
String id = "button1_stat";
String value = "";

const int led = 2;

void setup() {
  Serial.begin(115200);
  delay(10);
  pinMode(2, OUTPUT);
  digitalWrite(2, LOW);
 
  Serial.println();
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
 
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(200);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("WiFi connected");
  digitalWrite(2, HIGH);
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

String GetField(String str,int fcount){
 int i=0;
 char ch;
 int len=str.length();
 String str2="";
 while(fcount>=1 and i<len)
 {
  ch=str[i];
  //str2+=ch;
  if(ch!=',' & ch!=' ') {
    str2+=ch;
  }
  else
  {
   fcount--;
   if(fcount>0){
    str2="";
   }
  }
    i++;
 }
 return(str2);
}

String stat="OFF";
String line="";
String line2="";

void loop() {
  url=url2;

  if(stat=="ON"){
     digitalWrite(led,LOW);
  }
  else if(stat=="OFF"){
     digitalWrite(led, HIGH);
  }
  delay(500);
  Serial.println(stat);

  value="?";

  // Use WiFiClient class to create TCP connections
  WiFiClient client;
  const int httpPort = 80;
  if (!client.connect(host, httpPort)) {
    Serial.println("connection failed");
    return;
  }
  // We now create a URI for the request
  url += "?id=" + id;
  url += "&value=" + value;

  // This will send the request to the server
  client.print(String("GET ") + url + " HTTP/1.1\r\n" +
               "Host: " + host + "\r\n" +
               "Connection: close\r\n\r\n");

  url = url2;
  unsigned long timeout = millis();
  while (client.available() == 0) {
    if (millis() - timeout > 5000) {
      Serial.println(">>> Client Timeout !");
      client.stop();
      return;
    }
  }

  // Read all the lines of the reply from server and print them to Serial
  
  while (client.available()) {
    line = client.readStringUntil('\n');
    //Serial.println(line);
    if(char(line[0])=='>'){
      line.trim();
      line2=line;
    }
  }
  stat=GetField(line2,3);
}
```

##  โค้กศึกษา php
``` cmd
<?php
$id=$_GET["id"];
$value=$_GET["value"];
$value=trim($value);
$fname=$id.".txt";

if($value=="?"){
    $f=fopen($fname,"r")or die("Unable to open file!");
    echo fread($f,filesize($fname));
    fclose($f);  
}
elseif($value=="ON" || $value=="OFF")
 {
  $f=fopen($fname,"w");          //don;t append
  fputs($f,"> = ".$value);
  fclose($f);
  //
  $f=fopen($fname,"r")or die("Unable to open file!");
  echo fread($f,filesize($fname));
  fclose($f);
}

?>
```

##  โค้กศึกษา html
```cmd
<html xmlns="http://www.w3.org/1999/xhtml" lang="th" xml:lang="th">
<head>
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>
<h1><p>
    LED = <span id="led-state">__</span></p>
</h1>
<button onclick="toggleLED()"> กดปุ่ม </button> 
<br>
  <h4>
      การกดปุ่ม Toggle จะทำให้ไฟ LED ที่อยู่กับอุปกรณ์ <br>
      NodeMcu ติดและดับจริงๆ 
  </h4>
</body>
  
<script> 
var nextStat="?";
var stat="";
var reqStat="?";
var id="button1_stat";
var polling = setInterval(refleshDataNew, 800);

function toggleLED()
{
  console.log("button was clicked!");
  var xhr = new XMLHttpRequest();
  var url = "button1_proc.php?id="+id+"&value="+reqStat;
  xhr.responseType = 'text';

  xhr.onreadystatechange = function() 
  {
    if (this.readyState == 4 && this.status == 200) 
    {
      stat = this.responseText;
      if(stat=="> = ON")
       {
         nextStat="OFF";
         stat="ON"
       }
      else if(stat=="> = OFF")
       {
         nextStat="ON";
         stat="OFF"
       } 
     document.getElementById("led-state").innerHTML = stat; 
     reqStat=nextStat; 
   }
 }
  
  xhr.open("GET", url, true);
  xhr.send(); 
}
   
function refleshDataNew()
  {
    reqStat="?"  ;
    toggleLED();
  }  
 
document.addEventListener('DOMContentLoaded', toggleLED(), false); 
</script>
</html>
```
## ไดร์โค้ด
https://drive.google.com/drive/folders/1Cx6Dg8cA_dh96EwQfjODonTkhioHelQq

![451738052_8459339777411729_7512731771053446580_n](https://github.com/user-attachments/assets/d65ede91-3b15-4658-bb7a-0d5eb5d16963)

![451454614_1884124722086102_475948060001693463_n](https://github.com/user-attachments/assets/46398f2d-c014-42f0-b272-49257859cfae)


## ช่องยูทูป
https://youtu.be/ooBk5fZxgdQ
