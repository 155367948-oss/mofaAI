import streamlit as st
import random
import json
from collections import defaultdict

st.title("🎯 AI智能选号系统")

# ===== 数据 =====
try:
    with open("data.json","r") as f:
        data = json.load(f)
except:
    data = []

# ===== 模型 =====
def build_model(data):
    freq = defaultdict(int)
    for draw in data:
        for n in draw:
            freq[n] += 1
    return freq

def predict(freq):
    sorted_nums = sorted(freq.items(), key=lambda x:x[1], reverse=True)
    pool = [n for n,_ in sorted_nums[:30]]
    return sorted(random.sample(pool,9))

# ===== UI =====
if st.button("生成今日号码"):
    if len(data) < 5:
        st.warning("数据不足")
    else:
        freq = build_model(data)

        st.subheader("🎯 推荐三组：")
        for i in range(3):
            nums = predict(freq)
            st.success(f"第{i+1}组: {' '.join(map(str,nums))}")
            import requests
import json

def fetch():
    # 👉 换成真实开奖API
    url = "https://example.com/api"

    res = requests.get(url).json()

    data = []
    for item in res:
        nums = item["numbers"]
        data.append(nums)

    with open("data.json","w") as f:
        json.dump(data,f)

if __name__ == "__main__":
    fetch()
    []
    
