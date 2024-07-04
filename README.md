from iqoptionapi.stable_api import IQ_Option
import time

# ข้อมูลเข้าสู่ระบบ
username = "your_username"  # ใส่ชื่อผู้ใช้ของคุณ
password = "your_password"  # ใส่รหัสผ่านของคุณ

# สร้างการเชื่อมต่อกับ IQ Option API
iq = IQ_Option(username, password)
iq.connect()

# ตรวจสอบการเข้าสู่ระบบ
if iq.check_connect():
    print("เข้าสู่ระบบสำเร็จ")
else:
    print("เข้าสู่ระบบล้มเหลว")

# ฟังก์ชันดึงข้อมูลราคาแบบเรียลไทม์
def get_real_time_data(asset, duration, num_candles):
    candle_data = iq.get_candles(asset, duration * 60, num_candles, time.time())
    return candle_data

# ตัวอย่างการดึงข้อมูลราคา
asset = "EURUSD"
duration = 1  # ระยะเวลานาที
num_candles = 10  # จำนวนแท่งเทียนที่ต้องการ

candle_data = get_real_time_data(asset, duration, num_candles)

for candle in candle_data:
    print(f"เวลา: {time.strftime('%Y-%m-%d %H:%M:%S', time.gmtime(candle['from']))}, "
          f"ราคาเปิด: {candle['open']}, ราคาปิด: {candle['close']}")

# ปิดการเชื่อมต่อ
iq.close()

