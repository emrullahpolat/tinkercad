#tinkercad ile arduino sayı tahmin uygulaması kaynak kodları


#include <LiquidCrystal.h>

#include <Keypad.h>

long tahmin = 0;
long sayi;
char buton;
int i;

//Keypad kısmı
const byte satir = 4;
const byte sutun = 4;

char tus_takimi [satir][sutun] = {
  {'1','2','3'},
  {'4','5','6'},
  {'7','8','9'},
  {'0','0','='}
};

byte satir_pinleri[satir] = {A0,A1,A2,A3};
byte sutun_pinleri[sutun] = {A4,A5,2,3};
//Keypad map işlemi ile tuşlar tanıtılıyor
Keypad tuslar = Keypad(makeKeymap(tus_takimi), satir_pinleri,
                       sutun_pinleri, satir, sutun);

int rs=6, en=7, d4=11, d5=10, d6=9, d7=8;
LiquidCrystal lcd(rs,en,d4,d5,d6,d7);

void setup()
{
  //lcd ekran başlatılıyor
  lcd.begin(16,2);
  lcd.print("Sayı Tahmin Oyunu");
  delay(2000);
  lcd.clear();
  lcd.begin(16,2);
  //random sayı üretimi
  sayi = random(1,100);
}

void loop()
{
  
    while(1){
       //sayı için rakamlar isteniyor
       buton = tuslar.getKey(); //buton okuması
       if(i>=5){
            lcd.print("hakkınız doldu");
            break;
        }
       
       if(buton == '='){
            i++;
            if(tahmin > 100 && tahmin <=0){
                    lcd.print("0-100 arası sayı giriniz");
                    tahmin = 0;
                    delay(1000);
                    lcd.clear();
                    break;
            }else if(sayi > tahmin){
                    lcd.print("Daha Buyuk");
                    tahmin = 0;
                    delay(1000);
                    lcd.clear();
                    break;
            }else if(sayi < tahmin){
                    lcd.print("daha kucuk");
                    tahmin = 0;
                    delay(1000);
                    lcd.clear();   
                    break;         
            }else if(sayi == tahmin){
                    lcd.print("tebrikler bildiniz !!");
                    break;
            }
       }
    
       if(buton >= '0' && buton <= '9'){     
             tahmin = tahmin*10 + (buton - '0');
             lcd.setCursor(0,1);
             lcd.print(tahmin);
             
       }
           
   }//while kapanıs
 
}//loop kapanıs
