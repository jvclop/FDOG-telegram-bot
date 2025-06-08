from aiogram import Bot, Dispatcher, types, executor
import logging
import aiohttp
import os
import random

API_TOKEN = os.getenv("TELEGRAM_TOKEN")

logging.basicConfig(level=logging.INFO)

bot = Bot(token=API_TOKEN)
dp = Dispatcher(bot)


@dp.message_handler(commands=['start'])
async def send_welcome(message: types.Message):
    await message.reply(
        """
🐾 ¡Bienvenido al territorio de $FDOG!

Soy FDOGBot, tu guía cripto-canina en esta aventura.

🔽 Comandos útiles:
/price – Ver precio actual
/chart – Ver gráfico
/buy – Comprar $FDOG
/nfts – Info de nuestros NFTs
/airdrops – Recompensas activas
/roadmap – Plan de conquista
/community – Únete a la manada
/bark – Motivación bulldoguera

🔥 ¡Ladremos hasta la luna!
        """
    )


@dp.message_handler(commands=['price'])
async def send_price(message: types.Message):
    async with aiohttp.ClientSession() as session:
        try:
            async with session.get('https://price.jup.ag/v4/price?ids=FDOG') as resp:
                data = await resp.json()
                price_usd = data['data']['FDOG']['price']
                await message.reply(f"💰 Precio actual de $FDOG: ${price_usd:.6f} USD")
        except:
            await message.reply("🚫 Error al obtener el precio. Intenta más tarde.")


@dp.message_handler(commands=['chart'])
async def send_chart(message: types.Message):
    await message.reply("📈 Mira el gráfico en DEXtools: https://www.dextools.io/app/en/solana/pair-explorer")


@dp.message_handler(commands=['buy'])
async def send_buy_link(message: types.Message):
    await message.reply("🛒 Compra $FDOG aquí: https://jup.ag/swap/USDC-FDOG")


@dp.message_handler(commands=['nfts'])
async def send_nft_info(message: types.Message):
    await message.reply("🎨 Conoce nuestros NFTs en: https://mint.fdog.com")


@dp.message_handler(commands=['airdrops'])
async def send_airdrops(message: types.Message):
    await message.reply("🎁 Airdrops activos: próximamente en https://fdog.com/airdrops")


@dp.message_handler(commands=['roadmap'])
async def send_roadmap(message: types.Message):
    await message.reply("🚀 Revisa el roadmap aquí: https://fdog.com/roadmap")


@dp.message_handler(commands=['community'])
async def send_community_links(message: types.Message):
    await message.reply(
        "🌐 Únete a la manada:\n"
        "Telegram: https://t.me/FDOGarmy\n"
        "Twitter: https://x.com/FDOGsol\n"
        "Web: https://fdog.com"
    )


@dp.message_handler(commands=['bark'])
async def send_bark(message: types.Message):
    barks = [
        "WOOF! El dip no me asusta 🐶",
        "¡Ladra fuerte, hodl más fuerte! 🚀",
        "$FDOG no duerme, solo sube 🐾",
        "Tu perro no te juzga... pero el gráfico sí."
    ]
    await message.reply(random.choice(barks))


if __name__ == '__main__':
    executor.start_polling(dp, skip_updates=True)
