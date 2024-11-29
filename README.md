
import random
import logging
from telegram import Update
from telegram.ext import Updater, CommandHandler, CallbackContext

# Configurações do logging
logging.basicConfig(format='%(asctime)s • %(name)s • %(levelname)s • %(message)s', level=logging.INFO)

# Função para rolar dados
def rolar_dados():
    return random.randint(1, 6), random.randint(1, 6

# Função para determinar a pontuação
def pontuacao(dados):
    return sum(dados) % 10

# Função para jogar uma rodada
def jogar_rodada():
    dados_jogador = rolar_dados()
    dados_banqueiro = rolar_dados()
    pontuacao_jogador = pontuacao(dados_jogador)
    pontuacao_banqueiro = pontuacao(dados_banqueiro)

    if pontuacao_jogador > pontuacao_banqueiro:
        return "Jogador"
    elif pontuacao_jogador < pontuacao_banqueiro:
        return "Banqueiro"
    else:
        return "Empate"

# Comando para iniciar o jogo
def start(update: Update, context: CallbackContext):
    update.message.reply_text("Bem-vindo ao Bac Bo! Use /jogar para jogar uma rodada.")

# Comando para jogar uma rodada
def jogar(update: Update, context: CallbackContext):
    resultado = jogar_rodada()
    update.message.reply_text(f"O resultado é: {resultado}")

# Função principal para rodar o bot
def main():
    # Insira seu token aqui
    TOKEN = 'YOUR_TELEGRAM_BOT_TOKEN'

    # Cria o Updater e o dispatcher
    updater = Updater(TOKEN)
    dispatcher = updater.dispatcher

    # Adiciona comandos
    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(CommandHandler("jogar", jogar))

    # Inicia o bot
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
