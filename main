
unsigned long signa,t1,t2;   //time for which button is pressed
int inputPin = 3;                 //input pin for push button
int ledPin = 5;                   //outpu pin for LED
String code = "";               //string in which one alphabet is stored
String ip = "";

void setup() 
  {
    Serial.begin(9600);
    pinMode(inputPin, INPUT_PULLUP); //internal pullup resistor is used to simplify the circuit
    pinMode(ledPin,OUTPUT);
  }

void loop()
  {
  NextMorse:
    while (digitalRead(inputPin) == HIGH) {}
    t1 = millis();                            //time at button press
    digitalWrite(ledPin, HIGH);//LED on while button pressed
    
    while (digitalRead(inputPin) == LOW) {}
    t2 = millis();                            //time at button release
    digitalWrite(ledPin, LOW);                //LED off on button release
    
    signa = t2 - t1;                     //time for which button is pressed
    if (signa > 50)                      //to account for switch debouncing
      {
        code += readio();                       //function to read dot or dash
      }
    while ((millis() - t2) < 500)           //if time between button press greater than 0.5sec, skip loop and go to next alphabet
      {     
        if (digitalRead(inputPin) == LOW)
          {
            goto NextMorse;
          }
      }
    conv();           //function to decipher code into alphabet
    //Serial.println(ip);
  }

char readio()
  {
    if (signa < 500 && signa > 50)
      {
        return '.';                        //if button press less than 0.5sec, it is a dot
      }
    else if (signa > 500)
      {
        return '-';                        //if button press more than 0.5sec, it is a dash
      }
  }

void conv()
  {
    static String letters[] = {".-", "-...", "-.-.", "-..", ".", "..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--", "-.", "---", ".--.", "--.-",
                               ".-.", "...", "-", "..-", "...-", ".--", "-..-", "-.--", "--..", "WOW"};
    int i = 0;
    if (code == ".-.-.-")
      {
        //Serial.print(".");        //for break
        ip = ip+".";
      }
    else
      {
        while (letters[i] != "WOW")  //loop for comparing input code with letters array
          {
            if (letters[i] == code)
              {
                Serial.print(char('A' + i));
                ip=ip+(char('A'+i));
                break;
              }
              i++;
          }
        //if (letters[i] == "E")
          //{
            //Serial.println("<Wrong input>");  //if input code doesn't match any letter, error
          //}
      }
    code = "";                            //reset code to blank string
  }
