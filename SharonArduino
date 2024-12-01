#include <ESP8266WiFi.h>
#include <ESP8266HTTPClient.h>
#include <ArduinoJson.h>
#include <DFRobotDFPlayerMini.h>
#include <SoftwareSerial.h>
#include <Servo.h> 
#include <DFRobotDFPlayerMini.h>

Servo myservo; 
int pos = 0;                                        
int servoPin = 14;  

SoftwareSerial mySerial(12,13); // mp3 RX, TX
DFRobotDFPlayerMini myDFPlayer;
// WiFi 네트워크 설정
const char* ssid = ".";          // 연결할 WiFi SSID
const char* password = "20051025";  // WiFi 비밀번호

// 서버 정보 설정
const char* host = "sharonproject.ddns.net";  // Node.js 서버의 IP 주소
const int port = 5522; 

void setup() {
  pinMode (servoPin, OUTPUT);           
  myservo.attach(14, 500, 2500); 
  myservo.attach(14);                                
  Serial.begin(115200);
  mySerial.begin(9600);

  if (!myDFPlayer.begin(mySerial)) {    
    Serial.println("DFPlayer communication failed!!!!!!");
    while(true);
  }
  Serial.print("DFPlayer Mini 가 연결되었습니다.");
  myDFPlayer.volume(20);
  
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid,password); // WiFi 접속

  // WiFi 연결 대기
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
    Serial.print("Wi-Fi 연결중!... \n");
  }
  Serial.println();
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  sendGetRequest();
  delay(20);
}

void sendGetRequest() {
  if (WiFi.status() == WL_CONNECTED) { // WiFi가 연결된 경우에만 요청 전송
    WiFiClient client; // WiFiClient 객체 생성
    HTTPClient http;   // HTTPClient 객체 생성

    char url[100];
    snprintf(url, sizeof(url), "http://%s:%d/ard", host, port);  // url 문자열 생성 최적화
    http.begin(client, url); // 변경된 begin 함수: WiFiClient와 URL 전달
    int httpCode = http.GET(); // GET 요청 전송
    delay(1);

    if (httpCode > 0) { // 요청이 정상적으로 전송된 경우
      String payload = http.getString(); // 서버로부터의 응답을 받음
      Serial.println(payload); // 응답 내용을 출력

      // 받은 데이터가 JSON 형식이라면 파싱
      StaticJsonDocument<200> doc; 
      DeserializationError error = deserializeJson(doc, payload);
      if (!error) {
        handleActivity(doc);
      } else {
        Serial.println("Failed to parse JSON");
      }
    } else {
      Serial.print("Error on HTTP request: ");
      Serial.println(httpCode);
    }
    
    http.end(); // 요청 종료
  } else {
    Serial.println("WiFi Disconnected");
  }
}

