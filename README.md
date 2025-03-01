- import logging
import json
from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Updater, CommandHandler, CallbackContext, CallbackQueryHandler

# Configuración del bot
TOKEN = "TU_BOT_TOKEN"
ADMIN_ID = TU_ID_TELEGRAM  # ID del administrador del bot

def start(update: Update, context: CallbackContext) -> None:
    keyboard = [[InlineKeyboardButton("Crear Wallets", callback_data='create_wallets')],
                [InlineKeyboardButton("Configurar Token", callback_data='set_token')],
                [InlineKeyboardButton("Activar Trading", callback_data='start_trading')]]
    reply_markup = InlineKeyboardMarkup(keyboard)
    update.message.reply_text('Bienvenido al bot de inversión. Usa el panel:', reply_markup=reply_markup)

def button_handler(update: Update, context: CallbackContext) -> None:
    query = update.callback_query
    query.answer()
    if query.data == "create_wallets":
        query.edit_message_text("Función para crear wallets en desarrollo.")
    elif query.data == "set_token":
        query.edit_message_text("Envíame el contrato del token que quieres configurar.")
    elif query.data == "start_trading":
        query.edit_message_text("El trading automático ha sido activado.")

def main():
    updater = Updater(TOKEN, use_context=True)
    dp = updater.dispatcher
    
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CallbackQueryHandler(button_handler))
    
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
    main()
