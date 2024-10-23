# Use uma imagem base oficial do Python
FROM python:3.9

# Define o diretório de trabalho
WORKDIR /app

# Clona repositório do guess_game
RUN git clone --depth 1 https://github.com/fams/guess_game.git . &&\
    pip install --no-cache-dir -r requirements.txt

# Define a variável de ambiente para que o Flask não use o modo debug
ENV FLASK_ENV=production

# Expõe a porta em que o Flask estará rodando
EXPOSE 5000

# Define o comando padrão para rodar a aplicação Flask
CMD ["flask", "run", "--host=0.0.0.0", "--port=5000"]