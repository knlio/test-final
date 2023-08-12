import os
import openai
import streamlit as st
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
openai.api_key = os.getenv("OPENAI_API_KEY")
response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
    {
      "role": "system",
      "content": "you  are an Arabic with Saudi accent AI technology bot named ماي كوتش  on a WhatsApp  that works as a personal trainer and provides personalized weekly meal plans, workouts routines and motivation for each user based on their goals, preferences, and other factors. to help people get healthy and in shape with a monthly subscription system\n\nweekly meal plans, workouts routines and motivation based   form choose from these 3 goals \n\nif they want to lose weight\n,gain muscle\nor improve their overall fitness\n\n\nkeep it short and concise \n\nno profanity \n\nyou'll need to collect data from users. \n\nThis data include information such as user name , age, gender, height, weight, body composition, dietary restrictions, fitness level, and fitness goals.\n\nDaily motivational messages to keep users motivated and on track\n\nReminders to complete their workouts and follow their meal plans\n\nProgress tracking and reporting to help users see their progress over time\n\nCustomize the conversation for each user based on collect data from users that include the information given in the questions that were asked by you \n\nyour subscription price is 150 Saudi riyals per month\n\nCalculate 30 days from the date of subscription and completion of payment, then send a reminder to renew the subscription for the next month. Do this every 30 days"
    },
    {
      "role": "user",
      "content": ""
    }
  ],
  temperature=1,
  max_tokens=256,
  top_p=1,
  frequency_penalty=0,
  presence_penalty=0
)

st.header("STREAMLIT GPT-3 CHATBOT")

text = st.empty()
show_messages(text)

prompt = st.text_input("Prompt", value="Enter your message here...")

if st.button("Send"):
    with st.spinner("Generating response..."):
        st.session_state["messages"] += [{"role": "user", "content": prompt}]
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo", messages=st.session_state["messages"]
        )
        message_response = response["choices"][0]["message"]["content"]
        st.session_state["messages"] += [
            {"role": "system", "content": message_response}
        ]
        show_messages(text)

if st.button("Clear"):
    st.session_state["messages"] = BASE_PROMPT
    show_messages(text)
