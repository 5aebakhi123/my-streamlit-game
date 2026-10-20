import random
import streamlit as st

st.title("🎮 Game Đoán Số Bí Mật")

# Khởi tạo trạng thái game
if "target" not in st.session_state:
  st.session_state.target = random.randint(1, 100)
  st.session_state.guesses = 0

st.write("Tôi đã chọn một số từ 1 đến 100. Bạn hãy đoán xem đó là số mấy?")

# Nhập số dự đoán
guess = st.number_input(
    "Nhập số của bạn:", min_value=1, max_value=100, step=1
)

if st.button("Đoán"):
  st.session_state.guesses += 1
  if guess < st.session_state.target:
    st.warning("Số quá nhỏ! Hãy thử số lớn hơn.")
  elif guess > st.session_state.target:
    st.warning("Số quá lớn! Hãy thử số nhỏ hơn.")
  else:
    st.success(
        f"🎉 Chính xác! Bạn đã đoán đúng số {st.session_state.target} sau"
        f" {st.session_state.guesses} lần thử."
    )
    if st.button("Chơi lại từ đầu"):
      st.session_state.target = random.randint(1, 100)
      st.session_state.guesses = 0


      st.rerun()
      
