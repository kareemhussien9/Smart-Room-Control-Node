# Smart-Room-Control-Node
A smart IoT-based room monitoring system that reads temperature, humidity, motion, and battery status, then makes automatic decisions to control actuators such as fans, dehumidifiers, lights, and alarms. The project simulates real sensor behavior using Python conditionals and prints clear command outputs that represent actual IoT device actions.


temp_c = float(input("Temperature sensor reading C ? ")) #قراءه درجه حراره
humidity = float(input("Humidity sensor reading (%)? ")) #قراءة نسبة الرطوبة
motion = input("PIR motion sensor reading (yes/no)? ") == "y" #هل هناك حركة

print("Hot" if temp_c >= 30 else "not Hot") #طباعة اذا كانت درجة الحراره عاليه ام لا
print("Humid" if humidity >= 70 else "not Humid") #طباعة اذا كانت نسبة الرطوبة عاليه ام لا
print("Motion detected" if motion else "No motion detected") #طباعة اذا كانت هناك حركة ام لا

temp_c = float(input("Enter temperature (C): ")) #درجة الحراره
if temp_c >= 40: 
    print("ALERT: Overheat!") #تنبيه: ارتفاع درجة الحرارة
    print("CMD:FAN=HIGH") #امر: مروحة عالية
    print("CMD:ALARM=ON") #امر: تشغيل الانذار

elif temp_c >= 30:
    print("Warm") #دافئ
    print("CMD:FAN=MEDIUM") #امر: مروحة متوسطة

elif temp_c >= 20:
    print("Comfort") #مريح
    print("CMD:FAN=LOW") #امر: مروحة منخفضة
else:
    print("Cold") #بارد
    print("CMD:HEATER=OFF") #امر: إيقاف السخان

humidity = float(input("Humidity %: ")) #نسبة الرطوبة
window_open = input("Is window open? (y/n): ") == "y" #هل النافذة مفتوحة

if humidity >= 65 and not window_open: #اذا كانت نسبة الرطوبة عاليه والنافذة مغلقة
    print("CMD:DEHUMIDIFIER=ON") #امر: تشغيل مزيل الرطوبة
else:
    print("CMD:DEHUMIDIFIER=OFF") #امر: إيقاف مزيل الرطوبة

mode = input("Mode (Auto/Manual/Off): ") #وضع التشغيل
print(mode == "auto") #طباعة اذا كان الوضع تلقائي ام لا

status = input("Enter alarm status (alert/ok): ") #حالة الانذار
if status == "alert": #اذا كانت الحالة تنبيه
    print("CMD:ALARM=ON") #امر: تشغيل الانذار
else:
    print("CMD:ALARM=OFF") #امر: إيقاف الانذار

motion = input("Motion detected? (y/n): ") #هل تم الكشف عن حركة
hour = int(input("Hour (0-23): ")) #الساعة

if motion:
    if 23 <= hour or hour < 6: #اذا كانت الساعة بين 11 مساءً و 6 صباحًا
        print("Night motion") #طباعة حركة ليلية
        print("CMD:LIGHTS=ON(DIM)") #امر: تشغيل الأضواء (خفيفة)
        print("LOG:EVENT") #تسجيل الحدث
    else:
        print("Day motion") #طباعة حركة نهارية
        print("LOG:EVENT") #تسجيل الحدث
else:
    print("No motion.") #طباعة لا توجد حركة

soc = float(input("Battery state-of-charge % (0-100): ")) #حالة شحن البطارية

if soc > 100 or soc < 0: #اذا كانت حالة الشحن غير صالحة
    print("Invalid SoC.") #طباعة حالة شحن غير صالحة
elif soc >= 80: #اذا كانت حالة الشحن بين 80 و 100
    print("Battery grade: A") #طباعة درجة البطارية: A
elif soc >= 60: #اذا كانت حالة الشحن بين 60 و 79
    print("Battery grade: B") #طباعة درجة البطارية: B
elif soc >= 40: #اذا كانت حالة الشحن بين 40 و 59
    print("Battery grade: C") #طباعة درجة البطارية: C
elif soc >= 20: #اذا كانت حالة الشحن بين 20 و 39
    print("Battery grade: D") #طباعة درجة البطارية: D
else: #اذا كانت حالة الشحن اقل من 20
    print("Battery grade: E (critical)") #طباعة درجة البطارية: E (حرجة)

