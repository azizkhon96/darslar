# Heading1

Bu oddiy paragraph 



`Ths is code `

| N    | Ism familiya      | ikkinchi maydon |
| ---- | ----------------- | --------------- |
| 1    | Azizxon Avazxonov |                 |
| 2    |                   |                 |
| 3    |                   |                 |

#### **Shell script ahamiyati**

- Qayta-qayta bajariladigan ishlarni soddalashtirish
- Buyruqlar tarixini saqlash
- Instruksiyalarni ulashish
- Mantiqiy buyruqlarni & Sikllarni  amalga oshirish

**Shell script** — bu **shell** komandalarini ketma-ket yozilgan holda faylga yozilgan dastur bo‘lib, uni ishga tushirganda kompyuter har bir buyruqni ketma-ket bajaradi.

**Shell vs Bash vs Sh**

`Shell`   —  umumiy tushuncha bo'lib, u user va OS orasidagi interface. Shell foydalanuvchining buyruqlarini olib, ularni interpretatsiya qiladi, operatsion tizimga bajarish uchun uzatadi. Shellning quyidagi turlari bor: `sh, bash, zsh, fish, ksh`

`sh` — Bourne shell. Standart shell deb qaraladi, deyarli barcha tizimlarda mavjud.

`bash` — Bourne Again Shell. `sh`ning zamonaviy, rivojlangan versiyasi. Linuxdagi default shell turi.

#### **Bash da birinchi skript**

nano `my-script.sh`

```plaintext
#!/bin/bash

echo Serverni sozlash
chmod u+x my-script.sh
./my-script.sh
```

#### O'garuvchilar(Variables) 1-qism:

**O'zgaruvchini yaratish**

Sintatsis:

```plaintext
var_nomi=qiymat
```

**Qoidalar**:

- Katta-kichik harlar farqi: var ≠ Var

- = dan avval va keyin bo'sh joy bo'lmaslik. Xato: var_nomi = qiymat

- o'zgaruvchi nomida harflar,raqamlar va _ bu belgidan foydalanish. Raqam boshida kelmaslik kerak:

  ```plaintext
  HABAR="Salom Dunyo"
  HABAR_2=Salom
  RAQAM=1
  PI=3.142
  Yana_PI="3.142"
  Aralash=123abc
  ```

**O'zgaruvchi qiymatini chaqirish**

sintaksis:

```plaintext
echo $var_nomi
```

Qoidalar:

- Agar variable yaratilmagan bolsa , uni chop etishda xatolik yuz bermaydi, shunchaki bo'sh qiymat chop etiladi.
- Shell o'zgaruvchilarni string holatida saqlaydi, ammo ishga tushirishda o'zgaruvchilar o'z tiplariga mos holda ishlaydi:

```plaintext
~ x="hello"
~ expr $x + 1
expr: non-numeric argument
```

- O'zgaruchini chop etishda qo'shtirnoqdan foydalanish mumkin, ammo birtirnoqdan foydalanib bo'lmaydi

  ```plaintext
  echo "$VAR"   #Tog'ri sintaksis
  echo '$VAR'   #Xato sintaksis
  ```

- O'zgaruvchi qiymatini chaqirishdan ${} gulli qavslardan ham foydalanish mumkin, bu asosan ularni boshqa matnlardan ajratishda qo'llaniladi.

  ```plaintext
  nom=devops
  echo "File: ${nom}_hisobot"   #Tog'ri sintaksis
  echo "File: $nom_hisobot"     #Xato sintaksis
  ```

- Buyruq natijasini var ga o'zlashtirish

  ```plaintext
  var=$(buyruq)
  ```

**O'zgaruvchini o'chirish**

```plaintext
unset MYVAR
```

**User Input**

**read -** O'zgaruvchiga qiymatni kiritish (input) orqali beradi

```plaintext
read -p "Ismingizni kiriting" ISM
```

[OPTIONS]

-p - prompt chiqarish

-s - Ko'rinmas input

**O'zgaruvchi chegarasi(Variable Scope)**

Odatda variable faqat shu shell ga tasir qiladi, sub shell larga tasir qilmaydi. Agar uni ichki shell larga tasir qilishi xoxlasak export kalit so'zidan foydalaniladi.

