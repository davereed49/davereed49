- 👋 Hi, I’m @davereed49
- 👀 Writing a code for a project
- 🌱 I’m currently learning Arduino, keypad, neo pixels
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me .. catchdavereed@gmail.com

<!---
davereed49/davereed49 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
//                           DISCRIPTION OF LED /MONITOR BOARD                           12-30-22

Hi. I'm new to coding. All I know is what I've learned on Paul Mcquarters web sight on Arduino. I have a project in mind and brought a few Arduino Unos and a few other components toward learning about how I would go about this project.
This is a description of the project. First I should explain that I am into day trading. I'm using 3 monitors. one has my brokerage account where I place the entries and the other two are full of streaming charts. One has a list of 27 stocks listed down the edge of the screen that some may change from day to day. Before the session opens I run through the stocks to see which ones look like they're setting up for a play. Some are not in a good range to play profitably at the moment and are disqualified while others are in different stages; maybe an hour away from a good entry point, etc. 
What I would like to have is a narrow board mounted along side the monitor with corresponding numbers and a GBR LED, next to each listed stock. Then I could put a qualifying sign telling me which ones to go back to throughout the session to check up on. Once you get tied up trading one or two you get bogged down in going back through the list to see which ones are setting up for the next play.
I could use a switch of some kind next to each LED but I wouldn't want to do all the wiring, the expense of the switches and I really don't have the room; the ljsted stocks being 9.3 mm apart means the LEDs are 9.3 mm apart. 
Ultimately I would like to have a GUI that I could minimize and maximize to click green, blue, red or off next to each number, to address the corresponding LED.
But for now I would settle for a 4 X 4 keypad, the LED board, and an Arduino Uno. By the way, I'm handy and all so the board and hardware are no problem for me. And I'm getting together all of the components. In fact I think I have them all except the board itself which I'll probably have laser cut somewhere here in Phoenix. Also in my learning journey I've decided to go with GBR neo pixels over LEDs so I won't  have to use shift registers.
So, in a nutshell, I need to make a program that will use a 4 x 4 keypad to turn on a green-blue-red or off, neo pixel next to each of 27 stocks and also turn the whole bunch off when I'm through at the end a the session.
The keypads are written 1 through 0, A, B, C, D, * and #.   I would imagine an entry might be: 12A for green or 27C for red, 27D to turn it back off and *# to shut then all off or something like that.
So if you're into taking on that little challenge please get back with me.   Thanks

So far I've been able to put together this much code. I can enter a key and get a pixel to turn on the right color. I can't trun it off and I can't get it to recognize two and three key comands.

#include <Keypad.h>
#include <FastLED.h>

#define LED_PIN 11
#define NUM_LEDS 30

CRGB leds[NUM_LEDS];



const int ROW_NUM = 4;     //four rows
const int COLUMN_NUM = 4;  //four columns

char keys[ROW_NUM][COLUMN_NUM] = {
  { '1', '2', '3', 'A' },
  { '4', '5', '6', 'B' },
  { '7', '8', '9', 'C' },
  { '*', '0', '#', 'D' }
};

byte pin_rows[ROW_NUM] = { 9, 8, 7, 6 };       //connect to the row pinouts of the keypad
byte pin_column[COLUMN_NUM] = { 5, 4, 3, 2 };  //connect to the column pinouts of the keypad

Keypad keypad = Keypad(makeKeymap(keys), pin_rows, pin_column, ROW_NUM, COLUMN_NUM);

//putting this in (with changes) from Kp Ex #2 PC
const String nunber = "1";
String input_number;
//end

void setup() {
  Serial.begin(9600);
  pinMode(11, OUTPUT);
  FastLED.addLeds<WS2812, LED_PIN, GRB>(leds, NUM_LEDS);

  //Added this from KE #2 PC with change (number)
  input_number.reserve(32);  // maximum input characters is 33, change if needed
                             //end
}

void loop() {


  char key = keypad.getKey();
  //added from KE #2
  if (key) {
    Serial.println(key);
  }
  //end
  if (key) {
    leds[8] = CRGB(0, 255, 0);
    FastLED.show();
    delay(500);
  }

  if (key) {
    leds[4] = CRGB(0, 0, 255);
    FastLED.show();
    delay(500);
  }
}

