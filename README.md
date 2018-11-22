# Android_LuggagePastPickApp

# 어플 소개

sw융합 해커톤에 출품한 작품\

개발 플랫폼 : 안드로이드 스튜디오, Firebase, Google Spreadsheet

개발 개요

RFID를 이용하여 수하물 예상 도착 알림 서비스 어플리케이션

개발 필요성 : 수하물용 비행기가 연착이 되어서 무한정 기다리게 되면서 생각하게 된 아이디어

타겟 : 연착된 비행기를 기다리는 사람

상세내용

항공사에서 RFID를 등록한 후 어플리케이션 사용자에게 태그를 주면 사용자는 그 태그를 이용하여 어플리케이션에 자동으로 로그인한다.

이때 항공사에서 등록되지 않은 태그는 로그인이 되지 않는다.

수하물이 비행기에서 내리면서 태그가 리더기에 읽히면 사용자는 수하물이 도착한 정보를 휴대폰으로 알 수 있다.

# 개발환경 관계

nfc에 카드가 태깅되면 spreadsheet에 저장되게한다.

spreadsheet에서 정보를 가져와서 firebase에 저장되게한다.

firebase에서 정보를 가져와서 android의 변수에 저장되게한다. (이 과정을 위해서 이미 파이어베이스를 연결해 놓았다.) 

1.User()

[spreadsheet]

https://docs.google.com/spreadsheets/d/1Ky18cNLftrZCcH0kuFij8dk05H6UuZFmiMSV3MeVAa0/edit?usp=sharing

[script]
function writeDataToFirebase() {
  var sheet = SpreadsheetApp.openById("1Ky18cNLftrZCcH0kuFij8dk05H6UuZFmiMSV3MeVAa0");
  var mysheet = sheet.setActiveSheet(sheet.getSheets()[0]);
  var data = mysheet.getDataRange().getValues();
  var dataToImport = {};
  
  
  var firebaseUrl = "https://vist-rfid.firebaseio.com/";
  var secret = "jDdGbaqymeSbpEgXAty5OHnOI47TDSEqhljxpzRg";
  var base = FirebaseApp.getDatabaseByUrl(firebaseUrl,secret);
  
 
  for(var i = 1; i < data.length; i++) {
    var ID = data[i][1];
    
    dataToImport[ID] = "로그인 필요";
  }
 
  base.setData("User", dataToImport);
}


2.RFID

[spreadsheet]

https://docs.google.com/spreadsheets/d/1_BvT5diDqs2XiD1tvIDaTf_a5EBuOgvmQ2MgfDprU8I/edit?usp=sharing

[script]
function writeDataToFirebase() {
  var sheet = SpreadsheetApp.openById("1_BvT5diDqs2XiD1tvIDaTf_a5EBuOgvmQ2MgfDprU8I");
  var mysheet = sheet.setActiveSheet(sheet.getSheets()[0]);
  var data = mysheet.getDataRange().getValues();
  var dataToImport = {};
  
  
  var firebaseUrl = "https://vist-rfid.firebaseio.com/";
  var secret = "jDdGbaqymeSbpEgXAty5OHnOI47TDSEqhljxpzRg";
  var base = FirebaseApp.getDatabaseByUrl(firebaseUrl,secret);
  
 
  for(var i = 1; i < data.length; i++) {
    var ID = data[i][1];
    var TIME = data[i][2];
    var NUMBER = data[i][3];
    
    dataToImport[ID] = {
      ID : ID,
      TIME : TIME,
      NUMBER : NUMBER
    };
  }
 
  base.setData("rfid", dataToImport);
}


# Youtube 주소

< https://youtu.be/vpl9_RSFvDs >