```plaintext
export MYVAR="Salom" 
```

Script tugatilganidan keyin o'zgaruvchilar ham o'chiriladi, agar biz script tugatilgandan keyin ham o'zgaruvchini saqlab qolishni istasak source yoki . . dan foydalanamiz:

```plaintext
. ./myvar2.sh
source ./myvar2.sh
```

------

**Afirmetik Operatorlar**

Bash (( )) arifmetika uchun eng ommabop va butun sonlar uchun.

```plaintext
((a=3+4))
```

**Uning bazaviy amallari:**

\+ (Qo'shish), - (Ayrish), * (Ko'paytirish) , / (Butun bo'lish), % (Qoldiq), ** (Daraja)

**Taqqoslash operatori**

```plaintext
((5 < 10))     #true
```

== (Teng), != (Teng emas), < (Kichik) , > (Katta), <= (Kishik yoki Teng), >= (Katta yoki teng)

**Qo‘shimcha operatorlar:**

++, --, +=, -=, *=, :=, %=

```plaintext
((a=3, a++))    #a=4
((b=6, b += 3)  #b=9
```

**Mantiqiy operatorlar:**

&& (VA), || (YOKI), ! (INKOR)

```plaintext
((3<5 && 6>5))  #True
((!(5=3)))      #True
```

**Eslatma**: () qavs ifodani guruhlaydi, "," vergul bir nechta ifodani bir biridan ajratadi

------

**Shart operatorlari (Conditionals)Shart operatorlari (Conditionals)**

Bash-dagi shart operatorlari ma'lum shartlar to'g'ri yoki noto'g'ri ekanligiga qarab skriptingiz oqimini boshqarishga imkon beradi.

Bu sizga buyruqlarni qabul qilish, malum bir kod bloklarini bajarish va turli senariylarni dinamik tarzda boshqarish imkonini beradi.

**if** :

```plaintext
if [ ifoda ]
then
    # ifoda Rost qiymat bersa bajariladigan kodlar
fi
```

Namuna:

```plaintext
if test "$string1" = "$string2"; then
    echo "Stringlar bir xil"
fi
```

**if-else** :

```plaintext
if [[ -f "myfile.txt" ]]; then
    echo "'myfile.txt' deb nomlagan fayl mavjud"
else
    echo "'myfile.txt' deb nomlangan fayl mavjud emas"
fi
```

**if-elif-else**:

```plaintext
if [ $number -gt 0 ]; then
    echo "Raqam musbat son"
elif [ $number -lt 0 ]; then
    echo "Raqam manfy sonlarga kiradi"
else
    echo "Raqam 0 ga teng"
fi
```

**Ko'p ishlatiladigan SHART ifodalari va ularga namunalar:**

Stringlarni taqqoslash:

- `=`: String tengligi
- `!=`: String teng emasligi

Stringlarni testlash:

- `-z`: String bo'sh

- `-n`: String bo'sh emas

  Namuna:

  ```plaintext
  read -p "Ismingizni kiring : " name
  if [ -z "$name" ]; then
      echo "Siz ismingizni kiritmadingiz"
  fi
  ```

Raqamlarni taqqoslash:

- `-eq`: Equal (Teng)

- `-ne`: Not equal (Teng emas)

- `-gt`: Greater than (dan Katta)

- `-ge`: Greater than or equal (Katta yoki Teng)

- `-lt`: Less than (dan Kichik)

- `-le`: Less than or equal (Kichik yoki Teng)

  Namuna:

  ```plaintext
  if [ $number -gt 10 ]; then
      echo "Nomer 10 dan katta"
  fi
  ```

Filelarni testlash:

- `-e`: File exists (Borlikka tekshirish)

```plaintext
if [[ ! -z "$string" ]]; then
    echo "String pustoy emas."
fi
```

**Amaliy misol:**

1. Inson yoshini kiritganda uni ishlash yoshidaligi yoki emasligini chop etish
2. Kiritilgan sonni musbat, manfiy yoki 0 ga tengligini aniqlash

------

#### Loops

Agar biz biror taskni 20 marta takrorlashimiz kerak bo'lsa 20 qator kod yozishimiz shart emas, bunday paytda **for** va **while** takrorlash operatorlaridan foydalanish mumkin.

**for loops**

Sintaksis:

```plaintext
for narsa in royxat
do
  komanda1
  komanda2
done
```

**narsa** - royxat ichidagi har bir elementni qiymatini oladigan o'zgaruvchi

**royxat** - orasida probeldan iborat narsalar: so'z, nomer, fayl ...

Namuna1:

```plaintext
#!/bin/sh
for i in 1 2 3 4 5
do
  echo "Looping ... number $i"
done
```

Namuna2:

```plaintext
#!/bin/sh
for i in hello 1 * 2 goodbye 
do
  echo "Looping ... i is set to $i"
done
```

!!! *Ushbu kodni ishga tushiring va ni nima ma'no aks etganini ko'rishimiz mumkin, agar biz \* ni manosini o'zgartirmochi bo'lsak qo'shtirnoq yoki Escape belgisidan foydalanishimiz mumkin.*

```plaintext
for runlevel in 0 1 2 3 4 5 6 S
do
  mkdir rc${runlevel}.d
done
```

in bash:

```plaintext
mkdir rc{0,1,2,3,4,5,6,S}.d
```

**Raqamlar oralig'ida takrorlash**

```plaintext
for i in {1..10}              #{start..end..step}  bash4.0+   #{} ichida var ni qabul qimaydi
do
  echo "Number: $i"
done
```

**Amaliy misol:** 10 dan 20 gacha bo'lgan toq sonlarni chot etish

**Direktoriya ichidagi fallar orqali takrorlash**

```plaintext
for file in $(ls)
do
  echo "File: $file"
done
```

yoki

```plaintext
for file in *.txt
do
   echo "Topildi: $file"
done
```

**Komandani natijasidagi so'zlar boyicha takrorlash:**

```plaintext
for i in $(cat file.txt)
do
   echo "Topildi: $file"
done
```

**continue**

`continue`: Joriy takrorlashni o'tkazib yuboradi va ro'yxatdagi keyingi elementga o'tadi.

```plaintext
for i in 1 2 3 4 5
do
  if [[ $i -eq 3 ]]; then
    continue
  fi
  echo "Number: $i"
done
```

**break**

`break`: bu operator loop dan darxol chiqib ketish uchun ishlatiladi.

```plaintext
#!/bin/bash

target_file="important_document.txt"

for file in $(ls) 
do
  if [[ "$file" == "$target_file" ]]; then
    echo "Found the file: $file"
    break 
  fi
done
```

------

#### **while loops**

Sintaksis:

```plaintext
while shart; do
  # ushbu komanda shart True bolganda davom etaveradi
done
```

Namuna1:

```plaintext
raqam=0
while [ $raqam -lt 5 ]; do
  echo "Raqam: $raqam"
  ((raqam++))
done
```

Namuna2:

```plaintext
#!/bin/bash
input=salom
while [ "$input" != "hayr" ]
do 
  echo "Nimadur yozing (chiqish uchun hayr deb yozing)"
  read input
  echo "Siz yozdingiz: $input"
done
```

!!!*Bu yerda [ ] qavs va != belgilari va boshqa argumentlar orasida probel bo'lishi shart.*

Namuna3. Cheksiz takrorlash:

```plaintext
#!/bin/sh
while :
do
  echo "Biror narsa yozing (^C to quit)"
  read INPUT
  echo "Siz yozdingiz: $INPUT"
done
```

Namuna4. Fayl bilan ishlash.

```plaintext
count=0
while read -r qator; do
    ((count++))
    echo "${count}. $qator"
done < qatorlar.txt
```

*! read -r (bu option \ belgisini matn deb biladi)*

**Amaliy script**: Internet borligini doim tekshirib turish, internet borligida har 2 sekunda"Internet UP", uzilgan paytda "Internet Down" chop etsin.

**Amaliy script:** Biror nomladagi faylni yaratilishi kutadigan script yaratish. Agar fayl yaratilsa fayl topildi deb ekranga chop etish.

**Amaliy misol:** 60 dan 0 gacha teskari sanoq, har sekundda

------
