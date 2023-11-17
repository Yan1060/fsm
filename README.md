from telegram import Update, ParseMode
from telegram import ReplyKeyboardMarkup, ReplyKeyboardRemove
from telegram import InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Updater, Dispatcher
from telegram.ext import MessageHandler, CommandHandler, ConversationHandler, CallbackQueryHandler
from telegram.ext import CallbackContext
from telegram.ext import Filters

import logging
TOKEN = "6376650036:AAHf858D7GreG8iQAanhR-Ypqmt_aZVt1k0"

logger = logging.getLogger(__name__)

WAIT_NAME, WAIT_SURNAME, WAIT_BIRTHDAY = range(3)


def ask_name(update: Update, contex: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    logger.info(f"{username=} {user_id=} вызвал функцию ask_name")
    answer = [
        f"назави свою имя"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)

    return WAIT_NAME


def get_name(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    text = update.massage.text
    logger.info(f"{username=} {user_id=} вызвал функцию пуе_name")
    answer = [
        f"Твоя имя - {text}"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)
    return ask_surname(update, context)


def ask_surname(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    logger.info(f"{username=} {user_id=} вызвал функцию ask_surname")
    answer = [
        f"назави свою фамилию"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)

    return WAIT_SURNAME


def get_surname(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    text = update.massage.text
    logger.info(f"{username=} {user_id=} вызвал функцию get_surname")
    answer = [
        f"Твоя фамилия - {text}"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)


def ask_birthday(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    logger.info(f"{username=} {user_id=} вызвал функцию ask_birthday")
    answer = [
        f"назави свою дату рождения"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)

    return WAIT_BIRTHDAY


def get_birthday(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    text = update.massage.text
    logger.info(f"{username=} {user_id=} вызвал функцию ask_birthday")
    answer = [
        f"Твоя дата рождения - {text}"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)


def register(update: Update, context: CallbackContext):
    user_id = update.message.from_user.id
    username = update.message.from_user.username
    logger.info(f"{username=} {user_id=} вызвал функцию register")
    answer = [
        f"Привет!"
        f"Зарегистрировал тебя!"
    ]
    answer = "/n".join(answer)
    update.message.reply_text(answer)
    return ConversationHandler.END


register_handler = ConversationHandler(
    entry_points=[CommandHandler("register", ask_name)],
    states={
        WAIT_NAME: [MessageHandler(Filters.text, get_name)],
        WAIT_SURNAME: [MessageHandler(Filters.text, get_surname)],
        WAIT_BIRTHDAY: [MessageHandler(Filters.text, get_birthday)],
    },
    fallbacks=[]

)
