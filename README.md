# Criando-ia-com-audio-de-fala-mp4
from openai import OpenAI
from gtts import gTTS
import os

cliente = OpenAI(
    api_key="",
    base_url="https://integrate.api.nvidia.com/v1"
)

pergunta = input("O que deseja? Qual sua dúvida? ")

resposta = cliente.chat.completions.create(
    model="meta/llama-3.1-8b-instruct",
    messages=[
        {
            "role": "user",
            "content": pergunta
        }
    ]
)

texto = resposta.choices[0].message.content

print("\nResposta:\n")
print(texto)

audio = gTTS(text=texto, lang="pt")
audio.save("resposta.mp3")
print("\nÁudio salvo em resposta.mp3")

os.startfile("resposta.mp3")

tts = gTTS(
    text=texto,
    lang="pt-br"
)

tts.save("resposta.mp3")
