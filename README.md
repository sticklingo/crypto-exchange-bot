import requests
from telegram import Update, ForceReply
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext

# Ваш токен Telegram-бота
TELEGRAM_TOKEN = "7213630146:AAH4ylG1IVsemT2AtKW96CfTz7XTJSj6uos"

# Адрес кошелька TON
TON_WALLET_ADDRESS = "UQCd_x_JvxsbJYZqjHx9G9NYyQ6pAU5hs5epiBfKKOJQK--4"

# Функция для обработки команд Telegram
def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('Добро пожаловать! Отправьте количество HMK для обмена.')

def handle_message(update: Update, context: CallbackContext) -> None:
    try:
        amount_hmk = float(update.message.text)
        user_wallet = TON_WALLET_ADDRESS
        # Здесь логика для обработки транзакции
        # Предполагаем, что транзакция выполняется успешно
        update.message.reply_text(f'{amount_hmk} HMK успешно обменены и отправлены на ваш кошелек.')
    except ValueError:
        update.message.reply_text('Пожалуйста, введите корректное количество HMK.')

def main():
    # Инициализация бота Telegram
    updater = Updater(TELEGRAM_TOKEN, use_context=True)

    dispatcher = updater.dispatcher

    dispatcher.add_handler(CommandHandler("start", start))
    dispatcher.add_handler(MessageHandler(Filters.text & ~Filters.command, handle_message))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
