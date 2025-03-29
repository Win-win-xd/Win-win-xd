# IQ Option Scalping Script (EMA, Stochastic, CCI, Williams %R)

def check_trade_signal(data):
    ema_fast = ema(data, period=9)
    ema_slow = ema(data, period=21)
    stochastic_k, stochastic_d = stochastic(data, k_period=14, d_period=3)
    cci_value = cci(data, period=14)
    williams_r = williams_percent_r(data, period=14)

    # เงื่อนไขเข้า Buy
    if ema_fast > ema_slow and stochastic_k > stochastic_d and cci_value > -100 and williams_r > -80:
        return "BUY"

    # เงื่อนไขเข้า Sell
    elif ema_fast < ema_slow and stochastic_k < stochastic_d and cci_value < 100 and williams_r < -20:
        return "SELL"
    
    return "NO TRADE"

# ตัวอย่างการใช้งาน
market_data = get_market_data()  # ดึงข้อมูลราคาล่าสุด
signal = check_trade_signal(market_data)
print(f"Trade Signal: {signal}")