void handleActivity(JsonDocument& doc) {
  String doCode = doc["do"].as<String>();
  String voiceCode = doc["voiceCode"].as<String>();
  float voiceSpeed = doc["voiceSpeed"].as<float>();

    Serial.print("docode is \n");
    Serial.println(doCode);
    int rcode=0;
    int rvcode=1;
    int time= 0;
    if(doCode=="00"){
      rcode=0;
    }
    else if(doCode=="010"){
      rcode=1;
    }
    else if(doCode=="020"){
      rcode=2;
    }
    else if(doCode=="030"){
      rcode=3;
    }
    else if(doCode=="040"){
      rcode=4;
    }
    else if(doCode=="050"){
      rcode=5;
    }
    else if(doCode=="060"){
      rcode=6;
    }
    else if(doCode=="0240"){
      rcode=24;
    }
    else{
      rcode=404;
    }
    //Serial.print("rcode is \n");
    //Serial.print(rcode);
    Serial.print("\n");
    switch (rcode) {
      case 0:{
        //아무 행동 없음
        //Serial.println("아무 행동 없음");
        break;
        }
      case 1:{
        WiFiClient client; 
        HTTPClient http;

        Serial.println("게임 시작: 초기화 및 카운트다운 진행");

        myservo.write(0);

        myDFPlayer.playMp3Folder(24);

        char url[100];
        snprintf(url, sizeof(url), "http://%s:%d//ardIsVoicing", host, port);
        http.begin(client, url);
        http.GET();
        
        delay(4000);
        snprintf(url, sizeof(url), "http://%s:%d//ardIsNotVoicing", host, port);
        http.begin(client, url); 
        http.GET();
        break;
      }
      case 2:{
        WiFiClient client; 
        HTTPClient http;
        if(voiceCode=="8"){
        rvcode=8;
        time=(6000-650);
      }
      else if(voiceCode=="9"){
        rvcode=9;
        time=(5000-650);
      }
      else if(voiceCode=="10"){
        rvcode=10;
        time=(4285-650);
      }
      else if(voiceCode=="11"){
        rvcode=11;
        time=(3750-650);
      }
      else if(voiceCode=="12"){
        rvcode=12;
        time=(3333-650);
      }
      else if(voiceCode=="13"){
        rvcode=12;
        time=(3000-650);
      }
      else if(voiceCode=="14"){
        rvcode=14;
        time=(2727-650);
      }
      else if(voiceCode=="15"){
        rvcode=15;
        time=(2500-650);
      }
      else if(voiceCode=="16"){
        rvcode=16;
        time=(2307-650);
      }
      else if(voiceCode=="17"){
        rvcode=17;
        time=(2142-650);
      }
      else if(voiceCode=="18"){
        rvcode=18;
        time=(2000-650);
      }
      else if(voiceCode=="19"){
        rvcode=19;
        time=(1875-650);
      }
      else if(voiceCode=="20"){
        rvcode=20;
        time=(1764-650);
      }
      else if(voiceCode=="21"){
        rvcode=21;
        time=(1666-650);
      }
      else if(voiceCode=="22"){
        rvcode=22;
        time=(1578-650);
      }
      else{
        rvcode=23;
        time=(1500-650);
      }
      
        Serial.println("벽바라봄");
        myservo.write(180);  
        delay(650);

        Serial.println("음성재생");
        myDFPlayer.playMp3Folder(rvcode);  

        char url[100];
        snprintf(url, sizeof(url), "http://%s:%d//ardIsVoicing", host, port);
        http.begin(client, url); 
        http.GET();

        Serial.println(rvcode);
        Serial.println("\n");
        Serial.println(time);

        delay(time);
        myservo.write(0);
        delay(650);

        snprintf(url, sizeof(url), "http://%s:%d//ardIsNotVoicing", host, port);
        http.begin(client, url); 
        http.GET();
        Serial.println("플레이어 바라봄");

        break;

      }
      case 3:{
        Serial.println("모터를 회전하여 벽을 바라봄");
        myservo.write(180);                         
        delay(50);
        break;
      }
      case 4:{
        Serial.println("모터를 회전하여 플레이어를 바라봄");
        if(voiceCode=="8"){
        rvcode=8;
        time=6000;
      }
      else if(voiceCode=="9"){
        rvcode=9;
        time=5000;
      }
      else if(voiceCode=="10"){
        rvcode=10;
        time=4285;
      }
      else if(voiceCode=="11"){
        rvcode=11;
        time=3750;
      }
      else if(voiceCode=="12"){
        rvcode=12;
        time=3333;
      }
      else if(voiceCode=="13"){
        rvcode=12;
        time=3000;
      }
      else if(voiceCode=="14"){
        rvcode=14;
        time=2727;
      }
      else if(voiceCode=="15"){
        rvcode=15;
        time=2500;
      }
      else if(voiceCode=="16"){
        rvcode=16;
        time=2307;
      }
      else if(voiceCode=="17"){
        rvcode=17;
        time=2142;
      }
      else if(voiceCode=="18"){
        rvcode=18;
        time=2000;
      }
      else if(voiceCode=="19"){
        rvcode=19;
        time=1875;
      }
      else if(voiceCode=="20"){
        rvcode=20;
        time=1764;
      }
      else if(voiceCode=="21"){
        rvcode=21;
        time=1666;
      }
      else if(voiceCode=="22"){
        rvcode=22;
        time=1578;
      }
      else{
        rvcode=23;
        time=1500;
      }
        delay(time);
        myservo.write(0);                                                        
        break;
      }
      case 5:{
        Serial.println("제한 시간으로 인해 게임 종료");
        WiFiClient client; 
        HTTPClient http;

        char url[100];
        snprintf(url, sizeof(url), "http://%s:%d//ardIsVoicing", host, port);
        http.begin(client, url); 
        http.GET();
        
        myDFPlayer.playMp3Folder(5);  
       
        delay(3000);
        snprintf(url, sizeof(url), "http://%s:%d//ardIsNotVoicing", host, port);
        http.begin(client, url); 
        http.GET();
        break;
      }
      case 6:{
        Serial.println("남은 플레이어가 없어 게임 종료");
        WiFiClient client; 
        HTTPClient http;
        
        char url[100];
        snprintf(url, sizeof(url), "http://%s:%d//ardIsVoicing", host, port);
        http.begin(client, url); 
        http.GET();

        myDFPlayer.playMp3Folder(6);  
        
        delay(2000);
        snprintf(url, sizeof(url), "http://%s:%d//ardIsNotVoicing", host, port);
        http.begin(client, url); 
        http.GET();
        break;
      }
      default:{
        Serial.println("알 수 없는 행동 코드");
        break;
      }
  }
}
