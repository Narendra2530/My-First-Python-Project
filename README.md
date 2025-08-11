# My-First-Python-Project
An application of Youtube Script Generetor
My first python application

pip install langchain openai streamlit
import os
os.environ["OPENAI_API_KEY"]="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"
from langchain.chat_models import ChatOpenAI
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

llm= ChatOpenAI (model="gpt-3.5-turbo")

prompt= PromptTemplate(input_variable=["topic"],template="""
          Write a full Youtube video  script on the topic:"{topic}".Make it informative,
          engaging and beginner-friendly.
          Include an intro, main content,  and conclusion.""")



script_chain = LLMChain(llm=llm,prompt=prompt)

def generate_script(topic):
    return script_chain.run(topic=topic)


import streamlit as st

st.title("Youtube Script Generator")

user_input= st.text_input("Enter a Topic for your video:")

if user_input:
    script = generate_script(user_input)
    
    st.subheader("Generated Script:")
    st.write(script)
  
